# Lab 12: Implement Azure File Sync

**Table of Contents**

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Prepare the lab environment](#exercise-1-prepare-the-lab-environment)

[Exercise 2: Prepare Azure File Sync infrastructure](#exercise-2-prepare-azure-file-sync-infrastructure)

[Exercise 3: Prepare Azure File Sync infrastructure](#exercise-3-prepare-azure-file-sync-infrastructure)

## Overview

Use Azure File Sync to centralize your organization's file shares in Azure Files, while keeping the flexibility, performance, and compatibility of an on-premises file server. Azure File Sync transforms Windows Server into a quick cache of your Azure file share. You can use any protocol that's available on Windows Server to access your data locally, including SMB, NFS, and FTPS. You can have as many caches as you need across the world.

**Scenario and Objectives**

**XYZ Training Corporation** hosts its file shares in on-premises file servers. Considering its plans to migrate majority of its workloads to Azure, Adatum is looking for the most efficient method to replicate its data to file shares that will be available in Azure. To implement it, Adatum will use Azure File Sync.

After completing this lab, you will be able to:

-	Deploy an Azure VM by using an Azure Resource Manager template

-	Prepare Azure File Sync infrastructure

-	Implement and validate Azure File Sync 

## Pre-requisites:

-	ARM Template
-	An Azure file share in the same region that you want to deploy Azure File Sync. For more information, see:

*	Region availability for Azure File Sync.

*	Create a file share for a step-by-step description of how to create a file share.

-	At least one supported instance of Windows Server or Windows Server cluster to sync with Azure File Sync.

-	**Remote Desktop**

*	Remote desktop is a program or an operating system feature that allows a user to connect to a computer in another location, see that computer's desktop and interact with it as if it were local.

*	People use remote desktop access capabilities to do a variety of things, including the following:

*	Access a workplace computer from home or when traveling.

*	Access a home computer from other locations.

*	Fix a computer problem.

*	Perform administrative tasks.

*	Demonstrate something, such as a process or a software application

-	**Windows PowerShell ISE**

The Windows PowerShell Integrated Scripting Environment (ISE) is a host application for Windows PowerShell. In the ISE, you can run commands and write, test, and debug scripts in a single Windows-based graphic user interface. The ISE provides multiline editing, tab completion, syntax coloring, selective execution, context-sensitive help, and support for right-to-left languages. Menu items and keyboard shortcuts are mapped to many of the same tasks that you would do in the Windows PowerShell console. 

## Exercise 1: Prepare the lab environment

The main tasks for this exercise are as follows:

1.	Deploy an Azure VM by using an Azure Resource Manager template

### Task 1: Deploy an Azure VM by using an Azure Resource Manager template

1.	From the lab virtual machine, start **Microsoft Edge**, browse to the Azure portal at **http://portal.azure.com** and sign in by using a **Microsoft account** that has the Owner role in the Azure subscription you intend to use in this lab.

2.	In the Azure portal, navigate to the New blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/1.png?token=AEMYGFOLJJ67436LYXZBA625LPTTQ)

3.	From the New blade, search Azure Marketplace for **Template deployment**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/2.png?token=AEMYGFOB63AEIIJMHIK5F5K5LPTX6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/3.png?token=AEMYGFLCB2N37GA5HESLT3S5LPUAU)

4.	Use the list of search results to navigate to the **Custom deployment** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/4.png?token=AEMYGFN2LZE7ZFRHXTGDCVS5LPUDI)

5.	On the **Custom deployment** blade, select the **Build your own template in the editor**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/5.png?token=AEMYGFOMNSSR6H7NY464Q7K5LPUGS) 

6.	From the **Edit template** blade, load the template file **az-100-02b_azuredeploy.json**.

**Note:** Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter with a single data disk.

7.	Save the template and return to the **Custom deployment** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/6.png?token=AEMYGFJSS6QXVZZFJFJAGG25LPULK)

8.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/7.png?token=AEMYGFKNIGHEWXO563L4R4S5LPUOS)

9.	From the **Edit parameters** blade, load the parameters file **az-100-02b_azuredeploy.parameters.json**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/8.png?token=AEMYGFLWWIGON5XPT24IVM25LPVQU)

10.	Save the parameters and return to the **Custom deployment** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/9.png?token=AEMYGFJYX3PXEWJELGDVCZK5LPVTI)

11.	From the **Custom deployment** blade, initiate a template deployment with the following settings:

-	Subscription: the name of the subscription you are using in this lab
-	Resource group: the name of a new resource group **az1000201b-RG**
-	Location: the name of the Azure region which is closest to the lab location and where you can provision Azure VMs
-	Vm Size: **Standard_DS1_v2**
-	Vm Name: **az1000201b-vm1**
-	Admin Username: **adminuser**
-	Admin Password: **Password@1234**
-	Virtual Network Name: **az1000201b-vnet1**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/10.png?token=AEMYGFKW7PQ4A3Q35HCS7XC5LPVZ6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/11.png?token=AEMYGFOVUXZCLFSLSMKJ6A25LPV3E)

**Note:** To identify Azure regions where you can provision Azure VMs, refer to https://azure.microsoft.com/en-us/regions/offers/

**Note:** Do not wait for the deployment to complete but proceed to the next exercise. You will use the virtual machine included in this deployment in the next exercise of this lab.

**Note:** Keep in mind that the purpose of Azure VM az1000201b-vm1 is to emulate an on-premises file server in our scenario.

**Result:** After you completed this exercise, you have initiated a template deployment of an Azure VM az1000201b-vm1 that you will use in the next exercise of this lab.

## Exercise 2: Prepare Azure File Sync infrastructure

The main tasks for this exercise are as follows:

1.	Create an Azure Storage account and a file share

2.	Prepare Windows Server 2016 for use with Azure File Sync

3.	Run Azure File Sync evaluation tool

### Task 1: Create an Azure Storage account and a file share

1.	In the Azure portal, navigate to the **New blade**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/12.png?token=AEMYGFOBJOJYK4E2XESDNYK5LPWC6)

2.	From the **New blade**, search Azure Marketplace for **Storage account - blob, file, table, queue**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/13.png?token=AEMYGFPZQSWSQCMMA4JL2A25LPWF2)

3.	Use the list of search results to navigate to the **Create storage account** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/14.png?token=AEMYGFLO7E6SAPD4JFWR2YC5LPWII)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/15.png?token=AEMYGFIEAFQV53TV5CYLJVS5LPWJK)

4.	From the **Create storage account** blade, create a new storage account with the following settings:

-	Subscription: the same subscription you selected in the previous task
-	Resource group: the name of a new resource group **az1000202b-RG**
-	Storage account name: any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits
-	Location: the name of the Azure region which you selected in the previous task
-	Performance: **Standard**
-	Account kind: **Storage (general purpose v1)**
-	Replication: **Locally-redundant storage (LRS)**
-	Secure transfer required: **Disabled**
-	Allow access from: **All networks**
-	Hierarchical namespace: **Disabled**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/16.png?token=AEMYGFL4USB3P3VDRUVBRQC5LPWP4) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/17.png?token=AEMYGFMUNKSKNV6DYTSZBVC5LPWQ6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/18.png?token=AEMYGFNI3L6ESUKG2KHNFDK5LPWS4)

**Note:** Wait for the storage account to be provisioned but proceed to the next step.

5.	In the Azure portal, navigate to the blade representing the newly provisioned storage account.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/19.png?token=AEMYGFIEXXNU44ROFAQCH7K5LPWVO)

6.	From the storage account blade, display the properties of its File Service.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/20.png?token=AEMYGFPKKE7RL42RROKUQV25LPWXY) 

7.	From the storage account **Files** blade, create a new file share with the following settings:

-	Name: **az10002bshare1**
-	Quota: **none**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/21.png?token=AEMYGFP2C6YNG6Y7O54Q2PC5LPW34)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/22.png?token=AEMYGFJSTHFQBQWUPGNOBIC5LPW5Q)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/23.png?token=AEMYGFL7Q5YNEF4RWYLTEW25LPW6W)         

### Task 2: Prepare Windows Server 2016 for use with Azure File Sync

**Note:** Before you start this task, ensure that the template deployment you started in Exercise 0 has completed.

1.	In the Azure portal, navigate to the **az1000201b-vm1** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/24.png?token=AEMYGFNPSPIZ6N7CTSX56T25LPXBU)

2.	From the **az1000201b-vm1** blade, connect to the Azure VM via the RDP protocol and, when prompted to sign in, provide the following credentials:

-	Admin Username: **adminuser**
-	Admin Password: **Password@1234**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/25.png?token=AEMYGFOFUECBMCO3E6Q3UYC5LPXF4) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/26.png?token=AEMYGFPF5J6S57YTDUXKXDS5LPXHA) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/27.png?token=AEMYGFMML5H3PRQORQ4TFNC5LPXH4)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/28.png?token=AEMYGFNJXMVQX5KESYV5L725LPXIY)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/29.png?token=AEMYGFPJA5P5JSG3PHICRBK5LPXJW)

