## Lab 7: Implement Azure Site Recovery between Azure regions 

## Table of Contents 

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Implement prerequisites for migration of Azure VMs by using Azure Site Recovery](#exercise-1-implement-prerequisites-for-migration-of-azure-vms-by-using-azure-site-recovery)
   
[Exercise 2: Migrate an Azure VM between Azure regions by using Azure Site Recovery](#exercise-2-migrate-an-azure-vm-between-azure-regions-by-using-azure-site-recovery)
    
[Exercise 3: Remove lab resources](#exercise-3-remove-lab-resources)    
    

## Overview

The main aim of the lab is Azure Resource Manager template to deploy Azure VM and create Azure Site Recovery Vault. Azure site recovery vault to replicate content in azure VM disk and configure azure VM replication and replication settings.

### Scenario and Objectives

XYZ training labs corporation wants to implement Azure Site Recovery to facilitate migration and protection of Azure VMs between regions

After completing this lab, you will be able to:

- Implement Azure Site Recovery Vault
- Configure replication of Azure VMs between Azure regions by using Azure Site RecoveryLab files:

## Pre-Requisites

- **ARM Template**

All tasks in this lab are performed from the Azure portal Lab files:

- **https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Allfiles/Labfiles/Module_07/Azure_Site_Recovery_Between_Regions/az-101-01_azuredeploy.json?token=AHM6QYF4LEU2G2ULKTM42OS5LJZFC**

- **https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Allfiles/Labfiles/Module_07/Azure_Site_Recovery_Between_Regions/az-101-01_azuredeploy.parameters.json?token=AHM6QYDG3EQCKA7IGBZB3EC5LJZFG**

## Exercise 1: Implement prerequisites for migration of Azure VMs by using Azure Site Recovery

The main tasks for this exercise are as follows:

1. Deploy an Azure VM to be migrated by using an Azure Resource Manager template
2. Create an Azure Recovery Services vault

- **Azure Site Recovery Vault**

Azure Site Recovery (ASR) is a DRaaS offered by Azure for use in cloud and hybrid cloud architectures. As a disaster recovery platform, it makes it possible for Azure Virtual Machines, Hyper-V, physical on-prem systems, and VMWare to failover to and successfully failback once the disaster has been resolved. A near-constant data replication process makes sure copies are in sync.

- **Remote Desktop**

Remote desktop is a program or an operating system feature that allows a user to connect to a computer in another location, see that computer&#39;s desktop and interact with it as if it were local.

People use remote desktop access capabilities to do a variety of things, including the following:

1. Access a workplace computer from home or when traveling.
2. Access a home computer from other locations.
3. Fix a computer problem.
4. Perform administrative tasks.
5. Demonstrate something, such as a process or a software application

- **Cloud Shell**

Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work. Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.

### Task 1: Deploy an Azure VM to be migrated by using an Azure Resource Manager template

1. From the lab,after the chrome is opened browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com/) and sign in by using a Microsoft account that has the Owner role in the Azure subscription you intend to use in this lab.
2. In the Azure portal, navigate to the  **Create a resource**  blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/1.png?token=AK4K6SAXEI3ZAU456C72KMK5OIDKC)

3. From the  **Create a resource**  blade, search Azure Marketplace for  **Template deployment**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/2.png?token=AK4K6SCTJDVWWB6M5IZ43JS5OIDMW)
 
4. Use the list of search results to navigate to the  **Deploy a custom template**  blade.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/3.png?token=AK4K6SAE67LHJKARHD2V67K5OIDNU)

5. On the  **Custom deployment**  blade, click the  **Build your own template in the editor**  link. If you do not see this link, click  **Edit template**  instead.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/4.png?token=AK4K6SAKYY6SC5HOSKCHWJS5OIDOS)

6. From the  **Edit template**  blade, load the template file  **Labfiles\Module\_07\Azure\_Site\_Recovery\_Between\_Regions\az-101-01\_azuredeploy.json**.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/5.png?token=AK4K6SA22D743QQIGWIEE425OIDPU)

**Note:** Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.

7. Save the template and return to the  **Custom deployment**  blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/6.png?token=AK4K6SFKH7TAG77JEHE2B4S5OIDQW)

 
8. From the  **Custom deployment**  blade, navigate to the  **Edit parameters**  blade.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/7.png?token=AK4K6SGEXMW6PHHPYNQWR225OIDR2)


9. From the  **Edit parameters**  blade, load the parameters file  **Labfiles\Module\_07\Azure\_Site\_Recovery\_Between\_Regions\az-101-01\_azuredeploy.parameters.json**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/8.png?token=AK4K6SGDNOZCWU3YPENT6425OIDTK)
 
