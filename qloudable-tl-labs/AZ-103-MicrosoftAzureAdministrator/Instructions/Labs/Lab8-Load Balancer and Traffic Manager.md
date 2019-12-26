# Lab 8: Load Balancer and Traffic Manager

## Table of Content

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Deploy Azure VMs by using Azure Resource Manager templates](#exercise-1-deploy-azure-vms-by-using-azure-resource-manager-templates)

[Exercise 2: Implement Azure Load Balancing](#exercise-2-implement-azure-load-balancing)

[Exercise 3: Implement Azure Traffic Manager load balancing](#exercise-3-implement-azure-traffic-manager-load-balancing)


## Overview

The main aim of the lab is deployed Windows Server 2016 Datacenter with installed Web Server (IIS) role into availability sets in two Azure regions. In both the Region implemented and verified load balancing rules and NAT rules of Azure load balancers and implemented and verified Azure Traffic Manager load balancing.

All tasks in this lab are performed from the Azure portal (including a PowerShell Cloud Shell session) except for Exercise 1 Task 3, which includes steps performed from a Remote Desktop session to an Azure VM

### Scenario and Objectives

XYZ training labs corporation wants to implement Azure VM-hosted web workloads and facilitate their management for its subsidiary Contoso Corporation in a highly available manner by leveraging load balancing and Network Address Translation (NAT) features of Azure Load Balancer.

After completing this lab, you will be able to:

*	Deploy Azure VMs by using Azure Resource Manager templates

*	Implement Azure Load Balancing

*	Implement Azure Traffic Manager load balancing

## Pre-requisites

* Azure Portal

* ARM Template

* PowerShell 

* Remote Desktop

## Exercise 1: Deploy Azure VMs by using Azure Resource Manager templates

The main tasks for this exercise are as follows:

1.	Deploy management Azure VMs running Windows Server 2016 Datacenter with the Web Server (IIS) role installed into an availability set in the first Azure region by using an Azure Resource Manager template

2.	Deploy management Azure VMs running Windows Server 2016 Datacenter with the Web Server (IIS) role installed into an availability set in the second Azure region by using an Azure Resource Manager template

* **Traffic Manager profile**

Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness.

Traffic Manager uses DNS to direct client requests to the most appropriate service endpoint based on a traffic-routing method and the health of the endpoints. An endpoint is any Internet-facing service hosted inside or outside of Azure. Traffic Manager provides a range of traffic-routing methods and endpoint monitoring options to suit different application needs and automatic failover models. Traffic Manager is resilient to failure, including the failure of an entire Azure region.

* **Remote Desktop**

Remote desktop is a program or an operating system feature that allows a user to connect to a computer in another location, see that computer's desktop and interact with it as if it were local.

People use remote desktop access capabilities to do a variety of things, including the following:

* Access a workplace computer from home or when traveling.

* Access a home computer from other locations.

* Fix a computer problem.

* Perform administrative tasks.

* Demonstrate something, such as a process or a software application

* **Cloud Shell**

Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work. Linux users can opt for a Bash experience, while Windows users can opt for PowerShell.

* Load-balance incoming internet traffic to your VMs. This configuration is known as a Public Load Balancer.

* Port forward traffic to a specific port on specific VMs with inbound network address translation (NAT) rules.

* Provide outbound connectivity for VMs inside your virtual network by using a public Load Balancer.

* Create two VMs running a basic website on IIS.

* Create two test VMs to view Traffic Manager in action.

* Configure a DNS name for the VMs running IIS.

* Create a Traffic Manager profile.

* Add VM endpoints to the Traffic Manager profile.

* View Traffic Manager in action.

1. From the lab, after the chrome is opened and connected then browse to the Azure portal at http://portal.azure.com 

Using the Chrome browser, login into Azure portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/111.PNG?st=2019-09-05T10%3A19%3A13Z&se=2022-09-06T10%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=27XoFD8qjp7Qp6ZIIygBj4XfphBrfh4MTEM3avAWsF0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/112.PNG?st=2019-09-05T10%3A19%3A33Z&se=2022-09-06T10%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ohMLqNqucg%2F791A4EPHepDPnTdlixvK3hbVKptlFO6A%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/113.PNG?st=2019-09-05T10%3A20%3A01Z&se=2022-09-06T10%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IOR0gdsbRhUPMzC1MlknrKXBO8EO5eK0SYVETFxjdF4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/114.PNG?st=2019-09-05T10%3A20%3A28Z&se=2022-09-06T10%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2B%2BnC6l%2FAN8txvMULJxcp9ncX0XfZ4k%2FrLKqz4TYsLsw%3D)


### Task 1: Deploy management Azure VMs running Windows Server 2016 Datacenter with the Web Server (IIS) role installed into an availability set in the first Azure region by using an Azure Resource Manager template.

2.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/1.png?st=2019-09-05T08%3A59%3A14Z&se=2022-09-06T08%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6vOOZ6tvXcTM4zQDNRsJktWcFoT6gyCWsaXAPAsEDGw%3D)

3.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/2.png?st=2019-09-05T09%3A01%3A51Z&se=2022-09-06T09%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=G1Iy88zOWsvFz9fld7T8FmUwW9CbG2UwkKKlMEzkvPE%3D)
 
4.	Use the list of search results to navigate to the **Deploy a custom template** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/3.png?st=2019-09-05T09%3A02%3A31Z&se=2022-09-06T09%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8lvakK219EVk8SYkNAPXL9HAAw6UPQvXK8DsHdGAX6Y%3D)
 
5.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/4.png?st=2019-09-05T09%3A04%3A01Z&se=2022-09-06T09%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ccB2%2ByQIyHZPaF3hch9MnINrOrFxDuD7x25ebx0QJLs%3D)
 
6.	From the **Edit template** blade, Click on the below link and load the template file.

**Note**: Delete the default data.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_08/Load_Balancer_and_Traffic_Manager/az-101-03_01_azuredeploy.json?st=2019-09-06T04%3A01%3A42Z&se=2022-09-07T04%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m6YQDn24%2FSCap%2FZvFGIdKgw7%2F8IhYpH0O2CT%2BTO9C0E%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/5.png?st=2019-09-05T09%3A05%3A54Z&se=2022-09-06T09%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gphcN6S4R5rKxol7onSbZg5EJLFeUHnVJ83AY3AMXP4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/6.png?st=2019-09-05T09%3A06%3A22Z&se=2022-09-06T09%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=26RSCbI9r4pEymjwDcTqb5kAWPIT4avuPObDHGqARAw%3D) 
 
