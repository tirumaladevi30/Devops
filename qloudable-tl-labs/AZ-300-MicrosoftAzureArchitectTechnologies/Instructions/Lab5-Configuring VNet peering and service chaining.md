# Lab 5: Configuring VNet peering and service chaining

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Creating an Azure lab environment by using deployment templates](#exercise-1-creating-an-azure-lab-environment-by-using-deployment-templates)

[Exercise 2: Configuring VNet peering](#exercise-2-configuring-vnet-peering)

[Exercise 3: Implementing routing](#exercise-3-implementing-routing)

[Exercise 4: Validating service chaining](#exercise-4-validating-service-chaining)


## Overview

The Aim of this lab is about configure and manage Virtual Networks, further configuring VNet peering and service chaining.

### Scenario and Objectives

XYZ wants to implement service chaining between Azure virtual networks in its Azure subscription.

After completing this lab, you will be able to:

* Deploy Azure VMs by using Azure Resource Manager templates.

* Configure VNet peering.

* Implement routing

* Validate service chaining

## Pre-Requisites

* Familiarity with ARM template

* Familiarity with Azure cloud shell

* RDP session

**Note:** Azure Portal & Remote Desktop is part of the Lab environment

## Exercise 1: Creating an Azure lab environment by using deployment templates
  
The main tasks for this exercise are as follows:

1. Create the first Azure virtual network environment by using an Azure Resource Manager template

2. Create the second Azure virtual network environment by using an Azure Resource Manager template

* Azure Power shell 

Azure PowerShell is an extension of theâ€¯Windows PowerShell platform and scripting languageâ€¯developed to provideâ€¯cmdletsâ€¯for simplifying and automating the management ofâ€¯Azureâ€¯cloud services. Azure PowerShell cmdlets can help system administrators create, test, deploy and manage Azure cloud platform services using PowerShell.

* Azure CLI 

Azure CLIâ€¯is also aâ€¯command-lineâ€¯tool introduced by Microsoft which can use to manageâ€¯Azureâ€¯resources. This is allowing to use from a multiple platform such as Linux, Mac OS and Windows. The Azure CLI allows you to create and manage your Azure resources on Mac OS, Linux, and Windows.

### Task 1: Create the first Azure virtual network environment by using an Azure Resource Manager template
  
1. Using the Chrome browser, login into Azure portal with the below details.

**Azure login_ID:** {{azure-login-id}} <br>

**Azure login_Password:** {{azure-login-password}} <br>


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal1.png?st=2019-08-22T11%3A08%3A20Z&se=2020-08-23T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fm%2BDTeOkr2f0%2BS344uOTMlPzHxDsCisvhsf4Jo1LzmY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal2.png?st=2019-08-22T11%3A09%3A36Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ONwSsJE%2B5ENkff6wqI098VfdvzB77ezY7PxjamtqBgQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal3.png?st=2019-08-22T11%3A09%3A59Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5JhMvyxOF4PJSrB3u4M9KLit%2B9IqG6MrVjUObzyLaGg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal4.png?st=2019-08-22T11%3A10%3A23Z&se=2020-08-23T11%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QKaTSjnXbhdQ1wkIajvEAwwAJvuUfoQn7NBkmBQa2C4%3D)

2. In the Azure portal, start a **Bash** session within the **Cloud Shell**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/1.png?st=2019-08-29T06%3A30%3A41Z&se=2021-08-30T06%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Lm2KxhEY5JM5fy6HxZqXm5Mn%2FVpkGE%2BLJeoDP3h5z9c%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/2.png?st=2019-08-29T10%3A49%3A08Z&se=2021-08-30T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EiUGPkAx14uNSl4k2kFL%2Fj6k2kuJ7Bp%2Fa%2BP5KbFHHNU%3D)


3. If you are presented with the **You have no storage mounted** message, configure storage using the following settings:


**Subsciption**: the name of the target Azure subscription

**Cloud Shell region**: the name of the Azure region that is available in your subscription and which is closest to the lab location

**Resource group**: {{resource-group-name}} <br>

**Storage account**: a name of a new storage account

**File share**: a name of a new file share


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/3.png?st=2019-08-29T06%3A32%3A24Z&se=2021-08-30T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mAmuS2V5jum%2FRESHee4eR%2BwiLs1tU7Bm8l%2B%2FYdWJR8A%3D)

5. From the Cloud Shell pane, upload the first Azure Resource Manager template **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy0401.json?st=2019-08-27T05%3A02%3A26Z&se=2021-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GNu8s3UqYYg%2BVjwalBESPtn6pDRxOSpMV%2BALO097SPo%3D** into the home directory.

Run the below command to upload the file into the home directory.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy0401.json?st=2019-08-27T05%3A02%3A26Z&se=2021-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GNu8s3UqYYg%2BVjwalBESPtn6pDRxOSpMV%2BALO097SPo%3D"

```
6. From the Cloud Shell pane, upload the parameter file **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy04.parameters.json?st=2019-08-27T05%3A03%3A07Z&se=2021-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=D4SNNKwCTwau88OvwCnhaQhIblmHL5h1QeBsWe%2F15LI%3D** into the home directory.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy04.parameters.json?st=2019-08-27T05%3A03%3A07Z&se=2021-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=D4SNNKwCTwau88OvwCnhaQhIblmHL5h1QeBsWe%2F15LI%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/4.png?st=2019-08-29T06%3A32%3A59Z&se=2021-08-30T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=H3RMlhjsJjGXz1xFSgzPsmWpC%2BkKrK0SArXx%2FHxevcI%3D)

Run the below command to change the file names

```
mv "azuredeploy0401.json?st=2019-08-27T05%3A02%3A26Z&se=2021-08-28T05%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GNu8s3UqYYg%2BVjwalBESPtn6pDRxOSpMV%2BALO097SPo%3D" azuredeploy0401.json

mv "azuredeploy04.parameters.json?st=2019-08-27T05%3A03%3A07Z&se=2021-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=D4SNNKwCTwau88OvwCnhaQhIblmHL5h1QeBsWe%2F15LI%3D" azuredeploy04.parameters.json

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/5.png?st=2019-08-29T06%3A33%3A22Z&se=2021-08-30T06%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eV7fK1%2FcD4Yn2C15rdKcpOQNVCsXq84pfTvIeVK9r%2F0%3D)

