# Lab 5: Creating and Configuring Virtual Machines & Load balancer

## Table of Contents 

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Creating a virtual network](#exercise-1-creating-a-virtual-network)

[Exercise 2: Creating the Azure VM in an availability set](#exercise-2-creating-the-azure-vm-in-an-availability-set)
   
[Exercise 3: Configuring load balancing of Azure VMs](#exercise-3-configuring-load-balancing-of-azure-vms)
    
## Overview

The aim of this lab is to learn fundamental concepts of Azure VNets by creating a VNet, configuring it. You will also deploy Azure Load Balancer and its backend pool consisting of two Virtual Machines configured in different availibility sets. Once configured, you will test the load balancing functionality. 

### Scenario and Objectives

Contoso Corporation plans to deploy a number of Azure virtual machines in a load-balanced configuration. You plan to create a virtual network and configure an Azure load balancer to test this plan.

The main tasks for this exercise are as follows:

1.	Create a virtual network by using Azure Portal

2.	Create the first Azure VM in an availability set by using Azure Portal

3.	Create the second Azure VM in an availability set by using Azure Portal

4. Configuring load balancing of Azure VMs

## Pre-Requisites

* Azure Portal 

* Remote Desktop

* Familiar with Virtual Network

* Familiar with Load balancer

Note: Azure Portal & Remote Desktop is part of the Lab environment

## Exercise 1: Creating a virtual network

### Task 1: Create a virtual network by using the Azure portal

*	**Virtual Network**

Azure Virtual Network (VNet) is the building block for your private network in Azure. 
VNet is similar to a traditional network that you'd operate in your own data centre, but brings with it additional benefits of Azure's infrastructure such as scale, availability and isolation.

Using the Chrome browser, login into Azure portal with the below details.

**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/portallogin.PNG?st=2019-08-22T06%3A35%3A13Z&se=2020-08-23T06%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W3otmg6cV2Y50vams99Ch%2F8hDhMEJo2go1YN8NfVu4Q%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/portal4.PNG?st=2019-08-22T06%3A36%3A34Z&se=2020-08-23T06%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wXyJo28uGYUGVsHdba%2FC839CqxY%2FdaM20a7PDKa5a4I%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/portal1.PNG?st=2019-08-22T06%3A37%3A05Z&se=2020-08-23T06%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XmkBNJjLKMBJWuNfyS7W6j96GnIMvoRPGzmiDXTlUnc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/portal2.PNG?st=2019-08-22T06%3A37%3A43Z&se=2020-08-23T06%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Od1QlH7gae9bvBstOVeD1fU3wlLq0qBwRTGNgYWYzHc%3D)

1.	From the Azure portal, create a new virtual network by using the following settings:

**Note:** Leave all the settings to default except for the following.


**Name:** labVNet1

**Address space:** 10.0.0.0/16

**Subscription:** Select the default

**ResourceGroup:** {{resource-group-name}}

**Region:** {{Location}}

**Subnet name:** subnet0

**Address range:** 10.0.0.0/24


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/1.png?st=2019-08-22T06%3A31%3A54Z&se=2020-08-23T06%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cpWsaQnIFzHx%2FFjUzq3awbyNZ%2Bg6oMgYoowCwB3YH9Y%3D)
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/2.png?st=2019-08-22T06%3A38%3A25Z&se=2020-08-23T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m8uwORk3F7CRS6t1DlnHc4ba%2FDFN4N9yI8wuos12YkM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/3.png?st=2019-08-22T06%3A38%3A52Z&se=2020-08-23T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CsjBtCEmkxvthbWCPeeEEH1bccDpXnW1J%2FVnO8%2B6xqE%3D) 

 2. After 1-2 minutes, a VNET is created with the specified name.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/4.png?st=2019-08-22T06%3A39%3A17Z&se=2020-08-23T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=39t2wf6OgMsEvr7jOy1D%2FMxDSYdp9%2Bu7qBO5Up1%2B0iU%3D)

**Note:** *Ignore any messages about overlapping address spaces that might appear when you type the value in the Address space text box.*

## Exercise 2: Creating the Azure VM in an availability set

### Task 1: Create the first Azure VM in an availability set by using Azure Portal


*	**Virtual Machines**