*Note: Review the content of the template and note that it defines deployment of two Azure VMs hosting Windows Server 2016 Datacenter Core into an availability set.*

7.	Save the template and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/7.png?st=2019-09-05T09%3A06%3A47Z&se=2022-09-06T09%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DNNpt5OXJsD2pSQH9XgqO%2B2bzlW2qqlq%2BiRfSmtEN0Y%3D)
 
8.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/8.png?st=2019-09-05T09%3A07%3A10Z&se=2022-09-06T09%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kwspzfGsYq1tThqiDqI36VW2ZZGAft9l%2F1iYFD7ig6o%3D)
 
9.	From the **Edit parameters** blade, Click on the below link and load the parameters file.

**Note:** Delete the default data.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_08/Load_Balancer_and_Traffic_Manager/az-101-03_01_1_azuredeploy.parameters.json?st=2019-09-06T04%3A03%3A02Z&se=2022-09-07T04%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E3Ur1%2BNdqyd8fSOTAKMSD6jQePw0pf%2F6nOVH0nziHzk%3D

10.	Save the parameters and return to the **Custom deployment** blade.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/9.png?st=2019-09-05T09%3A07%3A34Z&se=2022-09-06T09%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BQBdxzhO94ghzSML3n5Tvf%2Bh%2BQs0amzL9xH0wL28In0%3D)

11.	From the **Custom deployment** blade, initiate a template deployment with the following settings:

* **Subscription:** `Select the default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234` <br>
* **Vm Name Prefix:** `az1010301w-vm` <br>
* **Nic Name Prefix:** `az1010301w-nic` <br>
* **Image Publisher:** `MicrosoftWindowsServer` <br>
* **Image Offer:** `WindowsServer` <br>
* **Image SKU:** `2016-Datacenter` <br>
* **Vm Size:** `Standard_D2s_v3` <br>
* **Virtual Network Name:** `az1010301-vnet` <br>
* **Address Prefix:** `10.101.31.0/24` <br>
* **Virtual Network Resource Group:** `{{resource-group-name}}` <br>
* **Subnet0Name:** `subnet0` <br>
* **Subnet0Prefix:** `10.101.31.0/26` <br>
* **Availability Set Name:** `az1010301w-avset` <br>
* **Network Security Group Name:** `az1010301w-vm-nsg` <br>
* **Modules Url:** `https://github.com/Azure/azure-quickstart-templates/raw/master/dsc-extension-iis-server-windows-vm/ContosoWebsite.ps1.zip` <br>
* **Configuration Function:** `ContosoWebsite.ps1\ContosoWebsite`

 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/10.png?st=2019-09-05T09%3A08%3A13Z&se=2022-09-06T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hlJzDwob8KUcGqdclkK8YGairTBJjsJJF%2FjQYlor0Jk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/11.png?st=2019-09-05T09%3A08%3A48Z&se=2022-09-06T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=A9sfrzOPD5MAORpI9m5%2BieLVsIh8Cwx2WxnKcdaBh4w%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/12.png?st=2019-09-05T09%3A09%3A12Z&se=2022-09-06T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=utgEz0P8Mvy%2BqHJMZ8x1oiht5KDQ23RR40i%2BKELOrJU%3D)

**Note:** To identify Azure regions where you can provision Azure VMs, refer to **https://azure.microsoft.com/en-us/regions/offers/**

**Note:** Do not wait for the deployment to complete but proceed to the next task.

### Task 2: Deploy management Azure VMs running Windows Server 2016 Datacenter with the Web Server (IIS) role installed into an availability set in the second Azure region by using an Azure Resource Manager template

1.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/13.png?st=2019-09-05T09%3A09%3A33Z&se=2022-09-06T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pyQDuPjjs89GuP4K3fAhQbCWxILQK8uocU5F5puMTV4%3D)
 
2.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/14.png?st=2019-09-05T09%3A09%3A58Z&se=2022-09-06T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3jjLBu%2BMaf8RPFNcaNJdqNRUlsCKORPd%2ByWkrczg9ec%3D)
 
3.	Use the list of search results to navigate to the **Deploy a custom template** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/15.png?st=2019-09-05T09%3A10%3A22Z&se=2022-09-06T09%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XJqcmUVYXlxPuSBh0Rz1HWVrClhrvL7ps2s4ayoF5Ng%3D)
 
4.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/16.png?st=2019-09-05T09%3A10%3A45Z&se=2022-09-06T09%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Sv2B9dZ30nhGG5KZSsAtLJ4dHq6tf%2F3U68MexAFSW2o%3D)
 
5.	From the **Edit template** blade, Click on the below link and load the template file.

**Note:** Delete the default data.

`https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_08/Load_Balancer_and_Traffic_Manager/az-101-03_01_azuredeploy.json?st=2019-09-06T04%3A03%3A46Z&se=2022-09-07T04%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=16RlewZGn5%2FJCUPUZxn5jvW6JZ3KPKWfUWV5oB547TI%3D`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/17.png?st=2019-09-05T09%3A11%3A11Z&se=2022-09-06T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g4HATSCSMQd%2Fa5Il%2FyKCmUP7kZM6Jyi1YtfjNWX21lc%3D)
 
**Note**: This is the same template you used in the previous task. You will use it to deploy a pair of Azure VMs to the second region.

6.	Save the template and return to the **Custom deployment** blade.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/18.png?st=2019-09-05T09%3A11%3A48Z&se=2022-09-06T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IEIRBXELgIq5Gw14aYqhJbJcR0e0dK8xyV56bz%2Bhor4%3D)

7.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/19.png?st=2019-09-05T09%3A12%3A12Z&se=2022-09-06T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SLtgHNywqKBgQ18oOrFnqhKLohD26xHpnxj5x1ljlxM%3D)
 
8.	From the **Edit parameters** blade, Click on the below link and load the parameters file.

**Note:** Delete the default data.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_08/Load_Balancer_and_Traffic_Manager/az-101-03_01_2_azuredeploy.parameters.json?st=2019-09-06T04%3A04%3A14Z&se=2022-09-07T04%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HVApD5rckAZshtkel1gvJQDhFgujJh0h7xJBimvNzeg%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/20.png?st=2019-09-05T09%3A12%3A34Z&se=2022-09-06T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ycmlup%2Fy1Z2yqP8z52jArtA7ogRwdzCL1sRszqw%2Bq3o%3D)
 