7. From the Cloud Shell pane, deploy the two Azure VMs hosting Windows Server 2016 Datacenter into the first virtual network by running:

   
az group deployment create --resource-group {{resource-group-name}} <br> --template-file azuredeploy0401.json --parameters @azuredeploy04.parameters.json --no-wait


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/6.png?st=2019-08-29T10%3A38%3A47Z&se=2021-08-30T10%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SHmiSCU593p%2BrJjlSNj7M%2FcOVMxOHouHjejdvBrdnHA%3D)

> **Note**: Do not wait for the deployment to complete but proceed to the next task.

### Task 2: Create the second Azure virtual network environment by using an Azure Resource Manager template

1. From the Cloud Shell pane, upload the second Azure Resource Manager template **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy0402.json?st=2019-08-27T05%3A03%3A58Z&se=2021-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8BtsE0cF1V2COMIF3pekMtjhZaxILBCRTESQ%2BElfSJM%3D** into the home directory.

Run the below comamnds to upload the file into the home directory

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T02/Module_03/azuredeploy0402.json?st=2019-08-27T05%3A03%3A58Z&se=2021-08-28T05%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8BtsE0cF1V2COMIF3pekMtjhZaxILBCRTESQ%2BElfSJM%3D"

mv azuredeploy0402.json\?st\=2019-08-27T05%3A03%3A58Z\&se\=2021-08-28T05%3A03%3A00Z\&sp\=rl\&sv\=2018-03-28\&sr\=b\&sig\=8BtsE0cF1V2COMIF3pekMtjhZaxILBCRTESQ%2BElfSJM%3D azuredeploy0402.json

