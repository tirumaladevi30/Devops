# Lab 3: Creating Virtual machines in Microsoft Azure

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Creating a VM from the Azure portal by using an Azure Marketplace image](#exercise-1-creating-a-vm-from-the-azure-portal-by-using-an-azure-marketplace-image)
    
[Exercise 2: Verifying the functionality of the VM](#exercise-2-verifying-the-functionality-of-the-vm)   
    
[Exercise 3: Configuring storage of a VM](#exercise-3-configuring-storage-of-a-vm)
    

## Overview

The aim of this Lab is to deploy the Windows Server 2016 Datacenter VM in Azure and attach two data disks to a deployed VM then connect the VM through RDP. 
Create service pool from the attached disks and export that pool into virtual disk, then mount a volume from the virtual disk.

### Scenario and Objectives

Orders at XYZ Training Labs Corporation have increased significantly. Currently, the order system runs on on-premises servers which provides other services. You have decided to migrate the order system to dedicated Azure VMs. The Azure VMs must include sufficient storage to accommodate increased volume of orders.

After completing this lab, you will be able to:

*	Create Azure VMs by using the Azure portal.

*	Connect to Azure VMs.

*	Attach a data disks to Azure VMs.

*	Create multidisk volumes on Azure VMs.

## Pre-Requisites

* Windows Server 2016 Datacenter

* Remote Desktop (RDP)

Note: Azure Portal access & Remote Desktop are provided as part of the Lab environment.

## Exercise 1: Creating a VM from the Azure portal by using an Azure Marketplace image

**Windows Server 2016 Datacenter**

Windows Server Datacenter is a server operating  system that enables a computer to handle network roles such as print server, domain controller, web server, and file server.

**Scenario**

To prepare for planned deployment, you decide to test the process of creating new Azure VMs from the Azure portal by using an Azure Marketplace images.

The main tasks for this exercise are as follows:

*	Create a VM

*	Verify VM creation

*	Prepare for the next module

### Task 1: Create a VM

1.	From the Azure Portal, create a new VM by using the Windows Server 2016 Datacenter Marketplace image and Resource Manager deployment model with the following settings:

Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Azure Portal Username }}

Azure Password: {{ Azure Portal Password }}

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/portalLogin.PNG?st=2019-08-27T04%3A13%3A10Z&se=2022-08-28T04%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=liEVDwFgm%2FxfkaX32QojdnVYOIoirrrRb%2FB2z%2FcXBg4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/portal4.PNG?st=2019-08-27T04%3A14%3A24Z&se=2022-08-28T04%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cq1T4QrR1JNm3WZduBVKpzx5dt54AvaByPmE7bq8Jf0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/portal1.PNG?st=2019-08-27T04%3A15%3A11Z&se=2022-08-28T04%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SxFfAoQ6NM0FmPF2jyzJT%2FEV4kpIRzlaa%2Bl%2BqT3g524%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/portal2.PNG?st=2019-08-27T04%3A15%3A56Z&se=2022-08-28T04%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iZudA3b6Eu4NNbosFTs6uKiky8819Nc%2BMs6ocQoE6Dk%3D)

> **Basics**

```

Subscription: Select the default

Resource group: {{ ResourceGroup }}

Virtual machine name: 10979E0301-vm

Region: {{ Location }} 

Availability options: No infrastructure redundancy required

Image: Windows Server 2016 Datacenter

Size: Standard DS1 v2 "This is the default size, don't change leave this as is"

Username: Student

Password: Password@123

Confirm password: Password@123

Inbound port rules: select Allow selected ports option

Select inbound ports: RDP

Already have a Windows license: No

```

> **Disks**

```

OS disk type: Standard HDD

Navigate to Advanced

Use managed disks: Yes

```

> **Networking**

```

Virtual network: accept the default value ( This will create a new virtual network )

Subnet: accept the default value ( This will create a /24 subnet named default within the IP address space of the virtual network )

Public IP address: (new) 10979E0301-vm-ip

Network security group: Basic

Public inbound ports: Allow selected ports

Select inbound ports: RDP

Accelerated networking: Off

Load balancing: No

```

> **Management**

```

Boot diagnostics: On

OS guest diagnostics: Off

Diagnostics storage account: accept the default value (this will create a new storage account)

Managed service identity: Off

Enable auto-shutdown: Off

Note: Don't make any changes to other settings, leave them as is.

```

> **Advanced**

```

Note: Don't make any changes to other settings, leave them as is.

```