Azure Virtual Machines (VM) is one of several types of on-demand, scalable computing resources that Azure offers.
An Azure VM gives you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it. However, you still need to maintain the VM by performing tasks, such as configuring, patching and installing the software that runs on it.

*  **Availability Set**

An Availability Set is a logical grouping capability for isolating VM resources from each other when they're deployed. 
Azure makes sure that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches. If a hardware or software failure happens, only a subset of your VMs are impacted and your overall solution stays operational. 
Availability Sets are essential for builing reliable cloud solutions.

1.	From the Azure portal, create a new virtual machine by choosing the Windows Server by click on **+** symbol , from windows server select Windows Server 2019 Datacenter image in the Azure Marketplace and by using the Resource Manager deployment model with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/change1.png?st=2019-12-18T11%3A37%3A22Z&se=2022-12-19T11%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lKJ9yAvzmAtnf24L87vwzZsNY1YixcLsUILdPog4xhg%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/change2.png?st=2019-12-18T11%3A37%3A45Z&se=2022-12-19T11%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3QiQ8MM%2F6b8VWm183kkh0SjvlcoMEfUVNYiwYnLk5%2FQ%3D)

> **Basics**

**Subscription:** Select the default

**ResourceGroup:** {{resource-group-name}}

**Virtual machine name:** 10979E0501-vm

**Region:** {{Location}}

**Availability options:** Availability set

**Availability set**: the name 10979E0501-avSet of a new availability set with the default number of fault domains and update domains

**Image:** Windows Server 2016 Datacenter

**Size:** accept the default size

**Username:** Student

**Password:** Password@123

**Confirm password:** Password@123

**Public inbound ports:** Allow selected ports

**Select inbound ports:** RDP

**Already have a Windows license?:** No



> **Disks**

```

OS disk type: Standard HDD

Use managed disks: yes

```

> **Networking**

```

Virtual network: labVNet1

Subnet: subnet0

Public IP address: None

NIC network security group: Basic

Public inbound ports: Allow selected ports

Select inbound ports: RDP

Accelerated networking: Off

Place this virtual machine behind an existing load balancing solution?: no

```

> **Management**

```

Boot diagnostics: Off

OS guest diagnostics: Off

Managed service identity: Off

Enable auto-shutdown: Off

Enable backup: Off

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
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/l5-3.png?st=2019-12-04T07%3A18%3A00Z&se=2026-12-05T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l9fVuy%2Fmb0MsKbyrtdVwijFCTvwAwWQWnUtcr9ys8UE%3D) 
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/8.png?st=2019-08-22T06%3A40%3A56Z&se=2020-08-23T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PrqKOazzlTQNtIomft7AWYZIDogGGWXkPzslLDjLzZk%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/9.png?st=2019-08-22T06%3A41%3A15Z&se=2020-08-23T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lIfGxqXOciVnyXBSHkwA2TQYheLPZ%2BUtPpf6fj55ang%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/10.png?st=2019-08-22T06%3A47%3A07Z&se=2020-08-23T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZAeR0v%2FHzTcMzx6cqUhtYkmZoj%2BznJMXsf%2BzhywW4cI%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/11.png?st=2019-08-22T06%3A47%3A24Z&se=2020-08-23T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4fZnowLKE3oKwyCaG1KM1MVA3NEmVizfNvyRHzEsG9Q%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/12.png?st=2019-08-22T06%3A47%3A41Z&se=2020-08-23T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h9sKqNFP6xxq%2BEOy%2BvU0ZpEA6k2BZBpNqiokUbQTyog%3D)

2. Wait for the deployment to complete.

**Note:** *The deployment might take about 5 minutes.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/13.png?st=2019-08-22T08%3A50%3A39Z&se=2020-08-23T08%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HYxn29C7m7HQ7lr0S5lkpWRAdI3hZfN1pK33ZSLdRTw%3D)

### Task 2: Create the second Azure VM in an availability set by using Azure Portal

1.	From the Azure portal, create a new virtual machine by choosing the Windows Server by click on **+** symbol , from windows server select Windows Server 2019 Datacenter image in the Azure Marketplace and by using the Resource Manager deployment model with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/change1.png?st=2019-12-18T11%3A39%3A09Z&se=2022-12-19T11%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tHaGSmo%2F3PlbX50Ednh3msbZ%2BejiipSII%2FCGMOjo%2FkY%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/change2.png?st=2019-12-18T11%3A37%3A45Z&se=2022-12-19T11%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3QiQ8MM%2F6b8VWm183kkh0SjvlcoMEfUVNYiwYnLk5%2FQ%3D)

 > **Basics**

**Subscription:** Select the default

**ResourceGroup:** {{resource-group-name}}

**Virtual machine name:** 10979E0502-vm

**Region:** {{Location}}

**Availability options:** Availability set

**Availability set:** the name 10979E0501-avSet of a new availability set with the default number of fault domains and update domains

**Image:** Windows Server 2016 Datacenter

**Size:** accept the default size

**Username:** Student

**Password:** Password@123

**Confirm password:** Password@123

**Public inbound ports:** Allow selected ports

**Select inbound ports:** RDP

**Already have a Windows license?:** No

```