```
2. From the Cloud Shell pane, deploy an Azure VM hosting Windows Server 2016 Datacenter into the second virtual network by running:


az group deployment create --resource-group {{resource-group-name}} <br> --template-file azuredeploy0402.json --parameters @azuredeploy04.parameters.json --no-wait
   

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/7.png?st=2019-08-29T10%3A39%3A19Z&se=2021-08-30T10%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jBxO%2Bg0oBfHXtL5fUnL8hWQgQ1q3KLBo9SIKpc5fTd4%3D)

> **Note**: The second template uses the same parameter file. 

> **Note**: Do not wait for the deployment to complete but proceed to the next exercise.

**Result**: After completing this exercise, you should have created two Azure virtual networks hosting Azure VMs running Windows Server 2016 Datacenter. 

## Exercise 2: Configuring VNet peering 
  
The task for this exercise is as follows:

* Configure VNet peering for both virtual networks

### Task 1: Configure VNet peering for both virtual networks
  
1. In the Chrome Browser window displaying the Azure portal, navigate to the **az3000401-vnet** virtual network blade.

Go to resource group {{resource-group-name}} <br> --> serach for **az3000401-vnet**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/9.png?st=2019-08-29T06%3A34%3A51Z&se=2021-08-30T06%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Nsn0PXy7KKCmRSfSd%2Bml7nwBTl7NA9kc8bz4xkTtP5o%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/10.png?st=2019-08-29T06%3A35%3A40Z&se=2021-08-30T06%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=I5VgeTTlJ2W%2FCsb8xsFuonFOiNgo7YOPHrZc13B79NU%3D)

2. From the **az3000401-vnet** blade, create a VNet peering with the following settings:

Go to **az3000401-vnet** blade -->Select **Peerings** -->Click **+Add** to create new vnet peering.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/11.png?st=2019-08-29T06%3A38%3A07Z&se=2021-08-30T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ojchkP8RZPwrJeyRv%2FrqN2ZIr3LkIJhZNe18a7kkeVY%3D)

```
Name of the peering from the first virtual network to the second virtual network: az3000401-vnet-to-az3000402-vnet

Virtual network deployment model: Resource manager

Subscription: the name of the Azure subscription you are using for this lab

Virtual network: az3000402-vnet
    
Name of the peering from the first virtual network to the second virtual network: az3000402-vnet-to-az3000401-vnet    
    
Allow virtual network access from the first virtual network to the second virtual nework: Enabled
    
Allow virtual network access from the second virtual network to the first virtual nework: Enabled    

Allow forwarded traffic from the first virtual network to the second virtual network: Disabled
    
Allow forwarded traffic from the second virtual network to the first virtual network: Disabled

Allow gateway transit: disabled
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/12.png?st=2019-08-29T06%3A40%3A20Z&se=2021-08-30T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=82eeBe8MpvUmH5DPUOH9WcJil2pgeYImr5YM1cTMD7U%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/13.png?st=2019-08-29T06%3A40%3A39Z&se=2021-08-30T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aeCFidCYTKDmxy7akN9hkrhVdnKz4Q7fJZtDmE9cs%2FU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/14.png?st=2019-08-29T06%3A48%3A18Z&se=2021-08-30T06%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xEWVGVDUyd2d58yZlciVprq9B80V6%2FzLgjUlI4070Ps%3D)

## Exercise 3: Implementing routing
  
The main tasks for this exercise are as follows:

1. Enable IP forwarding

2. Configure user defined routing 

3. Configure routing on an Azure VM running Windows Server 2016

### Task 1: Enable IP forwarding 
  
1. In Chrome Browser, navigate to the **az3000401-nic2** blade (the NIC of **az3000401-vm2**)

Go to resourcegorup overview section page and search for **az3000401-nic2**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/15.png?st=2019-08-29T06%3A49%3A04Z&se=2021-08-30T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EkYEU4bYiB81XOgli1%2FQArq63MC6M1yLTOnis1A0TvU%3D)

2. On the **az3000401-nic2** blade, modify the **IP configurations** by setting **IP forwarding** to **Enabled** and click **Save**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/16.png?st=2019-08-29T06%3A49%3A31Z&se=2021-08-30T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4t%2BkE36iICDB69r1KgosFzes%2FkxXHEr3T%2FFiWNX4%2BTs%3D)

### Task 2: Configure user defined routing 

1. In the Azure portal, create a new route table with the following settings:

Go to **+ Create a resource** blade and search for **Route table**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/17.png?st=2019-08-29T06%3A49%3A58Z&se=2021-08-30T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s3Oomdmw6NMIcJ%2FLhQPMvvIhQCWrVKqvoyFeozio%2BNM%3D)

Click **Create**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/18.png?st=2019-08-29T06%3A50%3A14Z&se=2021-08-30T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dhOTpElymNOdMSKAg2ZlSgmfXFoIwW8K2dHQ0haU9EU%3D)


**Name**: az3000402-rt1

**Subscription**: the name of the Azure subscription you use for this lab

**Resource group**: {{resource-group-name}} <br>

**Location**: {{location }} <br>
  
**Virtual network gateway route propagation**: Disabled


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/19.png?st=2019-08-29T06%3A51%3A47Z&se=2021-08-30T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=U%2Fgyz0%2FPwONCou6jYIlq2%2B3HgFrwEkzLIEw8g7tWRvI%3D)

2. In the Azure portal, add to the route table a route with the following settings: 

