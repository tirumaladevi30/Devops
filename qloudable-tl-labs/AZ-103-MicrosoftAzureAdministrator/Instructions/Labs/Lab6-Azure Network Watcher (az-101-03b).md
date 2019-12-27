# Lab 6: Use Azure Network Watcher for monitoring and troubleshooting network connectivity

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Prepare infrastructure for Azure Network Watcher-based monitoring](#exercise-1-prepare-infrastructure-for-azure-network-watcher-based-monitoring)

[Exercise 2: Use Azure Network Watcher to monitor network connectivity](#exercise-2-use-azure-network-watcher-to-monitor-network-connectivity)

## Overview

Overview of this lab is about deploying Azure VM's, Azure storage accounts, Azure SQL Database instances using ARM templates. After the resources provisioning, enabling the Network Watcher to monitor the network connectivity logs between the resources.

### Scenario and Objective
  
XYZ training labs corporation wants to monitor Azure virtual network connectivity by using Azure Network Watcher.

After completing this lab, you will be able to:

* Deploy Azure VMs, Azure storage accounts, and Azure SQL Database instances by using Azure Resource Manager templates.

* Use Azure Network Watcher to monitor network connectivity

## Pre-Requisites

* Lab Virtual Machine (windows virtual machine with PowerShell module installed)

* ARM Template

All tasks in this lab are performed from the Azure portal (including a PowerShell Cloud Shell session)

## Exercise 1: Prepare infrastructure for Azure Network Watcher-based monitoring
  
The main tasks for this exercise are as follows:

1.	Deploy Azure VMs, an Azure Storage account, and an Azure SQL Database instance by using an Azure Resource Manager template.

2.	Enable Azure Network Watcher service.

3.	Establish peering between Azure virtual networks.

4.	Establish service endpoints to an Azure Storage account and Azure SQL Database instance.

**Azure Network Watcher**

Azure Network Watcher provides tools to monitor, diagnose, view metrics, and enable or disable logs for resources in an Azure virtual network.

**Azure storage accounts**

Azure Storage is Microsoft's cloud storage solution for modern data storage scenarios. Azure Storage offers a massively scalable object store for data objects, a file system service for the cloud, a messaging store for reliable messaging, and a NoSQL store.

**Azure VMs**

Virtual Machines gives you the flexibility of Virtualization on a wide range of computing solutions with support for Linux, Windows Server, SQL Server, Oracle, IBM, SAP and more.

Each virtual machine has its own virtual hardware, including CPUs, memory, hard drives, network interfaces and other devices. The virtual hardware is then mapped to the real hardware on the physical machine which saves costs by reducing the need for physical hardware systems along with the associated maintenance costs that go with it, plus reduces power and cooling demand.

**Azure SQL Database**

Azure SQL Database is a relational database-as-a service using the Microsoft SQL Server Engine. SQL Database is a high-performance, reliable, and secure database you can use to build data-driven applications and websites in the programming language of your choice, without needing to manage infrastructure.

**ARM templates**

Azure Resource Manager allows you to provision your applications using a declarative template. In a single template, you can deploy multiple services along with their dependencies. The template consists of JSON and expressions that you can use to construct values for your deployment. Resource Manager provides a consistent management layer to perform tasks through Azure PowerShell, Azure CLI, Azure portal, REST API, and client SDKs.

**Resource manager provides the following features:**

* Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.

* Repeatedly deploy your solution through the development lifecycle and your resources are deployed in a consistent state.

* Manage your infrastructure through declarative templates rather than scripts.

* Define the dependencies between resources so they're deployed in the correct order.

* Apply access control to all services in your resource group because Role-Based Access Control (RBAC) is natively integrated into the management platform.

* Apply tags to resources to logically organize all the resources in your subscription.

### Task 1: Deploy Azure VMs, an Azure Storage account, and an Azure SQL Database instance by using Azure Resource Manager templates

1. Using the Chrome browser, login to Azure Portal with the below details:

```
 Azure Username : {{ Portal Username }}

 Azure Password : {{ Portal Password }}

```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/1.PNG?token=AIMANV6Z2MF2AJZB5DXBENS5N47XW) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/2.png?token=AIMANV5A4FGAIJOCWOGPZOS5N47ZG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/3.png?token=AIMANV722KZ42MCBNXFLCX25N474I)