> **Tags**

```
Note: Don't make any changes to other settings, leave them as is.

```

> **Review + Create**

```

After the Validation passed, select Create button

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/portal3.PNG?st=2019-08-27T04%3A19%3A06Z&se=2022-08-28T04%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GYBKlt%2FnlxfgeBlmjMWLHev6xRBcoUSsEU1HXALnP3U%3D) 
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/2.png?st=2019-08-27T04%3A19%3A47Z&se=2022-08-28T04%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qgziQfGfEj4Y8ifm9HW1yz9dGHofNg8KHkuXX%2Fq4wcA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-1.png?st=2019-08-27T04%3A20%3A26Z&se=2022-08-28T04%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cj%2BUzDQY%2FKHUrkTGgg6vkP4g0%2By9jcnP8US4Srrrp2o%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-2.png?st=2019-08-27T04%3A20%3A53Z&se=2022-08-28T04%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2cRT7U2IOw2ccMkOow6TWxFhG2QH%2FcfD7BmTZFG0erM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-3.png?st=2019-08-27T04%3A21%3A22Z&se=2022-08-28T04%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c8T0uyje5wdVBt8IsB%2BJ4lE9bRkrsA7ef7Luu6Atgto%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-4.png?st=2019-08-27T04%3A21%3A51Z&se=2022-08-28T04%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0mbYskjP%2BFsRZerWR1w2oWibH%2B5GAbmJ%2FoUXhRxIho4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-5.png?st=2019-08-27T04%3A22%3A17Z&se=2022-08-28T04%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZxI1%2BUn7SzvUDy8%2Bni3A%2BxFRJtezvdDFpPEz1jtHCZI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-6.png?st=2019-08-27T04%3A22%3A43Z&se=2022-08-28T04%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=807MWzrZKWlqFsTzu61gecdKHkKZ2pvSV8qdynZ0Ewc%3D)
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-7.png?st=2019-08-27T04%3A23%3A42Z&se=2022-08-28T04%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FhIv5XG55hbEFtUtSjS%2FmCGOzTVQQ%2BLGQpdnuG9QwJw%3D)
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-8.png?st=2019-08-27T04%3A24%3A08Z&se=2022-08-28T04%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=M6kymrRf%2Blq0%2BujA%2BOSQ%2FAGB9R%2FKb4c5CUbCVsIk%2FWA%3D)
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-24.png?st=2019-08-27T04%3A25%3A44Z&se=2022-08-28T04%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ctofrR9oI55FzqQIeycP3KcMZ8I1UYq4XaQgO02XM1A%3D)
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-10.png?st=2019-08-27T04%3A26%3A33Z&se=2022-08-28T04%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MTqi9rGmZME6mh54F3mCd2Zsd8Nvs%2F09TlaQncom%2F2o%3D)
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-11.png?st=2019-08-27T04%3A26%3A57Z&se=2022-08-28T04%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kWzQdX3FXDDXbYGfTqTN42e2YYlYUmdQ3%2FQbq4arHPA%3D)
 
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-12.png?st=2019-08-27T04%3A27%3A21Z&se=2022-08-28T04%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E96cPI506hR7dqlOSfQcdfRZByDQFndIcdSAH55pFRk%3D)
  
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-13.png?st=2019-08-27T04%3A27%3A43Z&se=2022-08-28T04%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=72BJekV%2Fkx5R%2FsDXLgJ4QMbnBJy%2BkK5iS2%2BqWM1Qw9w%3D)
 
 
2.	Review the **Your deployment is underway** blade.

3.	Wait for the deployment to complete.

4.	**Note:** *The deployment might take about 5 minutes* 

### Task 2: Verify VM creation

1. In the Azure Portal, on the **Your deployment is complete** blade, click **Go to resource**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-14.png?st=2019-08-27T04%3A28%3A10Z&se=2022-08-28T04%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qArAM9l%2FX3w524ntbftUOshPSFsqaea%2FPXxEnOTvN7g%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-15.png?st=2019-08-27T04%3A28%3A43Z&se=2022-08-28T04%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OiWMTUac1I0ota6r54bAcMz0%2FwNMPtM4Gr93jgvyz1Q%3D)

2.	Click **Activity log**. Note that the blade allows you to search for activities affecting the VM that you or other admins carried out.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/lab3-log.png?st=2019-08-27T04%3A29%3A28Z&se=2022-08-28T04%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iS3FrVjor0ZnqSVBZOSOX8QjrNneZI3mus5MF7qH0Gg%3D)


**Note:** *The list of events should include a single entry corresponding to the creation of the virtual machine. Activities represent changes to the state of the VM that you or other admins carried out, such as restarting it.*

3.	Click Overview.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-16.PNG?st=2019-08-27T04%3A30%3A03Z&se=2022-08-28T04%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MRs4xl6%2BDAhsn2PixfUKYNtj5eCJXc3ihw5G5PAaTZY%3D)
 
4.	Click Resource health.

    Navigate to Virtual machine and see resource health

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/12.png?st=2019-08-27T04%3A30%3A53Z&se=2022-08-28T04%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YpXJgmMt%2BM8nASm0uCRPl9MKi8iHj5nNRb%2B6xesJzjs%3D)

5.	Verify that there are no known Azure platform problems affecting this VM. Click **Refresh** if you receive a "Resource health unknown' message.

6.	Close the Resource health blade.

**Result:** Once you completed this lab, you have deployed a Microsoft Azure VM from the Azure Portal by using a Windows Server 2016 Datacenter Azure Marketplace image, as well as reviewed activity logs and resource health of the VM.

## Exercise 2: Verifying the functionality of the VM

**Scenario**

You successfully deployed your lab Azure VMs. Now you want to examine their properties from the Azure portal and connect to them.

The main tasks for this exercise are as follows:

1.	View the properties of the VM

2.	Connect to a VM

### Task 1: View the properties of the VM

1.	In the Google Chrome window, in the Azure Portal, on the **10979E0301-vm** blade, click **Overview**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/13.png?st=2019-08-27T04%3A31%3A22Z&se=2022-08-28T04%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dzK5d9bxOlghb4gfNYoMHc%2BxTRAiWY5tGgC%2BoZMV10E%3D)
 
2.	On the **10979E0301-vm** blade, review the **Essentials** section. You will notice that the VM has a public IP address, but not a corresponding Domain Name System (DNS) name label. In addition, the **Connect** button will be enabled  .

3.	Click **Properties** from Settings menu.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/14.png?st=2019-08-27T04%3A31%3A47Z&se=2022-08-28T04%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VEulEFUKaPywzHTpg20PWb4JKdtF8UDGp2H9l7gZUTg%3D)
 
4.	Notice that the VM also has a private IP address and the VM agent with a status of **Ready**.

### Task 2: Connect to a VM

1.	 In the Google Chrome window, in the Azure Portal, from the **10979E0301-vm** blade, establish an RDP connection to the **10979E0301-vm** VM by using the following credentials:

```

