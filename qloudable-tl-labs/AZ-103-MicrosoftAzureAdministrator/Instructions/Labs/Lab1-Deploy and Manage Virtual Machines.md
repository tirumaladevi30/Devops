# Deploy and Manage Virtual Machines

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Deploy Azure VMs by using the Azure Portal, Azure PowerShell and Azure Resource Manager Templates](#Exercise-1-deploy-azure-vms-by-using-the-azure-portal-azure-powershell-and-azure-resource-manager-templates)

[Exercise 2: Configure Networking Settings of Azure VMs running Windows and Linux Operating Systems](#Exercise-2-configure-networking-settings-of-azure-vms-running-windows-and-linux-operating-systems)

[Exercise 3: Deploy and Configure Azure VM Scale sets](#Exercise-3-deploy-and-configure-azure-vm-scale-sets)

## Overview

* The main Aim of the lab is deploying Azure VM running Windows Server 2016 Datacenter into an availability set by using the Azure Portal and deployed Azure VM running Windows Server 2016 Datacenter into the existing availability set by using Azure PowerShell and deployed two Azure VMs running Linux into availability set by using an Azure Resource Manager template.

* Configured static Private and public IP Addresses of Azure VMs and connected to Azure VM running Windows Server 2016 Datacenter via public IP Address and connected to Azure VM running Linux Ubuntu Server via Private IP Address.

* Deploy Azure VM scale set and identify available DNS name for an Azure VM scale set and install IIS on a scale set VM by using DSC extensions.

## Pre-requisites

* Powershell
* RDP
* Familiar with ARM Template
* Familiar with Virtual Machine Scale Set

### Scenario
  
XYZ wants to implement its workloads by using Azure Virtual Machines (VMs) and Azure VM scale sets

After completing this lab, you will be able to:

  *  Deploy Azure VMs by using the Azure Portal, Azure PowerShell and Azure Resource Manager Templates

  *  Configure Networking Settings of Azure VMs running Windows and Linux Operating Systems
  
  *  Deploy and Configure Azure VM Scale sets
  
All tasks in this lab are performed from the Azure Portal (including a PowerShell Cloud Shell session) except for Excercise 2 Task 2 and Exercise 2 Task 3, which include steps performed from a Remote Desktop session to an Azure VM

**Note:** *When not using Cloud Shell, the lab Virtual Machine must have Azure PowerShell module installed* https://docs.microsoft.com/en-us/powershell/azure/install-Az-ps

## Exercise 1: Deploy Azure VMs by using the Azure Portal, Azure PowerShell and Azure Resource Manager Templates

Using the Chrome browser, login into Azure Portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/1.png?st=2019-09-16T06%3A39%3A38Z&se=2022-09-17T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jn2W2yDOGMtqhslUkBXNxhtdT%2B%2Be46%2FmWJz9apG5jOw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/2.png?st=2019-09-16T06%3A40%3A26Z&se=2022-09-17T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QetzTN6vAeud3W%2FF368TLsYldMwuItXWZ9YPHcBIAcY%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/3.png?st=2019-09-16T06%3A41%3A11Z&se=2022-09-17T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5sSgDMmG91XKv4GEHqa7x0GaphcJPrDNSM6ld%2Bp5oY4%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/4.png?st=2019-09-16T06%3A41%3A34Z&se=2022-09-17T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zBrwR6bjNejcL5y9Q9tTs4diwR7F9sPYi4KZvOdj470%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a37.PNG?st=2019-09-18T04%3A35%3A02Z&se=2020-09-19T04%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ki4Pe5TN1s43k%2FM4C9Out1sJXU3CGPQJtjMHU3FE7ik%3D)


**Azure VM**

A Virtual Machine is a computer file, typically called an image, which behaves like an actual computer. In other words, creating a computer within a computer. It runs in a window, much like any other programme, giving the end user the same experience on a Virtual Machine as they would have on the host operating system itself. The Virtual Machine is sandboxed from the rest of the system, meaning that the software inside a Virtual Machine cannot escape or tamper with the computer itself. This produces an ideal environment for testing other Operating Systems including beta releases, accessing virus-infected data, creating operating system backups and running software or applications on Operating Systems for which they were not originally intended.
  
The main tasks for this Exercise are as follows:

1. Deploy an Azure VM running Windows Server 2016 Datacenter into an availability set by using the Azure portal.

2. Deploy an Azure VM running Windows Server 2016 Datacenter into the existing availability set by using Azure PowerShell.

3. Deploy two Azure VMs running Linux into an availability set by using an Azure Resource Manager template.


### Task 1: Deploy an Azure VM running Windows Server 2016 Datacenter into an availability set by using the Azure Portal

2. In the Azure Portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/6.png?st=2019-09-16T06%3A43%3A05Z&se=2022-09-17T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PP1huHBKKRQdyVkHCjB2AJFDkPIUGionZb0PVKtnNnc%3D) 

3. From the **Create a resource** blade, search Azure Marketplace for **Windows Server**. Select **Windows Server** from the search results list.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/7.png?st=2019-09-16T06%3A43%3A37Z&se=2022-09-17T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iaixa4djzdjExKTGUlF%2Ft62%2BPo1kv3cYAt7Iydh3zp4%3D) 

4. On the Windows Server page, use the drop-down menu to select **[smalldisk] Windows Server 2016 Datacenter**, and then click **Create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/8.png?st=2019-09-16T06%3A44%3A12Z&se=2022-09-17T06%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=L1Bqwj%2Fj8DlW%2BTF3br%2FA6xqx%2FaVFQcHIQRsQnmvom%2F0%3D) 

5. Use the **Create a Virtual Machine** blade to deploy a Virtual Machine with the following settings:

* **Subscription:** `Select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Virtual Machine name:** `az1000301-vm0` <br>
* **Region:** `{{location}}` <br>
* **Availability options:** `Availability set` <br>
* **Availability set:** Click `Create New`, and name the new availability set az1000301-avset0 with 2 fault domains and 5 update domains. Click OK. <br>
* **Image:** `[smalldisk] Windows Server 2016 Datacenter` <br>
* **Size:** `Standard DS1_v2` <br>
* **Username:** `Student` <br>
* **Password:** `Password@1234` <br>
* **Confirm Password:** `Password@1234` <br>
* **Public inbound ports:** `None` <br>
* **Already have a Windows license?:** `No` 
     
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/9.png?st=2019-09-16T06%3A45%3A44Z&se=2022-09-17T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HvUh%2B0sk84daPyJRa2Z4usPRmW3sgQvl2LMQb7284g0%3D) 
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/10.png?st=2019-09-16T06%3A46%3A32Z&se=2022-09-17T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rciUwh%2FuZrpknGDUhnRorz4z1JZyEkorYgQ4PS4Ec2c%3D) 
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a38.PNG?st=2019-09-18T04%3A48%3A38Z&se=2022-09-19T04%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FjrfNfFqy9DxjKv8I%2BFNgLLGm6S7PpM%2Fu7BGnnTQeqc%3D) 
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/12.png?st=2019-09-16T06%3A47%3A26Z&se=2022-09-17T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fOzUT8%2BK8glbndcUx5ruc1knikztI0s6jhcs9c2pWHA%3D) 

6. Click **Next : Disks >**.

  ```

   OS disk type: Standard HDD
   
   ```
  
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a39.PNG?st=2019-09-18T04%3A52%3A26Z&se=2022-09-19T04%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xsdKp3RYTq9h26ktXckdhbJBICd1kO7d8rV4ZKLLAWg%3D) 


7. Click **Next : Networking >**.

8. On the Networking tab, click **Create new** under Virtual Network. Use the virtual network name already assigned by default and specify the following:

```

   Virtual network Address range: 10.103.0.0/16

   Subnet name: subnet0

   Subnet Address range: 10.103.0.0/24
   
   ```
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/14.png?st=2019-09-16T06%3A48%3A55Z&se=2022-09-17T06%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aU0ExIzWDOhfAUXgRSeKHsKtWvojN%2BH%2BqJbcxD86Xn4%3D) 

 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/15.png?st=2019-09-16T06%3A49%3A15Z&se=2022-09-17T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J14HU7IoXlzaWpDakbHs1iICnto0fEhHYNs9%2BMMX8hI%3D) 


9. Click **OK**.

10. Leave all other default values, and click **Review + create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/16.png?st=2019-09-16T06%3A50%3A09Z&se=2022-09-17T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t3zKzLtyIOnYXWYlul%2B6DOngQhGodK0HZ40XVDLQ8lk%3D)

11. Click **Create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/17.png?st=2019-09-16T06%3A50%3A29Z&se=2022-09-17T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KiNT7gQpsVrJkD4n4U6wlolx%2BgQpbjLsRnf2IKAQDWI%3D)

   **Note**: *You will configure the network security group you create in this task in the second Exercise of this lab*

   **Note**: *Wait for the deployment to complete before you proceed to the next task. This should take about 5 minutes*.


### Task 2: Deploy an Azure VM running Windows Server 2016 Datacenter into the existing availability set by using Azure PowerShell

**PowerShell**

*	PowerShell is a task-based command-line shell and scripting language built on .NET. PowerShell helps system administrators and power-users rapidly automate tasks that manage Operating Systems (Linux, macOS, and Windows) and processes.

*	PowerShell commands let you manage computers from the command line. PowerShell providers let you access data stores, such as the registry and certificate store, as easily as you access the file system. PowerShell includes a rich expression parser and a fully developed scripting language.

1. From the Azure Portal, start a PowerShell session in the Cloud Shell pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/18.png?st=2019-09-16T06%3A56%3A43Z&se=2022-09-17T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=847NFTW3Z2mlgo%2FGqyWi%2BuRhShvBLUrO95HPTorQ7QA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/19.png?st=2019-09-16T06%3A57%3A14Z&se=2022-09-17T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UoWgW4qVa8tZZBz7ss%2FwqcJnLZDsX0ANpXF0WS6yEvc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a40.png?st=2019-09-18T04%3A55%3A48Z&se=2022-09-19T04%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ptbWzZ%2F1V4AzJ0Nc%2FNLNEahWl6fqV%2BMblYXJo7vE9NY%3D)


* **Resource group:** `{{resource-group-name}}` <br>

* **Storage Account Name:** `Create new Storage` <br>

* **File Share Name:** `Create new file share`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a41.PNG?st=2019-09-18T04%3A58%3A12Z&se=2022-09-19T04%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zQJmfYNONwPRTvZ3mdfA6ZtkxKIjh%2FCTdGu9oNPOe%2FE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/21.png?st=2019-09-16T06%3A57%3A56Z&se=2022-09-17T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JMFKFtYFry1nNVFUWtQOewXhh1ZDMSXBuR%2BXc4szLxk%3D)

   **Note**: *If this is the first time you are launching the Cloud Shell in the current Azure subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a Storage Account in an automatically generated resource group.*

2. In the Cloud Shell pane, run the following command:

   ```
   
   $vmName = 'az1000301-vm1'
   
   $vmSize = 'Standard_DS1_v2'
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/22.png?st=2019-09-16T06%3A59%3A10Z&se=2022-09-17T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ce2DM7xXt0cNulmI7Q9gXRL%2BCOoD8Yw6NDPc8snbXE0%3D)

    **Note**: *This sets the values of variables designating the Azure VM name and its size*

3. In the Cloud Shell pane, run the following commands:

 $resourceGroup = Get-AzResourceGroup -Name '{{resource-group-name}}'
   
 $location = $resourceGroup.Location
   
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/23.png?st=2019-09-16T06%3A59%3A33Z&se=2022-09-17T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3WvRLGRybiitvhaSKIgRc3fNVOSN0AOkHQGVYWwR33I%3D)

**Note**: These commands set the values of variables designating the target resource group and its location

4 In the Cloud Shell pane, run the following commands:

**Replace with ResourceGroup Name**

   $availabilitySet = Get-AzAvailabilitySet -ResourceGroupName $resourceGroup.ResourceGroupName -Name 'az1000301-avset0'
   
   $vnet = Get-AzVirtualNetwork -Name '{{resource-group-name}}-vnet' -ResourceGroupName $resourceGroup.ResourceGroupName
   
   $subnetid = (Get-AzVirtualNetworkSubnetConfig -Name 'subnet0' -VirtualNetwork $vnet).Id
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/24.png?st=2019-09-16T06%3A59%3A56Z&se=2022-09-17T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Q6e%2BBw8q%2BrfS6BVMfjIzrx7v88tCauH92GrX3CLbnps%3D)

**Note**: *These commands set the values of variables designating the availability set, virtual network, and subnet into which you will deploy the new Azure VM*

5. In the Cloud Shell pane, run the following commands:

   ``` 
   $nsg = New-AzNetworkSecurityGroup -ResourceGroupName $resourceGroup.ResourceGroupName -Location $location -Name "$vmName-nsg"
   
   $pip = New-AzPublicIpAddress -Name "$vmName-ip" -ResourceGroupName $resourceGroup.ResourceGroupName -Location $location -AllocationMethod Dynamic 
   
   $nic = New-AzNetworkInterface -Name "$($vmName)$(Get-Random)" -ResourceGroupName $resourceGroup.ResourceGroupName -Location $location -SubnetId $subnetid -PublicIpAddressId 
   $pip.Id -NetworkSecurityGroupId $nsg.Id
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/25.png?st=2019-09-16T07%3A00%3A22Z&se=2022-09-17T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Y%2FAZIkuBcA4vpGNoBm7xTbO8ZIgvqG98X4ZepQSk8H0%3D)

   **Note**: *These commands create a new network security group, public IP Address, and network interface that will be used by the new Azure VM*

   **Note**: *You will configure the network security group you create in this task in the second Exercise of this lab*

6. In the Cloud Shell pane, run the following commands:

   ```
   
   $adminUsername = 'Student'
   
   $adminPassword = 'Password@1234'
   
   $adminCreds = New-Object PSCredential $adminUsername, ($adminPassword | ConvertTo-SecureString -AsPlainText -Force)
   
   ```
   
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/26.png?st=2019-09-16T07%3A00%3A58Z&se=2022-09-17T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3bpLWXtcRSZFqppxFZ2CLQZ%2FHJF203a%2BVDMoMDsbDgA%3D)

**Note**: *These commands set the values of variables designating credentials of the local Administrator Account of the new Azure VM*

7. In the Cloud Shell pane, run the following commands:

   ```
   
   $publisherName = 'MicrosoftWindowsServer'
   
   $offerName = 'WindowsServer'
   
   $skuName = '2016-Datacenter'
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/27.png?st=2019-09-16T07%3A01%3A21Z&se=2022-09-17T07%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZgCAwD4Fb4KyDVJ2Qhr4%2FQZfWmG4oF8rgCBfUhBt1oY%3D)

   **Note**: *These commands set the values of variables designating the properties of the Azure Marketplace image that will be used to provision the new Azure VM*

8. In the Cloud Shell pane, run the following command:

   ```
   
   $osDiskType = (Get-AzDisk -ResourceGroupName $resourceGroup.ResourceGroupName)[0].Sku.Name
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/28.png?st=2019-09-16T07%3A01%3A43Z&se=2022-09-17T07%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1SBeuTxP%2FoHoBxtOOM%2FyvQYaJOpQjQqsgVwYl%2FXN6NY%3D)

   **Note**: *This command sets the values of a variable designating the operating system disk type of the new Azure VM*

9. In the Cloud Shell pane, run the following commands:

   ```
   
   $vmConfig = New-AzVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $availabilitySet.Id
   
   Add-AzVMNetworkInterface -VM $vmConfig -Id $nic.Id
   
   Set-AzVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $adminCreds 
   
   Set-AzVMSourceImage -VM $vmConfig -PublisherName $publisherName -Offer $offerName -Skus $skuName -Version 'latest'
   
   Set-AzVMOSDisk -VM $vmConfig -Name "$($vmName)_OsDisk_1_$(Get-Random)" -StorageAccountType $osDiskType -CreateOption fromImage
   
   Set-AzVMBootDiagnostic -VM $vmConfig -Disable
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/29.png?st=2019-09-16T07%3A03%3A31Z&se=2022-09-17T07%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=O7gWbHg2f6GHvMDPv2r79QGHvoqqv5PiYcGAscrt6RY%3D)
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/30.png?st=2019-09-16T07%3A03%3A52Z&se=2022-09-17T07%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HD5ftE%2FMkW57KaNnsoR%2FgnnI7uRLkvOCeIoXTbvX4q4%3D)
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/31.png?st=2019-09-16T07%3A04%3A15Z&se=2022-09-17T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tDEua9PZKp01iPHjNpOsssAqUcZ%2BXseIXxl4b2Wk3vI%3D)
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/32.png?st=2019-09-16T07%3A04%3A39Z&se=2022-09-17T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UtpaoCuDBO4viCARElveQMgkjNle1bewMYVqSKct4bM%3D)
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/33.png?st=2019-09-16T07%3A04%3A59Z&se=2022-09-17T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c0WKsc0dD9wXB0hNo%2BeqXEV2G6JOHv1kEIpxiHAtsPg%3D)
   
   

   **Note**: *These commands set up the properties of the Azure VM configuration object that will be used to provision the new Azure VM, including the VM size, its availability set, network interface, computer name, local Administrator credentials, the source image, the operating system disk, and boot diagnostics settings.*