9.	Save the parameters and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/21.png?st=2019-09-05T09%3A12%3A57Z&se=2022-09-06T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Efucn%2FWOEZ4%2BfOffLbxtKvWKiDcbha0EKCQJqk0RpHs%3D)
 
10.	From the **Custom deployment** blade, initiate a template deployment with the following settings:


* **Subscription:** `default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Region:** `{{location}}` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234` <br>
* **Vm Name Prefix:** `az1010302w-vm` <br>
* **Nic Name Prefix:** `az1010302w-nic` <br>
* **Image Publisher:** `MicrosoftWindowsServer` <br>
* **Image Offer:** `WindowsServer` <br>
* **Image SKU:** `2016-Datacenter` <br>
* **Vm Size:** `Standard_D2s_v3` <br>
* **Virtual Network Name:** `az1010302-vnet` <br>
* **Address Prefix:** `10.101.32.0/24` <br>
* **Virtual Network Resource Group:** `{{resource-group-name}}` <br>
* **Subnet0Name:** `subnet0` <br>
* **Subnet0Prefix:** `10.101.32.0/26` <br>
* **Availability Set Name:** `az1010302w-avset` <br>
* **Network Security Group Name:** `az1010302w-vm-nsg` <br>
* **Modules Url:** `https://github.com/Azure/azure-quickstart-templates/raw/master/dsc-extension-iis-server-windows-vm/ContosoWebsite.ps1.zip` <br>
* **Configuration Function:** `ContosoWebsite.ps1\ContosoWebsite`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/22.png?st=2019-09-05T09%3A13%3A24Z&se=2022-09-06T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ItYKYWvccPmvV5RdpScFxSxW0EHETST0zbTTRLoDGEc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/23.png?st=2019-09-05T09%3A13%3A57Z&se=2022-09-06T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zlX4A%2FMrZEbHv4vqpemAstQxzvJikMaeDqFntuZsa6g%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/24.png?st=2019-09-05T09%3A14%3A16Z&se=2022-09-06T09%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uXPLMbYep0xgFn0iS9fKLqm%2FRDzR7QXcO7BowHdRXKM%3D)
 
**Note:**  *Do not wait for the deployment to complete but proceed to the next exercise.*
**Result:** *After you completed this exercise, you have used Azure Resource Manager templates to initiate deployment of Azure VMs running Windows Server 2016 Datacenter with the Web Server (IIS) role installed into availability sets in two Azure regions.*

## Exercise 2: Implement Azure Load Balancing

The main tasks for this exercise are as follows:

1.	Implement Azure load balancing rules in the first region.
2.	Implement Azure load balancing rules in the second region.
3.	Implement Azure NAT rules in the first region.
4.	Implement Azure NAT rules in the second region.
5.	Verify Azure load balancing and NAT rules

### Task 1: Implement Azure load balancing rules in the first region

*	**Load Balancer**

A load balancer is a piece of hardware (or virtual hardware) that acts like a reverse proxy to distribute network and/or application traffic across different servers. A load balancer is used to improve the concurrent user capacity and overall reliability of applications. A load balancer helps to improve these by distributing the workload across multiple servers, decreasing the overall burden placed on each server.
Physical load balancing appliances are similar in appearance to routers. They are connected to your network infrastructure in the same manner as a router or another server. In contrast, virtual load balancing hardware is a program that emulates the addition of a new hardware solution. These virtual load balancers work in a manner similar to a virtual server or a virtual computer on your network. They act as a physical load balancer and distribute requests accordingly, saving you space and offering greater flexibility than many hardware balancers.


**Note:** Before you start this task, ensure that the template deployment you started in the first task of the previous exercise has completed.

1.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/25.png?st=2019-09-05T09%3A14%3A39Z&se=2022-09-06T09%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lDXFZlnfD6yQeLO7IleatS5hjQBx%2BUu3Q5NimfNSl8Y%3D)

2.	From the **Create a resource** blade, search Azure Marketplace for **Load Balancer.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/26.png?st=2019-09-05T09%3A15%3A00Z&se=2022-09-06T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qAsP4Il7NlEF5mSdDv9NvspUseAFPuh37Z6Sx5rUzPM%3D)
 
3.	Use the list of search results to navigate to the **Create load balancer** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/27.png?st=2019-09-05T09%3A15%3A20Z&se=2022-09-06T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HScEYiFz8GS3yW1zS1Fg6U72qcD1R8u8w7DWf2%2FRk8w%3D)
 
4.	From the **Create load balancer** blade, create a new Azure Load Balancer with the following settings:

* **Subscription:** `default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Name:** `az1010301w-lb` <br>
* **Region:** `{{location}}` <br>
* **Type:** `Public` <br>
* **SKU:** `Basic` <br>
* **Public IP address:** `a new public IP address named az1010301w-lb-pip` <br>
* **Assignment:** `Dynamic`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/28.png?st=2019-09-05T09%3A15%3A55Z&se=2022-09-06T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XZ6q4Gbf%2Bv%2BDzjnbxsVjMRtXQ7gfIEmiVBzyPJ42kAQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/29.png?st=2019-09-05T09%3A16%3A15Z&se=2022-09-06T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yncrsi8uuA%2F3cjorbkuhQGsY1j51CUNCy3zA%2F2%2BnXmw%3D)

**Note**: Click on the **Review+Create** 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/30.png?st=2019-09-05T09%3A16%3A37Z&se=2022-09-06T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=k2H6FcbcT3Tvd2hYsaEeyGJrK01asRFkiGX1sWOHymQ%3D)
 
5.	In the Azure portal, Go to **ResourceGroups** and Click on the created ResourceGroup, Navigate to the blade of the newly deployed Azure load balancer **az1010301w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/31.png?st=2019-09-05T09%3A17%3A05Z&se=2022-09-06T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pjosy5bxLcim9eBWXH7KCo6EfMYw0qoxu9%2BMfZU9HHo%3D)
 
6.	From the **az1010301w-lb** blade, display the **az1010301w-lb - Backend pools** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/32.png?st=2019-09-05T09%3A17%3A29Z&se=2022-09-06T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yDA3gHjwFtO1OYYBllgdwhfPbg9AAxU%2Bstm7G1vcI5o%3D)
 
7.	From the **az1010301w-lb - Backend pools** blade, add a backend pool with the following settings:

```
Name: az1010301w-bepool

