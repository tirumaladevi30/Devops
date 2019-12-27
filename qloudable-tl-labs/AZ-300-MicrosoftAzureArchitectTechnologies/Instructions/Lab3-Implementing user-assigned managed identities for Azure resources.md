# Managing Identities

# Lab 3: Implementing user-assigned managed identities for Azure resources

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Creating and configuring a user-assigned managed identity](#exercise-1-creating-and-configuring-a-user-assigned-managed-identity)

[Exercise 2: Validating functionality of user-assigned managed identities](#exercise-2-validating-functionality-of-user-assigned-managed-identities)

[Exercise 3: Remove lab resources](#exercise-3-remove-lab-resources)

## Overview

The Aim of this lab is about Managing Identities and Implementing user-assigned managed identities for Azure resources.

### Scenario and Objectives

XYZ wants to use manage identities to authenticate applications running in Azure VMs.

After completing this lab, you will be able to:

* Create and configure user-assigned managed identities

* Validate functionality of user-assigned managed identities

## Pre-Requisites

* Remote Desktop Connection

* File Explorer

* Azure portal subscription with Owner permissions

The Owner role gives the user full access to all resources in the subscription, including the right to delegate access to others.

* Azure Power shell 

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

* Azure CLI 

Azure CLI is also a command-line tool introduced by Microsoft which can use to manage Azure resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows. 

## Exercise 1: Creating and configuring a user-assigned managed identity.

The main tasks for this exercise are as follows:

1. Deploy an Azure VM running Windows Server 2016 Datacenter

2. Create a user-assigned managed identity.

3. Assign the user-assigned managed identity to the Azure VM.

4. Grant RBAC-based permissions to the user-assigned managed identity.

### Task 1: Deploy an Azure VM running Windows Server 2016 Datacenter

1. From the lab virtual machine, start Microsoft Edge and browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com) and sign in by using the Microsoft account that has the Owner role in the target Azure subscription.

2. In the Azure portal, in the Microsoft Edge window, start a **Bash** session within the **Cloud Shell**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/1.png?token=AIMANV7SPFEXJRZC65ZPKE25LIM44)

3. If you are presented with the **You have no storage mounted** message, configure storage using the following settings:

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/2.png?token=AIMANV2RKE4TV72MTY5MHCS5LINEG)

   - Subscription: the name of the target Azure subscription

   - Cloud Shell region: the name of the Azure region that is available in your subscription and which is closest to the lab location

   - Resource group: **az3000500-LabRG**

   - Storage account: a name of a new storage account

   - File share: a name of a new file share

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/3.png?token=AIMANVYXAZSMWMPXFUJDE525LIN2I)

4. From the Cloud Shell pane, create a resource group by running (replace the `<Azure region>` placeholder with the name of the Azure region that is available in your subscription and which is closest to the lab location)

   ```
   az group create --resource-group az3000501-LabRG --location <Azure region>
   ```
**Ex:** az group create --resource-group az3000501-LabRG --location EastUS

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/4.png?token=AIMANVZ5TD756FTVQKUBW325LIN4Q)

**Note:** Clone the repo using git bash, which consist all files and Templates as shown like below.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/5.png?token=AIMANV3OP22226PQ4RJ4TWK5LIN54)

5. From the Cloud Shell pane, upload the Azure Resource Manager template **\\allfiles\\AZ-300T01\\Module_05\\azuredeploy05.json** into the home directory.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/6.png?token=AIMANV7RHZ2JTUP6HCUN2ZC5LIN7W)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/7.png?token=AIMANVYZQEH5RDEAZTI44OS5LIOBO)

6. From the Cloud Shell pane, upload the parameter file **\\allfiles\\AZ-300T01\\Module_05\\azuredeploy05.parameters.json** into the home directory.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/8.png?token=AIMANV6EQGUEN6NPSZ374HS5LIOCW)

7. From the Cloud Shell pane, deploy an Azure VM hosting Windows Server 2016 Datacenter into the first virtual network by running:

   ```
   az group deployment create --resource-group az3000501-LabRG --template-file azuredeploy05.json --parameters @azuredeploy05.parameters.json
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/9.png?token=AIMANVZK5BF5JBSYGTULVHK5LIOEA)

   > **Note**: Wait for the deployment to complete. This might take about 5 minutes.

### Task 2: Create a user-assigned managed identity and assign it to the Azure VM.

1. From the Cloud Shell pane, run the following to create a user-assigned managed identity:

   ```
   az identity create --resource-group az3000501-LabRG --name az3000501-mi
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/10.png?token=AIMANV3E5M6N2HXUDZ2RIPC5LIOFK)

2. From the Cloud Shell pane, run the following to assign the user-assigned managed identity to the Azure VM:

   ```
   az vm identity assign --resource-group az3000501-LabRG --name az3000501-vm --identities az3000501-mi
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/11.png?token=AIMANVZOGYMCCG377OXSIQK5LIOGO)

### Task 3: Configure RBAC referencing the user-assigned managed identity.

1. From the Cloud Shell pane, run the following to create a resource group (replace the `<Azure region>` placeholder with the name of the Azure region into which you deployed the Azure VM in this exercise):

   ```
   az group create --resource-group az3000502-LabRG --location <Azure region>
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/12.png?token=AIMANV2JFZ4YUAASET2JMQC5LIOHO)

2. In the Azure portal, navigate to the **az3000502-LabRG - Access control (IAM)** blade.