User name: Student

Password: Password@123

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/15.png?st=2019-08-27T04%3A32%3A17Z&se=2022-08-28T04%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YxwQ1y%2F8OxXKod546N2YsPCpywAN2D2%2FpqmUAp7xz6I%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/lab3-8.png?st=2019-08-27T05%3A19%3A01Z&se=2022-08-28T05%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=um32JsVG432y%2B9Fzu43c30a4j%2BhyoeJV%2ByU%2FoI9sWUI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/lab3-9.png?st=2019-08-27T05%3A19%3A24Z&se=2022-08-28T05%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Uv7eDkqgUU2QExQ%2BDgUtD%2FOzuKBvfHJnDqXPwtrCJkU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/16.png?st=2019-08-27T04%3A33%3A42Z&se=2022-08-28T04%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=H8fdnTbvuzkxy7IZjeLNlt9ghVny97Qw8J3AENshEEA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/17.png?st=2019-08-27T04%3A34%3A04Z&se=2022-08-28T04%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mdOHibigygocrgZXncXzLe3ih91foZEP7nV4igMHydg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/18.png?st=2019-08-27T04%3A34%3A26Z&se=2022-08-28T04%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UtxjLc4hG0rxOeq38yWam2VSR0Lrl7u49oWpbG19V%2B0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/19.png?st=2019-08-27T04%3A34%3A48Z&se=2022-08-28T04%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YDKY78ImgZM8YhyqAgul8dzPMVzQ2%2BlCev%2Bhiy1ns0E%3D)
 
2.	Wait until the connection is successfully established.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/20.png?st=2019-08-27T04%3A35%3A10Z&se=2022-08-28T04%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jqI5h3seKQ6Ub%2BqObVS9ZFdSd9KT%2FvQu1JsEZ5cDVqA%3D)

