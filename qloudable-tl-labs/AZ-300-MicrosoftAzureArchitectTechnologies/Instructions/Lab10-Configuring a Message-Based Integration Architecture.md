# Lab: Configuring a Message-Based Integration Architecture
  
## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Configure and validate an Azure Function App Storage Blob trigger](#exercise-1-configure-and-validate-an-azure-function-app-storage-blob-trigger)

[Exercise 2: Configure and validate an Azure Event Grid subscription-based queue messaging](#exercise-2-configure-and-validate-an-azure-event-grid-subscription-based-queue-messaging)

[Exercise 3: Remove lab resources](#exercise-3-remove-lab-resources)

## Overview

The Aim of this lab is about Configuring a Message-Based Integration Architecture.

### Scenario and Objectives

**Scenario**

XYZ has several web applications that process files uploaded in regular intervals to their on-premises file servers. Files sizes vary, but they can reach up to 100 MB. XYZ is considering migrating the applications to Azure App Service or Azure Functions-based apps and using Azure Storage to host uploaded files. You plan to test two scenarios:

* using Azure Functions to automatically process new blobs uploaded to an Azure Storage container.

* using Event Grid to generate Azure Storage queue messages that will reference new blobs uploaded to an Azure Storage container.

These scenarios are intended to address a challenge common to a messaging-based architecture, when sending, receiving, and manipulating large messages. Sending large messages to a message queue directly is not recommended as they would require more resources to be used, result in more bandwidth to be consumed, and negatively impact the processing speed, since messaging platforms are usually fine-tuned to handle high volumes of small messages. In addition, messaging platforms usually limit the maximum message size they can process.

One potential solution is to store the message payload into an external service, like Azure Blob Store, Azure SQL or Azure Cosmos DB, get the reference to the stored payload and then send to the message bus only that reference. This architectural pattern is known as "claim check". The clients interested in processing that specific message can use the obtained reference to retrieve the payload, if needed. On Azure this pattern can be implemented in several ways and with different technologies, but it typically it relies on eventing to either automate the claim check generation and to push it into the message bus to be used by clients or to trigger payload processing directly. One of the common components included in such implementations is Event Grid, which is an event routing service responsible for delivery of events within a configurable period of time (up to 24 hours). After that, events are either discarded or dead lettered. If archival of event contents or replayability of event stream are needed, it is possible to facilitate this requirement by setting up an Event Grid subscription to the Event Hub or a queue in Azure Storage where messages can be retained for longer periods and archival of messages is supported.

In this lab, you will use Azure Storage Blob service to store files to be processed. A client just needs to drop the files to be shared into a designated Azure Blob container. In the first exercise, the files will be consumed directly by an Azure Function, leveraging its serverless nature. You will also take advantage of the Application Insights to provide instrumentation, facilitating monitoring and analyzing file processing. In the second exercise, you will use Event Grid to automatically generate a claim check message and send it to an Azure Storage queue. This allows a client application to poll the queue, get the message and then use the stored reference data to download the payload directly from Azure Blob Storage.

It is worth noting that the Azure Function in the first exercise relies on the Blob Storage trigger. You should opt for Event Grid trigger instead of the Blob storage trigger when dealing with the following requirements:

* blob-only storage accounts: blob storage accounts are supported for blob input and output bindings but not for blob triggers. Blob storage triggers require a general-purpose storage account.

 * high scale: high scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.

* reduced latency: if your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle. To avoid this latency, you can use an Event Grid trigger or switch to an App Service plan with the Always On setting enabled.

* processing of blob deletes events: blob delete events are not supported by blob storage triggers.

**Objectives**

After completing this lab, you will be able to:

•	Configure and validate an Azure Function App Storage Blob trigger

•	Configure and validate an Azure Event Grid subscription-based queue messaging

## Pre-Requisites

* Azure portal subscription with Owner permissions

The Owner role gives the user full access to all resources in the subscription, including the right to delegate access to others.

* Azure Power shell 

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell. 

* Azure CLI 

Azure CLI is also a command-line tool introduced by Microsoft which can use to manage Azure resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows. 

## Exercise 1: Configure and validate an Azure Function App Storage Blob trigger
  
The main tasks for this exercise are as follows:

1. Configure an Azure Function App Storage Blob trigger

2. Validate an Azure Function App Storage Blob trigger

### Task 1: Configure an Azure Function App Storage Blob trigger

1. **Login** by using the Microsoft account that has the Owner role in the target Azure subscription.

2. In the Azure portal, in the Microsoft Edge window, start a **Bash** session within the **Cloud Shell**. 

3. If you are presented with the **You have no storage mounted** message, configure storage using the following settings:

    - Subsciption: the name of the target Azure subscription

    - Cloud Shell region: the name of the Azure region that is available in your subscription and which is closest to the lab location

    - Resource group: **az300T0601-LabRG**

    - Storage account: a name of a new storage account

    - File share: a name of a new file share

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/1.png?token=AIMANV5PAFNO6YSQQQKI5XS5LTTHG)

4. From the Cloud Shell pane, run the following to generate a pseudo-random string of characters that will be used as a prefix for names of resources you will provision in this exercise:

   ```sh
   export PREFIX=$(echo `openssl rand 5 -base64 | cut -c1-7 | tr '[:upper:]' '[:lower:]' | tr -cd '[[:alnum:]]._-'`)
   ```

5. From the Cloud Shell pane, run the following to designate the Azure region into which you want to provision resources in this lab (make sure to replace the placeholder `<Azure region>` with the name of the target Azure region):

   ```sh
   export LOCATION='<Azure_region>'
   ```

6. From the Cloud Shell pane, run the following to create a resource group that will host all resources that you will provision in this lab:

   ```sh
   export RESOURCE_GROUP_NAME='az300T0602-LabRG'

   az group create --name "${RESOURCE_GROUP_NAME}" --location "$LOCATION"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/2.png?token=AIMANV2RWEPEVRZG2OOE63S5LTTIW)

7. From the Cloud Shell pane, run the following to create an Azure Storage account and a container that will host blobs to be processed by the Azure function:

   ```sh
   export STORAGE_ACCOUNT_NAME="az300t06st2${PREFIX}"

   export CONTAINER_NAME="workitems"

   export STORAGE_ACCOUNT=$(az storage account create --name "${STORAGE_ACCOUNT_NAME}" --kind "StorageV2" --location "${LOCATION}" --resource-group "${RESOURCE_GROUP_NAME}" --sku "Standard_LRS")

   az storage container create --name "${CONTAINER_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/3.png?token=AIMANV6NIV5NDTDX2Q2VZVS5LTTJU)

   > **Note**: The same storage account will be also used by the Azure function to facilitate its own processing requirements. In real-world scenarios, you might want to consider creating a separate storage account for this purpose.

8. From the Cloud Shell pane, run the following to create a variable storing the value of the connection string property of the Azure Storage account:

   ```sh
   export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string --name "${STORAGE_ACCOUNT_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" -o tsv)
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/4.png?token=AIMANV7QLFMY5MG4FFCCNRS5LTTKK)

9. From the Cloud Shell pane, run the following to create an Application Insights resource that will provide monitoring of the Azure Function processing blobs and store its key in a variable:

   ```sh
   export APPLICATION_INSIGHTS_NAME="az300t06ai${PREFIX}"

   az resource create --name "${APPLICATION_INSIGHTS_NAME}" --location "${LOCATION}" --properties '{"Application_Type": "other", "ApplicationId": "function", "Flow_Type": "Redfield"}' --resource-group "${RESOURCE_GROUP_NAME}" --resource-type "Microsoft.Insights/components"

   export APPINSIGHTS_KEY=$(az resource show --name "${APPLICATION_INSIGHTS_NAME}" --query "properties.InstrumentationKey" --resource-group "${RESOURCE_GROUP_NAME}" --resource-type "Microsoft.Insights/components" -o tsv)
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/5.png?token=AIMANV4CNGCUHX5TPIDPF3S5LTTLI)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/6.png?token=AIMANV4HWOJL7DOJSQRZC7K5LTTL6)

