# Lab 2: Microsoft Azure management tools

## Table of Contents 

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Using the Azure PowerShell modules](#exercise-1-using-the-azure-powerShell-modules)
    
[Exercise 2: Using the Azure CLI](#exercise-2-using-the-azure-cli)
    

## Overview

The aim of this Lab is to become familiarize with the primary Azure management tools. 

### Scenario and Objectives

To prepare for the deployment of Azure services, you want to become familiar with the primary Azure management tools. Most of your on-premises administrative tasks are automated by means of PowerShell scripts and Linux shell scripts. You have decided to test the use of Azure PowerShell and the Azure CLI.

After completing this lab, you will be able to:
* Install the Azure PowerShell modules and the Azure CLI.
* Use Azure PowerShell and the Azure CLI to connect to your Azure subscription.
* Run Azure PowerShell cmdlets and Azure CLI commands against your Azure subscriptions.


## Pre-Requisites

* Lab Virtual Machine
* Azure Power shell
* Azure CLI

Note: Pre-Requisites are provided as part of Lab environment

## Exercise 1: Using the Azure PowerShell modules

**Using the Chrome browser, login into Azure portal with the below details.**


**Azure login_ID:** {{azure-login-id}} 

**Azure login_Password:** {{azure-login-password}}

**Region:** {{Location}}

**ResourceGroup:** {{resource-group-name}}

**Subscription Id:** select the default from the dropdown

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a34.PNG?st=2019-09-11T10%3A06%3A54Z&se=2022-09-12T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vbKW8mRCpbMVMXv3AdOgA1P9p%2BcJDW5M0X3zBBdS05U%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a35.PNG?st=2019-09-11T10%3A07%3A18Z&se=2022-09-12T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Hb%2FXswZLoOoYFMFw0hAKVcSFaZR132jwv1JomheApdM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a36.PNG?st=2019-09-11T10%3A07%3A41Z&se=2022-09-12T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bqasX07ucQSHfScOUOhI1LZ2U9laEpUD4qBA%2BnUE4r0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a37.PNG?st=2019-09-11T10%3A08%3A05Z&se=2022-09-12T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t%2BCWBs%2BUSgfYJKVvx5cz7vMLKJXCZe3Q2rBnUohdyLA%3D)

**Lab Setup:**

1. Start a Remote Desktop session targeting FQDN of the Virtual Machine and provide username and password of your Azure VM.

2. You can start a Remote Destop client, by selecting the windows icon on top right side of the Lab Window.


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/4.PNG?st=2019-09-13T04%3A43%3A04Z&se=2022-09-14T04%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8wx3lo3%2FL8b99WjDcrsmEKbd02gKDgf2HMYJQuI3HCc%3D)


**VirtualMachine FQDN:** {{VmFqdn}}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/1.PNG?st=2019-09-13T04%3A31%3A26Z&se=2022-09-14T04%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=o0Va2QRAOpytP2YdyiFnCLms6BLT%2BuX1sUgjcP2%2BQ%2FI%3D)


**VirtualMachine Username:** {{VmUsername}}

**VirtualMachine Password:** {{VmPassword}}


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/2.PNG?st=2019-09-13T04%3A32%3A38Z&se=2022-09-14T04%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FhTGcR663Af5XJHidMu3PHROt9UZjYtCjRjiyFuxCbI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/3.PNG?st=2019-09-13T04%3A32%3A17Z&se=2022-09-14T04%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LiYAqh9lstmGM%2FNsN5G%2BAkqbfB%2FpIrCf7Lg8tT22rIA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/6.png?st=2019-09-13T04%3A34%3A34Z&se=2022-09-14T04%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oAyIYJ5YSvyq8V%2FZW630NzFvboAzyZTAGZoRSPxMc4c%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/5.PNG?st=2019-09-13T04%3A34%3A59Z&se=2022-09-14T04%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=A4Mo9hqIIpinYNzjXL%2F6VqLdpxh7qOILOsgiZox%2BJ%2Bo%3D)


**Scenario**

In this exercise, you will use the Azure PowerShell modules.

The main tasks for this exercise are as follows:

1.	Install the Azure PowerShell modules

2.	Connect to your Azure subscription