> **Disks**

```

OS disk type: Standard HDD

Use managed disks: yes

```

> **Networking**

```

Virtual network: labVNet1

Subnet: subnet0

Public IP address: None 

NIC network security group: Basic

Public inbound ports: Allow selected ports

Select inbound ports: RDP

Accelerated networking: Off

Place this virtual machine behind an existing load balancing solution?: no

```

> **Management**

```
Boot diagnostics: Off

OS guest diagnostics: Off

Managed service identity: Off

Enable auto-shutdown: Off 

Enable backup: Off

Note: Don't make any changes to other settings, leave them as is.

```

> **Advanced**

```

Note: Don't make any chnages to other settings, leave them as is.

```

> **Tags**

```

Note: Don't make any changes to other settings, leave them as is.



![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/l5-4.png?st=2019-12-05T06%3A56%3A01Z&se=2025-12-06T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TfxyftdgrUPxzdpLh%2F4pb2AK6gVSV8v%2FOnsTTznLvVo%3D) 
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/17.png?st=2019-08-22T06%3A51%3A01Z&se=2020-08-23T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QRwbjvWwjpEC4PMJoQJR2FxdHDJB1bw%2B0y%2F%2BlP%2FgLuQ%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/18.png?st=2019-08-22T06%3A51%3A18Z&se=2020-08-23T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kKKLag4%2F0q3z94rhcx7%2BnoZRYt69%2BSlBK1rc0LyTzZI%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/19.png?st=2019-08-22T06%3A51%3A44Z&se=2020-08-23T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DoD0Jmf3KGNTJSbK0vyG6GExEebZxMGUusHgudalFuQ%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/20.png?st=2019-08-22T06%3A52%3A06Z&se=2020-08-23T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xo7X8XtaeOlHbnNArtTYqhQjPXkf%2BJADPlpW7SEORGQ%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/21.png?st=2019-08-22T06%3A52%3A24Z&se=2020-08-23T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LxygAk%2FI3KyWriF4IO%2BjSKWWa8uyofeCFLOo%2FZFhU6Q%3D) 

2. Wait for the deployment to complete.

**Note:** *The deployment might take about 5 minutes.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/22.png?st=2019-08-22T06%3A52%3A49Z&se=2020-08-23T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7JQd7Ft6DCR06GuR63oFwxa51%2BOWNpFSpFquGAck%2Fbw%3D)

**Result:** Once you completed this exercise, you have created an Azure virtual network and deployed two Azure VMs in the same availability set into it.

## Exercise 3: Configuring load balancing of Azure VMs

**Scenario**

After creating the Azure virtual networks, you want to deploy two virtual machines into them and ensure that they can communicate directly by using their private IP addresses.

The main tasks for this exercise are as follows:

1.	Deploy an Azure load balancer

2.	Configure the Azure load balancer

3.	Test Azure load balancing

4.	Prepare for the next module

### Task 1: Deploy an Azure load balancer

*	**Load Balancer**

Load Balancer distributes traffic that arrive in the load balancer's frontend to backend pool instances, according to rules and health probes.
Load Balancer can scale your applications and create high availability for your services. Load Balancer supports inbound and outbound scenarios, provides low latency and high throughput.

1.	From the Azure portal, create an Azure load balancer with the following settings:

> **Basics**


**Subscription:** Select the default

**ResourceGroup:** {{resource-group-name}}

**Name:** 10979E0501-ilb

**Region:** {{Location}}

**Type:** Public

**SKU:** Basic

**Public IP address:** a new public IP address resource named 10979E0501-ilb-pip

**Assignment:** Dynamic 

**Note:** Don't make any changes to other settings, leave them as is.

```