Go to Newly created route table -->Select **Routes** -->Click **+Add** to create a new route in the route table.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/20.png?st=2019-08-29T06%3A52%3A23Z&se=2021-08-30T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IKv76mnLq2a8VcwzOWnTD%2F2MHHHBTeROW1VazXmKKSw%3D)

```
Route name: custom-route-to-az3000401-vnet

Address prefix: 10.0.0.0/22

Next hop type: Virtual appliance

Next hop address: 10.0.1.4
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/21.png?st=2019-08-29T06%3A54%3A20Z&se=2021-08-30T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0I6TwMpHmaJltIfH8bfVm%2BD7UNJ9nloFywad%2BggaN%2B4%3D)

3. In the Azure portal, associate the route table with the **subnet-1** of the **az3000402-vnet**.

With in the route table section blade select **subnets** -->click **+Associate**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/22.png?st=2019-08-29T06%3A54%3A44Z&se=2021-08-30T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7uOubRrZA%2B2%2Fy4Z5sA2j67zecV8fI4GiWEoEu8I2TRQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/23.png?st=2019-08-29T06%3A55%3A25Z&se=2021-08-30T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dW4jFM54vnCVggTENmEocRIV%2F%2FkmqjugGA0vYsV4%2Fjg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/24.png?st=2019-08-29T06%3A55%3A57Z&se=2021-08-30T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m%2BZMmNojjWsm8tgbhrcZ26u3IJvWcWt4ZUGmKmcM%2B%2BA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/25.png?st=2019-08-29T06%3A56%3A18Z&se=2021-08-30T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SB9P%2FrPFty8jrPINXK7C8x1879Gw9QM4DcOjwBNtk7M%3D)

### Task 3: Configure routing on an Azure VM running Windows Server 2016

1. Go to ResourceGroup {{ ResourceGroup }} -->select the **az3000401-vm2** -->on the overview page copy the **PublicIP** address of the vm. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/26.png?st=2019-08-29T06%3A57%3A23Z&se=2021-08-30T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6AG3LOl%2BfdVp3o09P3CNT3QsR9qg2sfgNqLXxszw5VQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/27.png?st=2019-08-29T06%3A58%3A22Z&se=2021-08-30T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2rTBn%2BJRMBPCm%2BYWo6E9N2dPSgI%2BmLgsUnY%2B%2FOy%2F9qs%3D)

On the lab computer, from the Azure portal, start a Remote Desktop session to **az3000401-vm2** Azure VM. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/28.png?st=2019-08-29T10%3A42%3A19Z&se=2021-08-30T10%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kReshTB7fotOZX0Y2wa2CJi3ZVvSzujTlOoD%2BEOGw2I%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/29.png?st=2019-08-29T06%3A59%3A45Z&se=2021-08-30T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=518JflBbb7un%2BOFNTkK8KDGZi2hsvg%2FFMcVJBJcC5Hc%3D)

2. When prompted to authenticate, specify the following credentials:

```
User name: adminuser

Password: Password@1234
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/30.png?st=2019-08-29T07%3A00%3A07Z&se=2021-08-30T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=P1iGPRfggdeiicD5BG4LPZ%2F8KAKN364muYbdj1LD5Bc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/31.png?st=2019-08-29T07%3A00%3A36Z&se=2021-08-30T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6X67%2B7OIYT78mrXETlpSieDkilceeJKXk9nw1X4Y3oU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/32.png?st=2019-08-29T07%3A01%3A08Z&se=2021-08-30T07%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Nc1iD%2BpD8OXa6V6YA4KQ22ZsQuM3%2FIp8SoScuiz%2FGew%3D)

3. Once you are connected to az3000401-vm2 via the Remote Desktop session, from **Server Manager**, install the **Remote Access** server role with the **Routing** role service and all required features. 

After Opening the **Server Manager Dashboard** -->Select **Add roles and features**.