3.	Within the RDP session to the Azure VM, in Server Manager, navigate to **File and Storage Services**, locate the data disk attached to the Azure VM, initialize it as a **GPT disk**, and use **New Volume Wizard** to create a single volume occupying entire disk with the following settings:

-	Drive letter: **S**
-	File system: **NTFS**
-	Allocation unit size: **Default**
-	Volume label: **Data**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/30.png?token=AEMYGFOQVL2CNCYKWWS563S5LPXTI)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/31.png?token=AEMYGFML3DGTQ2WDFR7VN6K5LPXUK)     

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/32.png?token=AEMYGFNNEJCE364RKMH7IMS5LPXVI) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/33.png?token=AEMYGFKH4HPEUPEUZTMFJB25LPXWK) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/34.png?token=AEMYGFN4EVK65Z2L5JHH32S5LPXXK) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/35.png?token=AEMYGFJGGN3NRCMPXS5KO7C5LPXYM) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/36.png?token=AEMYGFORFHUPO27GI45BVWK5LPXZQ)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/37.png?token=AEMYGFPBP6MHUTCLS723TQK5LPX2O)     

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/38.png?token=AEMYGFNT5UBJZGMJKCWO4DC5LPX3O)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/39.png?token=AEMYGFOHKI4U3ZBDH4E6DSS5LPX4W)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/40.png?token=AEMYGFIV4JDPOVEGP4I5ZOS5LPX5W)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/41.png?token=AEMYGFK5BGCHITFTNDPST725LPX6U)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/42.png?token=AEMYGFPSISDKQMTKNPP4W2C5LPX7S)       

4.	Within the RDP session, start a Windows PowerShell session as administrator.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/43.png?token=AEMYGFLJZPKLNESHSWBFQ3K5LPYQU)

5.	From the Windows PowerShell console, set up a file share by running the following:

$directory = New-Item -Type Directory -Path 'S:\az10002bShare'

New-SmbShare -Name $directory.Name -Path $directory.FullName -FullAccess 'Administrators' -ReadAccess Everyone   

Copy-Item -Path 'C:\WindowsAzure\*' -Destination $directory.FullName –Recurse

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/44.png?token=AEMYGFJIAJQZCQLACHYPQKK5LPYOW)

**Note:** To populate the file share with sample data, we use content of the C:\WindowsAzure folder, which should contain about 100 MB worth of files

6.	From the Windows PowerShell console, install the latest Az PowerShell module by running the following:

Install-Module -Name Az -AllowClobber

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/45.png?token=AEMYGFJD5K4UZW34NS73N4K5LPYWE)

**Note:** When prompted, confirm that you want to proceed with the installation from PSGallery repository.

### Task 3: Run Azure File Sync evaluation tool

1.	Within the RDP session to the Azure VM, from the Windows PowerShell console, install the latest version of Package Management and PowerShellGet by running the following:

Install-Module -Name PackageManagement -Repository PSGallery -Force

Install-Module -Name PowerShellGet -Repository PSGallery -Force

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/46.png?token=AEMYGFPM5IRXEZLG3HFB6O25LPY26)

**Note:** When prompted, confirm that you want to proceed with the installation of the NuGet provider.

2.	Restart the PowerShell session.

3.	From the Windows PowerShell console, install the Azure File Sync PowerShell module by running the following:

Install-Module -Name Az.StorageSync -AllowClobber -Force

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/47.png?token=AEMYGFIGFKER3VCJTX65J425LPY5S)

4.	From the Windows PowerShell console, install the Azure File Sync PowerShell module by running the following:

Invoke-AzStorageSyncCompatibilityCheck -Path 'S:\az10002bShare'

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/48.png?token=AEMYGFJVUSP7T6KDBIBDD4S5LPY7Q)

5.	Review the results and verify that no compatibility issues have been found.

**Result:** After you completed this exercise, you have created an Azure Storage account and a file share, prepare Windows Server 2016 for use with Azure File Sync, and run Azure File Sync evaluation tool

## Exercise 3: Prepare Azure File Sync infrastructure

The main tasks for this exercise are as follows:

1.	Deploy the Storage Sync Service

2.	Install the Azure File Sync Agent

3.	Register the Windows Server with Storage Sync Service

4.	Create sync groups and a cloud endpoint