2. In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/4.png?token=AIMANV7LZAZA4AHDISO7DO25N475I)

3. From the **Create a resource** blade, search Azure Marketplace for **Template deployment (deploy using custom templates)**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/5.png?token=AIMANV6ZQZLHQDH32O2BWTC5N476G)

4. Click **Create**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/6.png?token=AIMANV3XRTZI5PJEKNUA23S5N477G)

5. On the **Custom deployment** blade, click the **Build your own template** in the editor link. If you do not see this link, click **Edit template** instead. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/7.png?token=AIMANVY53WCWURPDXJB3DHS5N5AAC)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/8.png?token=AIMANVZTQOOXCMSXXHNDEV25N5AA6)

6. From the **Edit template** blade, load the template file **az-101-03b_01_azuredeploy.json**.

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_06/Network_Watcher/az-101-03b_01_azuredeploy.json?st=2019-08-29T07%3A03%3A12Z&se=2022-08-30T07%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FDxnYd1vRZQjz9imITtt0lJ6rxzmrDuZk%2FT%2BuBMplZk%3D**

> Note: Review the content of the template and note that it defines deployment of an Azure VM, an Azure SQL Database, and an Azure Storage account.

7. **Save** the template and return to the Custom deployment blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/9.png?token=AIMANV3UL3C3WB7JOWID63K5N5ABY)

8. From the Custom deployment blade, navigate to the Edit parameters blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/10.png?token=AIMANV63OAZDKHLITIJXZL25N5AC4)

9. From the **Edit parameters** blade, load the parameters file **az-101-03b_01_azuredeploy.parameters.json**.

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_06/Network_Watcher/az-101-03b_01_azuredeploy.parameters.json?st=2019-08-29T07%3A03%3A45Z&se=2022-08-30T07%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=R8elfA0AcOYDGNy328GKpAWLcEceLX%2Bw8S4obQ9cNf8%3D**

10. **Save** the parameters and return to the Custom deployment blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/11.png?token=AIMANVZPLFDFPSQTC3F7HDK5N5ADW)

11.	From the Custom deployment blade, initiate a template deployment with the following settings:

```
 Subscription: Select as default from the dropdown

 Resource group: {{ ResourceGroup }}

 Location: {{ Location }}

 Vm Size: Standard_DS1_v2

 Vm Name: az1010301b-vm1

 Admin Username: adminuser

 Admin Password: Password@1234

 Virtual Network Name: az1010301b-vnet1

 Sql Login Name: sqluser

 Sql Login Password: Password@1234

 Database Name: az1010301b-db1

 Sku Name: Basic

 Sku Tier: Basic

```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/12.png?token=AIMANV5LGU7LHH5HVD3O3625N5AEU)

> **Note**: To identify VM sizes available in your subscription in a given region, run the following from Cloud Shell and review the values in the **Restriction** column (where &lt;location&gt; represents the target Azure region):
   
```pwsh
Get-AzComputeResourceSku | where {$_.Locations -icontains "<location>"} | Where-Object {($_.ResourceType -ilike "virtualMachines")}
```
**Ex**: Get-AzComputeResourceSku | where {$_.Locations -icontains "East US"} | Where-Object {($_.ResourceType -ilike "virtualMachines")}

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/13.png?token=AIMANV52B6DKRFBJNDGXQNC5N5AFU)

> **Note**: To identify whether you can provision Azure SQL Database in a given region, run the following from Cloud Shell and ensure that the resulting **Status** is set to **Available** (where &lt;location&gt; represents the target Azure region):

 ```pwsh
 Get-AzSqlCapability -LocationName <regionname>
 ```
**Ex**: Get-AzSqlCapability -LocationName “East US”

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/14.png?token=AIMANV7TUJTGJBYWBUBSGCK5N5AGW)

> **Note**: Do not wait for the deployment to complete but proceed to the next step. 

12. In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/15.png?token=AIMANVZV7YZ2HLDYXFWO54K5N5AHW)

13. From the **Create a resource** blade, search Azure Marketplace for **Template deployment**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/16.png?token=AIMANV22XOPSMZY3ZUTMY7K5N5AIY)

14. In the results, click **Template deployment (deploy using custom templates)**, and then click **Create**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/17.png?token=AIMANV4GSMIQXAQS2ZH4X5K5N5AJ4)