10. From the Cloud Shell pane, run the following to create the Azure Function that will process events corresponding to creation of Azure Storage blobs:

   ```sh
   export FUNCTION_NAME="az300t06f${PREFIX}"

   az functionapp create --name "${FUNCTION_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --storage-account "${STORAGE_ACCOUNT_NAME}" --consumption-plan-location "${LOCATION}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/7.png?token=AIMANVZSCS35NKMOMDNKRT25LTTMS)

11. From the Cloud Shell pane, run the following to configure Application Settings of the newly created function, linking it to the Application Insights and Azure Storage account:

   ```sh
   az functionapp config appsettings set --name "${FUNCTION_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --settings "APPINSIGHTS_INSTRUMENTATIONKEY=$APPINSIGHTS_KEY" FUNCTIONS_EXTENSION_VERSION=~2

   az functionapp config appsettings set --name "${FUNCTION_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --settings "STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING" FUNCTIONS_EXTENSION_VERSION=~2
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/8.png?token=AIMANV7EHLGTDUBC6PDJ3XC5LTTNO)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/9.png?token=AIMANV354HDF7L6PDZ4HLHC5LTTOI)

12. Switch to the Azure portal and navigate to the blade of the Azure Function app you created earlier in this task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/10.png?token=AIMANV237MD2C5UTCEC2YIK5LTTPE)