5.	Create a server endpoint

6.	Validate Azure File Sync operations

### Task 1: Deploy the Storage Sync Service

1.	Within the RDP session to the Azure VM, in Server Manager, navigate to the Local Server view and turn off temporarily **IE Enhanced Security Configuration**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/49.png?token=AEMYGFMZD5Q6NJIXMDDFO4K5LPZEO)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/50.png?token=AEMYGFPUR3UKDXIEAMA5BH25LPZGA)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/51.png?token=AEMYGFIW4LEREKUOPON575K5LPZHG)         

2.	Within the RDP session to the Azure VM, start Internet Explorer, browse to the Azure portal at http://portal.azure.com and sign in by using the same Microsoft account you used previously in this lab.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/52.png?token=AEMYGFJSJLAYOUJT3LUSTQK5LPZJS)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/53.png?token=AEMYGFPPIGMUKC4B5HABG6S5LPZKU)     

3.	In the Azure portal, navigate to the **New** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/54.png?token=AEMYGFMGLO4UERESSKGKJKC5LPZOI) 

4.	From the **New** blade, search Azure Marketplace for **Azure File Sync**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/55.png?token=AEMYGFO66UC2P7ILJFODI7S5LPZPM) 

5.	Use the list of search results to navigate to the **Deploy Storage Sync** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/56.png?token=AEMYGFIKVEAQYTL2N4TEBIK5LPZR6)

6.	From the **Deploy Storage Sync** blade, create a Storage Sync Service with the following settings:

-	Name: **az1000202b-ss**
-	Subscription: the same subscription you selected in the previous task
-	Resource group: the name of a new resource group **az1000203b-RG**
-	Location: the name of the Azure region in which you created the storage account earlier in this exercise

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/57.png?token=AEMYGFLC5F57SROMEQ6DCYC5LPZV2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/58.png?token=AEMYGFPOTXJRAE4OGUOIDRK5LPZW2)

### Task 2: Install the Azure File Sync Agent.

1.	Within the RDP session, start another instance of Internet Explorer, browse to Microsoft Download Center at **https://go.microsoft.com/fwlink/?linkid=858257** and download the Azure File Sync Agent Windows Installer file **StorageSyncAgent_V6_WS2016.msi**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/59.png?token=AEMYGFOSFCIFS24X6YUK6DS5LPZ3A)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/60.png?token=AEMYGFOCATSCCUP5K2AEIVS5LPZ4S)     

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/61.png?token=AEMYGFIJFR3OZMSZEF2U2OS5LPZ5U)    

2.	Once the download completes, run the Storage Sync Agent Setup wizard with the default settings to install Azure File Sync Agent.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/62.png?token=AEMYGFPE4SFSXL3D2VYW2MK5LP2AS) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/63.png?token=AEMYGFKLMCNLXUTGRVGM54K5LP2BU) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/64.png?token=AEMYGFJH535QPQH2W2RXBQC5LP2CS)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/65.png?token=AEMYGFMQUCMCGKADHSNJ2MK5LP2DO)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/66.png?token=AEMYGFMZR2NVR4D4RI2X6D25LP2EO)

3.	After the Azure File Sync agent installation completes, the **Azure File Sync - Server Registration** wizard will automatically start.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/67.png?token=AEMYGFKODB3SMBRZ7GSHTW25LP2GW)

### Task 3: Register the Windows Server with Storage Sync Service

1.	From the initial page of the **Azure File Sync - Server Registration** wizard, sign in by using the same Microsoft account you used previously in this lab.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/68.png?token=AEMYGFOT6PCJXWOEX6KU4MS5LP2J2)

2.	On the **Choose a Storage Sync Service*** page of the **Azure File Sync - Server Registration** wizard, specify the following settings to register:

-	Azure Subscription: the name of the subscription you are using in this lab
-	Resource group: **az1000203b-RG**
-	Storage Sync Service: **az1000202b-ss**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/69.png?token=AEMYGFNAJLXDU73RNEHJ3YC5LP2OG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/70.png?token=AEMYGFKD7654KGHQHWYDRYS5LP2PK)

3.	When prompted, sign in again by using the same Microsoft account you used previously in this lab.

### Task 4: Create a sync group and a cloud endpoint

1.	Within the RDP session to the Azure VM, in the Azure portal, navigate to the **az1000202b-ss** Storage Sync Service blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/71.png?token=AEMYGFPBDZHZUOWQLCI4FGC5LP2SG)