15. On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/18.png?token=AIMANV53CTIA4R2LDCTZNQC5N5AK2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/19.png?token=AIMANV4TU24FSOAEBFWO2VK5N5AMC)

16. From the **Edit template** blade, load the template file **az-101-03b_02_azuredeploy.json**. 

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_06/Network_Watcher/az-101-03b_02_azuredeploy.json?st=2019-08-29T07%3A04%3A06Z&se=2022-08-30T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wz0oGnVB1dzG4hJ%2BUTIgi7IAyrh4qFzfMbE%2FZVJrOGI%3D**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/20.png?token=AIMANV7FTQXAXW37T4CWXXS5N5APA)

> **Note**: Review the content of the template and note that it defines deployment of an Azure VM.

17. Save the template and return to the **Custom deployment** blade. 

18. From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/21.png?token=AIMANV5DWH4TVVG7TFGXOP25N5AQO)

19. From the **Edit parameters** blade, load the parameters file **az-101-03b_02_azuredeploy.parameters.json**. 

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_06/Network_Watcher/az-101-03b_02_azuredeploy.parameters.json?st=2019-08-29T07%3A04%3A57Z&se=2022-08-30T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yJ0HCFIP2n5lLIQlrDCMCO0PyrlVvxqBvXFzfsevaoc%3D**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/22.png?token=AIMANVZ7WWBG6KM7V4P3ZZK5N5ARM)

20. Save the parameters and return to the **Custom deployment** blade. 

21. From the **Custom deployment** blade, initiate a template deployment with the following settings:

```
 Subscription: Select as default from the dropdown

 Resource group: {{ ResourceGroup }}

 Location: {{ Location }} 

 Note: The name of an Azure region where you can provision Azure VMs, but which is different from the one you selected during previous deployment, 

 Vm Size: Standard_DS1_v2

 Vm Name: az1010302b-vm2

 Admin Username: adminuser

 Admin Password: Password@1234

 Virtual Network Name: az1010302b-vnet2

```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/23.png?token=AIMANV5X7M3VIHVQQ6LXI7S5N5ASI)

> **Note**: Make sure to choose a different Azure region for this deployment

> **Note**: Do not wait for the deployment to complete but proceed to the next step. 

### Task 2: Enable Azure Network Watcher service

1. In the Azure portal, use the search text box on the **All services** blade to navigate to the **Network Watcher** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/24.png?token=AIMANVZHSMWOPOTUMRFACGC5N5ATO)

2. On the **Network Watcher** blade, verify that Network Watcher is enabled in both Azure regions into which you deployed resources in the previous task and, if not, enable it.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/25.png?token=AIMANV2LMPKBW6U7I7YVNCK5N5AUO)

### Task 3: Establish peering between Azure virtual networks

> **Note**: Before you start this task, ensure that the template deployment you started in the first task of this exercise has completed. 

1. In the Azure portal, navigate to the **az1010301b-vnet1** virtual network blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/26.png?token=AIMANV6YJSPWSVOXPE4GNZS5N5AVM)

2. From the **az1010301b-vnet1** virtual network blade, display the **az1010301b-vnet1 - Peerings** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/27.png?token=AIMANVZKZ2RRNQODHWCOUXS5N5AWE)

3. From the **az1010301b-vnet1 - Peerings** blade, create a VNet peering with the following settings:

    ```
     Name: az1010301b-vnet1-to-az1010302b-vnet2

     Virtual network deployment model: Resource manager

     Subscription: Select as default from the dropdown

     Virtual network: az1010302b-vnet2

     Name of peering from az1010302b-vnet2 to az1010301b-vnet1: az1010302b-vnet2-to-az1010301b-vnet1

     Allow virtual network access: Enabled

     Allow forwarded traffic: disabled

     Allow gateway transit: disabled

    ````

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/28.png?token=AIMANV52XU7NGPNUFJDKZAC5N5AXC)

> **Note**: The Azure portal allows you to configure both directions of the peering simultaneously. When using other management tools, each direction must be configured independently. 

### Task 4: Establish service endpoints to an Azure Storage account and Azure SQL Database instance

1. In the Azure portal, navigate to the **az1010301b-vnet1** virtual network blade.

2. From the **az1010301b-vnet1** virtual network blade, display the **Service endpoints** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/29.png?token=AIMANV6ZS577URKVKMXMSKK5N5A5I)

3. From the **az1010301b-vnet1 - Service endpoints** blade, add a service endpoint with the following settings:

    ```
     Service: Microsoft.Storage

     Subnets: subnet0

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/30.png?token=AIMANV6D4CILVRWZ5VB6ZFC5N5A6C)