13. On the Azure Function app blade, click **Functions** and then, click **+ New function**. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/11.png?token=AIMANV35CR3PARKIQEL3ETC5LTTP4)

14. On the **Function App runtime stack** blade, ensure that the **.NET** entry appears in the **Function Runtime stack** drop down list and click **Go**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/12.png?token=AIMANV762AYCZV7HSXSIYXC5LTTQU)

15. On the **Choose a template below or go to the quickstart** blade, click **Azure Blob Storage trigger** template.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/13.png?token=AIMANVZUNFCU5TEDR3QW3V25LTTRM)

16.	Scroll down and select Azure Blob Storage trigger.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/14.png?token=AIMANV5SH5HIITDP563VJFS5LTTSG)

17. On the **Extensions not Installed** blade, click **Install** and wait until the installation of the extension completes. Wait until the installation completes and click **Continue**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/15.png?token=AIMANV75H6WKSYPJZMSWGQ25LTTS2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/16.png?token=AIMANV37YVVA2HJAW244VR25LTTTS)

    > **Note**: Azure Functions V2 runtime implement bindings in the form of Nuget packages, referred to as "binding extensions" (in particular, the Azure Storage Blob binding uses the Microsoft.Azure.WebJobs.Extensions.Storage package). 

18. On the **Azure Blob Storage trigger** blade, specify the following and click **Create** to create a new function within the Azure function:

    - Name: **BlobTrigger**

    - Path: **workitems/{name}**

    - Storage account connection: **STORAGE_CONNECTION_STRING**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/17.png?token=AIMANV23TD2IALGHNTPAKW25LTTUI)

19. On the Azure Function app **BlobTrigger** function blade, review the content of the run.csx file. 

   ```csharp
   public static void Run(Stream myBlob, string name, ILogger log)
   {
       log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
   }
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/18.png?token=AIMANV4QJSJLQY6BQKMLOX25LTTVY)

    > **Note**: By default, the function is configured to simply log the event corresponding to creation of a new blob. In order to carry out blob processing tasks, you would modify the content of this file.

### Task 2: Validate an Azure Function App Storage Blob trigger

1. If necessary, restart the Bash session in the Cloud Shell.

2. From the Cloud Shell pane, run the following to repopulate variables that you used in the previous task:

   ```sh
   export RESOURCE_GROUP_NAME='az300T0602-LabRG'

   export STORAGE_ACCOUNT_NAME="$(az storage account list --resource-group "${RESOURCE_GROUP_NAME}" --query "[0].name" --output tsv)"

   export CONTAINER_NAME="workitems"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/19.png?token=AIMANV6DLYURYLOR7PMMKOK5LTTWQ)