2.	From the **az1000202b-ss** Storage Sync Service blade, navigate to the **Sync group blade** and create a new sync group with the following settings:

•	Sync group name: **az1000202b-syncgroup1**
•	Azure Subscription: the name of the subscription you are using in this lab
•	Storage account: the resource id of the storage account you created in the previous exercise
•	Azure File Share: **az10002bshare1**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/72.png?token=AEMYGFIPRWCH56SDBP6S5HS5LP2VW) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/73.png?token=AEMYGFNBJZMONNRDHTRUS6C5LP2W6)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/74.png?token=AEMYGFJA3AAKIZ4ZWZ5J7ES5LP2ZU)     

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/75.png?token=AEMYGFMHDDBM2MWGG7ABLW25LP222)    

### Task 5: Create a server endpoint

1.	Within the RDP session to the Azure VM, in the Azure portal, from the **az1000202b-ss** Storage Sync Service blade, navigate to the **az1000202b-syncgroup1** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/76.png?token=AEMYGFNN3RAJMVWLGICQ5D25LP26E)

2.	From the **az1000202b-syncgroup1** blade, navigate to the **Add server** endpoint blade and create a new server **endpoint** with the following settings:

-	Registered server: **az1000201b-vm1**
-	Path: **S:\az10002bShare**
-	Cloud Tiering: **Enabled**

1.	Always preserve the specified percentage of free space on the volume: **15**

2.	Only cache files that were accessed or modified within the specified number of days: **30**

-	Offline Data Transfer: **Disabled**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/77.png?token=AEMYGFOXMIISJJM7XJUIV2C5LP3F4)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/78.png?token=AEMYGFO7H7F57LTUVPASDFS5LP3HI)     

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/79.png?token=AEMYGFKXWR35OEHCMLGLEQK5LP3IM)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/80.png?token=AEMYGFPZ6XN23Q77ACFYPVK5LP3JK)     

### Task 6: Validate Azure File Sync operations

1.	Within the RDP session to the Azure VM, in the Azure portal, monitor the health status of the server endpoint **az100021b-vm1** on the **az1000202b-syncgroup1** blade, as it changes from Provisioning to Pending and, eventually, to a green checkmark.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/81.png?token=AEMYGFMLT54KRGAONRWSXNK5LP3NU)

**Note:** You should be able to proceed to the next step after a few minutes.

2.	In the Azure portal, navigate to the blade for the storage account you created earlier in the lab, switch to the **Files** tab and then click **az10002bshare1**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/82.png?token=AEMYGFOR7FHOP2FS4JNLMUC5LP3RI)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/83.png?token=AEMYGFIUBF24YSMXUYVPEH25LP3SK)

3.	On the **az10002bshare1** blade, click **Connect**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/84.png?token=AEMYGFJ3MONNLN2MEVTJ4FS5LP3U2)

4.	From the **Connect** blade, copy into Clipboard the PowerShell commands that connect to the file share from a Windows computer.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/85.png?token=AEMYGFN6FQKETL53UDT4OMK5LP3XC)

5.	Within the RDP session, start a Windows PowerShell ISE session.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/86.png?token=AEMYGFITOBCWVBUC6SP72BC5LP3Y4) 

6.	From the Windows PowerShell ISE session, open the script pane and paste into it the content of your local Clipboard.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/87.png?token=AEMYGFL23OBHKJKLHIT3WNS5LP33A)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/88.png?token=AEMYGFLFRJLPSWTPSQ3IRTS5LP342)

7.	Add the -Persist switch to the end of the line containing the New-PSDrive cmdlet.

8.	Execute the script and verify that its output confirms successful mapping of the Z: drive to the Azure Storage File Service share.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/89.png?token=AEMYGFKYXKQRB47OMVBI2K25LP36Y)

9.	Within the RDP session, start File Explorer, navigate to the Z: drive, and verify that it contains the same content as **S:\az10002bShare**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/90.png?token=AEMYGFNMMJ4LCD6V5G5UFOS5LP4AW)

10.	Display the Properties window of individual folders on the Z: drive, review the Security tab, and note that the entries represent NTFS permissions assigned to the corresponding folders on the S: drive.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab12/91.png?token=AEMYGFI6ZWBWZDCJX6CRCJS5LP4CE)

**Result:** After you completed this exercise, you have deployed the Storage Sync Service, installed the Azure File Sync Agent, registered the Windows Server with Storage Sync Service, created a sync group and a cloud endpoint, created a server endpoint, and validated Azure File Sync operations.