**Result:** *Once you completed this exercise, you have viewed properties of an Azure VM from the Azure portal and connected to the Azure VM by using Remote Desktop Protocol (RDP).*

## Exercise 3: Configuring storage of a VM

**Scenario**

Once you connected to your Azure VMs, you want to test creating multidisk volumes by attaching data disks then configuring them from the operating system that runs within the Azure VMs.

The main tasks for this exercise are as follows:

1.	Attach data disks to an Azure VM

2.	Create a two-disk volume in the Azure VM that runs Windows

3.	Prepare for the next module

### Task 1: Attach data disks to an Azure VM

1.	 In the Google Chrome window, in the Azure Portal, navigate to **10979E0301-vm** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/21.png?st=2019-08-27T04%3A35%3A35Z&se=2022-08-28T04%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=b3RBXEL6SkoK8C688LZPGyNBLI9FCAe0NmNSzhlV5OI%3D)
 
2.	From the **10979E0301-vm** blade, attach a new disk with the following settings:

```

Name: 10979E0301-vm_DataDisk1

Resource group: {{ ResourceGroup }}

Account type: Standard HDD

Source type: None (empty disk)

Size (GiB): 128
 
 ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/22.png?st=2019-08-27T04%3A35%3A59Z&se=2022-08-28T04%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=icEQJnvk0oZry5ixH69EX1XCuPfj3Wn1xmcuj3N3RyI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/23.png?st=2019-08-27T04%3A36%3A18Z&se=2022-08-28T04%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gmXLYvZzhKxjva6nfzLmbF8qm5RkttFiDfmLL8%2FDAW8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/lab3-10.png?st=2019-08-27T04%3A36%3A45Z&se=2022-08-28T04%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0qDcRv9Par%2FxIuDrBXE93rMPqOQ145MqlBod3NCXWg8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-18.PNG?st=2019-08-27T04%3A37%3A13Z&se=2022-08-28T04%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0niUFU88zmJvL7p1teEYeaOrWi%2FEvz4QL%2BNe8kPUQn8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-19.PNG?st=2019-08-27T04%3A37%3A33Z&se=2022-08-28T04%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Oeb9UGfmu%2FlXMbYNc66LYoxvWA79ga1EmGFgaFGXgTs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-20.PNG?st=2019-08-27T04%3A38%3A03Z&se=2022-08-28T04%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QmXxPkrGbtGeJTM77UBnc5o97vyUnBpD0lmju7L65Js%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-21.PNG?st=2019-08-27T04%3A38%3A24Z&se=2022-08-28T04%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kJTZBqL140ClcwCz4kpmRnjddJ1hd6%2Bb8w%2B6a2x6Xrc%3D)
 
3.	Wait until the first disk is provisioned and then set its host caching to **Read-only.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/25.png?st=2019-08-27T04%3A38%3A57Z&se=2022-08-28T04%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oajSXfnfCub6AMShlRSwb8RuVCrHgrEgjLbiFI8%2B05Y%3D)

4.	From the **10979E0301-vm** blade, attach a new disk with the following settings:

```

Name: 10979E0301-vm_DataDisk2

Resource group: {{ ResourceGroup }}

Account type: Standard HDD

Source type: None (empty disk)

Size (GiB): 128

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-23.png?st=2019-08-27T04%3A53%3A39Z&se=2022-08-28T04%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5h%2FsRfyASYQ5wt3l9PZ36ZfQB0j%2B%2F2Wuwl8G6zZtVU0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-19.PNG?st=2019-08-27T04%3A54%3A10Z&se=2022-08-28T04%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EUgZmHp2XFn0ZYppaNZMAm3GEBS07dEcB5ntNkZKVx4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-20.PNG?st=2019-08-27T04%3A54%3A34Z&se=2022-08-28T04%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GjlCXomKjvbHLFVX8Gcmm2hpTVcALsJTU1A8Ba4i7v8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/900-22.PNG?st=2019-08-27T04%3A56%3A06Z&se=2022-08-28T04%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8T5bbzIQbJsogvsEDTmsuKGojcIDWtfeWPy4by4uMwo%3D)
 
3.	Wait until the first disk is provisioned and then set its host caching to **Read-only.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/25.png?st=2019-08-27T04%3A56%3A37Z&se=2022-08-28T04%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=skXEDoyCfscxjcvjrCuJh6IBrfTPVwUDuiQNZKszXNo%3D)
 