IP version: IPv4

Associated to: Availability set

Availability set: az1010301w-avset

Virtual machine: az1010301w-vm0

Network IP configuration: az1010301w-nic0/ipconfig1 (10.101.31.4)

Virtual machine: az1010301w-vm1

Network IP configuration: az1010301w-nic1/ipconfig1 (10.101.31.5)

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/115.png?st=2019-09-06T05%3A06%3A13Z&se=2022-09-07T05%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s1ytjGj%2Bg7WbV7%2F1nCgCh%2FFg4%2BOQlQGZP4umpb3jfYI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/116.png?st=2019-09-06T05%3A25%3A23Z&se=2022-09-07T05%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TJ61ogy3YBlCDXHsbT0wM6hDSkZYR%2FOyNOE265dyabo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/117.png?st=2019-09-06T05%3A08%3A02Z&se=2022-09-07T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CyDd2xohAXztSyldgFj2EEI2SXT34UMx3waVIu0u%2Fls%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/118.png?st=2019-09-06T05%3A08%3A24Z&se=2022-09-07T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HAWLm7lMByTnfqzXu119uwfArUvNw70gOtTJLCwcMh0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/119.png?st=2019-09-06T05%3A12%3A22Z&se=2022-09-07T05%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8sMjI%2BnAJNlVm0H43D6gDoHViwMW8EiTQfH2Zyq5muU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/120.png?st=2019-09-06T05%3A11%3A24Z&se=2022-09-07T05%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SRjoyIq4rldKFH2gda7iCMVKlzAcL98LgisqTIPBlsY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/34.png?st=2019-09-05T09%3A18%3A16Z&se=2022-09-06T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CDEqb9dSuDsCTd3%2BqdtameoFkZeKX1VRkqUtSz9kMCs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/35.png?st=2019-09-05T09%3A18%3A35Z&se=2022-09-06T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9p3JzfHe9TGJEE4UaOrkijUBRv0uCem5rxvN5dLa2CA%3D)
  
**Note:** *It is possible that the IP addresses of the Azure VMs are assigned in the reverse order.*
**Note:** *Wait for the operation to complete. This should take less than a minute.*

8.	From the **az1010301w-lb - Backend pools** blade, display the **az1010301w-lb - Health probes** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/36.png?st=2019-09-05T09%3A18%3A57Z&se=2022-09-06T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tWcVX5hkvPE8LidRDkOXL4UQU3bWnskRfwp3GnNCQEA%3D)
 
9.	From the **az1010301w-lb - Health probes** blade, add a health probe with the following settings:

```
Name: az1010301w-healthprobe

Protocol: TCP

Port: 80

Interval: 5 seconds

Unhealthy threshold: 2 consecutive failures

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/37.png?st=2019-09-05T09%3A19%3A26Z&se=2022-09-06T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=r%2F5ce0PxPYvRZOYCrkrtYhQe9FCVtBDS4VPAJpISN9o%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/38.png?st=2019-09-05T09%3A20%3A08Z&se=2022-09-06T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=grNC55VcEAIKb9hZ9cwfmoPbyvTHcwhtAFvgZbecTY8%3D)
 
**Note:** *Wait for the operation to complete. This should take less than a minute.*

10.	From the **az1010301w-lb - Health probes** blade, display the **az1010301w-lb - Load balancing rules** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/39.png?st=2019-09-05T09%3A20%3A31Z&se=2022-09-06T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4oi1Z%2BraDUI%2FU7s3B2PDW3eLDPpAbEduE4m6Zrcpy80%3D)
 
11.	From the **az1010301w-lb - Load balancing rules** blade, add a load balancing rule with the following settings:

```

Name: az1010301w-lbrule01

IP Version: IPv4

Frontend IP address: LoadBalancerFrontEnd

Protocol: TCP

Port: 80

Backend port: 80

Backend pool: az1010301w-bepool (2 virtual machines)

Health probe: az1010301w-healthprobe (TCP:80)

Session persistence: None

Idle timeout (minutes):4

Floating IP (direct server return): Disabled

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/40.png?st=2019-09-05T09%3A21%3A00Z&se=2022-09-06T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OePYnMhKigODJZKFxDkHRSDnvuaECaRm455Qh%2B8ItRo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/41.png?st=2019-09-05T09%3A21%3A27Z&se=2022-09-06T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=n6ZNgzdSk6ZNQo8TA2Usgbbcceo7s%2B7bRML1oz1btwM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/42.png?st=2019-09-05T09%3A21%3A47Z&se=2022-09-06T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ASZjEsJ5KrMfTgVWkC5J8N7Gyt8iF1XE7%2BmH%2FzdNJ8E%3D) 
 
 
### Task 2: Implement Azure load balancing rules in the second region

**Note:** *Before you start this task, ensure that the template deployment you started in the second task of the previous exercise has completed.*

1.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/43.png?st=2019-09-05T09%3A22%3A15Z&se=2022-09-06T09%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wWhkgQclNmard5FrXrrD1OyiKJQOjUWF77%2FrsVBx4EA%3D)

2.	From the **Create a resource** blade, search Azure Marketplace for **Load Balancer.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/44.png?st=2019-09-05T09%3A22%3A37Z&se=2022-09-06T09%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mM4hR9RlGLVTNYfkc0CkAemLCz0r1d%2BTzMxMvFuM9Us%3D)
 
3.	Use the list of search results to navigate to the **Create load balancer blade.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/45.png?st=2019-09-05T09%3A23%3A00Z&se=2022-09-06T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vVq%2FVKyHPxBuwbGMlfE9eIbxzM6ymeMh5oSDuhePUf4%3D)
 
4.	From the **Create load balancer** blade, create a new Azure Load Balancer with the following settings:

* **Subscription:** `default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
***Name:** `az1010302w-lb` <br>
* **Type:** `Public` <br>
* **SKU:** `Basic` <br>
* **Public IP address:** `a new public IP address named az1010302w-lb-pip` <br>
* **Assignment:** `Dynamic` <br>


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/46.png?st=2019-09-05T09%3A23%3A23Z&se=2022-09-06T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zYCKLIwIUwpKbijIfCc5S4XolRK2iDAUja1aTKuY8Wc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/47.png?st=2019-09-05T09%3A23%3A43Z&se=2022-09-06T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3tIQ1wKh3%2F%2B5aGLY4UYFXbZxulXUjVSmJf8maabckFI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/48.png?st=2019-09-05T09%3A24%3A05Z&se=2022-09-06T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2hpJBZzfyPQDsBy%2B%2FKcVarOLqrewKpIC6doaOaKqRXE%3D)
  
5.	In the Azure portal, Go to **ResourceGroups** and Click on the created **ResourceGroup**, Navigate to the blade of the newly deployed Azure load balancer **az1010302w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/49.png?st=2019-09-05T09%3A24%3A47Z&se=2022-09-06T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cYb223Q2171m%2BNjLv3WoXfm%2Fm955DSmZeMif1HOvd3U%3D)
 
6.	From the **az1010302w-lb** blade, display the **az1010302w-lb - Backend pools** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/50.png?st=2019-09-05T09%3A25%3A09Z&se=2022-09-06T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pMhqJoUy4UBNr%2BRBiQIMOOoyFMwQH80mMQ7gIeHTrkg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/51.png?st=2019-09-05T09%3A27%3A00Z&se=2022-09-06T09%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2QTcwvyrUbHn7PfJisNCmod0hbx4KZbZVLSEyz98Ur8%3D)
 
7.	From the **az1010302w-lb - Backend pools** blade, add a backend pool with the following settings:

```

Name: az1010302w-bepool

IP version: IPv4

Associated to: Availability set

Availability set: az1010302w-avset

Virtual machine: az1010302w-vm0

Network IP configuration: az1010302w-nic0/ipconfig1 (10.101.32.4)

Virtual machine: az1010302w-vm1

Network IP configuration: az1010302w-nic1/ipconfig1 (10.101.32.5)

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/116.png?st=2019-09-06T05%3A31%3A53Z&se=2022-09-07T05%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Elh7sEuLVOSeSxyqnvR%2FHaGPCSuLza0A4VfP64VB19g%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/121.png?st=2019-09-06T05%3A12%3A50Z&se=2022-09-07T05%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6O5RBoM1qQODjRZqymbFacLJow3BLnuGeIoVkpyt7tA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/122.png?st=2019-09-06T05%3A13%3A16Z&se=2022-09-07T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SvsIvEUMxXckwK94ONNlMthGUkF9KPe1Z42axgkV3tM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/123.png?st=2019-09-06T05%3A13%3A56Z&se=2022-09-07T05%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=veSm1T88%2BW%2Bfn0yZ1gjHD9R6VTfS0wiXWCmHTuz30uo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/52.png?st=2019-09-05T09%3A29%3A20Z&se=2022-09-06T09%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VdAGcKWtwMVkiwD4YirQ2bBrARFHb1m1BLTCxQZ%2BpmQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/53.png?st=2019-09-05T09%3A30%3A05Z&se=2022-09-06T09%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Spt5pKjRK0ttWPeDK1kLE0uZ2tusKWkjt0bGndz1dJY%3D)
 
**Note:** *It is possible that the IP addresses of the Azure VMs are assigned in the reverse order.*
**Note:** *Wait for the operation to complete. This should take less than a minute.*

8.	From the **az1010302w-lb - Backend pools** blade, display the **az1010302w-lb - Health probes** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/54.png?st=2019-09-05T09%3A30%3A39Z&se=2022-09-06T09%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qZeojzEvsZlirbVmHEvWNM6XM0BQ7kAC5G%2FkGehPKuo%3D)
 
9.	From the **az1010302w-lb - Health probes** blade, add a health probe with the following settings:

```

Name: az1010302w-healthprobe

Protocol: TCP

Port: 80

Interval: 5 seconds

Unhealthy threshold: 2 consecutive failures

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/55.png?st=2019-09-05T09%3A31%3A39Z&se=2022-09-06T09%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NhJsg0soOvY%2BzlVZCHgDqYW9XR8XnKp3hACKquOtArQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/56.png?st=2019-09-05T09%3A32%3A03Z&se=2022-09-06T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wMcPQ00ulGfhxCcgChMBwITTddVKh4QnuLB%2BdppFMeQ%3D)
 
**Note**: *Wait for the operation to complete. This should take less than a minute.*

10.	From the **az1010302w-lb - Health probes** blade, display the **az1010302w-lb - Load balancing rules** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/57.png?st=2019-09-05T09%3A32%3A28Z&se=2022-09-06T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CoIXrrotWpE0heGJVgycxpArDisQO%2FH2N2I99Ftt%2Bz4%3D)
 
11.	From the **az1010302w-lb - Load balancing rules** blade, add a load balancing rule with the following settings:

```

Name: az1010302w-lbrule01

IP Version: IPv4

Frontend IP address: LoadBalancerFrontEnd

Protocol: TCP

Port: 80

Backend port: 80

Backend pool: az1010302w-bepool (2 virtual machines)

Health probe: az1010302w-healthprobe (TCP:80)

Session persistence: None

Idle timeout (minutes): 4

Floating IP (direct server return): Disabled

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/58.png?st=2019-09-05T09%3A32%3A59Z&se=2022-09-06T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=akgTmZHgIABxEVjcrCg5%2F33XxZsbtGpOA9Kk4wzh%2Fj8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/59.png?st=2019-09-05T09%3A33%3A21Z&se=2022-09-06T09%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=35Bfwi2NT3XDYsETVRd0lAF6E6OADl8NJF89pFuEe3k%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/60.png?st=2019-09-05T09%3A33%3A56Z&se=2022-09-06T09%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qAYgrJz1vqK7l%2F1Q2%2BCgvJGzGHStWr9VCW5NQQo81zg%3D)
 
### Task 3: Implement Azure NAT rules in the first region

1.	In the Azure portal, navigate to the blade of the Azure load balancer **az1010301w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/61.png?st=2019-09-05T09%3A34%3A21Z&se=2022-09-06T09%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0%2BtTYUm%2BK6prkrGXi55WOOLEK33ZRMiAH9bHWVT41iY%3D)
 
2.	From the **az1010301w-lb** blade, display the **az1010301w-lb - Inbound NAT rules** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/62.png?st=2019-09-05T09%3A34%3A42Z&se=2022-09-06T09%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HfEEbCB1%2BvSCEk23mXydd23SoiyOKU2auJH%2BtQ9JQIk%3D)
 
