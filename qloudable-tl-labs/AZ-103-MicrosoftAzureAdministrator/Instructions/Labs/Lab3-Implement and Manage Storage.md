# Implement and Manage Storage

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites) 

[Exercise 1: Prepare the Lab Environment](#exercise-1-prepare-the-lab-environment)

[Exercise 2: Implement and Use Azure Blob Storage](#exercise-2-implement-and-use-azure-blob-storage)

[Exercise 3: Implement and Use Azure File Storage](#exercise-3-implement-and-use-azure-file-storage)

## Overview

The Aim of this Lab is to Implement Azure Blob Storage and Manage Storage. In this lab you will create two Azure Storage Accounts, Review their Configuration Settings, Create a Blob Container, Upload Blobs into the Container, Copy the Container and Blobs between the Storage Accounts, and use a SAS key to Access one of the Blobs. 

In this Lab we are also Implement and Use Azure File Storage. you have Create an Azure File Service share, map a drive to the File share from an Azure VM, and use File Explorer from the Azure VM to create a folder and a file in the file share.

### Scenario& Objectives

XYZ Training Labs Corporation wants to leverage Azure Storage for hosting its data.

After completing this lab, you will be able to:

*	Deploy an Azure VM by using an Azure Resource Manager template

*	Implement and use Azure Blob Storage

*	Implement and use Azure File Storage

## Pre-requisites

1. Familiarity with Azure Portal

2. Familiarity with Remote Desktop Connection

3. Familiarity with Azure Virtual Machine (VM)

4. Familiarity with ARM Templates

All tasks in this lab are performed from the Azure Portal (including a PowerShell Cloud Shell session) except for Exercise 3 Task 2, which includes steps performed from a Remote Desktop session to an Azure VM

Note: When not using Cloud Shell, the lab Virtual Machine must have the Azure PowerShell 1.2.0 module (or newer) installed

Lab files:
* https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.json?st=2019-09-05T04%3A58%3A41Z&se=2025-09-06T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XaA%2Frfybo2Yt6YQigq1Pw1%2FsjLWSl6bsNvA6iGBsXmk%3D

* https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.parameters.json?st=2019-09-05T05%3A01%3A35Z&se=2025-09-06T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PEfg9bBv7zhFIm1CV1A3t1mJE5h7AoNw22qTi0GhGzk%3D


## Exercise 1: Prepare the Lab Environment

**Task 1: Deploy an Azure VM by using an Azure Resource Manager template**

1. Using the Chrome browser, login into Azure Portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/1.png?st=2019-09-05T05%3A06%3A55Z&se=2025-09-06T05%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=srwd16VfYobmWfr8DbUfTg0kKMcasXHnkv6bQvsKqko%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/2.png?st=2019-09-05T05%3A07%3A21Z&se=2025-09-06T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DkbB5GSIvWVYl0SCqI863mBTbJEl1e0avoImAkN2hFI%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/3.png?st=2019-09-05T05%3A07%3A57Z&se=2025-09-06T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Fm8vecWUsQO0HydYhPkYDqFoFM9ijuBj85BEoblB5tI%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/4.png?st=2019-09-05T05%3A09%3A07Z&se=2025-09-06T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lriFQO90wuKToAN9WDOlaYR8tDWoOqkk%2ByJfyZIuero%3D" alt="image-alt-text" >

2. In the Azure Portal, navigate to the **Subscriptions** blade by searching and click on that Subscriptions icon.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/5.png?st=2019-09-05T05%3A42%3A06Z&se=2025-09-06T05%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rnE6WPGk8Ondwe9HUysXTfOdqXzIxMyv4u9fkgLWy1Y%3D" alt="image-alt-text" >

3. From the **Subscriptions** blade, navigate to the blade displaying properties of your Azure subscription by click on the subscription name

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/6.png?st=2019-09-05T05%3A42%3A31Z&se=2025-09-06T05%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SSoEqZXJBy%2BsaIhhQdPcfDSyoeAswrBFdiYAcfYEtt0%3D" alt="image-alt-text" >

4.  From the blade displaying the properties of your subscription, navigate to its **Resource providers** blade.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/7.png?st=2019-09-05T05%3A42%3A54Z&se=2025-09-06T05%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vz3%2B4lyhKf%2F%2F9qIEk0i9MNxsBaOB3IOoszA%2F53gqSHc%3D" alt="image-alt-text" >

5. On the Resource providers blade, register the following resource providers (if these resource providers have not been yet registered):

*  Microsoft.Network

*  Microsoft.Compute

*  Microsoft.Storage

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/8.png?st=2019-09-05T05%3A43%3A17Z&se=2025-09-06T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZFkK4xlIVnUUR16g9X925hWgapp61bvK2114hDe1am0%3D" alt="image-alt-text" >

>  **Note:** This step registers the Azure Resource Manager Microsoft.Network, Microsoft.Compute, and Microsoft.Storage resource providers. This is a one-time operation (per subscription) required when using Azure Resource Manager templates to deploy resources managed by these resource providers (if these resource providers have not been yet registered).

1.	In the Azure Portal, navigate to the **Create a resource** blade.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/9.png?st=2019-09-05T05%3A43%3A46Z&se=2025-09-06T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Bpw8%2FAc5WOXmP8bZqRazm1uvnEcvWKr8GVGtAG7m1pM%3D" alt="image-alt-text" >

2.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment, then select Template deployment (deploy using customer templates)**.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/10.png?st=2019-09-05T05%3A44%3A14Z&se=2025-09-06T05%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DqVfc%2Fk%2FCNclda%2FDUaixnMIpvmc74FZNkd4ZjFu5a8o%3D" alt="image-alt-text" >

3.	Click **Create**.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/11.png?st=2019-09-05T05%3A44%3A35Z&se=2025-09-06T05%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GUNHHoPMz2YY%2FFbXosvg52cCviaP499GSot%2FHtW0X%2Fo%3D" alt="image-alt-text" >

4.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.
 
 <img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/12.png?st=2019-09-05T05%3A44%3A59Z&se=2025-09-06T05%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lYARX%2BmGb58vcEnpqUcrkqeH9biogArAokg%2BCTZEfD0%3D" alt="image-alt-text" >

 <img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/13.png?st=2019-09-05T05%3A45%3A29Z&se=2025-09-06T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=o6wdCLlXXULuIQcV3AerWzTarxn1WBeRbU1DBYcBAic%3D" alt="image-alt-text" >
 
5.	From the **Edit template** blade,clear the template body Copy and paste the below url in chrome new window copy the entire content display in that page paste it in template file.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.json?st=2019-09-05T04%3A58%3A41Z&se=2025-09-06T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XaA%2Frfybo2Yt6YQigq1Pw1%2FsjLWSl6bsNvA6iGBsXmk%3D.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/14.png?st=2019-09-05T05%3A46%3A44Z&se=2025-09-06T05%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JYpBYtaPhOVSLXq2C5UF5ZqhoQPj9iqvr6mQXuv3SRk%3D" alt="image-alt-text" >
 
>  **Note:** Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.

6.	Save the template and return to the **Custom deployment** blade.

7.	From the Custom deployment blade, navigate to the **Edit parameters** blade.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/15.png?st=2019-09-05T05%3A52%3A29Z&se=2025-09-06T05%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Az9vKPAMazUxrqPWMZ%2FKYa9Cw5wV9tSns23pXEZWq1M%3D" alt="image-alt-text" >

8.	From the **Edit parameters** blade,clear the existing content, Copy and paste the below url in chrome new window copy the entire content display in that page paste it in edit parameters 

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.parameters.json?st=2019-09-05T05%3A01%3A35Z&se=2025-09-06T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PEfg9bBv7zhFIm1CV1A3t1mJE5h7AoNw22qTi0GhGzk%3D
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/16.png?st=2019-09-05T05%3A55%3A34Z&se=2025-09-06T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=exQPjkEUgi2r0z5QF4%2FSAq9M3nnX%2FfiVVIx4aieLQ74%3D" alt="image-alt-text" >  

9. Save the parameters and return to the **Custom deployment** blade.
 
10.	From the **Custom deployment** blade, initiate a template deployment with the following settings:

* **Subscription:** `default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vm Size:** `Standard_DS1_v2` <br>
* **Vm Name:** `az1000201-vm1` <br>
* **Admin Username:** `Student` <br>
* **Admin Password:** `Password@1234` <br>
* **Virtual Network Name:** `az1000201-vnet`


<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/17.png?st=2019-09-05T05%3A59%3A33Z&se=2025-09-06T05%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EkLgExsqPFFh5DJDKqOWyKBhJuGakmIPDzHYEExfNqY%3D" alt="image-alt-text" >  
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/18.png?st=2019-09-05T06%3A07%3A05Z&se=2025-09-06T06%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Lxud5gOYmdd64tkL2o77yhN%2F4aELAJ%2FrYM8me9Q7%2FyU%3D" alt="image-alt-text" > 

> **Note**: Do not wait for the deployment to complete but proceed to the next exercise. You will use the Virtual Machine **az1000201-vm1** in the second exercise of this lab.

>  **Result:** After you completed this exercise, you have initiated template deployment of an Azure VM **az1000201-vm1** that you will use in the second exercise of this lab.

## Exercise 2: Implement and Use Azure Blob Storage

The main tasks for this exercise are as follows:

1.	Create Azure Storage Accounts

2.	Review configuration settings of Azure Storage Accounts

3.	Manage Azure Storage Blob Service

4.	Copy a container and blobs between Azure Storage Accounts

5.	Use a Shared Access Signature (SAS) key to access a blob

### Task 1: Create Azure Storage Accounts

1.	In the Azure Portal, navigate to the **Create a resource** blade.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/19.png?st=2019-09-05T06%3A09%3A06Z&se=2025-09-06T06%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OREIYMTGeLr3uMF2JmsotsG8vu22rEABxTNt7y1mJaI%3D" alt="image-alt-text" > 

2.	From the **Create a resource** blade, search Azure Marketplace for **Storage Account**.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/20.png?st=2019-09-05T06%3A09%3A37Z&se=2025-09-06T06%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qV6HgTQ%2BApw4bfgUrWJTO1vUdnYy0bkVDrRB0Ek6GPQ%3D" alt="image-alt-text" > 
 
3.	Use the list of search results to navigate to the **Create Storage Account** blade.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/21.png?st=2019-09-05T06%3A10%3A57Z&se=2025-09-06T06%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fvupZn5jNPccCHD%2FnP9OuHoeAcDBwl8uYq%2F%2FTlYrzD4%3D" alt="image-alt-text" > 
 
4.	From the **Create Storage Account** blade, create a new Storage Account with the following settings:

* **Subscription:** `Default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Storage Account name:** any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits <br>
* **Location:** `{{location}}` <br>
* **Performance:** `Standard` <br>
* **Account kind:** `Storage (general purpose v1)` <br>
* **Replication:** `Locally-redundant Storage (LRS)`


<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/22.png?st=2019-09-05T06%3A14%3A49Z&se=2025-09-06T06%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ue%2Bsd7iXN3lVdxemY40n7yj6Kcr0AGOiGgYe0WC4AtY%3D" alt="image-alt-text" >  

5.	 Click **Review + create**, and then click **Create**

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/23.png?st=2019-09-05T06%3A15%3A18Z&se=2025-09-06T06%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wcYdHd2u%2FBFbZjEz8vDANd70uz7RznL4AfsTM%2FB0ziA%3D" alt="image-alt-text" > 
 
6.	Do not wait for the Storage Account to be provisioned but proceed to the next step.

7.	In the Azure Portal, navigate to the **Create a resource** blade.

8.	From the **Create a resource** blade, search Azure Marketplace for **Storage Account**.

9.	Use the list of search results to navigate to the **Create Storage Account** blade.

10.	From the **Create Storage Account** blade, create a new Storage Account with the following settings:


* **Subscription:** `Default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Storage Account name:** any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits <br>
* **Location:** `{{location}}` <br>
* **Performance:** `Standard` <br>
* **Account kind:** `StorageV2 (general purpose v2)` <br>
* **Access tier:** `Hot` <br>
* **Replication:** `Geo-redundant Storage (GRS)` 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/24.png?st=2019-09-05T06%3A26%3A15Z&se=2025-09-06T06%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mCTNIEdiNH3aQp9coRqpc8V2a3pu%2BydgWgOH0%2Bmr4DM%3D" alt="image-alt-text" > 
 
11.	Click **Review + create**, then click **Create**.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/25.png?st=2019-09-05T06%3A26%3A36Z&se=2025-09-06T06%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AIrpiZyIrPOcIB%2F%2FFMNxK74YeW5OY4GarFjM%2FjcJZj4%3D" alt="image-alt-text" > 

12.	Wait for the Storage Account to be provisioned. This should take less than a minute.

### Task 2: Review configuration settings of Azure Storage Accounts

1.	In Azure Portal, navigate to the blade of the first Storage Account you created.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/26.png?st=2019-09-05T06%3A36%3A33Z&se=2025-09-06T06%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=G5n%2F5o%2FNF3b7IaK2Kc1sR6b5JGb7M%2FEXOmGuHn598so%3D" alt="image-alt-text" >   

2.	With your Storage Account blade open, review the Storage Account configuration in the **Overview** section, including the performance, replication, and Account kind settings.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/27.png?st=2019-09-05T06%3A37%3A14Z&se=2025-09-06T06%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6A8fhDSMy%2BzSV6YnR7azLSEWTTpyjSA08nX1k4RSp3g%3D" alt="image-alt-text" > 

3.	Display the **Access keys** blade. Note that you have the option of copying the values of Storage Account name, as well as the values of key1 and key2. You also have the option to regenerate each of the keys.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/28.png?st=2019-09-05T06%3A38%3A59Z&se=2025-09-06T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aHtAqFtVGBIXC%2F301vpSBNeeZl2WCHJ5pwjLnGLMRb0%3D" alt="image-alt-text" > 

4.	Display the **Configuration** blade of the Storage Account.

5.	On the **Configuration** blade, note that you have the option of performing an upgrade to **General Purpose v2** Account, enforcing secure transfer, and changing the replication settings to either **Geo-redundant Storage (GRS)** or **Read-access geo-redundant Storage (RA-GRS)**. However, you cannot change the performance setting (this setting can only be assigned when the Storage Account is created).

6.	Display the **Encryption** blade of the Storage Account. Note that encryption is enabled by default and that you have the option of using your own key.

>  **Note:** Do not change the configuration of the Storage Account.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/29.png?st=2019-09-05T06%3A39%3A23Z&se=2025-09-06T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sTjRPY8%2BkoGPwSb%2BaFc2ctrimRmQ4gH5t3SRIIc%2BeNU%3D" alt="image-alt-text" >                             
7.	In Azure Portal, navigate to the blade of the second Storage Account you created.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/30.png?st=2019-09-05T06%3A45%3A46Z&se=2025-09-06T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mzWO6vEoapYy0Yh5Yt1Y%2FdsePKP9uxqyi7vElxwb4PI%3D" alt="image-alt-text" > 
 
8.	With your Storage Account blade open, review the Storage Account configuration in the **Overview** section, including the performance, replication, and Account kind settings.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/31.png?st=2019-09-05T06%3A46%3A10Z&se=2025-09-06T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZgDZ2K1%2FVeFHWXueBp2S40jk4RS3l8ylb8mopxthjlc%3D" alt="image-alt-text" > 

9.	Display the **Configuration** blade of the Storage Account.

10.	On the **Configuration** blade, note that you have the option of disabling the secure transfer requirement, setting the default access tier to **Cool**, and changing the replication settings to either **Locally-redundant Storage (LRS)** or **Read-access geo-redundant Storage (RA-GRS)**. In this case, you also cannot change the performance setting.

11.	Display the **Encryption** blade of the Storage Account. Note that in this case encryption is also enabled by default and that you have the option of using your own key.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/32.png?st=2019-09-05T06%3A46%3A43Z&se=2025-09-06T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9BCZtsdjj9Aw3mhIeKboSSjjfQ3gltkvcgq67Wl0P44%3D" alt="image-alt-text" > 

### Task 3: Manage Azure Storage Blob Service

1.	In the Azure Portal, navigate to the **Blobs** blade of the first Storage Account.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/33.png?st=2019-09-05T07%3A17%3A53Z&se=2025-09-06T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vPlhDPbWtSoxidF9Gjn2igaWiJ3B%2FhI12rUrfy%2Bh%2FqU%3D" alt="image-alt-text" > 
 
2.	From the **Blobs** blade of the first Storage Account, create a new container named **az1000202-container** with the **Public access level** set to **Private (no anonymous access)**.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/34.png?st=2019-09-05T07%3A18%3A23Z&se=2025-09-06T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Zr2x2PtG4uebtESdpjRrdq9BjssrLU1mwGW0yKqdsU0%3D" alt="image-alt-text" > 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/35.png?st=2019-09-05T07%3A20%3A45Z&se=2025-09-06T07%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZTYMZX%2BSeLASG%2BrrxT%2BjMdmx1Qy5vjGJxdY%2FO%2Bv%2Fvu0%3D" alt="image-alt-text" > 

3.	From the **az1000202-container** blade, upload lab files **az-100-02_azuredeploy.json and az-100-02_azuredeploy.parameters.json** into the container.

Open the gitbash from console, run the below commands .

```

cd /

cd D/PhotonUser

curl "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.json?st=2019-09-05T04%3A58%3A41Z&se=2025-09-06T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XaA%2Frfybo2Yt6YQigq1Pw1%2FsjLWSl6bsNvA6iGBsXmk%3D" --output az-100-02_azuredeploy.json

curl "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_03/Implement_and_Manage_Storage/az-100-02_azuredeploy.parameters.json?st=2019-09-05T05%3A01%3A35Z&se=2025-09-06T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PEfg9bBv7zhFIm1CV1A3t1mJE5h7AoNw22qTi0GhGzk%3D" --output az-100-02_azuredeploy.parameters.json

```
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/71.png?st=2019-09-16T08%3A33%3A47Z&se=2025-09-17T08%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=S%2BDqvfwyhcxFem%2FGgEm8M7ahAdlOZF6kLaJjUGc%2Bk5g%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/68.PNG?st=2019-09-16T06%3A49%3A21Z&se=2025-09-17T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YcYya4%2B1d8ifQy%2F%2B%2FDj%2F5aKVRK6WNAgrCAcIo5IFPIg%3D" alt="image-alt-text" > 


Then go to the Storage Account blob in Azure Portal,click on the container name then upload the lab files 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/69.PNG?st=2019-09-16T06%3A50%3A34Z&se=2025-09-17T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iECYs1OaEoV4YaP93cG6qvyN2tZsdb02WbaRNVdQU3w%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/70.PNG?st=2019-09-16T06%3A51%3A28Z&se=2025-09-17T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OcAwLxgZLWkHPLuB418MZZPoWgDFfIQBARK4bj5wFAc%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/36.png?st=2019-09-05T07%3A21%3A19Z&se=2025-09-06T07%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uamY%2FlfkG199nLJTtaVi%2BankBm9GxDI2Xaa9w8LwP2o%3D" alt="image-alt-text" > 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/37.png?st=2019-09-05T07%3A21%3A43Z&se=2025-09-06T07%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J3DzZ1q3QbjhkBC576Hr0B14Ru3Na9k9G%2FnQ9%2BIkCTE%3D" alt="image-alt-text" > 

 
### Task 4: Copy a container and blobs between Azure Storage Accounts

1.	From the Azure Portal, start a PowerShell session in the Cloud Shell pane.
 
 >  **Note:** If this is the first time you are launching the Cloud Shell in the current Azure  subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a Storage Account in an automatically generated resource group.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/38.png?st=2019-09-05T09%3A08%3A33Z&se=2025-09-06T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=INY5TDgsJUoATentNxkih9ieqVQ1M5iofSlY9tgX1Iw%3D" alt="image-alt-text" > 

2. If you are presented with the “You have no Storage mounted” message,select Powershell and configure Storage using the following settings:

* **Subsciption:** `default` <br>
* **Cloud Shell region:** `{{location}}` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Storage Account:** a name of a new Storage Account which will be unique <br>
* **File share:** `cloudshell`

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/72.PNG?st=2019-09-16T09%3A30%3A47Z&se=2025-09-17T09%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NLTL3w%2BIU%2FIuhJSxirxwZugxUq6fMQMfLUV%2FOcJ1aJY%3D" alt="image-alt-text" > 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/73.png?st=2019-09-16T09%3A31%3A26Z&se=2025-09-17T09%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1e0IkOE4qRUuV4c64RRDFecx7IGnb91SPCXhIE5Zp7o%3D" alt="image-alt-text" > 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/74.PNG?st=2019-09-16T09%3A32%3A18Z&se=2025-09-17T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=28Q35pqFCqik7hKwc5n%2FEgRGL0qYOPVW%2BKZtaKTRib8%3D" alt="image-alt-text" >     

3.	In the Cloud Shell pane, run the following commands:

Update the Storage Account names with the deployed Storage Account names.

```
$containerName = 'az1000202-container'

$storageAccount1Name = 'storageaccountname1'

$storageAccount2Name =  'storgeaccountname2'

$storageAccount1Key1 = (Get-AzStorageAccountKey -ResourceGroupName '{{resource-group-name}}' -StorageAccountName $storageAccount1Name)[0].Value

$storageAccount2Key1 = (Get-AzStorageAccountKey -ResourceGroupName '{{resource-group-name}}' -StorageAccountName $storageAccount2Name)[0].Value

$context1 = New-AzStorageContext -StorageAccountName $storageAccount1Name -StorageAccountKey $storageAccount1Key1

$context2 = New-AzStorageContext -StorageAccountName $storageAccount2Name -StorageAccountKey $storageAccount2Key1

```       
      
>  **Note:** These commands set the values of variables representing the names of the blob container containing the blobs you uploaded in the previous task, the two storage Account, their corresponding keys, and the corresponding security context for each. You will use these values to generate a SAS token to copy blobs between storage Accounts by using the AZCopy command line utility.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/39.png?st=2019-09-16T11%3A44%3A43Z&se=2025-09-17T11%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mFLmM4vtYj%2BV1WfBqY867CFw9xVt7oi6o6iO%2Fn7JtkM%3D" alt="image-alt-text" > 
 
4.	 In the Cloud Shell pane, run the following command:

```  

New-AzStorageContainer -Name $containerName -Context $context2 -Permission Off

```  

>  **Note:** This command creates a new container with the matching name in the second storage Account

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/40.png?st=2019-09-05T09%3A17%3A41Z&se=2025-09-06T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ryW4nlJz%2FcdUZtmyXAr6ZkehWpbssQDFdKnwHNNuqGU%3D" alt="image-alt-text" >        

5.	In the Cloud Shell pane, run the following commands:

```  

$containerToken1 = New-AzStorageContainerSASToken -Context $context1 -ExpiryTime(get-date).AddHours(24) -FullUri -Name $containerName -Permission rwdl

$containerToken2 = New-AzStorageContainerSASToken -Context $context2 -ExpiryTime(get-date).AddHours(24) -FullUri -Name $containerName -Permission rwdl

```  

>  **Note:** These commands generate SAS keys that you will use in the next step to copy blobs between two containers.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/41.png?st=2019-09-05T09%3A18%3A23Z&se=2025-09-06T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vFNbEN8oLf4la4Ue%2FlCAYyGZL66xgVRWRGmQV%2BaGJV8%3D" alt="image-alt-text" > 
 
6.	In the Cloud Shell pane, run the following command:

```  

azcopy cp $containerToken1 $containerToken2 --recursive=true

```  

>  **Note:** This command uses the AzCopy utility to copy the content of the container between the two Storage Accounts.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/42.png?st=2019-09-05T09%3A19%3A25Z&se=2025-09-06T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Bg6fBNJB%2BIJm0NfVx7eeHm31tmrp1xGFqkQMHbcaO6A%3D" alt="image-alt-text" > 
      
7.	 Verify that the command returned the results confirming that the two files were transferred.

8.	Navigate to the **Blobs** blade of the second Storage Account and verify that it includes the entry representing the newly created **az1000202-container** and that the container includes two copied blobs.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/43.png?st=2019-09-05T09%3A19%3A56Z&se=2025-09-06T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Zycuj%2F4L1THxTfKwLwUKKVuKHjfz85hIPjzg45B%2Bu84%3D" alt="image-alt-text" >


### Task 5: Use a Shared Access Signature (SAS) key to access a blob

1.	From the **Blobs** blade of the second Storage Account, navigate to the container **az1000202-container**, and then open the **az-100-02_azuredeploy.json** blade.

2.	On the **az-100-02_azuredeploy.json** blade, copy the value of the **URL** property.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/44.png?st=2019-09-05T09%3A29%3A58Z&se=2025-09-06T09%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=47207sg9uWEOsr1Mqb4chCKjlNN4%2BXOh%2F71tZmMuAV4%3D" alt="image-alt-text" >
 
3.	Open another Microsoft Edge window and navigate to the URL you copied in the previous step.

>  **Note:** The browser will display the **ResourceNotFound**. This is expected since the container has the Public access level set to Private (no anonymous access).

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/45.png?st=2019-09-05T09%3A30%3A24Z&se=2025-09-06T09%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JVVr8cZDMltQL3wNRAbvJ4JR2AtpUJOPj%2BpOVJRGxqQ%3D" alt="image-alt-text" >

4.	On the **az-100-02_azuredeploy.json** blade, generate a shared access signature (SAS) and the corresponding URL with the following settings:

```  
 
Permissions: Read

Start date/time: specify the current date/time in your current time zone

Expiry date/time: specify the date/time 24 hours ahead of the current time

Allowed IP addresses: leave blank

Allowed protocols: HTTP

Signing key: Key 1

```  

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/46.png?st=2019-09-05T09%3A30%3A48Z&se=2025-09-06T09%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=S6X01G37iMLgcFm7OUw7RwF7pqfNGniOOY60biMJ9nI%3D" alt="image-alt-text" >
 
5.	On the **az-100-02_azuredeploy.json** blade, copy **Blob SAS URL**.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/47.png?st=2019-09-05T09%3A31%3A35Z&se=2025-09-06T09%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4VMWgndrJG8kfVma7irVXOColA1bVwaDb9fkb07EafI%3D" alt="image-alt-text" >
 
6.	From the previously opened Microsoft Edge window, navigate to the URL you copied in the previous step.

>  **Note:** This time, you will be prompted whether you want to open or save **az-100-02_azuredeploy.json**. This is expected as well, since this time you are no longer accessing the container anonymously, but instead you are using the newly generated SAS key, which is valid for the next 24 hours.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/48.png?st=2019-09-05T09%3A32%3A01Z&se=2025-09-06T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rWTBC9fV7X3MxtJ5J2V6prDbtJF%2FdZSS1FOK7BYJpFU%3D" alt="image-alt-text" >
 
7.	Close the Microsoft Edge window displaying the prompt.

>  **Result:** After you completed this exercise, you have created two Azure Storage Accounts, reviewed their configuration settings, created a blob container, uploaded blobs into the container, copied the container and blobs between the Storage Accounts, and used a SAS key to access one of the blobs.

## Exercise 3: Implement and Use Azure File Storage
 
The main tasks for this exercise are as follows:

1.	Create an Azure File Service share

2.	Map a drive to the Azure File Service share from an Azure VM

### Task 1: Create an Azure File Service share

1.	In the Azure Portal, navigate to the blade displaying the properties of the second Storage Account you created in the previous exercise.

2.	From the Storage Account blade, display the properties of its File Service.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/49.png?st=2019-09-05T09%3A50%3A43Z&se=2025-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z6WgLG9WlBT3qbj%2B%2BQZs%2FbIZuYuWux1V51zWz0ALrXM%3D" alt="image-alt-text" >

3.	From the Storage Account Files blade, create a new file share with the following settings:

```  

Name: az10002share1

Quota: 5 GB

```  
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/50.png?st=2019-09-05T09%3A51%3A14Z&se=2025-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qY4fmb126QF7Ufudy9j6oONo2pszSXQfF%2F1R0dJeArs%3D" alt="image-alt-text" >

### Task 2: Map a drive to the Azure File Service share from an Azure VM

> **Note**: Before you start this task, ensure that the template deployment you started in Exercise 0 has completed.

1.	Navigate to the **az10002share1** blade and display the **Connect** blade.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/51.png?st=2019-09-05T09%3A52%3A03Z&se=2025-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uM6ElkLmyEV9MdqHWWudW9R5QOmqW1JTa7romqxUcCI%3D" alt="image-alt-text" >

2.	From the **Connect** blade, copy into Clipboard the PowerShell commands that connect to the file share from a Windows computer.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/52.png?st=2019-09-05T09%3A52%3A28Z&se=2025-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E%2FuJpXPvHOy9bDVt%2ByAr74ibRTm91knEqYXIjxnlp1g%3D" alt="image-alt-text" >

3.	In the Azure Portal, navigate to the az1000201-vm1 blade. Copy the public IP address.
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/53.png?st=2019-09-05T10%3A07%3A16Z&se=2025-09-06T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BJo%2BhIJq2aMIevX2i3GD%2FNBbUa8rXXXDwelVtjBh5vk%3D" alt="image-alt-text" >

4.	From the **az1000201-vm1** blade, connect to the Azure VM via the RDP protocol and, when prompted to sign in, provide the following credentials:

```  

Admin Username: Student

Admin Password: Password@1234

```  

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/67.png?st=2019-09-13T09%3A09%3A36Z&se=2025-09-14T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZRoGzjWsLijl%2Bp%2F7pJt5uvhAO1mX9WIO2lytqh4jYSo%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/54.png?st=2019-09-05T10%3A07%3A50Z&se=2025-09-06T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qBoQdCRHbOMethqulrYdIgmT17MloI5MlG9tJ1fFo7M%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/55.png?st=2019-09-05T10%3A08%3A33Z&se=2025-09-06T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VSzBc3O4JCeUB86%2FvhlBZjXGctrzjr6U1Fc0oUUU%2FI4%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/56.png?st=2019-09-05T10%3A08%3A53Z&se=2025-09-06T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tlJe4oBXXPfVRWOPtnoNjz2y4mM5zaOLcYDTpt8zLdE%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/57.png?st=2019-09-05T10%3A09%3A15Z&se=2025-09-06T10%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8xoOwQ3Ld9ThpDH6akjRCybRaHSBS%2F2dmp1Qwxm%2BwL0%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/58.png?st=2019-09-05T10%3A09%3A38Z&se=2025-09-06T10%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=otm8f0%2BnyBTD2ShCP8uNKINRVPkzJSsMtzj%2BB3vakvg%3D" alt="image-alt-text" >
 
5.	Within the RDP session, start a Windows PowerShell ISE session.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/59.png?st=2019-09-05T10%3A10%3A00Z&se=2025-09-06T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=j5idXdYf6pehmlH3Wbhhxeoxa3vQwD3byJCIDdblYuo%3D" alt="image-alt-text" >

6.	From the Windows PowerShell ISE session, open the script pane and paste into it the content of your local Clipboard.

7.	Paste the script into the PowerShell ISE session, add -Persist at the end of the script, execute the script, and verify that its output confirms successful mapping of the Z: drive to the Azure Storage File Service share.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/60.png?st=2019-09-05T10%3A10%3A47Z&se=2025-09-06T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xTCTJey7qgrffOVan3xc0TA04P58zfi%2FbOFdSZRlZPY%3D" alt="image-alt-text" >
 
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/61.png?st=2019-09-05T10%3A11%3A31Z&se=2025-09-06T10%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Hg%2FYz%2FAcGZM33ioJFQWRTivuxaIRW5feZYXxnW52b34%3D" alt="image-alt-text" >

8.	Start File Explorer, navigate to the Z: drive and create a folder named **Folder1**.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/62.png?st=2019-09-05T10%3A12%3A19Z&se=2025-09-06T10%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a5tbeFQmJRUdtgJIhG%2B4%2BajuEhOMujd40GzQkw7YOQ8%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/63.png?st=2019-09-05T10%3A12%3A45Z&se=2025-09-06T10%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=p0cgCNKVBITEnaa8MSN%2BAobEerCd1RZ%2FQX9p81mf%2Fz0%3D" alt="image-alt-text" >
 
9.	In the File Explorer window, navigate to **Folder1** and create a text document named **File1.txt**.

>  **Note**: Make sure that you take into Account the default configuration of File Explorer that does not display known file extensions in order to avoid creating a file named **File1.txt.txt**.
    
<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/64.png?st=2019-09-05T10%3A13%3A10Z&se=2025-09-06T10%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bJmXpecKwlgwfBRZ4fq0MIXGKeFxrhn7VxmiKmtRXYU%3D" alt="image-alt-text" >

10.	From the PowerShell prompt, enter **Z:** to change the directory context to the mapped drive.

11.	From the PowerShell prompt, enter dir to list the contents of the drive. You should see the directory that you created from File Explorer.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/65.png?st=2019-09-05T10%3A13%3A32Z&se=2025-09-06T10%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a%2BVg2p%2B9U7x9qgLQia3TrdHeqPYGxF36hcdydMz6mXo%3D" alt="image-alt-text" >
 
12.	From the PowerShell prompt, enter cd Folder1 to change directories to the folder. Run the dir command again to list the file contents.

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab3/66.png?st=2019-09-05T10%3A13%3A50Z&se=2025-09-06T10%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=duLD7tq9zWBGTeJEUtGpsgjBi0IRZA6iB9E8j9nnIxU%3D" alt="image-alt-text" >

>  **Result**: After you completed this exercise, you have created an Azure File Service share, mapped a drive to the file share from an Azure VM, and used File Explorer from the Azure VM to create a folder and a file in the file share.
