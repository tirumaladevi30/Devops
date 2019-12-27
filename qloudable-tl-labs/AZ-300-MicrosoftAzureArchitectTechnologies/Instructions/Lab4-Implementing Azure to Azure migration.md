# Lab 4: Implementing Azure to Azure migration

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Implement prerequisites for migration of Azure VMs by using Azure Site Recovery](#exercise-1-implement-prerequisites-for-migration-of-azure-vms-by-using-azure-site-recovery)

[Exercise 2: Migrate an Azure VM between Azure regions by using Azure Site Recovery](#exercise-2-migrate-an-azure-vm-between-azure-regions-by-using-azure-site-recovery)

## Overview

The Aim of this lab is about Evaluating and Performing Server Migration to Azure and Implementing Azure to Azure migration.

### Scenario

XYZ Training Corporation wants to migrate their existing Azure VMs to another region.

### Objectives

After completing this lab, you will be able to:

* Implement Azure Site Recovery Vault

* Migrate Azure VMs between Azure regions

## Pre-Requisites

* Remote Desktop Connection

* File Explorer

* Azure portal subscription with Owner permissions

The Owner role gives the user full access to all resources in the subscription, including the right to delegate access to others.

* Azure Power shell 

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

* Azure CLI 

Azure CLI is also a command-line tool introduced by Microsoft which can use to manage Azure resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows. 

## Exercise 1: Implement prerequisites for migration of Azure VMs by using Azure Site Recovery

The main tasks for this exercise are as follows:

1. Deploy an Azure VM to be migrated

2. Create an Azure Recovery Services vault

### Task 1: Deploy an Azure VM to be migrated

1. Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Portal Username }}

Azure Password: {{ Portal Password }}

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/1.png?st=2019-08-27T04%3A38%3A29Z&se=2026-08-28T04%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7WnT7KIlzAjjVB3nMThOlfMi%2Fs3p1evvA%2Fv8XavUO5M%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/2.png?st=2019-08-27T04%3A38%3A57Z&se=2026-08-28T04%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=unGKnPOCic9oepFg0BzjFuGSvDfmP5F%2FcIzBsXsYxw4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/3.png?st=2019-08-27T04%3A39%3A26Z&se=2025-08-28T04%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uLqalbp658iQiUSpDD7gaUVc327GW6Jmq14lufsYKjM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/4.png?st=2019-08-27T04%3A39%3A47Z&se=2026-08-28T04%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nPhZOiNPzapOvYuHAK9JEew7eW5Zs4SibBjmM%2B879AY%3D)

2. In the Azure portal, in the Microsoft Edge window, start a **PowerShell** session within the **Cloud Shell**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/5.png?st=2019-08-27T10%3A56%3A38Z&se=2025-08-28T10%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l38Ey7Z%2FBmU%2BGKtiSiwT4v7mzZsN%2BOkosSnLLssmBEY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/6.PNG?st=2019-08-27T11%3A06%3A19Z&se=2025-08-28T11%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yOUnPZaVsjnpoG3HHPXH1UaTJBtD%2BYGLgknpu6V238U%3D)

3. If you are presented with the **You have no storage mounted** message, configure storage click on the **Show advanced settings**:

```
    
Subsciption: Select the default

Cloud Shell region: the name of the Azure region that is available in your subscription and which is closest to the lab location

Resource group:  {{ ResourceGroup }}

Storage account: a name of a new storage account

File share: cloudshell

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/7.PNG?st=2019-08-27T11%3A08%3A06Z&se=2025-08-28T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=scEyEX0lQxL010%2Fg1S2sCglUoU%2FXr0oFp%2FslJjLps3k%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/8.PNG?st=2019-08-27T11%3A08%3A38Z&se=2025-08-28T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mex0Ewh5yS2J%2Bf1WXWeNTMTHOV8i%2F0rJHgoPflE0PsQ%3D)


4. From the Cloud Shell pane, upload the Azure Resource Manager template 
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_01/azuredeploy06.json?st=2019-08-28T05%3A07%3A45Z&se=2025-08-29T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rrXBOlG6B5F7WxV4SjMwYQwaDEJVrgKRQ1ySDvBOnUI%3D
into the home directory.
use the below command to download the Azure resource manager template into the Cloud Shell pane home directory.

```

wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_01/azuredeploy06.json?st=2019-08-28T05%3A07%3A45Z&se=2025-08-29T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rrXBOlG6B5F7WxV4SjMwYQwaDEJVrgKRQ1ySDvBOnUI%3D"

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/9.PNG?st=2019-08-28T06%3A19%3A40Z&se=2025-08-29T06%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QGkjSB7sOIHDtnq%2B0kCDkLRpSck3K%2BBXccnsZDOCQFI%3D)

5. From the Cloud Shell pane, upload the parameter file https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_01/azuredeploy06.parameters.json?st=2019-08-28T05%3A08%3A15Z&se=2025-08-29T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LAkWPt37o5h3SNYOFe7x5ExzNcGpjWmswmpL3zQlS7g%3D into the home directory

```

wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_01/azuredeploy06.parameters.json?st=2019-08-28T05%3A08%3A15Z&se=2025-08-29T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LAkWPt37o5h3SNYOFe7x5ExzNcGpjWmswmpL3zQlS7g%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/10.PNG?st=2019-08-28T06%3A21%3A06Z&se=2025-08-29T06%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=X%2F3roLSddBfBqoqTrevUJd5PmQY3DWNuOyqWMUm6WVg%3D)

In Cloud Shell pane do the  **ls** to see the downloaded files.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/11.PNG?st=2019-08-28T06%3A29%3A49Z&se=2025-08-29T06%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gdM9bYT1yEGcOQCGBXGqW3bYG030JEwu86o52etnJDA%3D)

6. Run the below command to change the file names after downloading.

```

mv "azuredeploy06.json?st=2019-08-28T05%3A07%3A45Z&se=2025-08-29T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rrXBOlG6B5F7WxV4SjMwYQwaDEJVrgKRQ1ySDvBOnUI%3D" azuredeploy06.json

mv "azuredeploy06.parameters.json?st=2019-08-28T05%3A08%3A15Z&se=2025-08-29T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LAkWPt37o5h3SNYOFe7x5ExzNcGpjWmswmpL3zQlS7g%3D" azuredeploy06.parameters.json

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/12.PNG?st=2019-08-28T06%3A31%3A40Z&se=2025-08-29T06%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NrHx%2FRFVSxnEJ9hFcE5b1ZgxJZ0V2MWvXYyAFzA%2FgUA%3D)

7. From the Cloud Shell pane, deploy an Azure VM hosting Windows Server 2016 Datacenter by running:

```pwsh
New-AzResourceGroupDeployment -ResourceGroupName {{ ResourceGroup }} -TemplateFile azuredeploy06.json -TemplateParameterFile azuredeploy06.parameters.json
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/13.PNG?st=2019-08-28T06%3A26%3A45Z&se=2025-08-29T06%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FrdXZzscwv%2B1M4KZTXEUfQui5R3XwokV4LbdkzxaNm8%3D)

   > **Note**: Do not wait for the deployment to complete but instead proceed to the next task.

   > **Note**: If you are getting azuredeploy06.json not found, use -TemplateFile $HOME/azuredeploy06.json and -TemplateParameterFile $HOME/azuredeploy06.parameters.json

  ```
   New-AzResourceGroupDeployment -ResourceGroupName {{ ResourceGroup }} -TemplateFile $HOME/azuredeploy06.json -TemplateParameterFile $HOME/azuredeploy06.parameters.json
  
  ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/14.PNG?st=2019-08-28T06%3A27%3A36Z&se=2025-08-29T06%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LQnnBKWxPT9eylo79Sex48F1rmpOtmQ010Wy9IiEF%2Bw%3D)

### Task 2: Implement an Azure Site Recovery vault

1. From Azure Portal, create an instance of **Backup and Site Recovery (OMS)** Recovery Services vault with the following settings:

```

Name: vaultaz3000600

Subscription: Default

Resource group: {{ ResourceGroup }}

Location: the name of an Azure region that is available in your subscription and which is **different** from the region you deployed an Azure VM in the previous task

 ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/15.png?st=2019-08-28T06%3A42%3A41Z&se=2025-08-29T06%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HvJNG3YQAB2GjHOpqv8E3ynQWlYWLigapk2ESih8xzc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/16.PNG?st=2019-08-28T06%3A50%3A08Z&se=2025-08-29T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1RkCc6MQjYgNblyD6%2BLd5nKo2DCmIIL%2F0uLv8g8Dics%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/lab4-Implementing%20Azure%20to%20Azure%20migration/17.PNG?st=2019-08-28T06%3A51%3A00Z&se=2025-08-29T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MOj9AFzcRJtZF5GVfMB2BXXA45K0R%2F0Xi4ZwAM6NSDs%3D)

2. Wait until the vault is provisioned. This will take about a minute.

**Result**: After you completed this exercise, you have created an Azure VM to be migrated and an Azure Site Recovery vault that will host the migrated disk files of the Azure VM.

## Exercise 2: Migrate an Azure VM between Azure regions by using Azure Site Recovery

The main tasks for this exercise are as follows:

1. Configure Azure VM replication

2. Review Azure VM replication settings

3. Disable replication of an Azure VM and delete the Azure Recovery Services vault

### Task 1: Configure Azure VM replication

1. In the the Azure portal, navigate to the blade of the newly provisioned Azure Recovery Services vault.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/10.png?token=AGFEA6CT2RERE2KPAUA3HS25PCDSE" alt="image-alt-text" >

2. On the Recovery Services vault blade, click the **+ Replicate** button.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/11.png?token=AGFEA6HMEJW7V75LBCX2HWK5PCDSI" alt="image-alt-text" >

3. Enable replication by specifying the following settings:

```

Source: **Azure**

Source location: {{ location }}

Azure virtual machine deployment model: **Resource Manager**

Source resource group: {{ ResourceGroup }}

Virtual machines: az3000601-vm

Target location: the name of an Azure region that is available in your subscription and which is different from the region you deployed an Azure VM in the previous task

Target resource group: (new) az3000601-LabRG-asr

Target virtual network: (new) az3000601-vnet-asr

Cache storage account: accept the default setting

Replica managed disks: (new) 1 premium disk(s), 0 standard disk(s)

Target availability sets: Not Applicable

Replication policy: Create new

Name: 12-hour-retention-policy

Recovery point retention: 12 Hours

App consistent snapshot frequency: 6 Hours

Multi-VM consistency: No

```

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/12.png?token=AGFEA6H7EJLNWBPEAHQ5WCK5PCDSM" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/13.png?token=AGFEA6GZCB723WYGQKHDR5C5PCDSS" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/14.png?token=AGFEA6G3PBIQ32WYW7NSDBC5PCDSW" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/15.png?token=AGFEA6EASNXM2GMANYGMS3K5PCDS4" alt="image-alt-text" >

4. Initiate creation of target resources.

5. Enable the replication.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/16.png?token=AGFEA6FTUYYNG2I2EPAI3MC5PCDTA" alt="image-alt-text" >

   > **Note**: Wait for the operation of enabling the replication to complete. Then proceed to the next task.

### Task 2: Review Azure VM replication settings

1. In the Azure portal, from the Azure Site Recovery vault blade, navigate to the replicated item blade representing the Azure VM **az3000601-vm**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/17.png?token=AGFEA6CF4LYE5Y5YIQDHK6C5PCDTM" alt="image-alt-text" >

2. On the replicated item blade, review the **Health and status**, **Latest available recovery points**, and **Failover readiness** sections. Note the **Failover** and **Test Failover** entries in the toolbar. Scroll down to the **Infrastructure view**.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/18.png?token=AGFEA6FHVQHKBLQT3TDGQRS5PCDTQ" alt="image-alt-text" >

**Latest Recovery**:

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/19.png?token=AGFEA6CFNJICEVAWQDA5SUC5PCDTU" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/20.png?token=AGFEA6EGM5YIKC4S2FK2ABK5PCDTY" alt="image-alt-text" >

3. If time permits, wait until the status of the Azure VM changes to **Protected**. This might take additional 15-20 minutes. At that point, examine the values **Crash-consistent** and **App-consistent** recovery points. In order to view **RPO**, you should perform a test failover.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/21.png?token=AGFEA6CPMU4V3OXNNGEAGQS5PCDT6" alt="image-alt-text" >

### Task 3: Disable replication of an Azure VM and delete the Azure Recovery Services vault

1. In the Azure portal, disable replication of the Azure VM **az3000601-vm**.

2. Wait until the replication is disabled.

3. From the Azure portal, delete the Recovery Services vault.

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/22.png?token=AGFEA6DPEB2KNUEDMHH37AC5PCDUC" alt="image-alt-text" >

<img src="https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Images/Lab4/23.png?token=AGFEA6FZYM4OBMRZYV5CBM25PCDUG" alt="image-alt-text" >

   > **Note**: You must ensure that the replicated item is removed first before you can delete the vault.

**Result**: After you completed this exercise, you have implemented automatic replication of an Azure VM.