> **Tags**

```

Note: Don't make any changes to other settings, leave them as is.


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/23.png?st=2019-08-22T06%3A53%3A18Z&se=2020-08-23T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nVcNyRfHQXdVZPApT%2Be15ZmegO8nAt4j%2F2EKqzLHXj0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/24.png?st=2019-08-22T06%3A53%3A39Z&se=2020-08-23T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t8D0VoI4QXkuP5bN8mSYeN%2BFbbeKgrwtS%2BO3e2x73n0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/25.png?st=2019-08-22T06%3A54%3A00Z&se=2020-08-23T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=syWGp6Hxt2WKkefJpXFdOY%2B4XktbE5voy6KP2q522LQ%3D)
 
2.	Wait for the deployment to complete.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/26.png?st=2019-08-22T06%3A54%3A18Z&se=2020-08-23T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9HNwJbBDbXEb9Pf5Ftlynqdx6e2qMlibNuuEw%2Flpy9Y%3D)

### Task 2: Configure the Azure load balancer

1.	Configure the newly created load balancer with the backend pool named **10979E0501-ilb-bepool** and associate it to the availability set **10979E0501-avSet** with ipconfig1 of **10979E0501-vm0** and *ipconfig1 of 10979E0501-vm1.

Refresh the tab to see the rule after few minutes
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/27.png?st=2019-08-22T06%3A54%3A42Z&se=2020-08-23T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0xPGifV%2Fknifop7oZE%2BcIlUMXD5DTRGLWHJTbvwEu4U%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/28.png?st=2019-08-22T06%3A54%3A58Z&se=2020-08-23T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=U3anQc7SpubT6DbvWTkj%2B%2BlYspmm2qe2%2BgKs3fNChSY%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/29.png?st=2019-08-22T06%3A55%3A17Z&se=2020-08-23T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NKrgIC8EuioG6en%2B5QSJnIrTqzmBSg6IQ3pl5v29Qe8%3D) 
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/30.png?st=2019-08-22T06%3A55%3A39Z&se=2020-08-23T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VoTyO7lYPjx7%2B5XTNV12S25l5k06iLQThhoR98JUZbo%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/31.png?st=2019-08-22T06%3A55%3A56Z&se=2020-08-23T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XOynyAg6%2BH9%2BwbCL9hMdsILU1px9YYgVty%2BvrfdYEbc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/32.png?st=2019-08-22T06%3A56%3A35Z&se=2020-08-23T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PG9dOf2%2BZ013RHlAZQOkVNlC6lfCjhl7hvCq%2Bapmy5Y%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/33.png?st=2019-08-22T06%3A56%3A59Z&se=2020-08-23T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KctXy0ozYumJBYT6CleJWEY8jp%2BgpSO0O5YTkiQDOHM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/34.png?st=2019-08-22T06%3A57%3A17Z&se=2020-08-23T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=elHxGc5M9nNoeZ0s4p4lH%2B8SxOKK90Yb4mdDadGHmBU%3D)

2.	Configure the load balancer with the health probe that has the following settings:

```

Name: 10979E0501-ilb-probetcp3389

Protocol: TCP

Port: 3389 

Interval: 5

Unhealthy threshold: 2

```

Refresh the tab to see the rule after few minutes

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/35.png?st=2019-08-22T06%3A57%3A37Z&se=2020-08-23T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jBiefP7JTLhUSk0YvbN0KQ%2F0JfngMOye3K0Zww%2FevGE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/36.png?st=2019-08-22T06%3A57%3A54Z&se=2020-08-23T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Jsa%2F1tX5wzhW73Ue2ZXIB21rCEPRf6c1l5hIwIaD5sU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/37.png?st=2019-08-22T06%3A58%3A15Z&se=2020-08-23T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YXBeo5mlcrOS7QnPH5OwJ8JAXPGAayBe3OD5vWsJoO0%3D)
 

3.	Configure the load balancer with the following load balancing rule:

```

Name: 10979E0501-ilb-ruletcp3389

IP Version: IPv4

Frontend IP address: LoadBalancerFrontEnd

Protocol: TCP

Port: 3389

Backend port: 3389