**Note:** *The NAT functionality does not rely on health probes.*

3.	From the **az1010301w-lb - Inbound NAT rules** blade, add the first inbound NAT rule with the following settings:

```

Name: az1010301w-vm0-RDP

Frontend IP address: LoadBalancerFrontEnd

IP Version: IPv4

Service: Custom

Protocol: TCP

Port: 33890

Target virtual machine: az1010301w-vm0

Network IP configuration: ipconfig1 (10.101.31.4) or ipconfig1 (10.101.31.5)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/63.png?st=2019-09-05T09%3A35%3A06Z&se=2022-09-06T09%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NWbEK2KVP%2B5vBXqRhjGOPFX41VKxoRHVvqZK79T7qIE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/64.png?st=2019-09-05T09%3A35%3A26Z&se=2022-09-06T09%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xnb1gGiNdyQCkEYhgj0sXRWkLKRlDwXliEmtqC5%2FKGo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/65.png?st=2019-09-05T09%3A35%3A47Z&se=2022-09-06T09%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HGqPNVHJcW2IdGIdyy4krM2xi2NsVvy95en2oR3qBqE%3D)
  
**Note:** *Wait for the operation to complete. This should take less than a minute.*

4.	From the **az1010301w-lb - Inbound NAT rules** blade, add the second inbound NAT rule with the following settings:

```

Name: az1010301w-vm1-RDP

Frontend IP address: LoadBalancerFrontEnd

IP Version: IPv4

Service: Custom

Protocol: TCP

Port: 33891

Target virtual machine: az1010301w-vm1

Network IP configuration: ipconfig1 (10.101.31.4) or ipconfig1 (10.101.31.5)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/66.png?st=2019-09-05T09%3A36%3A23Z&se=2022-09-06T09%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W%2F8nz%2BzSQvX2Jp4RXX7IJLOtsFo0kAhcKlXExAckzfg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/67.png?st=2019-09-05T09%3A36%3A46Z&se=2022-09-06T09%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uToykn9WY1F85hgb7UbcF1Kh9qvYTNC7L42wNo6NXBU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/68.png?st=2019-09-05T09%3A37%3A05Z&se=2022-09-06T09%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4pOHZncSnbEAr2xUYsMaRE33Eh5Z%2ByK1uWIsClOWGAA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/69.png?st=2019-09-05T09%3A37%3A25Z&se=2022-09-06T09%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ngXc4kESoJ0STgSZPDmmOw%2FKzb2bF3BC2KiVYUOTZ14%3D)
 
**Note:** *Wait for the operation to complete. This should take less than a minute.*

### Task 4: Implement Azure NAT rules in the second region

1.	In the Azure portal, navigate to the blade of the Azure load balancer **az1010302w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/70.png?st=2019-09-05T09%3A37%3A46Z&se=2022-09-06T09%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BHlSr1id%2BzSd8i5gb83Za%2Fxvs4%2FjOjuRmvGT50NwNdQ%3D)
 
2.	From the **az1010302w-lb** blade, display the **az1010302w-lb - Inbound NAT rules** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/71.png?st=2019-09-05T09%3A49%3A18Z&se=2022-09-06T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nrmkQsFRI2yBVcTOz8a%2FZTY8vo8OnraYhbs7j36HD7k%3D)

3.	From the **az1010302w-lb - Inbound NAT rules** blade, add the first inbound NAT rule with the following settings:

```

Name: az1010302w-vm0-RDP

Frontend IP address: LoadBalancedFrontEnd

IP Version: IPv4

Service: Custom

Protocol: TCP

Port: 33890

Target virtual machine: az1010302w-vm0

Network IP configuration: ipconfig1 (10.101.32.4) or ipconfig1 (10.101.32.5)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/72.png?st=2019-09-05T09%3A49%3A43Z&se=2022-09-06T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2ZZQ112UR%2FiBD0%2FZSvdDoT2ZwrQDwrNkQevq1ZC2wDw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/73.png?st=2019-09-05T09%3A50%3A04Z&se=2022-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wuF1eY9CUxLBAXi9t8ndgZdtfLzG%2BxXLZe2jdT8aEOI%3D)

**Note:** *Wait for the operation to complete. This should take less than a minute.*

4.	From the az1010302w-lb - Inbound NAT rules blade, add the second inbound NAT rule with the following settings:

```

Name: az1010302w-vm1-RDP

Frontend IP address: LoadBalancedFrontEnd

IP Version: IPv4

Service: Custom

Protocol: TCP

Port: 33891

Target virtual machine: az1010302w-vm1

Network IP configuration: ipconfig1 (10.101.32.4) or ipconfig1 (10.101.32.5)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/74.png?st=2019-09-05T09%3A50%3A28Z&se=2022-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BalniLBqZiJoftByhJvOL%2F%2FV828V5iKWcDe9gr%2BVtHA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/75.png?st=2019-09-05T09%3A50%3A47Z&se=2022-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6O52uyz1OeouLnsjOfMpGUI0W%2F9f04sDst6Lr%2FUIuuo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/76.png?st=2019-09-05T09%3A51%3A06Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rVt0BFmA%2BnZp%2B553wf%2Fln7tRE1bhC9363G3QjekK%2Bs0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/77.png?st=2019-09-05T09%3A51%3A25Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SG5rvCYbmnswDt4ma5%2FQvMialPdhNooDrPMS3xdVkVc%3D)


**Note:** Wait for the operation to complete. This should take less than a minute.

### Task 5: Verify Azure load balancing and NAT rules.

1.	In the Azure portal, navigate to the blade of the Azure load balancer **az1010301w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/78.png?st=2019-09-05T09%3A51%3A43Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8lYrsGgZpIKcw9fM%2B%2Bx6XHgQlRsxpsb3MlBDvCQ9OiI%3D)
 
2.	On the **az1010301w-lb** blade, identify the public IP address assigned to the load balancer frontend.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/79.png?st=2019-09-05T09%3A52%3A03Z&se=2022-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sj94bI0UWukazMhWM76vFsTIuzBpP7ziajJnUtuLFF4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/80.png?st=2019-09-05T09%3A52%3A22Z&se=2022-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w9N8UjztkEeheuBszgeKYoIAt4cNlhOvHE1OZqgSfRI%3D)
 