3. From the Cloud Shell pane, run the following to upload a test blob to the Azure Storage account you created earlier in this task:

   ```sh
   export STORAGE_ACCESS_KEY="$(az storage account keys list --account-name "${STORAGE_ACCOUNT_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --query "[0].value" --output tsv)"

   export WORKITEM='workitem1.txt'

   touch "${WORKITEM}"

   az storage blob upload --file "${WORKITEM}" --container-name "${CONTAINER_NAME}" --name "${WORKITEM}" --auth-mode key --account-key "${STORAGE_ACCESS_KEY}" --account-name "${STORAGE_ACCOUNT_NAME}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/20.png?token=AIMANVZ3VFMFPPVGGHTLX3S5LTTXK)

4. In the Azure portal, navigate back to the blade displaying the Azure Function app you created in the previous task.

5. On the Azure Function app blade, click **Monitor** entry in the **Functions** section. 

6. Note a single event entry representing uploading of the blob. Click the entry to view the **Invocation Details** blade.

    > **Note**: Since the Azure function app in this exercise runs in the Consumption plan, there may be a delay of up to several minutes between uploading a blob and the function being triggered. It is possible to minimize the latency by implementing the Function app by using an App Service (rather than Consumption) plan.


7. On the **Invocation Details** blade, click the link **Run in Application Insights**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/21.png?token=AIMANV6NYLU4BVA6NR27BDS5LTTYO)

8. In the Application Insights portal, review the autogenerated Kusto query and its results.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/22.png?token=AIMANV3R7UIX7LQZZV3QDQC5LTTZG)

## Exercise 2: Configure and validate an Azure Event Grid subscription-based queue messaging 
  
The main tasks for this exercise are as follows:

1. Configure an Azure Event Grid subscription-based queue messaging 

2. Validate an Azure Event Grid subscription-based queue messaging 

### Task 1: Configure an Azure Event Grid subscription-based queue messaging 

1. If necessary, restart the Bash session in the Cloud Shell.

2. From the Cloud Shell pane, run the following to generate a pseudo-random string of characters that will be used as a prefix for names of resources you will provision in this exercise:

   ```sh
   export PREFIX=$(echo `openssl rand 5 -base64 | cut -c1-7 | tr '[:upper:]' '[:lower:]' | tr -cd '[[:alnum:]]._-'`)
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/23.png?token=AIMANVY3FLNWARQEJBEER3S5LTT2C)

3. From the Cloud Shell pane, run the following to identify the Azure region hosting the target resource group and its existing resources: 

   ```sh
   export RESOURCE_GROUP_NAME_EXISTING='az300T0602-LabRG'

   export LOCATION=$(az group list --query "[?name == '${RESOURCE_GROUP_NAME_EXISTING}'].location" --output tsv)

   export RESOURCE_GROUP_NAME='az300T0603-LabRG'

   az group create --name "${RESOURCE_GROUP_NAME}" --location $LOCATION
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/24.png?token=AIMANV2XWFXOEJGJ22Z3WOK5LTT3A)

4. From the Cloud Shell pane, run the following to create an Azure Storage account and its container that will be used by the Event Grid subscription that you will configure in this task:

   ```sh
   export STORAGE_ACCOUNT_NAME="az300t06st3${PREFIX}"

   export CONTAINER_NAME="workitems"

   export STORAGE_ACCOUNT=$(az storage account create --name "${STORAGE_ACCOUNT_NAME}" --kind "StorageV2" --location "${LOCATION}" --resource-group "${RESOURCE_GROUP_NAME}" --sku "Standard_LRS")

   az storage container create --name "${CONTAINER_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/25.png?token=AIMANV757E7OGVIECKQUKP25LTT3U)