3.	Use Azure PowerShell cmdlets

### Task 1: Install the Azure PowerShell modules

**Azure Power shell**

Azure PowerShell is an extension of the Windows PowerShell platform and scripting language developed to provide cmdlets for simplifying and automating the management of Azure cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

1.	Open Google Chrome on your lab, and then browse to *https://azure.microsoft.com/en-us/downloads/*.

2.	In the **Command-line tools** section, click **Windows install** under **PowerShell** to download         **WindowsAzurePowerShellGet.3f.3f.3fnew.exe** and start the Web Platform Installer.

3.	In the **Web Platform Installer 5.0** window, note the **Install** button but do not click on it. Instead, click **Exit** to close    the **Web Platform Installer 5.0** window.

4. Do not initiate the installation. Instead, close Google Chrome.

   **Note:** PowerShell is already preinstalled on the lab virtual machine.**

5. Need to install PowerShell modules 

6. Start the PowerShell as an administrator and type the following commands.

```

Install-Module -Name AzureRM.profile -RequiredVersion 5.8.2

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a24.PNG?st=2019-09-11T09%3A15%3A28Z&se=2022-09-12T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fXl%2BNiV7FnQx35bq45wn3ssYzojsqYau859wxzaTnjU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a25.PNG?st=2019-09-11T09%3A14%3A24Z&se=2022-09-12T09%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xionoPyfi4uFBeIAEatqLsBa9735jaz6Zhq6Ykxn0Mc%3D)

```

Install-Module -Name Azure.Storage -RequiredVersion 4.5.0

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a26.PNG?st=2019-09-11T09%3A15%3A57Z&se=2022-09-12T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iZCtokoUWwwBvN3AdfuHuoF4VzY2canq7USlkZGdOqg%3D)

```
Install-Module -Name AzureRM.Resources -RequiredVersion 6.0.1

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a27.PNG?st=2019-09-11T09%3A16%3A22Z&se=2022-09-12T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fvvUIRY3tX3o6v%2Fk%2FpA0LvGzJluFpauGfqBN7g0itbw%3D)

**References:**

https://www.powershellgallery.com/packages/AzureRM.profile/5.8.2

https://www.powershellgallery.com/packages/Azure.Storage/4.5.0

https://www.powershellgallery.com/packages/AzureRM.Resources/6.0.1

### Task 2: Connect to your Azure subscription

1.	 Start the Windows PowerShell as an administrator.

2.	In the **Administrator: Windows PowerShell** window, list all the available Azure PowerShell modules by running the following cmdlet:

```
Get-Module -ListAvailable -Name Azure*

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a1.PNG?st=2019-09-11T09%3A16%3A55Z&se=2022-09-12T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xbeT20ZCZUT7X2VC4nMu5xo5xPCi%2FLCKIotAej7iLF0%3D)

```
Get-Module -ListAvailable -Name powershell*

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a2.png?st=2019-09-11T09%3A17%3A15Z&se=2022-09-12T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7atzG8ywHCyQ6u1tlAQE7AkURYe6yvack5XrMXhHqdY%3D)

**Note:** *The output contains a list of a number of Azure-specific PowerShell modules, including AzureRM. modules, the Azure PowerShell module, and the Azure.Storage module.*

3.	Sign in to your Azure subscription with the Microsoft account that is the Service Administrator of your Azure subscription by running the following Azure PowerShell cmdlet:

```
Connect-AzureRmAccount

```

Login to Azure Portal using below details

**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

**Note:** *The cmdlet returns the list of subscriptions associated with your Microsoft account.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a3.png?st=2019-09-11T09%3A17%3A36Z&se=2022-09-12T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GPuAJ5m9j%2FuKIfhnPqxVDV%2BN0l1XxS8fuAr6TxLUoCI%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a4.png?st=2019-09-11T09%3A17%3A58Z&se=2022-09-12T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TFCA2LF8u6JwfHcWCtSv2v4EApf07uy5ocELoZ9swLM%3D)

### Task 3: Use Azure PowerShell cmdlets

1.	Back at the **Administrator: Windows PowerShell** prompt, retrieve the list of subscriptions associated with your Microsoft account by running the following cmdlet:

```
Get-AzureRmSubscription

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a5.png?st=2019-09-11T09%3A18%3A42Z&se=2022-09-12T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RgLQeMrc2KdjR1arlQsicH7ScDHags4J5ec%2FI%2B5M3CM%3D) 