10. Save the parameters and return to the  **Custom deployment**  blade.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/9.png?token=AK4K6SBZXLFW7VKBG3QU4TS5OIDUI)

11. From the  **Custom deployment**  blade, initiate a template deployment with the following settings:

   - Subscription: the name of the subscription you are using in this lab
   - Resource group: the name of a new resource group  **az1010101-RG**
   - Location: the name of the Azure region which is closest to the lab location and where you can provision Azure VMs
   - Vm Name:  **az1010101-vm**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/10.png?token=AK4K6SAY6XVQ5EZUARWXETC5OIDVM)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/11.png?token=AK4K6SF4DDY3XMM3VUFRPNC5OIDWO)

**Note:** To identify Azure regions where you can provision Azure VMs, refer to [**https://azure.microsoft.com/en-us/regions/offers/**](https://azure.microsoft.com/en-us/regions/offers/)

**Note:** Do not wait for the deployment to complete but proceed to the next task. You will use the virtual machine  **az1010101-vm**  in the second exercise of this lab.

### Task 2: Implement an Azure Site Recovery vault

1. In the Azure portal, navigate to the  **Create a resource**  blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/12.png?token=AK4K6SAJA5LGRDUWF4WHA4S5OIDX4)

 
2. From the  **Create a resource**  blade, search Azure Marketplace for **Backup and Site Recovery (OMS)**.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/13.png?token=AK4K6SDPRKL65LW6K6JEV7C5OID3Q)


3. Use the list of search results to navigate to the  **Recovery Services vault**  blade.
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/14.png?token=AK4K6SB6TSC4YL57ORDBVKS5OID4S)

 
4. Use the  **Recovery Services vault**  blade, to create a Site Recovery vault with the following settings:

   - Name:  **vaultaz1010102**
   - Subscription: the same Azure subscription you used in the previous task of this exercise
   - Resource group: the name of a new resource group  **az1010102-RG**
   - Location: the name of an Azure region that is available in your subscription and which is different from the region you deployed the Azure VM in the previous task of this exercise

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/15.png?token=AK4K6SE7QCARWVJJR3HITU25OID5Q)

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/16.png?token=AK4K6SFXWAY5L73BVCHIO2K5OID6Q)

**Result:** After you completed this exercise, you have initiated deployment of an Azure VM by using an Azure Resource Manager template and created an Azure Site Recovery vault that will be used to replicate content of the Azure VM disk files.

## Exercise 2: Migrate an Azure VM between Azure regions by using Azure Site Recovery

The main tasks for this exercise are as follows:

1. Configure Azure VM replication
2. Review Azure VM replication settings

### Task 1: Configure Azure VM replication

**Note:** Before you start this task, ensure that the template deployment you started in the first exercise has completed.

1. In the Azure portal, navigate to the blade of the newly provisioned Azure Recovery Services vault  **vaultaz1010102**.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/17.png?token=AK4K6SCGLLG2TWZZCD7GKFC5OID7W)


2. From the  **vaultaz1010102**  blade, configure the following replication settings:

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/18.png?token=AK4K6SGLOH7Y7NENQLTAVLC5OIEBM)

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/19.png?token=AK4K6SEHY5SIJILVD3RBON25OIECI)

   - Source:  **Azure**
   - Source location: the same Azure region into which you deployed the Azure VM in the previous exercise of this lab
   - Azure virtual machine deployment model:  **Resource Manager**
   - Source subscription: the same Azure subscription you used in the previous exercise of this lab
   - Source resource group:  **az1010101-RG**
   - Virtual machines:  **az1010101-vm**
   - Target location: the name of an Azure region that is available in your subscription and which is different from the region you deployed an Azure VM in the previous task. If possible, use the same Azure region     into which you deployed the Azure Site Recovery vault.
   - Target resource group: **(new) az1010101-RG-asr**
   - Target virtual network: **(new) az1010101-vnet-asr**
   - Cache storage account: accept the default setting
   - Replica managed disks: **(new) 1 premium disk(s), 0 standard disk(s)**
   - Target availability sets:  **Not Applicable**
   - Replication policy: the name of a new replication policy  **12-hour-retention-policy**
   - Recovery point retention:  **12 Hours**
   - App consistent snapshot frequency:  **6 Hours**
   - Multi-VM consistency:  **No**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/20.png?token=AK4K6SFBUS3E2GHLSTZZKHK5OIEDK)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/21.png?token=AK4K6SH67HZ2R3W637ZQGTK5OIEEG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/22.png?token=AK4K6SHIBEY5RWPHM7NNCNC5OIEFA)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/23.png?token=AK4K6SDLBHWKFIZFMS7DHHS5OIEF4)

 