10. In the Cloud Shell pane, run the following command:

   ```
   
   New-AzVM -ResourceGroupName $resourceGroup.ResourceGroupName -Location $location -VM $vmConfig
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/34.png?st=2019-09-16T07%3A05%3A24Z&se=2022-09-17T07%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=33i05IhvNe2GTl6sCqRoFodVZQ%2BtOUdxT9VJ5Pkr7ig%3D)

   **Note**: *This command initiates deployment of the new Azure VM*

   **Note**: *Do not wait for the deployment to complete but instead proceed to the next task.*


### Task 3: Deploy two Azure VMs running Linux into an availability set by using an Azure Resource Manager template

**ARM Template**

*	Successful Cloud Administrators start this role with experience on Operating Systems, Virtualization, Cloud Infrastructure, Storage structures, and Networking.

1. In the Azure Portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/35.png?st=2019-09-16T07%3A11%3A23Z&se=2022-09-17T07%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tblq7OFPF3iSDL6jWp8zU%2BviQaL%2Be4Qj6%2FAtKcUB23w%3D)

2. From the **Create a resource** blade, search Azure Marketplace for **Template deployment**, and select **Template deployment (deploy using custom templates)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/36.png?st=2019-09-16T07%3A12%3A21Z&se=2022-09-17T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8PHjHJrXbxguyG7K8U5JLCKOz%2FeT71bGArkk8VMjSWw%3D)

3. Click **Create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/37.png?st=2019-09-16T07%3A12%3A43Z&se=2022-09-17T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VSjX%2BHA5ypm3n62SxEM0jlifvXxwOIVz2uFKVOcbJtc%3D)

4. On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit Template** instead.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/38.png?st=2019-09-16T07%3A13%3A07Z&se=2022-09-17T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kz7en7IQWcLB43Kj7S4ZHkXR1ZTG6lLXfj%2FYLtLcOCY%3D)

5. From the Edit template blade, Click on the below link and load the template file.

**Note: Delete the default data.**

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Deploy_and_Manage_Virtual_Machines/az-100-03_azuredeploy.json?st=2019-09-18T05%3A09%3A21Z&se=2022-09-19T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LadpOVi8uz8IKJGsjpa0o9pBK7sY%2FskEqf0YcGs0oro%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/39.png?st=2019-09-16T07%3A13%3A31Z&se=2022-09-17T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YYWAPwC1d%2BwHMNg9ZphB4WocvJIpbnmDnhae%2F8udLr8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/40.png?st=2019-09-16T07%3A14%3A53Z&se=2022-09-17T07%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kpIRCjEmdyu6eJZW7kHqHmIsiQrruCuQ5tNKW9fOldc%3D)

   **Note**: *Review the content of the template and note that it defines deployment of two Azure VMs hosting Linux Ubuntu into an availability set and into the existing virtual network **az1000301-vnet0**. This virtual network does not exist in your deployment. You will be changing the virtual network name in the parameters below.*

6. Save the template and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/41.png?st=2019-09-16T07%3A16%3A38Z&se=2022-09-17T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d9az1nacjXs4h3v7FrJJjD5Eg5RBdejxqlsVlIGOKNE%3D)

7. From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/42.png?st=2019-09-16T07%3A16%3A59Z&se=2022-09-17T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=crvXiFlg90ryw8PtFYulkn2md9Dbmp5C4BEV1ZXNsaI%3D)

8. From the Edit template blade, Click on the below link and load the template file.

   **Note: Delete the default data.**
   
   https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Deploy_and_Manage_Virtual_Machines/az-100-03_azuredeploy.parameters.json?st=2019-09-18T05%3A12%3A59Z&se=2022-09-19T05%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UXqWFz39a8L%2BUgnXAfFo1LwsistfEA%2BKM5SEp8p1enE%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/43.png?st=2019-09-16T07%3A17%3A18Z&se=2022-09-17T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=av4k6NoJ%2BPEJYF9VGR6dbEqQP%2BZqYx7VeMiOLAp3KA4%3D)

9. Save the parameters and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/44.png?st=2019-09-16T07%3A17%3A38Z&se=2022-09-17T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bd8hH7XpXUdGHOjlHGxi5wkui7gEUdZgnn%2BVAr3R4%2Fs%3D)

10. From the **Custom deployment** blade, initiate a template deployment with the following settings:

* **Subscription:** `Select the default`
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vm Name Prefix:** `az1000302-vm`
* **Nic Name Prefix:** `az1000302-nic`
* **Pip Name Prefix:** `az1000302-ip`
* **Admin Username:** `Student`
* **Admin Password:** `Password@1234`
* **Virtual Network Name:** `{{resource-group-name}}-vnet` (change this value from the template default)
* **Image Publisher:** `Canonical`
* **Image Offer:** `UbuntuServer`
* **Image SKU:** `16.04.0-LTS`
* **Vm Size:** `Standard_DS1_v2`
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/45.png?st=2019-09-16T07%3A18%3A00Z&se=2022-09-17T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1v3tYEWgiqky3nJ9U46AjlNbrzvsjCyXbeZwxW3eAIc%3D)
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/46.png?st=2019-09-16T07%3A18%3A20Z&se=2022-09-17T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oR%2Fhbgf9IhmNWVLcOmrLKtY57lZ3bYyyDu%2Byc7fstyc%3D)

**Note**: *Wait for the deployment to complete before you proceed to the next task. This should take about 5 minutes.*
   
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/47.png?st=2019-09-16T07%3A18%3A40Z&se=2022-09-17T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yjrtE3kgVb9kFDJEoVpIyDFeqJU45witTIkdg4KJcaU%3D)

**Result**: After you completed this Exercise, you have deployed an Azure VM running Windows Server 2016 Datacenter into an availability set by using the Azure Portal, deployed another Azure VM running Windows Server 2016 Datacenter into the same availability set by using Azure PowerShell, and deployed two Azure VMs running Linux Ubuntu into an availability set by using an Azure Resource Manager template.

**Note**: *You could certainly use a template to deploy two Azure VMs hosting Windows Server 2016 datacenter in a single task (just as this was done with two Azure VMs hosting Linux Ubuntu server). The reason for deploying these Azure VMs in two separate tasks was to give you the opportunity to become familiar with both the Azure Portal and Azure PowerShell-based deployments.*

## Exercise 2: Configure Networking Settings of Azure VMs running Windows and Linux Operating Systems
  
The main tasks for this Exercise are as follows:

1. Configure Static Private and Public IP Addresses of Azure VMs

2. Connect to an Azure VM running Windows Server 2016 Datacenter via a public IP Address

3. Connect to an Azure VM running Linux Ubuntu Server via a Private IP Address

### Task 1: Configure Static Private and Public IP Addresses of Azure VMs

1. In the Azure Portal, Navigate to the **ResourceGroup** then click on the **ResourceGroup** and navigate to the **az1000301-vm0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/48.png?st=2019-09-16T07%3A24%3A08Z&se=2022-09-17T07%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uYsF0u%2FKW8YcQuqlj7y1DXWefQf%2FJ90cr%2BOQ%2BwN3Kok%3D)

2. From the **az1000301-vm0** blade, navigate to the **Networking** blade, displaying the configuration of the public IP Address **az1000301-vm0-ip**, assigned to its network interface.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/49.png?st=2019-09-16T07%3A24%3A32Z&se=2022-09-17T07%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sSwAzJ%2Bt5PUWDkY8R0GJe2jtbnfi1N%2FAWOsBpTBoL04%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/50.png?st=2019-09-16T07%3A24%3A53Z&se=2022-09-17T07%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QDpI0OA2rkAy%2FYjFXYHDuWlMuUA0MWNGWR3bqPYqr50%3D)

3. From the **Networking** blade, click the link representing the public IP Address.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/51.png?st=2019-09-16T07%3A25%3A13Z&se=2022-09-17T07%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pdjB4s9GLO%2BBB46kpRAK%2FX5RUMydbBpK4%2BIBfTsnULg%3D)

4. On the az1000301-vm0-ip blade, click **Configuration**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/52.png?st=2019-09-16T07%3A25%3A34Z&se=2022-09-17T07%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2r6DtMa3QetjaarhvL0YbEqRhlu1TMiJx4Mc3GV%2Bwrs%3D)

5. Change the assignment of the public IP Address to **Static**, and then click **Save**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/53.png?st=2019-09-16T07%3A25%3A53Z&se=2022-09-17T07%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8S6oWnjaC%2Fz%2BKQBhHwZln8EIjBziHbk%2FZZqH1%2F2rUVs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/54.png?st=2019-09-16T07%3A26%3A12Z&se=2022-09-17T07%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5arQK5ZcEFUs1AhMqOw9D0RAOiPupHlv58qgcJ1hK0o%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/55.png?st=2019-09-16T07%3A26%3A30Z&se=2022-09-17T07%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GkWkXwGQzS1Yc214cziujlsQycJlsM6Cu6DZEHyqMRw%3D)

**Note**: *Take a note of the public IP Address assigned to the network interface of **az1000301-vm0**. You will need it later in this Exercise.*

6. In the Azure Portal, navigate to the **az1000302-vm0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/56.png?st=2019-09-16T08%3A33%3A14Z&se=2022-09-17T08%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FGxhwkRnBm0hhZzUcq9uvVt%2B1ecCtqyPbmQrHmTrjME%3D)

7. From the **az1000302-vm0** blade, display the **Networking** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/57.png?st=2019-09-16T08%3A34%3A09Z&se=2022-09-17T08%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vwVFnW5BVe7NDlyKYa70tKuXLVFI1LpIOFQTAGngxDw%3D)

8. From the **az1000302-vm0 - Networking** blade, click the link representing the network interface.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/58.png?st=2019-09-16T08%3A34%3A39Z&se=2022-09-17T08%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=drZ7VTEXI7rXoecVnJoXoWricvKaufY6nvxGPfz0jJk%3D)

9. From the blade displaying the properties of the network interface of **az1000302-vm0**, navigate to its **IP configurations** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/59.png?st=2019-09-16T08%3A35%3A03Z&se=2022-09-17T08%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=u38k%2BeElNdIptYfXz1LV9zRXX%2FiV1np36fv%2FRYqBMmw%3D)

10. On the **IP configurations** blade, configure the **ipconfig1** Private IP Address to be static and set it to **Private Ip**, and then click **Save**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/60.png?st=2019-09-16T08%3A35%3A26Z&se=2022-09-17T08%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FMey8HT2LTiOuQVu3cMx9l61vojj4CtK9u2mmRxzsAM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/61.png?st=2019-09-16T08%3A35%3A47Z&se=2022-09-17T08%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ndXG%2BGRIGNU6OCqTdZxw3dnkDB9%2BGxt9Q%2FggNGYwNCQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/62.png?st=2019-09-16T08%3A36%3A22Z&se=2022-09-17T08%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C0p%2FpxNZgxH1SNwRcVE1suDS1lFMQg6QM2RbmztZQUY%3D)

**Note**: *Changing the Private IP Address assignment requires restarting the Azure VM.*

**Note**: *It is possible to connect to Azure VMs via either statically or dynamically assigned public and Private IP Addresses. Choosing static IP assignment is commonly done in scenarios where these IP Addresses are used in combination with IP filtering, routing, or if they are assigned to network interfaces of Azure VMs that function as DNS servers.*


### Task 2: Connect to an Azure VM running Windows Server 2016 Datacenter via a public IP Address

1. In the Azure Portal, navigate to the **az1000301-vm0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/63.png?st=2019-09-16T08%3A42%3A27Z&se=2022-09-17T08%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Dtk5Gq9egBcNA3%2FGDj952Y9ifQZ%2FtdAJ52wMWHRl9g0%3D)

2. From the **az1000301-vm0** blade, navigate to the **Networking** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/64.png?st=2019-09-16T08%3A42%3A53Z&se=2022-09-17T08%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=j7Y44TVyRTb6HRCZZrCCC5%2FfsqrH0hmjrlNIezRjD0A%3D)

3. On the **az1000301-vm0 - Networking** blade, review the inbound port rules of the network security group assigned to the network interface of **az1000301-vm0**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/65.png?st=2019-09-16T08%3A43%3A52Z&se=2022-09-17T08%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mUf5QKOifq1LNcpiLXnDpEEslrVlMgO2J44hSFfiZ%2Bo%3D)

   **Note**: *The default configuration consisting of built-in rules block inbound connections from the internet (including connections via the RDP port TCP 3389)*

4. Add an inbound security rule to the existing network security group with the following settings:

```

   Source: Any

   Source port ranges: *

   Destination: Any

   Destination port ranges: 3389

   Protocol: TCP

   Action: Allow

   Priority: 100

   Name: AllowInternetRDPInBound
   
   ```
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/66.png?st=2019-09-16T08%3A46%3A31Z&se=2022-09-17T08%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ohjy6T%2FvINNvrG8AK00CTj7%2FOCIPun0lEpJL295M0wU%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/67.png?st=2019-09-16T08%3A47%3A16Z&se=2022-09-17T08%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=U3ileXOMHbahbYMNyOsLSxztRXuyLAHs131USI9UBYc%3D)

5. In the Azure Portal, display the **Overview** pane of the **az1000301-vm0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/68.png?st=2019-09-16T08%3A47%3A44Z&se=2022-09-17T08%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MszuDDcW6%2FWqEakseYPU3gwz2cFN857zItOQwonojDs%3D)

6. From the **Overview** pane of the **az1000301-vm0** blade, click **Connect** and generate an RDP file and use it to connect to **az1000301-vm0**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/69.png?st=2019-09-16T08%3A48%3A24Z&se=2022-09-17T08%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mP7XHA58sqy4xfZdtvgoLiywzft1KO2NH8rZHGdwymw%3D)

7. When prompted, authenticate by specifying the following credentials:

```

   User name: Student

   Password: Password@1234
   
   ```
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/70.png?st=2019-09-16T08%3A48%3A50Z&se=2022-09-17T08%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XHBCJ7ZO9iEZ4%2BQiKtGrBO86QlXNoaIErWATQ7CS54w%3D)
  
  8. Double click on the downloaded zip and save it then connect to the RDP session. 
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/71.png?st=2019-09-16T08%3A49%3A14Z&se=2022-09-17T08%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QMETEdparwQ3mm6Q1bH6b0TziaVGoXakho1km9jqWJI%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/72.png?st=2019-09-16T08%3A49%3A40Z&se=2022-09-17T08%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Yf3DvMhMFYo8CO3z69Z2vx6uOO8YIyw%2BDhJtwqbOrlg%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/73.png?st=2019-09-16T08%3A50%3A01Z&se=2022-09-17T08%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FmwbSMdPUH4%2Bp8ahxBIkuQyk7BCBAfRLMPAtmtyIoJA%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/74.png?st=2019-09-16T08%3A50%3A22Z&se=2022-09-17T08%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mIpD79ORD8TFRzYwvrcnM46U7I8MvPbk18AuZKpmUKs%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/75.png?st=2019-09-16T08%3A50%3A44Z&se=2022-09-17T08%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ATi8c9sgIdvC0kEINhTUknGvac7BIxPjA1N3ap0MRsc%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/76.png?st=2019-09-16T08%3A51%3A03Z&se=2022-09-17T08%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mrmsnbr7%2FDU4dMcd3%2FaqfgYUliEoL0mk6%2B5DbZIPrtM%3D)
  

### Task 3: Connect to an Azure VM running Linux Ubuntu Server via a Private IP Address

**Remote Desktop**

*	Remote desktop is a program or an operating system feature that allows a user to connect to a computer in another location, see that computer's desktop and interact with it as if it were local.

*	People use remote desktop access capabilities to do a variety of things, including the following:

*	Access a workplace computer from home or when traveling.

*	Access a home computer from other locations.

*	Fix a computer problem.

*	Perform administrative tasks.

*	Demonstrate  a process or a software application
 
1. Within the RDP session to **az1000301-vm0**, start **Command Prompt**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/77.png?st=2019-09-16T08%3A55%3A56Z&se=2022-09-17T08%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=x27U4rbUUuroAWlwTj6%2F0dMhJC%2FT1vSiVLTmAL2mdF8%3D)

2. From the Command Prompt, run the following:

   ```
   nslookup az1000302-vm0
   
   ```
   
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a43.png?st=2019-09-18T05%3A41%3A47Z&se=2022-09-19T05%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=G2A6Zn5xLgCQWruh2yQ%2Fq7ctkTuKxRVNdU1pk98uPug%3D)

3. Examine the output and note that the name resolves to the IP Address you assigned in the first task of this Exercise (**10.103.0.100**).

   **Note**: *This is expected. Azure provides built-in DNS name resolution within a virtual network.*

4. Within the RDP session to **az1000301-vm0**, from Server Manager, click **Local Server**, then disable **IE Enhanced Security Configuration**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/79.png?st=2019-09-16T08%3A56%3A39Z&se=2022-09-17T08%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=e2fejUYC%2FQXzhyaukBHbxIvkwdWRLejiuU2IHDWmhk4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/80.png?st=2019-09-16T08%3A57%3A00Z&se=2022-09-17T08%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E%2FdEKrgMXPlD3XHLBZiT4o1STZAIjbky%2BBHP%2FaaIPJc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/81.png?st=2019-09-16T08%3A57%3A21Z&se=2022-09-17T08%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Y85v94lszg61wBUpv%2BIoELi65pH2INE53HWYW6GzApk%3D)


5. Within the RDP session to **az1000301-vm0**, start Internet Explorer and download **putty.exe** from [**https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html**](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a42.png?st=2019-09-18T05%3A35%3A14Z&se=2022-09-19T05%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nv2B1WGieLAB%2BE4Dv4NrkUHUo0EG4BzoCYlC%2BxZZtFg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/83.png?st=2019-09-16T08%3A58%3A01Z&se=2022-09-17T08%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Hza685V0JtTKS7Y2Wi9HggZQRmJqEMes%2FUVtpvtSVbE%3D)

6. Use **putty.exe** to verify that you can successfully connect to **az1000302-vm0** on its Private IP Address via the **SSH** protocol (TCP 22). or you can take Private Ip Address from this task in 2nd point.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/84.png?st=2019-09-16T09%3A00%3A08Z&se=2022-09-17T09%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0UO%2FY9yQJQ%2BuDa3RM6oRYct788%2FKcrL0LZeb1oRIJXo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/85.png?st=2019-09-16T09%3A00%3A38Z&se=2022-09-17T09%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=I33B%2FEjDlXQ5ZKpxT240E7rrrtTwD7bXlWI5QEbG%2Feg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a44.png?st=2019-09-18T05%3A44%3A22Z&se=2022-09-19T05%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mMe5Bfr7RYcsrJc0zaD5%2Fds9fjUeb0eHnA7A9YtoctY%3D)

7. When prompted, authenticate by specifying the following values:

```

    User name: Student

    Password: Password@1234
    
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/87.png?st=2019-09-16T09%3A01%3A33Z&se=2022-09-17T09%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w2fov%2F%2F%2B6u0R%2BL1Cia36YIBlJcNJSTq%2Bmxk65rHBhmU%3D)

   **Note**: *Both the username and password are case sensitive.*
 