5.	Wait until the second is provisioned and then set its host caching to **Read-only**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/27.png?st=2019-08-27T04%3A57%3A02Z&se=2022-08-28T04%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FBAIut%2F9d5NQW7A187292BAmB5W%2FzwINofb0H%2FyqSAA%3D)
 
6.	Save your changes.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/28.png?st=2019-08-27T04%3A57%3A23Z&se=2022-08-28T04%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GbLO74BCLRxGYFeMAEw2xMu4ytje03upa6nwkRHBfug%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/29.png?st=2019-08-27T04%3A57%3A48Z&se=2022-08-28T04%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=84OmIckJrhtFXcf8Q1FKa1y6G4xDsKFbwjF4WHJ1jIc%3D)
 
### Task 2: Create a two-disk volume in the Azure VM that runs Windows

**Storage Pool**

A Storage Pool is one or more physical, internal , external disks or other various interfaces which extend more than one disk into one or more and create fault tolerance and other features. By using Server Manager, you can create a storage pool and span multiple disks into one and manage volumes and disks.

1.	Switch to the Remote Desktop session window. If prompted, on the Networks pane, click **No**.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/30.png?st=2019-08-27T04%3A58%3A15Z&se=2022-08-28T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BRhC879BKnD5nmroh61PMePVYWArMaPyLZ7mTaciR3M%3D)

2.	While connected to the 10979E0301-vm Azure VM, from the **Server Manager** window, create a storage pool named, consisting of two newly attached disks.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/lab3-11.png?st=2019-08-27T04%3A58%3A51Z&se=2022-08-28T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aNE%2BAKIixLQUELikZPKb1un%2BQfB%2Bir4pf6ZyIIFxgK4%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/32.png?st=2019-08-27T04%3A59%3A22Z&se=2022-08-28T04%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kpi0bczYjkubJEm4wew8%2Bldu4RetzHVYdrZC42PTiAI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/33.png?st=2019-08-27T04%3A59%3A44Z&se=2022-08-28T04%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2aCD79YZQTgQUAFqXA%2B0wqKsEyO40AB1jbiCXTO2N1I%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/34.png?st=2019-08-27T05%3A00%3A02Z&se=2022-08-28T05%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NnALV5KxiNCGSeFPF1bWC7gPs3N9M5DO9N1yURDycOA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/35.png?st=2019-08-27T05%3A00%3A23Z&se=2022-08-28T05%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=S427cb8XEWK6wnzYIqQZ%2BdsVnUtvxsoM30w90GdC2sY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/36.png?st=2019-08-27T05%3A00%3A46Z&se=2022-08-28T05%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=36MN9DjHdbwXGooECu9424spI6hSJZvrydI5N%2FAaxZk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/37.png?st=2019-08-27T05%3A01%3A05Z&se=2022-08-28T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=S8FPu%2BRwV7ST8Xl0bneVa%2BUZqcTblitfn73F2NNypdM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/38.png?st=2019-08-27T05%3A01%3A23Z&se=2022-08-28T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GoiQHd3nSXmc3YZz4KAN%2FnTD%2FSlKycNN4Szwj6L4BUg%3D)

**Virtual Disk**

Virtual disk is a collection of one or more physical disks from a created storage pool. The layout of  data across the physical disks can increase the reliability and performance of the virtual disk.

3.	From the Server Manager window, create a new virtual disk named **VirtualDisk1** by using **StoragePool1** with the **StoragePool1Simple** storage layout, the **Fixed** provisioning type, and the maximum size.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/39.png?st=2019-08-27T05%3A01%3A45Z&se=2022-08-28T05%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PniteA3mQ0CecesYtijdsn4QF8YnU6WW5XAgcng0xdk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/40.png?st=2019-08-27T05%3A02%3A05Z&se=2022-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FQiXPm%2FWujnlsbOe%2BKmN3e3PBLKK0vI1T5l1W7MBhC0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/41.png?st=2019-08-27T05%3A02%3A25Z&se=2022-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rnIE9I%2BaUgJqC1A%2B%2FcJ1Qh0z%2BWDhzwAOtKIsiH7N%2FRk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/42.png?st=2019-08-27T05%3A02%3A45Z&se=2022-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BUqiwJkpM%2B3F1Qvm7P%2FoYqcwkvHnDG0dkKW9DItfu3Y%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/43.png?st=2019-08-27T05%3A03%3A05Z&se=2022-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1xF3Yaj0BEFyNLeaVIJbvBraKlUpTo0v%2BGNgHN3YZEs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/44.png?st=2019-08-27T05%3A03%3A26Z&se=2022-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MCuhXfi%2BV61cCFAY9mwHVpMDwiWj1UiLRLVm8it5fQc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/45.png?st=2019-08-27T05%3A03%3A45Z&se=2022-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m8Ja%2FNxx%2FpRgj7%2Fs7m9IR40PEq0qct7Ek4N3PcEK1Ww%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/46.png?st=2019-08-27T05%3A04%3A05Z&se=2022-08-28T05%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Fd0pYGYjFOxXh%2BUyO26oFvSdUrxXbaiDopcYt87n2AU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/47.png?st=2019-08-27T05%3A04%3A26Z&se=2022-08-28T05%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aloycUdeHweSCmMRn4MKVlWZ9J9v8ZYYv5gH0DutGrY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/48.png?st=2019-08-27T05%3A04%3A47Z&se=2022-08-28T05%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8Wiqgyn7G5xmUou9s20RKMo9IFHiv1Va7F%2BGK6k3W%2B0%3D)