Backend Pool: 10979E0501-ilb-bepool (2 virtual machines)

Probe: 10979E0501-ilbprobetcp3389 (TCP:3389)

Session persistence: None

Idle timeout: 4

Floating IP (direct server return): Disabled

```

Refresh the tab to see the rule after few minutes

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/38.png?st=2019-08-22T06%3A58%3A36Z&se=2020-08-23T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=r8UPPs4zNC8NiVzXR1mO7AJXID8wvHwAYiAg2Qs9Mu0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/39.png?st=2019-08-22T06%3A58%3A53Z&se=2020-08-23T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3baej1Uvt7ykGvFAfG1Uv%2F%2Bs0aqNSpCJ%2BnJinlcak8A%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/40.png?st=2019-08-22T06%3A59%3A12Z&se=2020-08-23T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tvY40TRPO88tfSrRvCXLTG25um7o%2FoKTyivCn7NYbdI%3D)
 

4.	On the 10979E0501-ilb blade, review the **Essentials** section and identify the public IP address assigned to the load balancer.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/41.png?st=2019-08-22T06%3A59%3A30Z&se=2020-08-23T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qVmqea0rZg1aCQhhrKwpRDXtCApZlyMMchI%2FnZHukt8%3D)

**Note:** *This configuration will allow you to connect to either of two Azure VMs via RDP even though neither of them has directly assigned public IP address. The Azure VMs in this configuration can host as highly available jump hosts for connections to other Azure VMs within the same Azure virtual network.*

### Task 3: Test Azure Load Balancer

1.	From the Azure portal, identify the IP address of the **10979E0501-ilb** load balancer.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/42.png?st=2019-08-22T06%3A59%3A48Z&se=2020-08-23T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pg1MxF852SX%2BL%2F%2BedDORQgPOAaJmfDdpAg3z9nqTR6Y%3D)
 
2.	Start a Remote Desktop session targeting the IP address of the load balancer and provide username and password of your Azure VM.

3. You can start a Remote Destop client, by selecting the windows icon on top right side of the Lab Window 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/Screenshot%20(87).png?st=2019-08-22T07%3A00%3A12Z&se=2020-08-23T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=daRlKC9%2BjonHTz%2BgiGFreJ2CwfHifASpZzZH4fa8FFE%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/43.png?st=2019-08-22T07%3A00%3A32Z&se=2020-08-23T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hnBwGo9biLRc7lRR6YmrpbnJJw2z3C%2FNoh4kTfr9wkU%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/44.png?st=2019-08-22T07%3A00%3A49Z&se=2020-08-23T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lCUPawX1POp7IxdAp6bnKWVl5XEO4cPamxvt2zKdJM0%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/45.png?st=2019-08-22T07%3A01%3A12Z&se=2020-08-23T07%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F%2FuZWWppu9XPn%2F9TWZf1nN8xQWFzh%2F66naCv89xIYcw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/46.png?st=2019-08-22T07%3A01%3A28Z&se=2020-08-23T07%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Hs5a7jCiWD%2For%2FDNumVR5W5v%2FeoXlZQ8G5H0zH%2BlX%2F0%3D)

4.	Identify the Azure VM that you connected to via the Remote Desktop session.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/47.png?st=2019-08-22T07%3A02%3A00Z&se=2020-08-23T07%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s2ZI80dqHCvjpOd8zR5wWas4sxh3TEVOycSviSiASM8%3D)
 
5.	From the Remote Desktop sessions to the Azure VM, shut down its operating system. This will automatically terminate the Remote Desktop session.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/Screenshot%20(88).png?st=2019-08-22T07%3A02%3A26Z&se=2020-08-23T07%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NZMV6xr693qtHrK5%2FfGENVRcfxHnorvXb1zRtkT5dzM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab5-Create%20and%20configure%20virtual%20networks/Screenshot%20(89).png?st=2019-08-22T07%3A02%3A43Z&se=2020-08-23T07%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=siqXg6ktHDy37k%2BCGrqz0Vlp6aZ8dtfeIdCTD1E2KXw%3D)

5.	Start a Remote Desktop session targeting the IP address of the load balancer.

6.	Identify the Azure VM that you connected to via the Remote Desktop session. Note that you were automatically redirected to the other Azure VM.

**Result:** Once you completed this exercise, you have deployed an Azure load balancer and tested its functionality.