Follow the Installation setup procedure as shown in the below screenshots.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/33.png?st=2019-08-29T07%3A02%3A40Z&se=2021-08-30T07%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E0C7YhPuzPjBeDMcuk4xAxG8VlSbbJ8pUGC7%2BQgQH3E%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/lb5-1.png?st=2019-08-29T10%3A40%3A17Z&se=2021-08-30T10%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6DTwS8IHCCiM1krRbsb2dd4tLqMFLQ6vl7Mp9PQdqfE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/34.png?st=2019-08-29T07%3A25%3A42Z&se=2021-08-30T07%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aYlnGj%2BCihT4Dpkq9hNB%2FIpeyX2eG2oxfljSMpKoEzs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/35.png?st=2019-08-29T07%3A26%3A10Z&se=2021-08-30T07%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WzfjSaGpOnhjstNNI11GeFwteDptJjJs%2F9XIysIN9KA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/36.png?st=2019-08-29T07%3A26%3A31Z&se=2021-08-30T07%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kPE3NXQAHUkFMR6txAjcZg6srd3UOlO3k%2FlcEQdTn7Q%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/37.png?st=2019-08-29T07%3A27%3A10Z&se=2021-08-30T07%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3Hh1NTQcUW8o%2FwmCGEmrdYDGmWUFz4sjSiQrWudsyyc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/38.png?st=2019-08-29T07%3A27%3A28Z&se=2021-08-30T07%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bRnBEzwqxIdPTzUlNxCA5smfjnFfsbQWwxGSuDrDeaw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/lb5-2.png?st=2019-08-29T10%3A44%3A44Z&se=2021-08-30T10%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4IAKC9ulj6i3RsFHIUpAR81wN3fSsdYJMoPVP2GkMP4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/39.png?st=2019-08-29T07%3A27%3A50Z&se=2021-08-30T07%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BptOpbyfVq1MrK5mYmxCMGJB7oq%2Fgtr2JOyDjLiqWPs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/40.png?st=2019-08-29T07%3A28%3A17Z&se=2021-08-30T07%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Bmc6mkEvwcJ3j%2Fv5IyhDKH9ARBUuXhJ%2BVbCgUQaN9qc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/41.png?st=2019-08-29T07%3A28%3A41Z&se=2021-08-30T07%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8k4TDLpseCEWH43fXwxfIi6NNSc%2FEy8o%2BokZSj2d9R8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/42.png?st=2019-08-29T07%3A29%3A03Z&se=2021-08-30T07%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=y%2FdGdccnlUELVaCQYFav28jkk3PsWPU9iZgnZQnYQuM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/43.png?st=2019-08-29T07%3A29%3A23Z&se=2021-08-30T07%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RX4cNg5FRTfzhIZzz6hFOw%2Fnn8v36CpADG2aQYpZtP8%3D)

4. In the Remote Desktop session to az3000401-vm2, start the **Routing and Remote Access** console. 

5. In the **Routing and Remote Access** console, run **Routing and Remote Access Server Setup Wizard** and enable **LAN routing**. 

Right click on the **vm name** and choose **Remote Access managemnet**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/44.png?st=2019-08-29T07%3A07%3A52Z&se=2021-08-30T07%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gGf4OwznZD1T2VIhMyOJ0gUlzx7XOz10k0t6InAr1Y4%3D)

On the configuration select **Direct Access and VPN only**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/46.png?st=2019-08-29T07%3A08%3A41Z&se=2021-08-30T07%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uCz7CE9jDF9a8vtRrUgELqUF144VERh%2F4oqRm7u3Rpw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/45.png?st=2019-08-29T07%3A08%3A24Z&se=2021-08-30T07%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mBAIGKH237zM7pniT44E5H8xKE8V93octHxFBh9fYuo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/47.png?st=2019-08-29T07%3A09%3A23Z&se=2021-08-30T07%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1CEQYK1d6MpnnEFlrb%2BKLMB%2BY7l75EU7vf6e3kisVw4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/48.png?st=2019-08-29T07%3A09%3A46Z&se=2021-08-30T07%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=frd32gkCfpdAr5aL3v3FApFz19Y5h6FtfrUQINb5KqI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/49.png?st=2019-08-29T07%3A10%3A03Z&se=2021-08-30T07%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cFMLk0plhNtGnbVqMoXT7YSOjxQjc2FV58FwZ%2BTqLMI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/50.png?st=2019-08-29T07%3A12%3A21Z&se=2021-08-30T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=O5Z2GazPXTcvYZmTqJgGMJ8mHXkhjiffTwbBVHICB5Y%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/lb5-3.png?st=2019-08-29T10%3A46%3A52Z&se=2021-08-30T10%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MPiCKFjqr328S8HepXVNfBoCbH667x24mFfV1i4rqQ4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/lb5-4.png?st=2019-08-29T10%3A47%3A12Z&se=2021-08-30T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ma31vGLl%2FGsS3F04yoPivIgYTCxVbgjpz%2Bsf5f88v%2FQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/lb5-5.png?st=2019-08-29T10%3A47%3A28Z&se=2021-08-30T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IBQd5Ncb3BXQ%2F8a%2FhuD3Ctuwn63udRiMTKQ34fPm6ao%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/51.png?st=2019-08-29T07%3A12%3A40Z&se=2021-08-30T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ybH8kEMx9m21VIlY5YXqPfvwTM334PtPRrRwiGQ6Gfg%3D)


