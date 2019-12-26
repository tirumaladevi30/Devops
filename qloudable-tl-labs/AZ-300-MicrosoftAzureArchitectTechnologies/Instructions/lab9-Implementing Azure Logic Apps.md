# Lab: Implementing Azure Logic Apps

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites) 

[Exercise 1: Set up the lab environment that consists of an Azure storage account and an Azure logic app](#exercise-1-prepare-the-lab-environment-that-consists-of-an-azure-storage-account-and-an-azure-logic-app)

[Exercise 2: Configure Azure logic app to monitor changes to a resource group](#exercise-2-configure-azure-logic-app-to-monitor-changes-to-a-resource-group)

[Exercise 3: Remove lab resources](#exercise-3-remove-lab-resources)


## Overview

The aim of this lab is to Implement and Manage Application Services. In this lab exercise 1, you must create a storage account, a logic app that you will configure in the next exercise 2 of this lab, and an Azure AD service principal that you will reference during that configuration. In this lab you must configure an Azure logic app to monitor changes to a resource group.

### Scenario and Objectives

XYZ training Corporation wants to implement custom monitoring of changes to a resource group.

After completing this lab, you will be able to:
*	Create an Azure logic app
*	Configure integration of an Azure logic app and an Azure event grid

## Pre-requisites

1.	Familiarity with azure portal 

2.	Microsoft outlook Account with same azure portal account Id.
 
All tasks in this lab are performed from the Azure portal. 

## Exercise 1: Set up the lab environment that consists of an Azure storage account and an Azure logic app

The main tasks for this exercise are as follows:

1.	Create an Azure storage account
2.	Create an Azure logic app
3.	Create an Azure AD service principal
4.	Assign the Reader role to the Azure AD service principal
5.	Register the Microsoft.EventGrid resource provider

### Task 1: Create a storage account in Azure

1.	From the lab virtual machine, start Microsoft Edge and browse to the Azure portal at http://portal.azure.com and sign in by using the Microsoft account that has the Owner role in the target Azure subscription.

2.	From Azure Portal, create a new storage account with the following settings:
 
     -  Subscription: the name of the target Azure subscription

     -  Resource group: a new resource group named **az3000701-LabRG**

     -  Storage account name: any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits

     -  Location: the name of the Azure region that is available in your subscription and which is closest to the lab location

     -  Performance: **Standard**

     -  Account kind: **Storage (general purpose v1)**

     -  Replication: **Locally-redundant storage (LRS)**

     -  Secure transfer required: **Enabled**

     -  Virtual network: **All networks**

     -  Hierarchical namespace: **Disabled**
	
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/1.png?token=AGFEA6GUEQBLOXHYS7VHETC5MNUJ6" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/2.png?token=AGFEA6DM7GYLGW4TXUCMX525MNU7O" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/3.png?token=AGFEA6EXPJCFOTP5KCYGUMS5MNU7S" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/4.png?token=AGFEA6AYBEYPCT4PSS2RPTK5MNU7Y" alt="image-alt-text" >


> **Note**: Do not wait for the deployment to complete but instead proceed to the next task.

### Task 2: Create an Azure logic app

1.	From Azure Portal, create an instance of **Logic App** with the following settings:

	- Name: **logicapp3000701**

	- Subscription: the name of the target Azure subscription

	- Resource group: the name of a new resource group **az3000702-LabRG**

	- Location: the same Azure region into which you deployed the storage account in the previous task

	- Log Analytics: **Off**
       
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/5.png?token=AGFEA6E36FM5BGNSFGKWZNC5MNU72" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/6.png?token=AGFEA6FDCUM3QFJM6I2UPEC5MNU76" alt="image-alt-text" >

2.	Wait until the vault is provisioned. This will take about a minute.

### Task 3: Create an Azure AD service principal

1.	In the Azure portal, in the Microsoft Edge window, start a **PowerShell** session within the **Cloud Shell**.
 
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/7.png?token=AGFEA6ELK5GLRLT6FWZL4FK5MNVAE" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/8.png?token=AGFEA6F3JCCGYLBZZ22HWKK5MNVAI" alt="image-alt-text" >

2.	If you are presented with the “**You have no storage mounted**” message, configure storage using the following settings:

	- Subsciption: the name of the target Azure subscription

	- Cloud Shell region: the name of the Azure region that is available in your subscription and which is closest to the lab location

	- Resource group: the name of a new resource group **az3000700-LabRG**

	- Storage account: a name of a new storage account

	- File share: a name of a new file share

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/9.png?token=AGFEA6DOUUO5FCPA4E3BLR25MNVAK" alt="image-alt-text" >

3.	From the Cloud Shell pane, run the following to create a new Azure AD application that you will associate with the service principal you create in the subsequent steps of this task:

 **$password = 'Password@1234'**
 **$securePassword = ConvertTo-SecureString -Force -AsPlainText -String $password**
 **$aadApp30007 = New-AzADApplication -DisplayName 'aadApp30007' -HomePage 'http://aadApp30007' -IdentifierUris 'http://aadApp30007' -Password $securePassword**

4.	From the Cloud Shell pane, run the following to create a new Azure AD service principal associated with the application you created in the previous step:

**New-AzADServicePrincipal -ApplicationId $aadApp30007.ApplicationId.Guid**

5.	In the output of the **New-AzureRmADServicePrincipal** command, note the value of the **ApplicationId** property. You will need this in the next exercise of this lab.
 
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/10.png?token=AGFEA6ETSEP3VECCRHQBZ625MNUKE" alt="image-alt-text" >

6.	From the Cloud Shell pane, run the following to identify the value of the **Id** property of the current Azure subscription and the value of the **TenantId** property of the Azure AD tenant associated with that subscription (you will also need them in the next exercise of this lab):

**Get-AzSubscription**

7.	Close the Cloud Shell pane.

### Task 4: Assign the Reader role to the Azure AD service principal

1.	In the Azure portal, navigate to the blade displaying properties of your Azure subscription.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/11.png?token=AGFEA6GGVDARLD5OGG22M4S5MNUKK" alt="image-alt-text" >
 
2.	On the Azure subscription blade, click **Access control (IAM)**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/12.png?token=AGFEA6EA3LCRGDCKX5VPGOS5MNUKM" alt="image-alt-text" >

3.	Assign the **Reader** role within the scope of the Azure subscription to the **aadApp30007** service principal.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/13.png?token=AGFEA6FNWTOKSQC2YDG2S7C5MNUKQ" alt="image-alt-text" >
 
### Task 5: Register the Microsoft.EventGrid resource provider

1.	In the Azure portal, in the Microsoft Edge window, reopen the **PowerShell** session within the **Cloud Shell**.

2.	From the Cloud Shell pane, run the following to register the Microsoft.EventGrid resource provider:

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/14.png?token=AGFEA6DQCEZESMKH44BVFES5MNUKS" alt="image-alt-text" >

**Register-AzResourceProvider -ProviderNamespace Microsoft.EventGrid**
 
3.	Close the Cloud Shell pane.

> **Result**: After you completed this exercise, you have created a storage account, a logic app that you will configure in the next exercise of this lab, and an Azure AD service principal that you will reference during that configuration.

## Exercise 2: Configure Azure logic app to monitor changes to a resource group

The main tasks for this exercise are as follows:

1.	Add a trigger to the Azure logic app
2.	Add an action to the Azure logic app
3.	Identify the callback URL of the Azure logic app
4.	Configure an event subscription
5.	Test the logic app

### Task 1: Add a trigger to the Azure logic app

1.	In the the Azure portal, navigate to the **Logic App Designer** blade of the newly provisioned Azure logic app.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/15.png?token=AGFEA6GPD6GOZLGDYKOSPF25MNUKW" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/16.png?token=AGFEA6AOG3ZUN6FSHY5Q4A25MNUKY" alt="image-alt-text" >
 
2.	Click **Blank Logic App**. This will create a blank designer workspace and display a list of connectors and triggers to add to the workspace.

3.	Search for **Event Grid** triggers and, in the list of results, click the **When a resource event occurs (preview)** Azure Event Grid trigger to add it to the designer workspace.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/17.png?token=AGFEA6F77DN43AG7W3PEQAS5MNUK4" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/18.png?token=AGFEA6BX5TK4CUNWDD4GTYC5MNUMQ" alt="image-alt-text" >

4.	In the **Azure Event Grid** tile, click the **Connect with Service Principal** link, specify the following values, and click **Create**:
	
    - Connection Name: **egc30007**
	
    - Client ID: the **ApplicationId** property you identified in the previous exercise

	- Client Secret: **Password1234**
	
    - Tenant: the **TenantId** property you identified in the previous exercise
 
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/19.png?token=AGFEA6BI4QIKT6A7C3YJEB25MNUMU" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/20.png?token=AGFEA6HKMSA37EH7PLRFUEK5MNVAO" alt="image-alt-text" >

5.	In the **When a resource event occurs** tile, specify the following values:

	- Subscription: the subscription **Id** property you identified in the previous exercise

	- Resource Type: **Microsoft.Resources.resourceGroups**

	- Resource Name: **/subscriptions/subscriptionId/resourceGroups/az3000701-LabRG**, where **subscriptionId** is the subscription Id property you identified in the previous exercise

	- Event Type Item - 1: **Microsoft.Resources.ResourceWriteSuccess**

	- Event Type Item - 2: **Microsoft.Resources.ResourceDeleteSuccess**

6.	Click **Add new parameter** and select **Subscription Name**

7.	In the **Subscription Name** text box, type **event-subscription-az3000701** and click **Save**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/21.png?token=AGFEA6FKOHCFZ2TUNZBBEXC5MNVOA" alt="image-alt-text" >
 
### Task 2: Add an action to the Azure logic app

1.	In the Azure portal, on the Logic App Designer blade of the newly provisioned Azure logic app, click **+ New step**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/22.png?token=AGFEA6GL6AZ2M7R53NHJUTS5MNVOG" alt="image-alt-text" >

2.	In the **Choose an action** pane, in the **Search connectors and actions** text box, type Outlook.

3.	In the list of results, click **Outlook.com**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/23.png?token=AGFEA6DMU7Z6I4MLHAP3V7S5MNVOK" alt="image-alt-text" >
 
4.	In the list of actions for **Outlook.com**, click **Outlook.com - Send an email**.

5.	In the **Outlook.com** pane, click **Sign in**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/24.png?token=AGFEA6HGUX2P5CZ2EHKMWK25MNVOQ" alt="image-alt-text" >

6.	When prompted, authenticate by using the Microsoft Account you are using in this lab.

7.	When prompted for the consent to grant Azure Logic App permissions to access Outlook resources, click **Accept**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/25.png?token=AGFEA6EXQS7LWWTD6L57NJC5MNVOS" alt="image-alt-text" >

8.	In the **Send an email** pane, specify the following settings and click **Save**:

	- To: the name of your Microsoft Account

	- Subject: type Resource updated: and, in the Dynamic Content column to the right of the Send an email pane, click Subject.
	
    - Body: type Resource group:, in the Dynamic Content column to the right of the Send an email pane, click Topic, type Event type:, in the Dynamic Content  column to the right of the Send an email pane, click Event Type, type Event ID:, in the Dynamic Content column to the right of the Send an email pane, click ID, type Event Time:, and in the Dynamic Content column to the right of the Send an email pane, click Event Time.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/26.png?token=AGFEA6G2WQKPQSFPR657PUC5MNVOW" alt="image-alt-text" >

### Task 3: Identify the callback URL of the Azure logic app

1.	In the Azure portal, navigate to the **logicapp3000701** blade and, in the **Summary** section, click **See trigger history**. Ignore any **Forbidden** error messages.
 
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/27.png?token=AGFEA6D3YNBDWS3XJ3RXYYK5MNVO2" alt="image-alt-text" >

2.	On the **When_a_resource_event_occurs** blade, copy the value of the **Callback url [POST]** text box.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/28.png?token=AGFEA6HADKXI37N5LDJI6SK5MNVO6" alt="image-alt-text" >
 
### Task 4: Configure an event subscription

1.	In the Azure portal, navigate to the **az3000701-LabRG** resource group and, in the vertical menu, click Events.

2.	On the **az3000701-LabRG - Events** blade, click **Web Hook**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/29.png?token=AGFEA6GHNDZWJMLP6ZYHHUC5MNVPE" alt="image-alt-text" >
 
3.	On the **Create Event Subscription** blade, in the **Filter to Event Types** drop down list, ensure that only the checkboxes next to the **Resource Write Success** and **Resource Delete Success** are selected.

4.	In the **Name** text box within the **EVENT SUBSCRIPTION DETAILS** section, type **event-subscription-az3000701**.

5.	In the **Endpoint Type** drop down list, ensure that **Web Hook** is selected and click the **Select an endpoint** link.

6.	On the **Select Web Hook** blade, in the **Subscriber Endpoint**, paste the value of the **Callback url [POST]** of the Azure logic app you copied in the previous task and click **Confirm Selection**.

7.	Click **Create**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/30.png?token=AGFEA6BISISFFL7HAKYNALK5MNVPI" alt="image-alt-text" >
  
<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/31.png?token=AGFEA6D74YQZJL7NJRK6SOS5MNVYK" alt="image-alt-text" >

 
### Task 5: Test the logic app

1.	In the Azure portal, navigate to the **az3000701-LabRG** resource group and, in the vertical menu, click **Overview**.

2.	In the list of resources, click the Azure storage account you created in the first exercise.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/32.png?token=AGFEA6EA7VGLWM2FT6XOCZS5MNVPQ" alt="image-alt-text" >
 
3.	On the storage account blade, in the vertical menu, click **Configuration**.

4.	On the configuration blade, set the **Secure transfer required** setting to **Disabled** and click on **Save**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/33.png?token=AGFEA6CHYQPAH3PADSIME7K5MNVPU" alt="image-alt-text" >
 
5.	Navigate to the **logicapp3000701** blade, click **Refresh**, and note that the **Runs history** includes the entry corresponding to configuration change of the Azure storage account.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/34.png?token=AGFEA6EGOV2NIPA4TDL757S5MNVPY" alt="image-alt-text" >
 
6.	Navigate to the inbox of the email account you configured in this exercise and verify that includes an email generated by the logic app.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/35.png?token=AGFEA6ERXEF5MBLBBGN6MXC5MNVP4" alt="image-alt-text" >
 
> **Result**: After you completed this exercise, you have configured an Azure logic app to monitor changes to a resource group.

## Exercise 3: Remove lab resources

### Task 1: Open Cloud Shell

1.	At the top of the portal, click the **Cloud Shell** icon to open the Cloud Shell pane.

2.	If needed, switch to the Bash shell session by using the drop-down list in the upper left corner of the Cloud Shell pane.

3.	At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list all resource groups you created in this lab:

**az group list --query "[?starts_with(name,'az30007')]".name --output tsv**

4.	Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

### Task 2: Delete resource groups

1.	At the Cloud Shell command prompt, type in the following command and press Enter to delete the resource groups you created in this lab

**az group list --query "[?starts_with(name,'az30007')]".name --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'**

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/lab9/36.png?token=AGFEA6HMO3JTMV4Q24ZJE4C5MNVQC" alt="image-alt-text" >
     
2.	Close the **Cloud Shell** prompt at the bottom of the portal.

> **Result**: In this exercise, you removed the resources used in this lab.