3. From the **az3000502-LabRG - Access control (IAM)** blade, assign the Owner role to the newly created user-assigned managed identity.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/13.png?token=AIMANV5DL5RN37N2K7HB6GC5LIOJE)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/14.png?token=AIMANVZSL4M7QG4U75NWJ6C5LIOKK)

**Result**: After you completed this exercise, you have created and configured a user-assigned managed identity.

## Exercise 2: Validating functionality of user-assigned managed identities

The main tasks for this exercise are as follows:

1. Configure an Azure VM for authenticating via user-assigned managed identity.

2. Validate functionality of user-assigned managed identity from the Azure VM.

### Task 1: Configure an Azure VM for authenticating via user-assigned managed identity.

1. In the Azure portal, navigate to the **az3000501-vm** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/15.png?token=AIMANV6ELJISDCBRSWROVOC5LIOME)

2. Connect to the Azure VM by using Remote Desktop and authenticate by providing the following credentials:

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/16.png?token=AIMANV37PZI5DTLDJQL4MWS5LION6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/17.png?token=AIMANV53IKWTWJNJABMSSNK5LIOQY)

   - Username: **Student**

   - Password: **Pa55w.rd1234**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/18.png?token=AIMANVZIGTYV3U2UOMOTMPK5LIOTW)

3. Once you establish a Remote Desktop session, you will be presented with an **Administrator: C:\\Windows\\system32\\cmd.exe** window. To start a PowerShell session, at the command prompt, type `PowerShell` and press Enter.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/19.png?token=AIMANV2MBWH5ARCT4SUP6QC5LIOVC)

4. From the PowerShell prompt, run the following to install the latest version of the PowerShellGet module (press Enter if prompted for confirmation):

   ```pwsh
   Install-Module -Name PowerShellGet -Force
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/20.png?token=AIMANV7S4VCZNK56P3JDBFS5LIOXI)

5. From the PowerShell prompt, run the following to install the latest version of the Az module (type **Y** and press Enter when prompted for confirmation):

   ```pwsh
   Install-Module -Name Az -AllowClobber
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/21.png?token=AIMANV6DWGVR4OGNYG42GZ25LIOY2)

6. Exit the current PowerShell session by typing `exit` and pressing Enter and then start it again by typing at the command prompt `PowerShell` and pressing Enter.

7. From the PowerShell prompt, run the following to install the the pre-release version of the PowerShellGet module:

   ```pwsh
   Install-Module -Name PowerShellGet -AllowPrerelease
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/22.png?token=AIMANV266IMVNKX3HTVC2K25LIOZ6)

8. From the PowerShell prompt, run the following to install the the pre-release version of the AzureRM.ManagedServiceIdentity module:

   ```pwsh
   Install-Module -Name Az.ManagedServiceIdentity -AllowPrerelease
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/23.png?token=AIMANV2MILZ43DK7G2DRBJS5LIO3W)

### Task 2: Validate functionality of user-assigned managed identity from the Azure VM.

1. From the PowerShell prompt, run the following to sign-in as the user-assigned managed identity:

   ```pwsh
   Add-AzAccount -Identity
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/24.png?token=AIMANV4OPZKTZKTZ2EWMHWS5LIO5C)

2. From the PowerShell prompt, run the following to attempt to retrieve the currently used managed identity:

   ```pwsh
   (Get-AzVM -ResourceGroupName az3000501-LabRG -Name az3000501-vm).Identity
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/25.png?token=AIMANVYGUAOGITO4NQPO3J25LIO6K)

3. Note the error message. As the message states, the current security context does not grant sufficent authorization to the target resource. To resolve this issue, switch to the Azure portal, navigate to the **az3000501-LabRG - Access control (IAM)** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/26.png?token=AIMANV2POHSFWWWVHOKGV6C5LIO76)

4. From the **az3000501-LabRG - Access control (IAM)** blade, assign the Reader role to the user-assigned managed identity **az3000501-mi**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/27.png?token=AIMANV22FNO7UVG2SFC74425LIPBM)

5. Switch back to the Remote Desktop session, and, from the PowerShell prompt, run the following to attempt to retrieve the currently used managed identity:

   ```pwsh
   (Get-AzVM -ResourceGroupName az3000501-LabRG -Name az3000501-vm).Identity
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/28.png?token=AIMANV522KAUHHCLUTC74AS5LIPC2)

6. From the PowerShell prompt, run the following to store location in a variable:

   ```pwsh
   $location = (Get-AzResourceGroup -Name az3000502-LabRG).Location
   ```

7. From the PowerShell prompt, run the following to create a public IP address resource:

   ```pwsh
   New-AzPublicIpAddress -Name az3000502-pip -ResourceGroupName az3000502-LabRG -AllocationMethod Dynamic -Location $location
   ```

8. Verify that the command completed successfully.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/29.png?token=AIMANV4XDISX2BN6K7A4HFK5LIPEO)

**Result**: After you completed this exercise, you have validated the functionality of the user-defined managed identity.

## Exercise 3: Remove lab resources

### Task 1: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open the Cloud Shell pane.

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list all resource groups you created in this lab:

   ```
   az group list --query "[?starts_with(name,'az30005')]".name --output tsv
   ```

3. Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/30.png?token=AIMANV45W34CDH3YNVUB6C25LIPIE)

### Task 2: Delete resource groups

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to delete the resource groups you created in this lab

   ```sh
   az group list --query "[?starts_with(name,'az30005')]".name --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'
   ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab3/31.png?token=AIMANVZE3FSUKXUPNMS62PS5LIPKQ)

2. Close the **Cloud Shell** prompt at the bottom of the portal.

**Result**: In this exercise, you removed the resources used in this lab.