4. Repeat the step to create a second service endpoint:

    ```
     Service: Microsoft.Sql

     Subnets: subnet0

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/31.png?token=AIMANV6626MF3DCT7CMQJU25N5BWK)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/32.png?token=AIMANV5VKNYKOFSYWP2WEGS5N5BXG)

5. In the Azure portal, navigate to the **resource group** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/33.png?token=AIMANV7X7KRSEDPJ6VQZMP25N5BYA)

6. From the **resource group** blade, navigate to the blade of the storage account included in the resource group. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/34.png?token=AIMANV243UULMJQTHNIORAK5N5BZE)

7. From the storage account blade, navigate to its **Firewalls and virtual networks** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/35.png?token=AIMANV37FS4NTQ5LOEU33GS5N5B2C)

8. From the **Firewalls and virtual networks** blade of the storage account, configure the following settings:

    ```
     Allow access from: Selected networks

     Virtual networks: 

         VIRTUAL NETWORK: az1010301b-vnet1

             SUBNET: subnet0
    ```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/36.png?token=AIMANV5GYYWLR5CPG3UTEKS5N5B3A)

```
 Firewall: 

     ADDRESS RANGE: none

 Exceptions: 

     Allow trusted Microsoft services to access this storage account: Enabled

     Allow read access to storage logging from any network: Disabled

     Allow read access to storage metrics from any network: Disabled

```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/37.png?token=AIMANV6VGHWWBLI5NV47ZSC5N5B34)

9. In the Azure portal, navigate to the **resource group** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/38.png?token=AIMANV4GHDN2ZK4OQW7ZRVC5N5B42)

10. From the **resource group** blade, navigate to the **az1010301b** Azure SQL Server blade. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/39.png?token=AIMANV7QLBPWIMBVFWNVJV25N5B5W)

11. From the Azure SQL Server blade, navigate to its server's **Firewalls and virtual networks** blade.

12. From the **Firewalls and virtual networks** blade of the Azure SQL Database server, configure the following settings:

    ```
     Allow access to Azure services: ON

     No firewall rules configured 

     Virtual networks:

         Name: az1010301b-vnet1

         Subscription: Select as default from the dropdown

         Virtual network: az1010301b-vnet1

         Subnet name: subnet0/ 10.203.0.0/24
    
    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/40.png?token=AIMANV67XTTX4ALHXDIHD7S5N5B6S)

**Result**: After you completed this exercise, you have deployed Azure VMs, an Azure Storage account, and an Azure SQL Database instance by using Azure Resource Manager templates, enabled Azure Network Watcher service, established global peering between Azure virtual networks, and established service endpoints to an Azure Storage account and Azure SQL Database instance.

## Exercise 2: Use Azure Network Watcher to monitor network connectivity
  
The main tasks for this exercise are as follows:

1. Test network connectivity to an Azure VM via virtual network peering by using Network Watcher

2. Test network connectivity to an Azure Storage account by using Network Watcher

3. Test network connectivity to an Azure SQL Database by using Network Watcher

### Task 1: Test network connectivity to an Azure VM via virtual network peering by using Network Watcher

1. In the Azure portal, navigate to the **Network Watcher** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/41.png?token=AIMANV5IDRVHMYD2TSPX6GK5N5B7I)

2. From the **Network Watcher** blade, navigate to the **Connection troubleshoot**.

3. On the **Network Watcher - Connection troubleshoot** blade, initiate a check with the following settings:

    ```
     Source: 

         Subscription: Select as default from the dropdown

         Resource group: {{ ResourceGroup }}

         Source type: Virtual machine

         Virtual machine: az1010301b-vm1

     Destination: Specify manually

         URI, FQDN or IPv4: 10.203.16.4
    ```
> **Note**: **10.203.16.4** is the private IP address of the second Azure VM az1010302b-vm1 which you deployed to another Azure region

```
     Probe Settings:

         Protocol: TCP

         Destination port: 3389

     Advanced settings:

         Source port: blank

```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/42.png?token=AIMANV3H6HPLBN6XLPXIG5C5N5CAA)