3. From the  **Configure settings**  blade, initiate creation of target resources and wait until you are redirected to the  **Enable replication**  blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/24.png?token=AK4K6SCNQJASFPC4XQMK4JK5OIEGW)

 
4. From the  **Enable replication**  blade, enable the replication.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/25.png?token=AK4K6SDADVDLLY7DLADYTRC5OIEHS)

 
### Task 2: Review Azure VM replication settings

1. In the Azure portal, navigate to the  **vaultaz1010102 - Replicated items**  blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/26.png?token=AK4K6SC77PS6XROBHYMH6D25OIELO)


2. On the  **vaultaz1010102 - Replicated items**  blade, ensure that there is an entry representing the  **az1010101-vm**  Azure VM and verify that its  **REPLICATION HEALTH**  is  **Healthy**  and that its  **STATUS**  is  **Enabling protection**.

 ![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/27.png?token=AK4K6SALNM6ORS4I46ZT7QS5OIEMS)


3. From the  **vaultaz1010102 - Replicated items**  blade, display the replicated item blade of the  **az1010101-vm**  Azure VM.


![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/28.png?token=AK4K6SDCEHHWH6266ZO6YPK5OIENS)

 
4. On the  **az1010101-vm**  replicated item blade, review the  **Health and status** ,  **Failover readiness** ,  **Latest recovery points** , and  **Infrastructure view**  sections. Note the  **Failover**  and  **Test Failover**  toolbar icons.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/29.png?token=AK4K6SHU426MJKL3UDHGPBS5OIEOQ)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/30.png?token=AK4K6SBOQG7BKHIPHI7553K5OIEPO)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/31.png?token=AK4K6SFSQR5ZXRTLW5MW3NK5OIEQS)


 
**Note:** The remaining steps of this task are optional and not graded.

5. If time permits, wait until the replication status changes to  **100% synchronized**. This might take additional 90 minutes.
6. Examine the values of  **RPO** , as well as  **Crash-consistent**  and  **App-consistent**  recovery points.
7. Perform a test failover to the  **az1010101-vnet-asr**  virtual network.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/32.png?token=AK4K6SA6EB5L6NOTW73W3MS5OIERY)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/33.png?token=AK4K6SHT4IM4PM37HH4JZVS5OIESU)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/34.png?token=AK4K6SED22LAG3UXO6J2RAC5OIETY)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/35.png?token=AK4K6SBBV2ABXOM27TIGZSS5OIEUU)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/36.png?token=AK4K6SFGOEJSTRX6MG2KOJS5OIEVS)


 **Result:** After you completed this exercise, you have configured replication of an Azure VM and reviewed Azure VM replication settings.

## Exercise 3: Remove lab resources

### Task 1: Open Cloud Shell

1. At the top of the portal, click the  **Cloud Shell**  icon to open the Cloud Shell pane.
2. At the Cloud Shell interface, select  **Bash**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/37.png?token=AK4K6SA6QXEIMKP5ANFBIYK5OIEWQ)

3. At the  **Cloud Shell**  command prompt, type in the following command and press  **Enter**  to list all resource groups you created in this lab:

az group list --query &quot;[?starts\_with(name,&#39;az10101&#39;)].name&quot; --output tsv

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/38.png?token=AK4K6SF2GC66WXCZWBXIC3C5OIEXQ)

 
4. Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

### Task 2: Delete resource groups

1. At the  **Cloud Shell**  command prompt, type in the following command and press  **Enter**  to delete the resource groups you created in this lab

         az group list --query &quot;[?starts\_with(name,'az10101')].name&quot; --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab7/39.png?token=AK4K6SBBH3W6FSHQLOEY46K5OIEYY)

**Note:** If you encounter an error similar to &quot;...cannot perform delete operation because following scope(s) are locked...&quot; then you need to run the following steps to remove the lock on the resource that prevents its deletion:

     lockedresource=$(az resource list --resource-group az1010101-RG-asr --resource-type Microsoft.Compute/disks --query &quot;[?starts\_with(name,'az10101')].name&quot; --output tsv)

     az disk revoke-access -n $lockedresource --resource-group az1010101-RG-asr

     lockid=$(az lock show --name ASR-Lock --resource-group az1010101-RG-asr --resource-type Microsoft.Compute/disks --resource-name $lockedresource --output tsv --query id)

     az lock delete --ids $lockid

     az group list --query &quot;[?starts\_with(name,'az10101')].name&quot; --output tsv | xargs -L1 bash -c &#39;az group delete --name $0 --no-wait --yes';

2. Close the  **Cloud Shell**  prompt at the bottom of the portal.

**Result:** In this exercise, you removed the resources used in this lab.