5. From the Cloud Shell pane, run the following to create a variable storing the value of the Resource Id property of the Azure Storage account:

   ```sh
   export STORAGE_ACCOUNT_ID=$(az storage account show --name "${STORAGE_ACCOUNT_NAME}" --query "id" --resource-group "${RESOURCE_GROUP_NAME}" -o tsv)
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/26.png?token=AIMANV2NOCLDXPO3RXBVZK25LTT4M)

6. From the Cloud Shell pane, run the following to create the Storage Account queue that will store messages generated by the Event Grid subscription that you will configure in this task:

   ```sh
   export QUEUE_NAME="az300t06q3${PREFIX}"

   az storage queue create --name "${QUEUE_NAME}" --account-name "${STORAGE_ACCOUNT_NAME}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/27.png?token=AIMANV4XWUIJX6R4YEAAFGC5LTT5I)

7. From the Cloud Shell pane, run the following to create the Event Grid subscription that will facilitate generation of messages in Azure Storage queue in response to blob uploads to the designated container in the Azure Storage account:

**Note:** You must have registered the Eventgrid in your Subscription.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/28.png?token=AIMANV52QWICJNSUAWQ2AKS5LTT54)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/29.png?token=AIMANV3C73OQQPV3E4EPUEK5LTT6U)

   ```sh
   export QUEUE_SUBSCRIPTION_NAME="az300t06qsub3${PREFIX}"

   az eventgrid event-subscription create --name "${QUEUE_SUBSCRIPTION_NAME}" --included-event-types 'Microsoft.Storage.BlobCreated' --endpoint "${STORAGE_ACCOUNT_ID}/queueservices/default/queues/${QUEUE_NAME}" --endpoint-type "storagequeue" --source-resource-id "${STORAGE_ACCOUNT_ID}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/30.png?token=AIMANV7XSO43DU6JY4VFXFS5LTT7U)

### Task 2: Validate an Azure Event Grid subscription-based queue messaging 

1. From the Cloud Shell pane, run the following to upload a test blob to the Azure Storage account you created earlier in this task:

   ```sh
   export AZURE_STORAGE_ACCESS_KEY="$(az storage account keys list --account-name "${STORAGE_ACCOUNT_NAME}" --resource-group "${RESOURCE_GROUP_NAME}" --query "[0].value" --output tsv)"

   export WORKITEM='workitem2.txt'

   touch "${WORKITEM}"

   az storage blob upload --file "${WORKITEM}" --container-name "${CONTAINER_NAME}" --name "${WORKITEM}" --auth-mode key --account-key "${AZURE_STORAGE_ACCESS_KEY}" --account-name "${STORAGE_ACCOUNT_NAME}"
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/31.png?token=AIMANV3IEH5UNTVKW7FZDE25LTUA2)

2. In the Azure portal, navigate to the blade displaying the Azure Storage account you created in the previous task of this exercise. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/32.png?token=AIMANV4HVWFLSPV2WCF3IKS5LTUBQ)

3. On the blade of the Azure Storage account, click **Queues** to display the list of its queues. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/33.png?token=AIMANV5SBB7RN55IUFOWYH25LTUCO)

4. Click the entry representing the queue you created in the previous task of this exercise.

5. Note that the queue contains a single message. Click its entry to display the **Message properties** blade. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/34.png?token=AIMANV2QQDVY6LQ7C22NN225LTUC6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/35.png?token=AIMANV65OUTUIAIXJSSZ4US5LTUDW)

6. In the **MESSAGE BODY**, note the value of the **url** property, representing the URL of the Azure Storage blob you uploaded in the previous task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/36.png?token=AIMANV7B7CUP563X4XE4YV25LTUYU)

## Exercise 3: Remove lab resources

### Task 1: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open the Cloud Shell pane.

2. If needed, switch to the Bash shell session by using the drop down list in the upper left corner of the Cloud Shell pane.

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list all resource groups you created in this lab:

   ```
   az group list --query "[?starts_with(name,'az300T06')]".name --output tsv
   ```

4. Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/37.png?token=AIMANVYWSY7FICZS4IZFW725LTUHU)

### Task 2: Delete resource groups

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to delete the resource groups you created in this lab

   ```sh
   az group list --query "[?starts_with(name,'az300T06')]".name --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab10/38.png?token=AIMANV67RLUB5PCDIYHTUW25LTUJA)

2. Close the **Cloud Shell** prompt at the bottom of the portal.

**Result**: In this exercise, you removed the resources used in this lab.