4. Wait until results of the connectivity check are returned and verify that the status is **Reachable**. Review the network path and note that the connection was direct, with no intermediate hops in between the VMs.

> **Note**: If this is the first time you are using Network Watcher, the check can take up to 5 minutes.

### Task 2: Test network connectivity to an Azure Storage account by using Network Watcher

1. From the Azure Portal, start a PowerShell session in the Cloud Shell. 

> **Note**: If this is the first time you are launching the Cloud Shell in the current Azure subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a storage account in an automatically generated resource group.

2. In the Cloud Shell pane, run the following command to identify the IP address of the blob service endpoint of the Azure Storage account you provisioned in the previous exercise:

```pwsh
[System.Net.Dns]::GetHostAddresses($(Get-AzStorageAccount -ResourceGroupName 'az1010301b-RG')[0].StorageAccountName + '.blob.core.windows.net').IPAddressToString
```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/43.png?token=AIMANV4APGILPCFS4LC5B725N5CA4)

3. Note the resulting string and, from the **Network Watcher - Connection troubleshoot** blade, initiate a check with the following settings:

    ```
     Source: 

         Subscription: Select as default from the dropdown

         Resource group: {{ ResourceGroup }}

         Source type: Virtual machine

         Virtual machine: az1010301b-vm1

     Destination: Specify manually

         URI, FQDN or IPv4: the IP address of the blob service endpoint of the storage account you identified in the previous step of this task

     Probe Settings:

         Protocol: TCP

         Destination port: 443

     Advanced settings:

         Source port: blank

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/44.png?token=AIMANV5VHM66SA3AGEOVG5S5N5CB2)

4. Wait until results of the connectivity check are returned and verify that the status is **Reachable**. Review the network path and note that the connection was direct, with no intermediate hops in between the VMs, with minimal latency. 

> **Note**: The connection takes place over the service endpoint you created in the previous exercise. To verify this, you will use the **Next hop** tool of Network Watcher.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/45.png?token=AIMANV6OGJI6TPCNC3YN4FK5N5CCQ)

5. From the **Network Watcher - Connection troubleshoot** blade, navigate to the **Network Watcher - Next hop** blade and test next hop with the following settings:

    ```
     Subscription: Select as default from the dropdown

     Resource group: {{ ResourceGroup }}

     Virtual machine: az1010301b-vm1

     Network interface: az1010301b-nic1

     Source IP address: 10.203.0.4

     Destination IP address: the IP address of the blob service endpoint of the storage account you identified earlier in this task

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/46.png?token=AIMANVYJZB4ED2RWMBF3UXS5N5CDI)

6. Verify that the result identifies the next hop type as **VirtualNetworkServiceEndpoint**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/47.png?token=AIMANV2J3IOKCTW57ROJ76C5N5CEQ)

7. From the **Network Watcher - Connection troubleshoot** blade, initiate a check with the following settings:

    ```
     Source: 

         Subscription: Select as default from the dropdown

         Resource group: {{ ResourceGroup }}

         Source type: Virtual machine

         Virtual machine: az1010302b-vm2

     Destination: Specify manually

         URI, FQDN or IPv4: the IP address of the blob service endpoint of the storage account you identified earlier in this task

     Probe Settings:

         Protocol: TCP

         Destination port: 443

      Advanced settings:

         Source port: blank
    
    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/48.png?token=AIMANVZNSFISCSI67IZ4EYK5N5CF4)

8. Wait until results of the connectivity check are returned and verify that the status is **Reachable**. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/49.png?token=AIMANV7Z72UEVDWT2427ITC5N5CGW)

> **Note**: The connection is successful, however it is established over Internet. To verify this, you will use again the **Next hop** tool of Network Watcher.

9. From the **Network Watcher - Connection troubleshoot** blade, navigate to the **Network Watcher - Next hop** blade and test next hop with the following settings:

    ```
     Subscription: Select as default from the dropdown

     Resource group: {{ ResourceGroup }}

     Virtual machine: az1010302b-vm2

     Network interface: az1010302b-nic1

     Source IP address: 10.203.16.4

     Destination IP address: the IP address of the blob service endpoint of the storage account you identified earlier in this task

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/50.png?token=AIMANV4FF5HJNCBH4RJ72JK5N5CHQ)

