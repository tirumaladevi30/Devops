
# Lab 6: Implementing Azure Storage access controls

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Creating and configuring an Azure Storage account](#exercise-1-creating-and-configuring-an-azure-storage-account)
    
[Exercise 2: Creating and managing blobs](#exercise-2-creating-and-managing-blobs)   
    

## Overview

The aim of this Lab is to create a Storage account and Add container to it, then upload data into the container and give the access by using SaaS token.

### Scenario and Objectives

XYZ Corporation wants to protect content residing in Azure Storage

You will be able to:

* Create an Azure Storage account.
* Upload data to Azure Storage.
* Implement Azure Storage access controls.

## Pre-Requisites

* Familiar with Storage Account

* Powershell

## Exercise 1: Creating and configuring an Azure Storage account

The main tasks for this exercise are as follows:

1.	Create a storage account in Azure
2.	View the properties of the storage account

### Task 1: Create a storage account in Azure

**Storage Account**

An Azure storage account contains all your Azure Storage data objects: blobs, files, queues, tables, and disks. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS.

1.	Start Google Chrome and browse to the Azure portal at http://portal.azure.com and sign in by using the Microsoft account.

Using the Chrome browser, login into Azure portal with the below details.


**Azure login_ID:** {{azure-login-id}} <br>

**Azure login_Password:** {{azure-login-password}}<br>

 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/1.png?st=2019-08-30T05%3A02%3A03Z&se=2022-08-31T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HcsLrLR5p%2B%2Fi8Tqc5%2F2QvI7eZR7OI9IoJaW4AruQ%2BhI%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/2.png?st=2019-08-30T05%3A02%3A55Z&se=2022-08-31T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=T%2Bx0mo7CqG2Em3rKu0pODIP8CWXA17nacrDlHiZNLWs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/portal1.PNG?st=2019-08-30T05%3A03%3A21Z&se=2022-08-31T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jW1pjQanSiOrLUXCpD4SmiWO%2B4B8OjKo8mtMmmC1Fzo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/portal2.PNG?st=2019-08-30T05%3A03%3A54Z&se=2022-08-31T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3VyAZiVWhjuIPn0lPQAZGFLimfyMeccJVlCKICVkVHg%3D)

2.	From Azure Portal, create a new storage account with the following settings:

**Basics**



**Subscription**: Select the default
**Resource group**: {{resource-group-name}} <br>
**Storage account name**: any valid, unique name between 3 and 24 characters consisting of lowercase letters and digits
**Location**: {{location}} <br>
**Performance**: Standard
**Account kind**: Storage (general purpose v1)
**Replication**: Locally-redundant storage (LRS)


**Advanced**

```
Secure transfer required: Disabled
Virtual network: All networks
Blob soft delete: Disabled
Hierarchical namespace: Disabled

```

**Tags**

```
Note: Don't make any changes to other settings, leave them as is.

```

**Review + Create**

```
After the Validation passed, select Create button

```


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/3.png?st=2019-08-30T05%3A04%3A25Z&se=2022-08-31T05%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CdkhhOaYfMxRwM4U5CEuaBK%2BdCGjtduoKQzKAAy1k40%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/4.png?st=2019-08-30T05%3A04%3A49Z&se=2022-08-31T05%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0lWHY9nvg3q4vPYKzYknQV4Yd3KFZbjYE6YhLr64WQI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-5.PNG?st=2019-08-30T05%3A07%3A07Z&se=2022-08-31T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GxolDK4FpFN1i08v2X%2B%2B9FAXc3lT3n9EEmt9bwjgqzU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/6.png?st=2019-08-30T05%3A07%3A38Z&se=2022-08-31T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BLIFvoFjfH7FG5e2UXH1XhpdsdBjPfKWtOK%2F8zFu1yI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/7.png?st=2019-08-30T05%3A07%3A58Z&se=2022-08-31T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jJD93yWbg4%2BWK9HNhZ8YlnqyXmy%2FOM8Z6kPOuOroAgU%3D)

3.	Wait for the storage account to be provisioned. This will take about a minute.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-3.png?st=2019-08-30T05%3A08%3A26Z&se=2022-08-31T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w82BVsMIjaqI34ADHu8OcfnkvDX7IZT9XUElQUzQyEU%3D)

### Task 2: View the properties of the storage account