8. Once you successfully authenticated, terminate the RDP session to **az1000301-vm0**.

9. On the lab Virtual Machine, in the Azure Portal, navigate to the **az1000302-vm0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/88.png?st=2019-09-16T09%3A01%3A57Z&se=2022-09-17T09%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BW9D9ethMRYG%2BY%2FJRdN5sDYQRqlN%2FONK9TxzflBqvig%3D)

10. From the **az1000302-vm0** blade, navigate to the **Networking** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/89.png?st=2019-09-16T09%3A02%3A32Z&se=2022-09-17T09%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0vjiQSyKMxy5HP6GVR4LVYB1RetzY8g20PY9J38lWyw%3D)

11. On the **az1000302-vm0 - Networking** blade, review the inbound port rules of the network security group assigned to the network interface of **az1000301-vm0** to determine why your SSH connection via the Private IP Address was successsful.

   **Note**: *The default configuration consisting of built-in rules allows inbound connections within the Azure virtual network environment (including connections via the SSH port TCP 22).*

**Result**: After you completed this Exercise, you have configured static Private and public IP Addresses of Azure VMs, connected to an Azure VM running Windows Server 2016 Datacenter via a public IP Address, and connect to an Azure VM running Linux Ubuntu Server via a Private IP Address


## Exercise 3: Deploy and Configure Azure VM Scale Sets