10. Verify that the result identifies the next hop type as **Internet**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/51.png?token=AIMANVZHJRAGEGH3FVNGYD25N5CII)

### Task 3: Test network connectivity to an Azure SQL Database by using Network Watcher

1. From the Azure Portal, start a PowerShell session in the Cloud Shell. 

2. In the Cloud Shell pane, run the following command to identify the IP address of the Azure SQL Database server you provisioned in the previous exercise:

```pwsh
[System.Net.Dns]::GetHostAddresses($(Get-AzSqlServer -ResourceGroupName 'az1010301b-RG')[0].FullyQualifiedDomainName).IPAddressToString
```
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/52.png?token=AIMANV3HAI7BAZAGFXCYBBC5N5CJW)

3. Note the resulting string and, from the **Network Watcher - Connection troubleshoot** blade, initiate a check with the following settings:

    ```
    Source: 

        Subscription: Select as default from the dropdown

        Resource group: {{ ResourceGroup }}

        Source type: Virtual machine

        Virtual machine: az1010301b-vm1

    Destination: Specify manually

        URI, FQDN or IPv4: the IP address of the Azure SQL Database server you identified in the previous step of this task

    Probe Settings:

        Protocol: TCP

        Destination port: 1433

    Advanced settings:

        Source port: blank

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/53.png?token=AIMANV7365PHBL7ITSVCTYS5N5CKY)

4. Wait until results of the connectivity check are returned and verify that the status is **Reachable**. Review the network path and note that the connection was direct, with no intermediate hops in between the VMs, with low latency. 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/54.png?token=AIMANVZ2GYOXKHSGODREPT25N5CLQ)

> **Note**: The connection takes place over the service endpoint you created in the previous exercise. To verify this, you will use the **Next hop** tool of Network Watcher.

5. From the **Network Watcher - Connection troubleshoot** blade, navigate to the **Network Watcher - Next hop** blade and test next hop with the following settings:

    ```
    Subscription: Select as default from the dropdown

    Resource group: {{ ResourceGroup }}

    Virtual machine: az1010301b-vm1

    Network interface: az1010301b-nic1

    Source IP address: 10.203.0.4

    Destination IP address: the IP address of the Azure SQL Database server you identified earlier in this task

    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/55.png?token=AIMANV2EUXICWBFZQMX5ES25N5CMK)

6. Verify that the result identifies the next hop type as **VirtualNetworkServiceEndpoint**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/56.png?token=AIMANVZ5X5RR7D5OOJSOC3S5N5CNC)

7. From the **Network Watcher - Connection troubleshoot** blade, initiate a check with the following settings:

    ```
    Source: 

        Subscription: select the default from the dropdown

        Resource group: {{ ResourceGroup }}

        Source type: Virtual machine

        Virtual machine: az1010302b-vm2

    Destination: Specify manually

        URI, FQDN or IPv4: the IP address of the Azure SQL Database server you identified earlier in this task

    Probe Settings:

        Protocol: TCP

        Destination port: 1433

    Advanced settings:

        Source port: blank
    
    ```

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/57.png?token=AIMANV25RORFZNUJUZ3KOAS5N5COW)

8. Wait until results of the connectivity check are returned and verify that the status is **Reachable**. 

> **Note**: The connection is successful, however it is established over Internet. To verify this, you will use again the **Next hop** tool of Network Watcher.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/58.png?token=AIMANV5PRRKO5Y5M552HIRS5N5CPQ)

9. From the **Network Watcher - Connection troubleshoot** blade, navigate to the **Network Watcher - Next hop** blade and test next hop with the following settings:

    ````
     Subscription: select the default from the dropdown

     Resource group: {{ ResourceGroup }}

     Virtual machine: az1010302b-vm2

     Network interface: az1010302b-nic1

     Source IP address: 10.203.16.4

     Destination IP address: the IP address of the Azure SQL Database server you identified earlier in this task
    
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/59.png?token=AIMANV4RUUTYT4A3PNNAZI25N5CQW)

10. Verify that the result identifies the next hop type as **Internet**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/Lab6/60.png?token=AIMANV7BR2MVJWOPUQ6IATS5N5CRO)

**Result**: After you completed this exercise, you have used Azure Network Watcher to test network connectivity to an Azure VM via virtual network peering, network connectivity to Azure Storage, and network connectivity to Azure SQL Database.