1.	In Azure Portal, with your storage account blade open, review the Overview section, including the location, replication, and performance settings.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/300-4.PNG?st=2019-08-29T07%3A41%3A20Z&se=2022-08-30T07%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wey1A1OXtlbgPy1EGEWtuVK%2FMcfSPwSmka%2BHEb1zCSs%3D)

2.	Display the **Access keys** blade. On the access keys blade, note that you have the option of copying the values of storage account names including key1 and key2. You also can regenerate both keys.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/12.png?st=2019-08-30T05%3A08%3A59Z&se=2022-08-31T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pwzFloa8H1s4eGVwatPi%2FRZ2Xvur1weFrr2H%2Fcwm44g%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/13.png?st=2019-08-30T05%3A09%3A22Z&se=2022-08-31T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7MxP99jcFe2%2FF5iMFr5s7pgUP%2BaFfjW3WodKVnoRu0Q%3D)

3.	Display the Configuration blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/14.png?st=2019-08-30T05%3A09%3A42Z&se=2022-08-31T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9ry9Mvhw1NGDA5dK8g0ShYKDcCA1krEX15UUf8TKSnY%3D)

4.	On the **Configuration** blade, notice that you have the option of performing an upgrade to **General Purpose v2** account and changing the replication settings. However, you cannot change the performance setting (this can only be assigned when the storage account is created).

**Result:** After you completed this exercise, you have created your Azure Storage and examined its properties.

## Exercise 2: Creating and managing blobs

The main tasks for this exercise are as follows:

1.	Create a container
2.	Upload data to the container by using the Azure portal
3.	Access content of Azure Storage account by using a SAS token

### Task 1: Create a container

1.	In the Azure portal, navigate to the blade displaying the properties of the storage account you created in the previous task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/15.png?st=2019-08-30T05%3A10%3A03Z&se=2022-08-31T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9tWexcd73Og15D3Quzb2Q5AYMPm2YYWsd0G%2BCK034Y4%3D)

2.	From the storage account blade, create a new blob container with the following settings:

```

    Name: labcontainer
    Access type: Private

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/16.png?st=2019-08-30T05%3A10%3A23Z&se=2022-08-31T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tiMuk2NHnWQvq%2F35QdiUlu6pmSQC03dhyhKwdbkjYx8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/17.png?st=2019-08-30T05%3A10%3A42Z&se=2022-08-31T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Bkd6zX3zIfucrJvNVvEnBmRZDJksB8ULEUW1tyI8Xhw%3D)

### Task 2: Upload data to the container by using the Azure portal

1.	In the Azure portal, navigate to the **labcontainer** blade.

2.	Download image from the Google Chrome and save it. Upload image from saved folder.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/lab6-18.png?st=2019-11-07T10%3A53%3A54Z&se=2026-11-08T10%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1RpDDO9BcxSkzvyJ%2FKtAAIrCs7%2B2%2FcF8k0jIPaeG1f0%3D)


https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/uploaded-image.PNG?st=2019-08-29T07%3A30%3A21Z&se=2022-08-30T07%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hQHT8xQ0XKSF%2B3VarTwehKumPCgb7fsYTrxr9dWD%2FlA%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-6.PNG?st=2019-08-30T05%3A11%3A32Z&se=2022-08-31T05%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PS6v%2F8D6bCAX1XiBPuCQKE6eOz8Idqj4Q30B4G%2FNPjE%3D)

3. 	From the **labcontainer** blade, upload the file

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/19.png?st=2019-08-30T05%3A11%3A58Z&se=2022-08-31T05%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NQkWc499ZoOoplUaeoqJEWl8YKhd2mjDgwEYM7LZPvI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/19.png?st=2019-08-30T05%3A11%3A58Z&se=2022-08-31T05%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NQkWc499ZoOoplUaeoqJEWl8YKhd2mjDgwEYM7LZPvI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-8.PNG?st=2019-08-30T05%3A12%3A41Z&se=2022-08-31T05%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d497cSoNy3GkI7TF7D8mwMKhvTuJfb9wO7aWFzUuGGg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-9.PNG?st=2019-08-30T05%3A13%3A00Z&se=2022-08-31T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BWvXmnYeyKhpJr0sVjWM0ScOV7ozpI1Vn97JB7ls0FM%3D)

### Task 3: Access content of Azure Storage account by using a SAS token

1.	From the **labcontainer** blade, identify the URL of the newly uploaded blob.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-17.PNG?st=2019-08-30T05%3A13%3A24Z&se=2022-08-31T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=thYyZncyxB9PfyDnRDn1P1lZscF%2F%2BTvfYxoGrvmojIE%3D)

2.	Start Google Chrome and navigate to that URL.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-18.PNG?st=2019-08-30T05%3A13%3A48Z&se=2022-08-31T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s9wsgi6pMPhwge7MwHwW7i65YaNZZDMN3TZnwUfPWos%3D)

3.	Note the **ResourceNotFound** error message. This is expected since the blob is residing in a private container, which requires authenticated access.
4.	Switch to the Google Chrome window displaying the Azure portal and, on your **uploaded image** blade, switch to the **Generate SAS** tab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-20.PNG?st=2019-08-30T05%3A14%3A14Z&se=2022-08-31T05%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dguoV8fODfBF%2BrNbg5q1jYfSz5L6%2FhYunzl4k0VQVjQ%3D)

5.	On the **Generate SAS** tab, enable the **HTTP** option and generate blob SAS token and the corresponding URL.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/26.png?st=2019-08-30T05%3A14%3A43Z&se=2022-08-31T05%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ab4ahYGR0pYDGPgt6G1lMAXmOQWQZwl%2BTWegicxz4H4%3D)

6.	Open a new Google Chrome window and, in the navigate to the URL generated in the previous step.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/27.png?st=2019-08-30T05%3A15%3A03Z&se=2022-08-31T05%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vY8vuQ%2BGdyMJl12%2F9t5OJ3nsWX7GjVeq7r8rk2RSQSk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-19.PNG?st=2019-08-30T05%3A15%3A25Z&se=2022-08-31T05%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7CYJvOK46aXz2ECRFnhzh9sGRpiKrF2S9ZE3AarB9w8%3D)

7.	Note that you can view the image. This is expected since this time you are authorized to access the blob based on the SAS token included in the URL.

### Task 4: Access content of Azure Storage account by using a SAS token and a stored access policy.

1.	In the Azure portal, navigate to the **labcontainer** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/29.png?st=2019-08-30T05%3A15%3A46Z&se=2022-08-31T05%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4%2BXo9RHxfkqiNURiQQ0FfxsQjT72ySwwtpm1AgDZ%2BzA%3D)

2.	From the **labcontainer** blade, navigate to the **labcontainer - Access policy** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/30.png?st=2019-08-30T05%3A16%3A06Z&se=2022-08-31T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vin4GWFJWBPi7uUhGxm2j%2BJTG7k3jkzDMfeCNQ%2FVGr0%3D)

3.	Add a new policy with the following settings:

```

    Identifier: labcontainer-read
    Permissions: Read
    Start time: current date and time
    Expiry time: current date and time + 24 hours

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/31.png?st=2019-08-30T05%3A16%3A28Z&se=2022-08-31T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mlTigTwrLo%2BMhfGYrkef37ganocWP20AQxMTRFLqXSE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/32.png?st=2019-08-30T05%3A16%3A47Z&se=2022-08-31T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W6NNm9v9%2FU9XiKlCJSCgtnaXRUqbm%2FGaLfOPsxDdbgA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/33.png?st=2019-08-30T05%3A17%3A05Z&se=2022-08-31T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nM%2BalS2oo0R89JxcembXoPu5WSv%2BHnp9erd8riND9og%3D)

4.	In the Azure portal, in the Google Chrome window, start a **PowerShell** session within the **Cloud Shell.**

**Powershell**

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/34.png?st=2019-08-30T05%3A17%3A22Z&se=2022-08-31T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iYTwc0F0nF4aCI6ubh5iILF4xrIAwKP6tIK7fh6ibLI%3D)

5.	If you are presented with the **You have no storage mounted** message, configure storage using the following settings:



* Subscription: Select the default
* Cloud Shell region: East US 
* Resource group: {{resource-group-name}} <br>
* Storage account: use existing
* File share: a name of a new file share


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/36.png?st=2019-08-30T05%3A17%3A45Z&se=2022-08-31T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gKneHG%2B9BUEuVAJ2by1Wx2j%2BouxSy%2FURLwVLh%2BaRuKg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-11.PNG?st=2019-08-30T05%3A18%3A09Z&se=2022-08-31T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9YZNlJKrImWZQvMZmZmVQiYt6gAgiqMqiJQ7NuzROqY%3D)

6.	From the Cloud Shell pane, run the following to identify the storage account resource you created in the first exercise of this lab and store it in a variable:

**Ex:**

**$storageAccount = (Get-AzStorageAccount -ResourceGroupName 'existing ResourceGroup Name')[0]**
 

$storageAccount = (Get-AzStorageAccount -ResourceGroupName {{resource-group-name}} <br>)[0]


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-12.PNG?st=2019-08-30T05%3A18%3A28Z&se=2022-08-31T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sRrTUFOoXPR3CHaGzIGm%2Bmxz96lPCRN86dA7uijy5EU%3D)

7.	From the Cloud Shell pane, run the following to establish security context granting full control to the storage account:

```

$keyContext = $storageAccount.Context

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/39.png?st=2019-08-30T05%3A18%3A53Z&se=2022-08-31T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0eoU3NriX7J8LP%2Fz4EJeJC2FQswV1lZP5CZQescH4mc%3D)

8.	From the Cloud Shell pane, run the following to create a blob-specific SAS token based on the access policy you created in the previous task:

**Ex:**

**$sasToken = New-AzStorageBlobSASToken -Container 'labcontainer' -Blob 'Uploaded file name' -Policy labcontainer-read -Context $keyContext**
    
```

$sasToken = New-AzStorageBlobSASToken -Container 'labcontainer' -Blob 'uploaded-image.png' -Policy labcontainer-read -Context $keyContext

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-14.PNG?st=2019-08-30T05%3A19%3A17Z&se=2022-08-31T05%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kjrKXjXYp4UUZtd0Ni7Yv5r2cdFxa1hEiOFWB%2B2g2Tk%3D)

9.	From the Cloud Shell pane, run the following to establish security context based on the newly created SAS token:

```

$sasContext = New-AzStorageContext $storageAccount.StorageAccountName -SasToken $sasToken

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/41.png?st=2019-08-30T05%3A19%3A40Z&se=2022-08-31T05%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Xa4%2BNni6k0ORnQKSe8aQV07cqWKY3LYrbOdB1tkuWsQ%3D)

10.	From the Cloud Shell pane, run the following to retrieve properties of the blob:

**Ex:**

**Get-AzStorageBlob -Container 'labcontainer' -Blob 'Uploaded file name' -Context $sasContext**
    
```

Get-AzStorageBlob -Container 'labcontainer' -Blob 'uploaded-image.png' -Context $sasContext

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-15.PNG?st=2019-08-30T05%3A20%3A06Z&se=2022-08-31T05%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RtVIgehzvm18wHoTbWIGYEJKUIMii4VsDot45eTdW%2Bc%3D)

11.	Verify that you successfully accessed the blob.
12.	Minimize the Cloud Shell pane.

### Task 5: Invalidate a SAS token by modifying its access policy.

1.	In the Azure portal, navigate to the **labcontainer - Access policy** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/300-21.PNG?st=2019-08-30T05%3A20%3A31Z&se=2022-08-31T05%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xV0DU4%2FBcGFOu2VjAoC%2B%2BxhruJZQu%2BUOBFSBzBQORfE%3D)

2.	Edit the existing policy **labcontainer-read** by setting its start and expiry time date.

**Note: Give the expired date**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/44.png?st=2019-08-30T05%3A20%3A54Z&se=2022-08-31T05%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BMJPoPNj0v8q7BXFtvngo6yERJ%2Fk9OCr2pFlVdHy7Kc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/45.png?st=2019-08-30T05%3A21%3A16Z&se=2022-08-31T05%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NogUoZSUGSTLfZGaq%2BQO33iSqQQkT53OIi%2BUi6PD1eQ%3D)

3.	Reopen the Cloud Shell pane.
4.	From the Cloud Shell pane, re-run the following to attempt retrieving properties of the blob:

**Ex:**

**Get-AzStorageBlob -Container 'labcontainer' -Blob 'Uploaded file Name' -Context $sasContext**
    
```

Get-AzStorageBlob -Container 'labcontainer' -Blob 'uploaded-image.png' -Context $sasContext

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab6-Implementing%20Azure%20Storage%20access%20controls/46.png?st=2019-08-30T05%3A21%3A44Z&se=2022-08-31T05%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ITx%2Brm8b3rWGdbCwZzVzYVehayLB6TQuBcgTjsHDZBE%3D)

5.	Verify that you no longer can access the blob.

**Result:** After you completed this exercise, you have created a blob container, uploaded a file into it, and tested access control by using a SAS token and a stored access policy.