The main tasks for this Exercise are as follows:

1. Identify an available DNS name for an Azure VM scale set deployment

2. Deploy an Azure VM Scale Set

3. Install IIS on a Scale Set VM by using DSC extensions

### Task 1: Identify an available DNS name for an Azure VM Scale Set deployment

1. From the Azure Portal, start a PowerShell session in the Cloud Shell pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/90.png?st=2019-09-16T09%3A05%3A11Z&se=2022-09-17T09%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Qz25qasdznjAnK4OwtM1BdUn6IG4%2FUi6S0XVo1Iy8RA%3D)

2. In the Cloud Shell pane, run the following command, substituting the placeholder &lt;custom-label&gt; with any string which is likely to be unique.

 $rg = Get-AzResourceGroup -Name {{resource-group-name}}
   
 Test-AzDNSAvailability -DomainNameLabel <custom-label> -Location $rg.Location
   
 **EX: Test-AzDnsAvailability -DomainNameLabel hgddjhkjldjkkjdjkkkllksgjg -Location $rg.Location**

3. Verify that the command returned **True**. If not, rerun the same command with a different value of the &lt;custom-label&gt; until the command returns **True**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/91.png?st=2019-09-16T09%3A10%3A48Z&se=2022-09-17T09%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5CzX18LJCz%2BMwpdK0OozXmL87clQFKX7iwuHZvT3upM%3D)