2.	Select the target Azure subscription by running the following cmdlet, replacing <value of the subscription id property> with the value of the Subscription Id property returned by the Get-AzureRmSubscription cmdlet:
    

**value of Subscription Id:** {{subscriptionId}}
   

```

Select-AzureRmSubscription -SubscriptionId <value of subscriptionid>

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a6.png?st=2019-09-11T09%3A19%3A04Z&se=2022-09-12T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IHOOKUPP0QBVaX4qF8%2BkDCRINGJBrRs7M5FnpHtq%2BW0%3D) 

**Note:** *If you had multiple subscriptions, you would use the preceding cmdlet to specify the Azure subscription you want to work with in the current PowerShell session.*

3.	To retrieve the types of Azure Resource Manager resources you can create in your subscription by running the following cmdlet:

```
Get-AzureRmResourceProvider

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a7.png?st=2019-09-11T09%3A19%3A26Z&se=2022-09-12T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LVYBq%2B9zuS9ZLUJVF4Vk5JDDyVi1Wd81vaYJk2uyzFQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a8.png?st=2019-09-11T09%3A19%3A47Z&se=2022-09-12T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kvVSiU9cDKPFZ48hyzGT2rTfXyDvU289fXLxp3O0bEo%3D)

**Note:** *This cmdlet lists each Azure Resource Provider, its registration state (the provider must be registered before you can use it), and the list of resource types you can create by referencing it.*

4.	Identify the list of resources that are implemented by the Microsoft.Compute Azure Resource Manager resource provider (which includes Azure Virtual Machines) by running the following cmdlet:

```
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Compute

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a9.png?st=2019-09-11T09%3A20%3A14Z&se=2022-09-12T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4WXFWXpOGVOD6DcxoucaWsNIrpAIjfFunyQOtt9dL3w%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a10.png?st=2019-09-11T09%3A20%3A40Z&se=2022-09-12T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4nl%2FOU%2FgjB%2BvFD11lM5T9BfUYaDDRRUScFkWhxYHzeI%3D)

5.	Identify the list of resources that are implemented by the Microsoft.Compute by running the following cmdlet: Azure Resource Manager resource provider in the East US Azure region.

```
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Compute -Location 'East US'

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a11.png?st=2019-09-11T09%3A21%3A02Z&se=2022-09-12T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6FE7Hz2bob4AauSY9cGL97ZrKKOHYdNOzdEMOWfBFe0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a12.png?st=2019-09-11T09%3A21%3A29Z&se=2022-09-12T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PCItMXkzT%2B6BcW7o9nEUgdHPbaG56nkqKeEUNlnsyQI%3D)
 
6.	Close the Windows PowerShell.

**Result:** *Once you completed this exercise, you have successfully used the Azure PowerShell modules.*

## Exercise 2: Using the Azure CLI

**Azure CLI**

Azure CLI is also a command-line tool introduced by Microsoft which can use to manage Azure resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows.

## Scenario

In this exercise, you will install and use the Azure CLI.

The main tasks for this exercise are as follows:

1.	Install the Azure CLI

2.	Connect to your Azure subscription by using the Azure CLI

3.	Manage your Azure subscription by using the Azure CLI

4.	Prepare for the next module

### Task 1: Install the Azure CLI

1.	In Google Chrome, browse to https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest and note the **Download the MSI installer** link.

2.	Do not initiate the installation. Instead, close Google Chrome.

**Note: Azure CLI is already preinstalled on the lab VM.**

### Task 2: Connect to your Azure subscription by using the Azure CLI

1.	Start the command prompt as an administrator.

2.	In the **Administrator: Command Prompt** window, type the following command:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a32.png?st=2019-09-11T09%3A21%3A57Z&se=2022-09-12T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Fc0lj4gM%2BNnMXWlyIE%2Bn7MJeg2OUVnVWKw%2FplSJ%2BeWM%3D)

**Note:** *A summary of the most-common Azure CLI commands displays.*

3.	At the command prompt, run the following command:

```
az login

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a31.png?st=2019-09-11T09%3A22%3A33Z&se=2022-09-12T09%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sFjWXuUlqPGMiF%2BUo9PGDXz%2F3q786lmSq%2FC8M1chc5k%3D)

Login into Azure CLI using below details

**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a13.png?st=2019-09-11T09%3A22%3A57Z&se=2022-09-12T09%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JjF%2BUzNC4BSrDG4z1v7NKbEsrZR%2Fu8WwH5jbTttTxWE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a14.png?st=2019-09-11T09%3A23%3A16Z&se=2022-09-12T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=o%2BzGo5fkaS2LT%2BN%2FfKRWVm%2BgYyIXNBS6o1Tji11%2BmOs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a15.png?st=2019-09-11T09%3A23%3A36Z&se=2022-09-12T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hkQXnVN4YQiDv1MQ9xZwjR9djTdgwf%2B70znPv55gtxE%3D) 

 
4.	When prompted, sign in with the Microsoft account that is the Service Administrator of your Azure subscription.

5.	Back in the **Administrator: Command Prompt** window, note the JSON-formatted output displaying information about the current session, including the ID of the subscription that your account is associated with.

6.	In case of an error, repeat the steps 3 through 5.

### Task 3: Manage your Azure subscription by using the Azure CLI

1.	List your subscriptions by running the following command:

```
az account list

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a16.png?st=2019-09-11T09%3A24%3A01Z&se=2022-09-12T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=28l5yXhupdnE3Lf5%2FKl1nui74%2BBRUzj3Jt5YS7eWcc8%3D) 

2.	Copy the value of the **id** property displayed in the output of the preceding command.

3.	Run the following command, pasting the copied entry to replace the value of the <value of the subscription id property> placeholder:

**value of Subscription Id:** {{subscriptionId}}

```
az account set --subscription <value of the subscription id>

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a17.png?st=2019-09-11T09%3A24%3A27Z&se=2022-09-12T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1s%2BZaF%2Fn9yL880BGtnNqoMhgjTA51rw0RJIcSqoNSFo%3D)

**Note:** *If you had multiple subscriptions, you would use the preceding command to specify the Azure subscription you want to work with in the current Azure CLI session.*

4.	To retrieve the types of Azure Resource Manager providers available in your subscription, run the following command:

```
az provider list

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a18.png?st=2019-09-11T09%3A24%3A47Z&se=2022-09-12T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HalSg1jyjKMcMogEC%2FNA5t9cBzit%2B5d16mCd5kDUBmM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a19.png?st=2019-09-11T09%3A25%3A06Z&se=2022-09-12T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1r3Wgz5QwCGYNgVZSuoQxrW0Xz%2F9zieQDalGLP1qjXQ%3D)
 
**Note:** *The output of the command contains each Azure Resource Provider available in your subscription and its registration state (the provider must be registered before you can use it).*

5.	To list all the Azure datacenters available in the current subscription, run the following command:

```
az account list-locations

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a20.png?st=2019-09-11T09%3A25%3A28Z&se=2022-09-12T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CHg8NbIFG6%2BWk6PJJLBXjiM%2BcVbZNYJAckq0ob4G7kw%3D) 

6.	To identify the list of resources that are implemented by the Microsoft.Compute provider (which includes Azure Virtual Machines) along with the list of locations where they are available, run the following command:

```
az provider show --namespace Microsoft.Compute

```
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a21.png?st=2019-09-11T09%3A25%3A54Z&se=2022-09-12T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DxnxqiT7J9tGh65fc2NhblCdfhduSF6RCkbWBe%2BTOlI%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a22.png?st=2019-09-11T09%3A26%3A16Z&se=2022-09-12T09%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4%2FSLAUyCoFdIYOJCfS5wzwSLrcAAEcdsc6jq1KVUb24%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab2-Microsoft%20Azure%20Management%20tools/a23.png?st=2019-09-11T09%3A26%3A35Z&se=2022-09-12T09%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W9%2BQlzzHMDtmhO6L89OhO9bqJbEbwSAAjajnL7mocVM%3D)
 
7.	Close the **Administrator: Command Prompt** window.

**Result:** *Once you completed this exercise, you have used the Azure CLI.*
