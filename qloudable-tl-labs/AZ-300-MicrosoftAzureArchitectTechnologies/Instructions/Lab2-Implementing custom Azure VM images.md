# Deploying and Managing Virtual Machines (VMs)

# Lab 2: Implementing custom Azure VM images

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites) 

[Exercise 1: Installing and configuring HashiCorp Packer](#exercise-1-installing-and-configuring-hashicorp-packer)

[Exercise 2: Creating a custom image](#exercise-2-creating-a-custom-image)

[Exercise 3: Deploying a custom image](#exercise-3-deploying-a-custom-image)

[Exercise 4: Remove lab resources](#exercise-4-remove-lab-resources)

## Overview

The Aim of this lab is to Deploy, Manage Virtual Machines (VMs) and Implement custom Azure VM images. 

### Scenario

XYZ wants to create custom Azure VM images.

### Objectives

After completing this lab, you will be able to:

* Install and configure HashiCorp Packer

* Create a custom VM image

* Deploy an Azure VM based on a custom image

## Pre-requisites

* Azure portal subscription with Owner permissions

The Owner role gives the user full access to all resources in the subscription, including the right to delegate access to others.

* Azure Power shell 

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

* Azure CLI 

Azure CLI is also a command-line tool introduced by Microsoft which can use to manage Azure resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows. 

## Exercise 1: Installing and configuring HashiCorp Packer

The main tasks for this exercise are as follows:

1. Download HashiCorp Packer

2. Configure HashiCorp Packer prerequisites

### Task 1: Download HashiCorp Packer

1. From the lab virtual machine, start Microsoft Edge and browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com) and sign in by using the Microsoft account that has the Owner role in the target Azure subscription.

2. In the Azure portal, in the Microsoft Edge window, start a **Bash** session within the **Cloud Shell**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/1.png?token=AE7OLVIAYC4JFI6SGU2B2GK5KY26M)

3. If you are presented with the **You have no storage mounted** message, configure storage using the following settings:

   - Subsciption: the name of the target Azure subscription

   - Cloud Shell region: the name of the Azure region that is available in your subscription and which is closest to the lab location

   - Resource group: **az3000300-LabRG**

   - Storage account: a name of a new storage account

   - File share: a name of a new file share

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/2.png?token=AE7OLVMZV4XP6DEMS2TQUKC5KY24Y)

4. From the Cloud Shell pane, run the following to download the Packer compressed installation media:

   ```
   wget https://releases.hashicorp.com/packer/1.3.1/packer_1.3.1_linux_amd64.zip
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/3.png?token=AE7OLVNO4VJ4NKDBLQPJKR25KY27U)

5. From the Cloud Shell pane, run the following to unzip the Packer installation media:

   ```
   unzip packer_1.3.1_linux_amd64.zip
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/4.png?token=AE7OLVNXNWWIK75PWYPZUN25KY3AI)

### Task 2: Configure HashiCorp Packer prerequisites

1. From the Cloud Shell pane, run the following to create a resource group and store the JSON output in a variable (replace the `<Azure region>` placeholder with the name of the Azure region that is available in your subscription and which is closest to the lab location):

   ```sh
   RG=$(az group create --name az3000301-LabRG --location <Azure region>)
   ```
**Ex:** RG=$(az group create --name az3000301-LabRG --location EastUS)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/5.png?token=AE7OLVNFW5XBLT4TDEHJHQK5KY3BS)