6. Go to windows **Start** -->and search for **Services** to Start **Routing and Remote Access** service.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/52.png?st=2019-08-29T07%3A14%3A28Z&se=2021-08-30T07%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rfNpDsthWUFfMp9gxDKTmGa8vTDgTxUQT0PsMj6o1co%3D)

Select **Routing and Remote Access** -->Right click on the service to select **Properties** and follow the below procedure.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/53.png?st=2019-08-29T07%3A14%3A49Z&se=2021-08-30T07%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qBYP7QdbW%2F8%2Bonjoa5b0cmWcldTcS3%2BDGpjH19Zvs%2Bo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/54.png?st=2019-08-29T07%3A15%3A14Z&se=2021-08-30T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cq9oBrN4eD1N%2FtJoqvZJ1Dnnj84VWs4Y95gwuutPOZA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/55.png?st=2019-08-29T07%3A15%3A34Z&se=2021-08-30T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=r%2FMsvhxq42WgpYk6IYJKKDvxKWaMv4eOhHST94YBCOI%3D)

7. In the Remote Desktop session to az3000401-vm2, start the **Windows Firewall with Advanced Security** console and enable **File and Printer Sharing (Echo Request - ICMPv4-In)** inbound rule for all profiles.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/56.png?st=2019-08-29T07%3A15%3A58Z&se=2021-08-30T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cj0hKE9bq%2F4meDFESSuCqoSNlSUngnH%2Fcn7VMB04eNc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/57.png?st=2019-08-29T07%3A16%3A15Z&se=2021-08-30T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E%2B0HvSib%2FzBpBMY8sc8PE%2BzPeQCoOEXy25x8D3pvO4E%3D)

8. After Enabling.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/58.png?st=2019-08-29T07%3A16%3A33Z&se=2021-08-30T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FNW3zxDoIEGmHFbILeEwxV3Q3KIbgk9IlEU38%2FahDSU%3D)

**Result**: After completing this exercise, you should have configured custom routing within the second virtual network.

## Exercise 4: Validating service chaining
  
The main tasks for this exercise are as follows:

1. Configure Windows Firewall with Advanced Security on an Azure VM

2. Test service chaining between peered virtual networks

### Task 1: Configure Windows Firewall with Advanced Security on the target Azure VM

1. Go to ResourceGroup {{ ResourceGroup }} -->select the **az3000401-vm1** -->on the overview page copy the **PublicIP** address of the vm. 

On the lab computer, from the Azure portal, start a Remote Desktop session to **az3000401-vm1** Azure VM. 

2. When prompted to authenticate, specify the following credentials:

```
User name: adminuser

Password: Password@1234
```
3. In the Remote Desktop session to az3000401-vm1, start the **Windows Firewall with Advanced Security** console and enable **File and Printer Sharing (Echo Request - ICMPv4-In)** inbound rule for all profiles.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/59.png?st=2019-08-29T07%3A17%3A13Z&se=2021-08-30T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Po9QzkLdNA7z%2B9oSnd6kdMS%2FWMeKOsMPPTfxkGTXfwg%3D)

### Task 2: Test service chaining between peered virtual networks
  
1. On the lab computer, from the Azure portal, start a Remote Desktop session to **az3000402-vm1** Azure VM. 

2. When prompted to authenticate, specify the following credentials:

```
User name: **adminuser**

Password: **Password@1234**
```

3. Once you are connected to **az3000402-vm1** via the Remote Desktop session, start **Windows PowerShell**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/60.png?st=2019-08-29T07%3A17%3A40Z&se=2021-08-30T07%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7BqjP8tIb9eJdityjTqD6Xl0f2zvg4DzywMzuGj2ouU%3D)

4. In the **Windows PowerShell** window, run the following:

   ```pwsh
   Test-NetConnection -ComputerName 10.0.0.4 -TraceRoute
   ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab%205%20-%20Configuring%20VNet%20peering%20and%20service%20chaining/61.png?st=2019-08-29T07%3A18%3A01Z&se=2021-08-30T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QB0UteacN6ZrzqGoXYORn3S%2F9MIHnFhuwSCMB%2Bieb68%3D)

5. Verify that test is successful and note that the connection was routed over 10.0.1.4

**Result**: After completing this exercise, you should have validated service chaining between peered virtual networks.