3.	In the chrome window, open a new tab and browse to the IP address you identified in the previous step.
4.	Verify that the tab displays the default Internet Information Services home page.

Ex:

**http://Loadbalancer Punlic ip address**
 
 http://40.112.171.221
 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/81.png?st=2019-09-05T09%3A52%3A42Z&se=2022-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1x3oS9tbLz4pFPoUFwcqxwLlXj0ZvBOgP01rAwN460M%3D)
 
5.	Close the browser tab displaying the default Internet Information Services home page.
6.	In the Azure portal, navigate to the blade of the Azure load balancer **az1010301w-lb.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/82.png?st=2019-09-05T09%3A53%3A00Z&se=2022-09-06T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d%2FCser0fL3i0GNJ5SODvnotMhM7qrg0Cwvp09ZJ%2FVVw%3D)
 
7.	On the **az1010301w-lb** blade, identify the public IP address assigned to the load balancer frontend.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/83.png?st=2019-09-05T09%3A53%3A22Z&se=2022-09-06T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HvH0aL3SvCY70hP4X6%2Faa6HKw%2FCgrcvJkPXWhyFVOdM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/84.png?st=2019-09-05T09%3A53%3A42Z&se=2022-09-06T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=swJbx8zXti5cbPm%2BfSAr1J3v%2FfSdKlDqhD1o1ioYqY0%3D)

8.	From the lab virtual machine, run the following command, after replacing the <az1010301w-lb_public_IP> placeholder with the IP address you identified in the previous task:

**mstsc /v:<az1010301w-lb_public_IP>:33890**

**Note:** *This command initiates a Remote Desktop session to the **az1010301w-vm0** Azure VM by using the **az1010301w-vm0-RDP** NAT rule you created in the previous task.*

Open the RDP seesion in the platform.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/85.png?st=2019-09-05T09%3A54%3A05Z&se=2022-09-06T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SPmppzXZ%2Bcc%2By6MmMBkO%2F00jH6tdswjM0plqI7nB54s%3D)
 
9.	When prompted to sign in, provide the following credentials:

**Admin Username: adminuser**
**Admin Password: Password@1234**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/86.png?st=2019-09-05T09%3A54%3A34Z&se=2022-09-06T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FaM4I0e0Bu50y4az8JYts1W%2FFlFOQ8PbWQ6m36Vzp%2B0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/87.png?st=2019-09-05T09%3A54%3A52Z&se=2022-09-06T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2MwCEp783KQBAnJzBGgpC9a2IgjU35xKkHkq4kaaHlg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/88.png?st=2019-09-05T09%3A55%3A11Z&se=2022-09-06T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4tTsYiaXQtPpQSrxCTfFlDOWoU%2FeyEwZDnvxSqfXG3A%3D)
 
10.	Once you sign in, from the command prompt, run the following command:

```
Hostname

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/89.png?st=2019-09-05T09%3A55%3A32Z&se=2022-09-06T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9SW6cK8c7QakQAE5D5wmF6JcQnah5Ybqz6VNLGi058c%3D)

11.	Review the output and verify that you are actually connected to the **az1010301w-vm0** Azure VM.

**Note:** *Repeat the same tests for the second region.*

**Result:** *After you completed this exercise, you have implemented and verified load balancing rules and NAT rules of Azure load balancers in both regions.*

## Exercise 3: Implement Azure Traffic Manager load balancing

The main tasks for this exercise are as follows:

1.	Assign DNS names to public IP addresses of Azure load balancers
2.	Implement Azure Traffic Manager load balancing
3.	Verify Azure Traffic Manager load balancing

### Task 1: Assign DNS names to public IP addresses of Azure load balancers

**Note:** *This task is necessary because each Traffic Manager endpoint must have a DNS name assigned.*

1.	In the Azure portal, navigate to the blade of the public IP address resource associated with the Azure load balancer in the first region named **az1010301w-lb-pip.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/90.png?st=2019-09-05T09%3A56%3A39Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7C%2FuK52wxTS9w3Hg97l8fovQmvAsWjiAa14WfXDQLhE%3D)
 
2.	From the **az1010301w-lb-pip** blade, display its **Configuration** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/91.png?st=2019-09-06T05%3A45%3A40Z&se=2022-09-07T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=D%2FkOHQdKK5gp09Loun%2F7EL5j3QYZsJsYBEQDi8ELK0U%3D)
 
3.	From the **az1010301w-lb-pip - Configuration** blade set the **DNS name label** of the public IP address to a unique value.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/92.png?st=2019-09-05T09%3A57%3A18Z&se=2022-09-06T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FtLuHDK%2FIt%2Bnk1LyXlGHURGd3xNsRZNKPd76tkW8kr8%3D)
 
**Note:** *The green check mark in the **DNS name label (optional)** text box will indicate whether the name you typed in is valid and unique.*

4.	Navigate to the blade of the public IP address resource associated with the Azure load balancer in the second region named **az1010302w-lb-pip**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/93.png?st=2019-09-05T09%3A57%3A38Z&se=2022-09-06T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a1mXLgkdSoYQ%2FTrBJmqDcN2tg10q6O6LpFMRYwYzVcI%3D)
 
5.	From the **az1010302w-lb-pip** blade, display its **Configuration** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/94.png?st=2019-09-05T09%3A57%3A57Z&se=2022-09-06T08%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=n2IOEDkv%2BAd0%2FYEIDuF4GtAOHvLMye%2FOUeBoNo0JyBE%3D)
 
6.	From the **az1010302w-lb-pip - Configuration** blade set the **DNS name label** of the public IP address to a unique value.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/95.png?st=2019-09-05T09%3A58%3A31Z&se=2022-09-06T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FrV6UQqzG7ab0PawtxYEWmS2%2BtQN0%2F1GDgzKBm1Cq2M%3D)

**Note:** *The green check mark in the **DNS name label (optional)** text box will indicate whether the name you typed in is valid and unique.*

### Task 2: Implement Azure Traffic Manager load balancing

1.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/96.png?st=2019-09-05T09%3A58%3A57Z&se=2022-09-06T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5bRAK5vK7Fh3%2FFvUK3HrsLN7cp5IPrkd15psQwsA%2BYg%3D)
 
2.	From the **Create a resource** blade, search Azure Marketplace for **Traffic Manager profile**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/97.png?st=2019-09-05T09%3A59%3A19Z&se=2022-09-06T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=j6OEkQM5VTAeMCIh7BCfBveqEKMKu6vPdCi7rPTVI6A%3D)
 
3.	Use the list of search results to navigate to the **Create Traffic Manager profile** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/98.png?st=2019-09-05T09%3A59%3A39Z&se=2022-09-06T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QiiAgnXEHIFcjy9ECNPRnufFP%2FH8enC0bH7c%2BtFJWlc%3D)
 
4.	From the **Create Traffic Manager profile** blade, create a new Azure Traffic Manager profile with the following settings:

* **Name:** `a globally unique name in the trafficmanager.net DNS namespace` <br>
* **Routing method:** `Weighted` <br>
* **Subscription:** `Select the default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Region:** `{{azure-rg-location}}`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/99.png?st=2019-09-05T10%3A00%3A01Z&se=2022-09-06T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0g2zWKJd4YV2VbmFTf5vemakl7AW4bDuKsr4HfP%2BTA4%3D)
 