2. From the Cloud Shell pane, run the following to create a service principal that will be used by Packer and store the JSON output in a variable:

   ```sh
   AAD_SP=$(az ad sp create-for-rbac)
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/6.png?token=AE7OLVJCRFIOYSD4LNAD6725KY3CO)

**Result**: After you completed this exercise, you have downloaded HashiCorp Packer and configured its prerequisites.

## Exercise 2: Creating a custom image

The main tasks for this exercise are as follows:

1. Configure a Packer template

2. Build a Packer-based image

### Task 1: Configure a Packer template

1. From the Cloud Shell pane, run the following to retrieve the value of the service principal appId and store it in a variable

   ```sh
   CLIENT_ID=$(echo $AAD_SP | jq -r .appId)
   ```

2. From the Cloud Shell pane, run the following to retrieve the value of the service principal password and store it in a variable

   ```sh
   CLIENT_SECRET=$(echo $AAD_SP | jq -r .password)
   ```

3. From the Cloud Shell pane, run the following to retrieve the value of the service principal tenant ID and store it in a variable

   ```sh
   TENANT_ID=$(echo $AAD_SP | jq -r .tenant)
   ```

4. From the Cloud Shell pane, run the following to retrieve the value of the subscription ID and store it in a variable:

   ```sh
   SUBSCRIPTION_ID=$(az account show --query id | tr -d '"')
   ```

5. From the Cloud Shell pane, run the following to retrive the value of the resource group location and store it in a variable:

   ```sh
   LOCATION=$(echo $RG | jq -r .location)
   ```

6. From the Cloud Shell pane, upload the Packer template **\\allfiles\\AZ-300T01\\Module_03\\template03.json** into the home directory. To upload a file, click the document icon that has an up and down arrow in the Cloud Shell pane. 

7. From the Cloud Shell pane, run the following to replace the placeholder for the value of the **client_id** parameter with the value of the **\$CLIENT_ID** variable in the Packer template:

   ```sh
   sed -i.bak1 's/"$CLIENT_ID"/"'"$CLIENT_ID"'"/' ~/template03.json
   ```

8. From the Cloud Shell pane, run the following to replace the placeholder for the value of the **client_secret** parameter with the value of the **\$CLIENT_SECRET** variable in the Packer template:

   ```sh
   sed -i.bak2 's/"$CLIENT_SECRET"/"'"$CLIENT_SECRET"'"/' ~/template03.json
   ```

9. From the Cloud Shell pane, run the following to replace the placeholder for the value of the **tenant_id** parameter with the value of the **\$TENANT_ID** variable in the Packer template:

   ```sh
   sed -i.bak3 's/"$TENANT_ID"/"'"$TENANT_ID"'"/' ~/template03.json
   ```

10. From the Cloud Shell pane, run the following to replace the placeholder for the value of the **subscription_id** parameter with the value of the **\$SUBSCRIPTION_ID** variable in the Packer template:

   ```sh
   sed -i.bak4 's/"$SUBSCRIPTION_ID"/"'"$SUBSCRIPTION_ID"'"/' ~/template03.json
   ```

11. From the Cloud Shell pane, run the following to replace the placeholder for the value of the **location** parameter with the value of the **\$LOCATION** variable in the Packer template:

   ```sh
   sed -i.bak5 's/"$LOCATION"/"'"$LOCATION"'"/' ~/template03.json
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/7.png?token=AE7OLVNSM72T7ZW2N2EWMK25KY3DM)

### Task 2: Build a Packer-based image

1. From the Cloud Shell pane, run the following to build the packer-based image:

   ```sh
   ./packer build template03.json
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/8.png?token=AE7OLVIU3C2VU34WHJHJRMS5KY3D4)

2. Monitor the built progress until it completes.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/9.png?token=AE7OLVOVTNWA4AQBINNGVIS5KY3EM)

   > **Note**: The build process might take about 10 minutes.

**Result**: After you completed this exercise, you have created a Packer template and used it to build a custom image.

## Exercise 3: Deploying a custom image

The main tasks for this exercise are as follows:

1. Deploy an Azure VM based on a custom image

2. Validate Azure VM deployment

### Task 1: Deploy an Azure VM based on a custom image

1. From the Cloud Shell pane, run the following to deploy an Azure VM based on the custom image.

   ```sh
   az vm create --resource-group az3000301-LabRG --name az3000301-vm --image az3000301-image --admin-username adminuser --generate-ssh-keys
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/10.1.png?token=AE7OLVPH5QFCAEQSORNBACC5KY3FA)

2. Wait for the deployment to complete

   > **Note**: The deployment process might take about 3 minutes.

3. Once the deployment completes, from the Cloud Shell pane, run the following to allow inbound traffic to the newly deployed VM on TCP port 80:

   ```sh
   az vm open-port --resource-group az3000301-LabRG --name az3000301-vm --port 80
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/11.png?token=AE7OLVK3HIUW2YYZCFSGKU25KY3FW)

### Task 2: Validate Azure VM deployment

1. From the Cloud Shell pane, run the following to identify the IP address associated with the newly deployed Azure VM.

   ```sh
   az network public-ip show --resource-group az3000301-LabRG --name az3000301-vmPublicIP --query ipAddress
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/12.png?token=AE7OLVONCQH234MW5VMHZQK5KY3GK)

2. Start Microsoft Edge and navigate to the IP address you identified in the previous step.

3. Verify that Microsoft Edge displays the **Welcome to nginx!** page.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/13.png?token=AE7OLVOI3H2QQH7KGORISL25KY3G4)

**Result**: After you completed this exercise, you have deployed an Azure VM based on a custom image and validated the deployment.

## Exercise 4: Remove lab resources

### Task 1: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open the Cloud Shell pane.

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list all resource groups you created in this lab:

   ```sh
   az group list --query "[?starts_with(name,'az3000301')]".name --output tsv
   ```

3. Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/14.png?token=AE7OLVNV7XQBS7UVE7H43UC5KY3HO)

### Task 2: Delete resource groups

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to delete the resource groups you created in this lab

   ```sh
   az group list --query "[?starts_with(name,'az3000301')]".name --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab2/15.png?token=AE7OLVPEXCCKZWGULPDN3UK5KY3IC)

2. Close the **Cloud Shell** prompt at the bottom of the portal.

**Result**: In this exercise, you removed the resources used in this lab.
