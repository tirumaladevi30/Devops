# Lab 6: Configure Azure Cloud storage

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Creating and configuring an Azure Storage account](#exercise-1-creating-and-configuring-an-zzure-storage-account)

[Exercise 2: Creating and managing blobs](#exercise-2-creating-and-managing-blobs)
  
## Overview

The aim of this lab is to create and configure Azure Storage.


### Scenario & Objectives

XYZ Training Labs Corporation uses its on-premises file servers to store its data. You want to test transferring these files to Azure Storage.

After you complete this lab, you will be able to:

* Create an Azure Storage account.

* Upload data to Azure Storage.

## Pre-Requisites

* Familiar with Storage Account

## Exercise 1: Creating and configuring an Azure Storage account

Before you start managing your data in Azure, you should first create a storage account and examine its properties.text file.

The main tasks for this exercise are as follows:

1.	Create a storage account in Azure

2.	View the properties of the storage account

### Task 1: Create a storage account in Azure

**Storage Account:**

An Azure storage account contains all of your Azure Storage data objects: blobs, files, queues, tables, and disks. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS. Data in your Azure storage account is durable and highly available, secure, and massively scalable.

1.  Using the Chrome browser, login into Azure portal with the below details.

**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/1.png?st=2019-08-23T09%3A53%3A57Z&se=2049-06-24T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=u1HSLRJvmLduVhSHcKLRu%2FjlyoW4TC74vailJhfq9w0%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/2.png?st=2019-08-23T09%3A55%3A54Z&se=2025-08-24T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AzpqokfJ5KaMk%2F8P0PgFAFCJ7%2B0vfjTt4aT4u8%2Flv4M%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/3.png?st=2019-08-23T09%3A56%3A53Z&se=2025-08-24T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dmPL2LoX8Py2afBo5wbZF14IBfsX%2B%2ByjwjvfWlrD3CM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/4.png?st=2019-08-23T10%3A17%3A45Z&se=2025-08-24T10%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lLlFIQi%2F59e9mXgAla7JgW5ozB%2FQ9KV7oG08ET3c6IY%3D)

2.	From Azure Portal, create a new storage account with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/5.png?st=2019-08-23T10%3A24%3A14Z&se=2025-08-24T10%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GNQWj4aVGt4FV6f2wtkzBP4kl%2Br0LMoFGIwj19Oe%2Faw%3D)

**ResourceGroup:** {{resource-group-name}}

**Region:** {{Location}}

```
Subscription: {{subscriptionId}}

Storage account name: any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits

Performance: Standard

Account kind: Storage (general purpose v1)

Replication: Locally-redundant storage (LRS)

Security (Secure transfer required): Disabled

Virtual network: All Networks

Data Protection: Disabled

Data Lake Storage Gen2 (Hierarchical namespace): Disabled

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/6.png?st=2019-08-23T10%3A29%3A42Z&se=2025-08-24T10%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wie7RTND%2Fmju201XkyWvGB7UT43X3sbzWrGy78Px96E%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/7.png?st=2019-08-23T10%3A31%3A23Z&se=2024-08-24T10%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=F79%2BdazjUTy%2FrY2pUj89HaPo8mlAea9HPcQDX7rTvI0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/8.png?st=2019-08-23T10%3A31%3A59Z&se=2025-08-24T10%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a9JQQgva9V1OSZltjhd5Lxyu%2B2o6lfssO%2BHaJtApnno%3D)

3.	Wait for the storage account to be provisioned. This will take about a minute. When the deployment completes, the portal will display the storage account with its Settings blade open.

4.	After creating the new storage account, you will be notified with a notification in Azure portal.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/9.png?st=2019-08-23T10%3A32%3A43Z&se=2025-08-24T10%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3WtJPBBp73Wx%2FiNcZ64iK%2Bk3lz2gwS6iUrcqR4HJy%2BY%3D)

### Task 2: View the properties of the storage account

1.	In Azure Portal, with your storage account blade open, review the Overview section and resource.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/10.png?st=2019-08-23T10%3A33%3A15Z&se=2025-08-24T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dM%2BCJf0po3Pxc6usP7%2BrjqE6kd58PMDyXLV1IW%2BQGJc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/11.png?st=2019-08-23T10%3A33%3A38Z&se=2025-08-24T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=v0WKg%2FJJDB4a5NkXFfJxIxjjYO1QVsghGVwaa0gyTdw%3D)

2.	Display the Access keys blade. On the access keys blade, note that you have the option of copying the values of storage account names including key1 and key2. You can also  regenerate both keys.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/12.png?st=2019-08-23T10%3A44%3A07Z&se=2025-08-24T10%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J5PPc57ePTRADVVEHdJcttYxpi0Hw9qKaBGhgEnyZak%3D)

3.	Display the Configuration blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/13.png?st=2019-08-23T10%3A45%3A00Z&se=2025-08-24T10%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VcSZOxgQY9HP%2BwdrUxw1lfzs2Cma1x%2B2yliSsfAgwd0%3D)

4.	On the Configuration blade, notice that you have the option of performing an upgrade to General Purpose v2 account and changing the replication settings. However, you cannot change the performance setting (this can only be assigned when the storage account is created).

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/14.png?st=2019-08-23T10%3A47%3A30Z&se=2025-08-24T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9dCz86XxH2BYqQDwcqP%2BQkqKw55%2FQkPsnPEgcQbsMs8%3D)

**Result:** After you completed this exercise, you have created your Azure Storage and examined its properties.

## Exercise 2: Creating and managing blobs

**Scenario**

Now that you have created and configured your storage account, you need to perform transfer of your on-premises data.

The main tasks for this exercise are as follows:

1.	Create a container

2.	Upload data to the container by using the Azure portal

3.	Access content of Azure Storage account by using a SAS token

### Task 1: Create a container

1.	In the Azure portal, navigate to the storage account blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/15.png?st=2019-08-23T10%3A49%3A15Z&se=2025-08-24T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mOzoCQBX4Bx6dEZtBV1nV4Kb3hK75LW2Q97Nkv8toYQ%3D)

2.	From the storage account blade, create a new blob container with the following settings:

  ```

  Name: labcontainer
  
  Access type: Private

  ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/16.png?st=2019-08-23T10%3A49%3A44Z&se=2025-08-24T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wL3v4CiIC0quEhSalEjAdpX5P%2BLMKHCgyWVxc7QvuSQ%3D)