4.	From the Server Manager window, create a new 254 GB volume as drive F formatted with the NTFS file system and a default allocation unit.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/49.png?st=2019-08-27T05%3A05%3A23Z&se=2022-08-28T05%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c%2FizuBDpWTnHjDOwqdFOuGm1jE1dkcH%2Fmn3PA69ZQN4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/file3.png?st=2019-08-29T05%3A16%3A31Z&se=2022-08-30T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SeHM7l9WZD8AufoJ%2FKm7QbcyCnNBhHNPIcjef4GOd4I%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/file4.png?st=2019-08-29T05%3A25%3A06Z&se=2022-08-30T05%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=i5iasH0hguTdWPkt3caGUAC4kyiFOrGu%2BpGH3SzuzeQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/50.png?st=2019-08-27T05%3A05%3A45Z&se=2022-08-28T05%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CRbvyPNoLp%2FD5DHlOVCylO%2BvbtZdpPhQYVzZNxsix5E%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/51.png?st=2019-08-27T05%3A06%3A03Z&se=2022-08-28T05%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uJazSfHDUfX25dJF7ZwGEHZ1Er0y3Qs1Ft6xMAWf4g4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/52.png?st=2019-08-27T05%3A06%3A23Z&se=2022-08-28T05%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mSz4J7jqXDXSPtjWIxZfxkbT0EXUMj6TGCRGYHJK3%2FA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/53.png?st=2019-08-27T05%3A06%3A43Z&se=2022-08-28T05%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ApYU2p8wgq5UokF2fOkEdn1Ddo1%2FTDTK1WFwNlVc6hY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/54.png?st=2019-08-27T05%3A07%3A01Z&se=2022-08-28T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tblVxNjTP%2B8f589aQG006fXger5hWBcdM02TVidUP1s%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/55.png?st=2019-08-27T05%3A07%3A18Z&se=2022-08-28T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BEtWJzWPtXDrW1t%2F1iiVVL9efzhE70SU1D43rQbAcOM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3/56.png?st=2019-08-27T05%3A07%3A38Z&se=2022-08-28T05%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ip%2BqjASP%2BerWBzVOreexAX%2FOQjrkHa8KdP6QqO7ydVc%3D)

5.	From the desktop of, 10979E0301-vm open File Explorer and verify that there is a new drive F with 253 GB of available disk space.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/Screenshot%20(1).png?st=2019-08-29T05%3A10%3A16Z&se=2022-08-30T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6cJSNK%2BEf938Iq%2FEz7B81MLpjmeFNGFGqgLacyEnNUU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/file1.png?st=2019-08-29T05%3A13%3A40Z&se=2022-08-30T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Qi7Ztzw1N524tT4VXUeXPexHHtW%2FFYWc5H8wPPyfjQ0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab3%20-%20Creating%20Virtual%20machines%20in%20Microsoft%20Azure/file2.png?st=2019-08-29T05%3A14%3A36Z&se=2022-08-30T05%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FSDY1%2BmfXk6B30chhAJ9WhQYsWiFi9rxUO92vu3xprc%3D)

6.	Close the Remote Desktop session to 10979E0301-vm.


**Result:** Once you completed this lab, you have attached two data disks to the Azure VM from the Azure Portal and created a two-disk volume in an Azure VM that runs Windows Server 2016 Datacenter by using Storage Spaces.