5.	In the Azure portal, navigate to the blade of the newly provisioned Traffic Manager profile.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/100.png?st=2019-09-05T10%3A00%3A27Z&se=2022-09-06T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ePSjL6TZoYV%2BJlZlEKJEvaahkwfhgdNDUhOS8%2B7BntM%3D)
 
6.	From the Traffic Manager profile blade, display its **Configuration** blade and review the configuration settings.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/101.png?st=2019-09-05T10%3A00%3A47Z&se=2022-09-06T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mS%2BbiIBTwFcFvIXp4%2FozWBBiU5Ud6f5V2fxlUYADPQk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/102.png?st=2019-09-05T10%3A01%3A12Z&se=2022-09-06T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6SgfNkCw8l8KmL0aZ38bAqjJMJZalQzKlj%2F2BE4hZtY%3D)
 
**Note:** *The default TTL of the Traffic Manager profile DNS records is 60 seconds*

7.	From the Traffic Manager profile blade, display its **Endpoints** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/103.png?st=2019-09-05T10%3A01%3A32Z&se=2022-09-06T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mfl3Fdvs3ca1hrJ9sfUB5AMCVGDmy4Bm2Dvf9fTdd1o%3D)
 
8.	From the **Endpoints** blade, add the first endpoint with the following settings:

```

Type: Azure endpoint

Name: az1010301w-lb-pip

Target resource type: Public IP address

Target resource: az1010301w-lb-pip

Weight: 100

Custom Header settings: leave blank

Add as disabled: leave blank

```

9.	From the **Endpoints** blade, add the second endpoint with the following settings:

```

Type: Azure endpoint

Name: az1010302w-lb-pip

Target resource type: Public IP address

Target resource: az1010302w-lb-pip

Weight: 100

Custom Header settings: leave blank

Add as disabled: leave blank

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/104.png?st=2019-09-05T10%3A01%3A51Z&se=2022-09-06T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ggc08uIe585DTlrv1ryDqHZNuaa4BMnkhloLrT7DHBE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/105.png?st=2019-09-05T10%3A02%3A14Z&se=2022-09-06T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ItjTaJ61wXI0PdmgPg2iAZ8GxMjSQ%2FnSMEfMhXc0abM%3D)
 
10.	On the **Endpoints** blade, examine the entries in the **MONITORING STATUS** column for both endpoints. Wait until both are listed as **Online** before you proceed to the next task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/106.png?st=2019-09-05T10%3A02%3A33Z&se=2022-09-06T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7hAgpSguvbzmi6qXyugdZ6bAcz8zkVzLCif3UMipwpY%3D)
 
### Task 3: Verify Azure Traffic Manager load balancing

1.	From the **Endpoints** blade, switch to the **Overview** section of the Traffic Manager profile blade.

2.	Note the DNS name assigned to the Traffic Manager profile (the string following the **http://** prefix).

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/107.png?st=2019-09-05T10%3A02%3A55Z&se=2022-09-06T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CCVgr6qkKIHrFcCmEvFfw0Segn%2FNETmPG%2BQDnSOXvQg%3D)
 
3.	From the Azure Portal, start a PowerShell session in the Cloud Shell pane.

* **Region:** `{{azure-rg-location}}`
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Storage account name:** `sampl123` (A name of a new Storage Account) <br>
* **File Share Name:** `sampltest` (A name of a new file share)


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/125.png?st=2019-09-13T09%3A46%3A16Z&se=2022-09-14T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t1IHui2xPGU0hT64zNBcDJeHhxMhw0FQdFeq6O0gYrk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/126.png?st=2019-09-13T09%3A47%3A30Z&se=2022-09-14T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TsglEPjnH9fJp%2F%2BGImI8tyKdWbgcspErpzPRHH171oE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/124.PNG?st=2019-09-13T09%3A48%3A02Z&se=2022-09-14T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8SFVNc9JRh2REO%2FP%2B824ottAEv06Bui%2B7wMr12inGwQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/127.PNG?st=2019-09-13T09%3A58%3A52Z&se=2022-09-14T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lxUjQc5lne0yQyVE5FiL1MQLnNsFPvDD8E9jQq%2FFNNc%3D)

 
**Note:** If this is the first time you are launching the Cloud Shell in the current Azure subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a storage account in an automatically generated resource group.

4.	In the Cloud Shell pane, run the following command, replacing the <TM_DNS_name< placeholder with the value of the DNS name assigned to the Traffic Manager profile you identified in the previous task:

```

nslookup <TM_DNS_name>

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/109.png?st=2019-09-05T10%3A03%3A35Z&se=2022-09-06T10%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZhRwwFZolXnJiTmgeXs3UmFugTuk8yTHNcvxmmIbCak%3D)

5.	Review the output and note the **Name** entry. This should match the DNS name of the one of the Traffic Manager profile endpoints you created in the previous task.

6.	Wait for at least 60 seconds and run the same command again:

```

nslookup <TM_DNS_name>

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab8/110.png?st=2019-09-05T10%3A04%3A04Z&se=2022-09-06T10%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RBJUX0bu4kX%2FtgfRwK086ZWk1NX4tEl6HhjdpSEPj88%3D)
 
7.	Review the output and note the **Name** entry. This time, the entry should match the DNS name of the other Traffic Manager profile endpoint you created in the previous task.

> **Result**: After you completed this exercise, you have implemented and verified Azure Traffic Manager load balancing.