4. Note the value of the &lt;custom-label&gt; that resulted in the successful outcome. You will need it in the next task


### Task 2: Deploy an Azure VM Scale Set

1. In the Azure Portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/92.png?st=2019-09-16T09%3A15%3A38Z&se=2022-09-17T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bBXKF%2F0LDvSm0hDPuDqOUnaFg2nhhUkeUFaZcFz5%2BXc%3D)

2. From the **Create a resource** blade, search Azure Marketplace for **Virtual Machine Scale Set**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/93.png?st=2019-09-16T09%3A16%3A03Z&se=2022-09-17T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uVci0mBnu3jDmNQ%2FUMg9nrcJPW%2FoGuY8IkX91WODws0%3D)

3. Use the list of search results to navigate to the **Create Virtual Machine Scale Set** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/94.png?st=2019-09-16T09%3A16%3A24Z&se=2022-09-17T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BPBSidYwAGvWpiaEQUdWAGlUixpac8J%2Bp5yHNfgzqDw%3D)

4. Use the **Create Virtual Machine Scale Set** blade to deploy a Virtual Machine Scale Set with the following settings:

* **Virtual Machine Scale Set name:** `az1000303vmss0` <br>
* **Operating system disk image:** `Windows Server 2016 Datacenter` <br>
* **Subscription:** `Select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Availability zone:** `None` <br>
* **Username:** `Student` <br> 
* **Password:** `Password@1234` <br>
* **Confirm Password:** `Password@1234` <br>
* **Instance count:** `1` <br>
* **Instance size:** `Standard DS1 v2` <br>
* **Deploy as low priority:** `No` <br>
* **Use managed disks:** `Yes` <br>
* **Autoscale:** `Disabled` <br>
* **Choose Load balancing options:** `Load balancer` <br>
* **Public IP Address name:** `az1000303vmss0-ip` <br>
* **Domain name label:** you identified in the previous task `(hgddjhkjldjkkjdjkkkllksgjg)` <br>
* **Virtual network:** `az1000303-vnet0 ` <br>
* **Address range:** `10.203.0.0/16` <br>
* **Subnet name:** `subnet0` <br>
* **Subnet Address range:** `10.203.0.0/24` <br>
* **Public IP Address per instance:** `Off` <br>
* **Accelerated Networking:** `Off` <br>
* **NIC network security group:** `Basic` <br>
* **Select inbound ports:** `HTTP` <br>
* **Boot diagnostics:** `Off` <br>
* **System assigned managed identity:** `Off`
   
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/95.png?st=2019-09-16T09%3A17%3A04Z&se=2022-09-17T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XUt%2BfFVwJr9uMmQoB5A%2B1vpVBFqp1cLoLR64jwNSBrI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/96.png?st=2019-09-16T09%3A17%3A28Z&se=2022-09-17T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zJcip3A7df90P7Xv7%2BsuAi8KkQjLkUwwZJvRLNmgVF4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/97.png?st=2019-09-16T09%3A17%3A48Z&se=2022-09-17T09%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Zkyn%2BTSrQKwiZQ%2BxCSFz5XNNO9bdPtYwVPbJcBGpP68%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/98.png?st=2019-09-16T09%3A18%3A08Z&se=2022-09-17T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4bcx%2B%2BuCsNgQqy7gd5ZJR0E4iKtnEvqK1ERxJ%2BnrOs8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a45.PNG?st=2019-09-18T07%3A20%3A58Z&se=2022-09-19T07%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8TdU%2BcExHJjFbjhZu5t6luYAQKrOjMGpWap1zN70duk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/99.png?st=2019-09-16T09%3A18%3A28Z&se=2022-09-17T09%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JM%2BEOD5p2qBQW6AK%2B3VveRSBQLcwlSTj8R7%2F%2Fem9JLU%3D)


 **Note**: *Wait for the deployment to complete before you proceed to the next task. This should take about 5 minutes.*


### Task 3: Install IIS on a Scale Set VM by using DSC extensions

1. In the Azure Portal, navigate to the **ResourceGroup** and click on it then Navigate to the **az1000303vmss0** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/100.png?st=2019-09-16T09%3A23%3A18Z&se=2022-09-17T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Fl96dfqWYj7eM56QavunnI%2BYKn6VWXcpqurQ8bpBDbY%3D)

2. From the **az1000303vmss0** blade, display its Extension blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/101.png?st=2019-09-16T09%3A23%3A42Z&se=2022-09-17T09%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wTmdsg8UkuG8xma%2F%2F55WPaezMZUYdle6nIon5vRBdyY%3D)

3. From the **az1000303vmss0 - Extension** blade, add the **PowerShell Desired State Configuration** extension with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/102.png?st=2019-09-16T09%3A24%3A04Z&se=2022-09-17T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RLN66F3UlYicgmK4pPpEfmjnSy%2BT52kI2QrncwVek0Y%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/103.png?st=2019-09-16T09%3A24%3A23Z&se=2022-09-17T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=O1ZhXCl5uH1qlgiBdAnXPtPeh3GXzUYwiO8Zgbx32GY%3D)

4. Click on **Create**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/104.png?st=2019-09-16T09%3A24%3A45Z&se=2022-09-17T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kHLqkeP%2Fa3%2BH7VMInsPVP35wSYKLKkr5mPOEY3OJVYE%3D)

   **Note**: *The DSC configuration module is available for upload from **az-100-03_install_iis_vmss.zip**. The module contains the DSC configuration script that installs the Web Server (IIS) role.*
   
   Open the below link in Chrome, Download the Zip file and save it in folder and upload from save folder.
   
   https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Deploy_and_Manage_Virtual_Machines/az-100-03_install_iis_vmss.zip?st=2019-09-18T06%3A08%3A39Z&se=2022-09-18T21%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YSwL21toJo46hHy8iZRsCiIduUfbvgddM8byP0FW60s%3D
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a46.PNG?st=2019-09-18T07%3A09%3A36Z&se=2022-09-19T07%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s5%2B%2BcWPRPqkFko63SkddpetSq3fk00xTZVjljJbmJa4%3D)
   
   ```

   Configuration Modules or Script: "az-100-03_install_iis_vmss.zip"

   Module-qualified Name of Configuration: az-100-03_install_iis_vmss.ps1\IISInstall

   Configuration Arguments: leave blank

   Configuration Data PSD1 File: leave blank

   WMF Version: latest

   Data Collection: Disable

   Version: 2.76

   Auto Upgrade Minor Version: Yes
   
   ```
   
   ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a48.PNG?st=2019-09-18T07%3A10%3A06Z&se=2022-09-19T07%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OD1z041CdkKKd3Etao1KdO0AQGvJT%2BqRpm%2B%2FlmzX2eE%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/105.png?st=2019-09-16T09%3A25%3A07Z&se=2022-09-17T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tKCgaLjn3qCg3Sf9ZBYpXjXlxMpsb%2FghhOrpEvHkUFc%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/106.png?st=2019-09-16T09%3A25%3A32Z&se=2022-09-17T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3UBfsjbgsLRk29VeDaGSZ8atYvhjzyhlhqfO8ciu9jc%3D)

5. Navigate to the **az1000303vmss0 - Instances** blade and initiate the upgrade of the **az1000303vmss0_0** instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/107.png?st=2019-09-16T09%3A25%3A54Z&se=2022-09-17T09%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dKhrzKZU7pzD78bcuieNR%2BbpPS5Gj1NoFewinzjEJIo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a49.PNG?st=2019-09-18T07%3A12%3A10Z&se=2022-09-19T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=k8CriWqXe7R7XTTTqQmsRUmL%2FQ%2B4OuzuqbIV3ap3%2B6I%3D)

   **Note**: *The update will trigger application of the DSC configuration script. Wait for upgrade to complete. This should take about 5 minutes. You can monitor the progress from the **az1000303vmss0 - Instances** blade.*

6. Once the upgrade completes, navigate to the **Overview** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/108.png?st=2019-09-16T09%3A26%3A19Z&se=2022-09-17T09%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PMD8MivKDQcSYnez15iTKWhFl9JQCK09aJruKU8dN34%3D)

7. On the **az1000303vmss0-ip** blade, note the public IP Address assigned to **az1000303vmss0**.

 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a51.png?st=2019-09-18T07%3A15%3A56Z&se=2022-09-19T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AZaBDjBmWvulUSaHsBrrPzvq%2BtVhFbL6uMuzdnw6cog%3D)

8. Start Microsoft Edge and navigate to the public IP Address you identified in the previous step.

**http:// Public Ip Address**
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab1/a50.PNG?st=2019-09-18T07%3A16%3A30Z&se=2022-09-19T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AAghyhUsbRyvFYY5gNf1zfPA68F183mKI5rcgV6HHW4%3D)

9. Verify that the browser displays the default IIS home page.


**Result**: After you completed this Exercise, you have identified an available DNS name for an Azure VM Scale Set deployment, deployed an Azure VM Scale Set, and installed IIS on a Scale Set VM by using the DSC Extension.