### Task 2: Upload data to the container by using the Azure portal

1. In chroome new window copy and paste the below url and right click on the displayed image, save the image with name splashscreen.contrast-black.png in downloads path.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/splashscreen.contrast-black.png?st=2019-08-26T07%3A10%3A50Z&se=2025-08-27T07%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WLUtmcE4uzYICVQxC7LS6hmRjR%2BF2pyBwQ1NNgq%2Fs98%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/25.PNG?st=2019-08-26T07%3A17%3A00Z&se=2025-08-27T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HSqoVleDSRz%2BBx6qi%2BcAuraoFhoVIS4A6qkIiHq83kY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/26.PNG?st=2019-08-26T07%3A18%3A12Z&se=2025-08-27T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LE0XOzhTNo2X8FMIi%2FNWOt252uqhjNMf9HitEhPRt44%3D)

2.	In the Azure portal, navigate to the blade displaying the newly created container.From the container blade, upload the saved image with name splashscreen.contrast-black.png in downloads.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/17.png?st=2019-08-26T06%3A01%3A03Z&se=2025-08-27T06%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jfGDEXENwweNoK8ptkMuWMZ%2BU8eyt%2B46viGl4aNZnck%3D)

### Task 3: Access content of Azure Storage account by using a SAS token

1.	From the **labcontainer** blade, identify the URL of the newly uploaded blob.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/18.png?st=2019-08-26T06%3A01%3A48Z&se=2025-08-27T06%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IPd1n8QoSxcdo6WPV3EK43oik6gkr7dGRAv0rrurIkI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/19.png?st=2019-08-26T06%3A02%3A24Z&se=2025-08-27T06%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xFktlVYXuRxHBhCiIOT8o6MPfUgz70lHJzTLcc5UEjs%3D)

2.	Start Chrome and navigate to that URL.

3.	Note the **ResourceNotFound** error message. This is expected since the blob is residing in a private container, which requires authenticated access.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/20.png?st=2019-08-26T06%3A03%3A04Z&se=2025-08-27T06%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ncs4hHLhYGDiZs8Nds%2BzA9uJt251%2Fv0R659CgBVFsNA%3D)

4.	Switch to the Chrome window displaying the Azure portal and, on the **splashscreen.contrast-white_scale-400.png** blade, switch to the Generate SAS tab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/21.png?st=2019-08-26T06%3A03%3A43Z&se=2025-08-27T06%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=S811OPvErGAZs8tJALfwOnOluuxCKQ%2F8%2FMrcOi4sUvI%3D)

5.	On the **Generate SAS tab**, enable the **HTTP** option and **Generate blob SAS token and URL.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/22.png?st=2019-08-26T06%3A04%3A14Z&se=2025-08-27T06%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MDPL1gM%2FPUHsDSm0Rt8oKLVyFhdNr7SYSc9UiNxHF5Y%3D)


6.	Open a new Chrome window and, in the navigate to the URL generated in the previous step.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/23.png?st=2019-08-26T06%3A04%3A44Z&se=2025-08-27T06%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3%2B2wdIObrdnKG%2BGFECA9bI%2BIRST6J3JFncCLBamM0sg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/24.png?st=2019-08-26T06%3A05%3A06Z&se=2025-08-27T06%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fYrnvDfT5WI1fr6ria%2Bhrv4TGb2m%2BsIrrZ0sEJCmOrU%3D)

7.	Note that you can view the image. This is expected since this time you are authorized to access the blob based on the SAS token included in the URL.

8.	Close all Chrome windows.

**Result:** After you completed this exercise, you have created a blob container, uploaded a file into it, and accessed it by using a SAS token.
