# Lab 5: VNet Peering and Service Chaining

## Table of content

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Prepare the Azure environment](#exercise-1-prepare-the-azure-environment)	

[Exercise 2: Configure VNet peering](#exercise-2-configure-vnet-peering)	

[Exercise 3: Implement custom routing](#exercise-3-implement-custom-routing)	

[Exercise 4: Validating service chaining](#exercise-4-validating-service-chaining)	


## Overview

The main aim of the lab is Azure Resource Manager to deployed three Azure VM and created two Azure virtual networks. Also implemented custom routing between peered virtual networks and validated service chaining between peered virtual networks.	

### Scenario and objective
XYZ training labs corporation wants to implement service chaining between Azure virtual networks in its Azure subscription.	

After completing this lab, you will be able to:	

-	Create Azure virtual networks and deploy Azure VM by using Azure Resource Manager templates.	

-	Configure VNet peering.	

-	Implement custom routing	

-	Validate service chaining	

All tasks in this lab are performed from the Azure portal except for Exercise 2 Task 3, Exercise 3 Task 1, and Exercise 3 Task 2, which include steps performed from a Remote Desktop session to an Azure VM

## Pre-requisites

1.	ARM Template	

2.	PowerShell	

**Lab files:**	

*   https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_01_azuredeploy.json?st=2019-09-17T11%3A34%3A10Z&se=2025-09-18T11%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=H8OtvJC0GFSeGKh2Ez4wG%2B8Uq%2F5YGB4TxQKIOjgAHRE%3D	

* https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_02_azuredeploy.json?st=2019-09-17T11%3A34%3A47Z&se=2025-09-18T11%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nce7dOQwsZPn7wS%2BvGepLcCLqVWvPekm%2BPg9MKV%2Bd3Q%3D	

* https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_azuredeploy.parameters.json?st=2019-09-17T11%3A35%3A24Z&se=2025-09-18T11%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=igz6jADJM3TSdPbwSQtDPOhblX%2B767E1dCtftBngWgU%3D


## Exercise 1: Prepare the Azure environment	

The main tasks for this exercise are as follows:	

1.	Create the first virtual network hosting two Azure VMs by using an Azure Resource Manager template	

2.	Create the second virtual network in the same region hosting a single Azure VM by using an Azure Resource Manager template	

-	**Azure Virtual Network**	

Azure Virtual Network (VNet) is the fundamental building block for your private network in Azure. VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks. VNet is similar to a traditional network that you'd operate in your own data center but brings with its additional benefits of Azure's infrastructure such as scale, availability, and isolation.	

-	**Azure VM**	

A virtual machine is a computer file, typically called an image, which behaves like an actual computer. In other words, creating a computer within a computer. It runs in a window, much like any other programme, giving the end user the same experience on a virtual machine as they would have on the host operating system itself. The virtual machine is sandboxed from the rest of the system, meaning that the software inside a virtual machine cannot escape or tamper with the computer itself. This produces an ideal environment for testing other operating systems including beta releases, accessing virus-infected data, creating operating system backups and running software or applications on operating systems for which they were not originally intended.	

-	**Azure Resource Manager**	

Azure Resource Manager is the deployment and management service for Azure. It provides a consistent management layer that enables you to create, update, and delete resources in your Azure subscription. You can use its access control, auditing, and tagging features to secure and organize your resources after deployment.	


### Task 1: Create the first virtual network hosting two Azure VMs by using an Azure Resource Manager template	

1.	Using the Chrome browser, login into Azure portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/l1.png?st=2019-09-17T11%3A40%3A52Z&se=2025-09-18T11%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XTAI0kJuGIsxFGSCxEkT6RZyXIDqDaSf5TIV9ivAbdQ%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/l2.png?st=2019-09-17T11%3A41%3A19Z&se=2025-09-18T11%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BXQ1qlW%2BFN2L%2FslGGRtiLu8sxdRlaclYBCIUp2H2Trk%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/l3.png?st=2019-09-17T11%3A41%3A41Z&se=2025-09-18T11%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZpaZUcdFi6t7XiI3IxbbooorgplkrR6dAGpht%2BgzAU0%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/l4.png?st=2019-09-17T11%3A42%3A02Z&se=2025-09-18T11%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zHXDd2QwZ3TeVwGqRi1JQ%2BI70%2F4eQ65O6%2FMQBT%2BpW4s%3D" alt="image-alt-text" >	

2.	In the Azure portal, navigate to the **Create a resource** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/1.png?st=2019-09-17T11%3A57%3A48Z&se=2025-09-18T11%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lSf4xW%2FrNhHlFBEA5whFksbBDG%2Bec8dzxgubjhB1kyA%3D)	

3.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/2.png?st=2019-09-17T11%3A58%3A27Z&se=2025-09-18T11%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sVS3Ilx5yGwCoR4vJE1xA8tpWsG%2BYtZvO0KVtjRBu38%3D)	

4.	Use the list of search results to navigate to the **Template deployment (deploy using custom templates)** blade, and then click **Create**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/3.png?st=2019-09-17T11%3A59%3A06Z&se=2025-09-18T11%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FD2dhYFnrlWVgaPiVwXfHJnuL317jPjRrigI2R2nodk%3D)	

5.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/4.png?st=2019-09-17T11%3A59%3A49Z&se=2025-09-18T11%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=K2x9yhEXI4QozGWT9DFQdKiHsb9PIdRrTNrwtWhv5r8%3D)	

6.	From the **Edit template** blade, clear the existing content, Copy and paste the below url in chrome new window copy the entire content display in that page paste it in template file.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_01_azuredeploy.json?st=2019-09-17T11%3A34%3A10Z&se=2025-09-18T11%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=H8OtvJC0GFSeGKh2Ez4wG%2B8Uq%2F5YGB4TxQKIOjgAHRE%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/91.PNG?st=2019-09-18T05%3A46%3A23Z&se=2025-09-19T05%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vZ%2FZCJCdT1fLJG1itoQs3zmxkjiAcRIGRlEcIWuN3FE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/5.png?st=2019-09-17T12%3A00%3A42Z&se=2025-09-18T12%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fAcZ3XsoAqOJ3MFfLZ%2B4pIaDOWCE2vPrIwKOFY6jZ1A%3D)	

**Note:** *Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.*	

7.	Save the template and return to the **Custom deployment** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/6.png?st=2019-09-17T12%3A01%3A11Z&se=2025-09-18T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4METVT%2FA%2FzVakbC72UwljRKZxMQiAXYMBySiyiUGmzU%3D)	

8.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/7.png?st=2019-09-17T12%3A01%3A39Z&se=2025-09-18T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=F2j62ytMbjCx6aJXf1ObD4toYSGrWvAMjrZYqXDgX9Y%3D)	

9.	From the **Edit parameters** blade, clear the existing content, Copy and paste the below url in chrome new window copy the entire content display in that page paste it in edit parameters.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_02_azuredeploy.json?st=2019-09-17T11%3A34%3A47Z&se=2025-09-18T11%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nce7dOQwsZPn7wS%2BvGepLcCLqVWvPekm%2BPg9MKV%2Bd3Q%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/92.PNG?st=2019-09-18T05%3A48%3A42Z&se=2025-09-19T05%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c6V0m9648bA7ISZ8eLBPovBJorBrA8HcDwlwuyrKtPA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/8.png?st=2019-09-17T12%3A02%3A05Z&se=2025-09-18T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ybq%2F4w5cm3o4T5lWdcpT5C%2B%2Fo75xpybtGbnyLO2OejA%3D)	

10.	Save the parameters and return to the **Custom deployment** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/9.png?st=2019-09-17T12%3A02%3A30Z&se=2025-09-18T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=loB%2FV%2FFM6sUBdAqYTuRZ8zf%2FwQMKIXDwPpqsw7LPFO4%3D)	

11.	From the **Custom deployment** blade, initiate a template deployment with the following settings:	

* **Subscription:** `default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vm Size:** `Standard_DS2_v2`<br>	
* **Vm1Name:** `az1000401-vm1` <br>
* **Vm2Name:** `az1000401-vm2` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234` <br>
* **Virtual Network Name:** `az1000401-vnet1` 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/10.png?st=2019-09-17T12%3A02%3A58Z&se=2025-09-18T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pu9lJADqD9wVbJnvms3dxysl5tQDhIgvefQKtUnzjDw%3D) 	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/11.png?st=2019-09-17T12%3A04%3A10Z&se=2025-09-18T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ob2I2KVki0IBjYewzRdQNdnDSghGLlBV6Y8MClivrDs%3D)	


**Note:** Do not wait for the deployment to complete but proceed to the next task. You will use the network and the virtual machines included in this deployment in the second exercise of this lab.	

### Task 2: Create the second virtual network in the same region hosting a single Azure VM by using an Azure Resource Manager template	

1.	In the Azure portal, navigate to the **Create a resource** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/12.png?st=2019-09-17T12%3A04%3A36Z&se=2025-09-18T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4RT0Elxjm1RTbRYbke5WDzsLc9NJ0MdPRHii8DyKlbg%3D)	

2.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment.**	

3.	Use the list of search results and select the **Template deployment (deploy using custom templates)** result, and then click **Create**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/13.png?st=2019-09-17T12%3A05%3A04Z&se=2025-09-18T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FKRtsSZwqRtXsUwDSPiMYlJKdfF%2BhunDf23oXTK5Q%2F4%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/14.png?st=2019-09-17T12%3A05%3A28Z&se=2025-09-18T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SvUOhwa%2FgtIm3loyanw4O7VtFwjW%2BfHFLuXg3kn3l4w%3D)	

4.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/15.png?st=2019-09-17T12%3A05%3A49Z&se=2025-09-18T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=elQU7BAvRcZmvMj1xiR%2FRUWSqcqh9laCcz7eycHzDyY%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/16.png?st=2019-09-17T12%3A06%3A17Z&se=2025-09-18T12%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ll3aQBAntx7THa8hb4Qo9QKv6RL0CecMpUAImv7m9Co%3D)	

5.	From the **Edit template** blade,clear the template body Copy and paste the below url in chrome new window copy the entire content display in that page paste it in template file.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_azuredeploy.parameters.json?st=2019-09-17T11%3A35%3A24Z&se=2025-09-18T11%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=igz6jADJM3TSdPbwSQtDPOhblX%2B767E1dCtftBngWgU%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/93.PNG?st=2019-09-18T05%3A55%3A30Z&se=2025-09-19T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2ZODTivtKM4zZ3rvuhCjIsoHZkKC%2FnvhaFo8sYiI1mk%3D) 	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/17.png?st=2019-09-17T12%3A06%3A40Z&se=2025-09-18T12%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CeuTIsFDk%2F29zRuGD98dtzCJFqBEQHxGYe1IKrhTlo8%3D) 	

**Note**: Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.	

6.	Save the template and return to the **Custom deployment** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/18.png?st=2019-09-17T12%3A07%3A09Z&se=2025-09-18T12%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ygm3ONXUxBaJU7rpKL%2B1MbGIjWI04nR2Ax0dGLilfAs%3D)	

7.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/19.png?st=2019-09-17T12%3A07%3A47Z&se=2025-09-18T12%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5TJtAx%2B1SuRhk9ENB9WEBm5XpVsNg5rMSlnTI7VEF1k%3D)	

8.	From the **Edit parameters** blade, clear the existing content, Copy and paste the below url in chrome new window copy the entire content display in that page paste it in edit parameters.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_05/VNet_Peering_and_Service_Chaining/az-100-04_02_azuredeploy.json?st=2019-09-17T11%3A34%3A47Z&se=2025-09-18T11%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nce7dOQwsZPn7wS%2BvGepLcCLqVWvPekm%2BPg9MKV%2Bd3Q%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/92.PNG?st=2019-09-18T05%3A48%3A42Z&se=2025-09-19T05%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c6V0m9648bA7ISZ8eLBPovBJorBrA8HcDwlwuyrKtPA%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/20.png?st=2019-09-17T12%3A08%3A14Z&se=2025-09-18T12%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aFDpdaMsaPpLvqT4iNmwQrVxiiO%2FXLxe2ONeKaNnbf8%3D)	

9.	Save the parameters and return to the **Custom deployment** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/21.png?st=2019-09-17T12%3A08%3A38Z&se=2025-09-18T12%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MXHFtFVjd5cF2x%2FPu13lYZevCLRv5eeixJ6cEgWnDyY%3D)	

10.	From the **Custom deployment** blade, initiate a template deployment with the following settings:	

* **Subscription:** `default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{ location }}` <br>
* **Vm Size:** `Standard_DS2_v2` <br>	
* **VmName:** `az1000402-vm3` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234` <br>
* **Virtual Network Name:** `az1000402-vnet2` 


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/22.png?st=2019-09-17T12%3A09%3A04Z&se=2025-09-18T12%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F5XZpXh234eG%2B9MSnR9Q8IokLBUpPpDt0QiCP5f6A0A%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/23.png?st=2019-09-17T12%3A09%3A41Z&se=2025-09-18T12%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IsJ314Jc5lQ6GbpXNWx0ZO%2BY5D4Sxk2Mk7vymws2h8Q%3D)	

**Note:** Do not wait for the deployment to complete but proceed to the next task. You will use the network and the virtual machines included in this deployment in the second exercise of this lab.	

**Result:** After you completed this exercise, you have created two Azure virtual networks and initiated deployments of three Azure VM by using Azure Resource Manager templates.	

## Exercise 2: Configure VNet peering	

The main tasks for this exercise are as follows:	

1.	Configure VNet peering for the first virtual network	

2.	Configure VNet peering for the second virtual network	

### Task 1: Configure VNet peering for the first virtual network	

1.	In the Azure portal, navigate to the **az1000401-vnet1** virtual network blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/24.png?st=2019-09-17T12%3A10%3A05Z&se=2025-09-18T12%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JfBTD5BmlISSRhrYw%2FIgIpLmv8emGTJ3oH%2Bgg87eIpM%3D)	

2.	From the **az1000401-vnet1** virtual network blade, display its **Peerings** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/25.png?st=2019-09-17T12%3A10%3A25Z&se=2025-09-18T12%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vHYvbQ%2FJyQGmQEksUrnLVBUWAn9I2PUa1kN%2Fd6koDW8%3D)	

3.	From the **az1000401-vnet1 - Peerings** blade, click **+ Add** to create a VNet peering with the following settings:	

* **Name:** `az1000401-vnet1-to-az1000402-vnet2` <br>
* **Virtual network deployment model:** `Resource manager` <br>
* **Subscription:** `default` <br>
* **Virtual network:** `az1000402-vnet2` <br>
* **Name of peering from az1000402-vnet2 to az1000401-vnet1:** `az1000402-vnet2-to-az1000401-vnet1` <br>
* **Allow virtual network access:** `Enabled` <br>
* **Allow forwarded traffic:** `disabled` <br>
* **Allow gateway transit:** `disabled`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/26.png?st=2019-09-17T12%3A10%3A51Z&se=2025-09-18T12%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rOMzGteY7%2B4QKU5YQy1Kh4YdCymrwZGWXuipn3a%2FrRs%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/27.png?st=2019-09-17T12%3A11%3A10Z&se=2025-09-18T12%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HIUsB1JXdSt2xYwhdMo4xBiF5NhBdKW%2Fb%2BPwwpFVUpQ%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/28.png?st=2019-09-17T12%3A11%3A36Z&se=2025-09-18T12%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l45ZpfsX9BMdCuJP3Xqe4xd7zC8cXR53OIDRaTaHdu8%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/29.png?st=2019-09-17T12%3A12%3A02Z&se=2025-09-18T12%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=v%2FRhgketfOovQNwek%2BpHHnoj%2FHoUQ7THrzDww6CJWYQ%3D)	


**Note:** Because you have administrative access to both virtual networks, the portal is configuring both directions (from vnet1 to vnet2, AND vnet2 to vnet1) in a single action. From the CLI, PowerShell, or REST API, these tasks must be performed independently.	

## Exercise 3: Implement custom routing	

The main tasks for this exercise are as follows:	

1.	Enable IP forwarding for a network interface of an Azure VM	

2.	Configure user defined routing	

3.	Configure routing in an Azure VM running Windows Server 2016	

### Task 1: Enable IP forwarding for a network interface of an Azure VM	

**Note:** Before you start this task, ensure that the template deployments you started in Exercise 0 have completed.	

1.	In the Azure portal, navigate to the blade of the second Azure VM **az1000401-vm2**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/30.png?st=2019-09-17T12%3A12%3A28Z&se=2025-09-18T12%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2uRBE7VzMCsJjt6PfKx0MS76dhuKaUrNzYZVH1WlTac%3D)	

2.	From the **az1000401-vm2** blade, display its **Networking** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/31.png?st=2019-09-17T12%3A12%3A51Z&se=2025-09-18T12%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xE5mWTtoDKeHdS1jMRo%2FbZnibZqL9Soy7gcuh772SdU%3D)	

3.	From the **az1000401-vm2 - Networking** blade, display the blade of the network adapter (**az1000401-nic2**) of the Azure VM.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/32.png?st=2019-09-17T12%3A13%3A09Z&se=2025-09-18T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WOfrz7fJCGrzErGjuHuZtaUlRV9H%2BtS3y8b%2FaPQRo8s%3D)	

4.	From the **az1000401-nic2** blade, display its **IP configurations** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/33.png?st=2019-09-17T12%3A13%3A30Z&se=2025-09-18T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wQUabdUw%2BOfmvgqCWgovG4SWsPUK5hA1kYPTmTSSblY%3D)	

5.	From the **az1000401-nic2 - IP configurations** set IP forwarding to **Enabled**, and then click **Save**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/34.png?st=2019-09-17T12%3A13%3A49Z&se=2025-09-18T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hEzkMSwYXpNricOD4P%2B72WiYW4%2FN9StxrqmYe%2FuoUEs%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/35.png?st=2019-09-17T12%3A14%3A16Z&se=2025-09-18T12%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GuqdBjiT1ohyetECIea5kmWb2xO1ESwExrjnVo1kyWo%3D)	

**Note:** *The Azure VM az1000401-vm2, which network interface you configured in this task, will function as a router, facilitating service chaining between the two virtual networks.*	

### Task 2: Configure user defined routing	

1.	In the Azure portal, navigate to the **Create a resource** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/36.png?st=2019-09-17T12%3A15%3A50Z&se=2025-09-18T12%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0p9MgCpHqCsacX9pdWvPtMHu3bYLl%2Fl7sL6jPk%2BF5Bo%3D)	

2.	From the **Create a resource** blade, search Azure Marketplace for **Route table**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/37.png?st=2019-09-17T12%3A16%3A59Z&se=2025-09-18T12%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=33Bldh%2FOowPztvC9VrzqXPetudFksF9eVmkIwkbqOcI%3D)	

3.	Select **Route table**, and then click **Create**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/38.png?st=2019-09-17T12%3A17%3A21Z&se=2025-09-18T12%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pK6WMKoAtYnrpPL326FTEAyZMnPM9sF%2Bok5q08APxMg%3D)	

4.	From the **Create route table** blade, create a new route table with the following settings:	

* **Name:** `az1000402-rt1` <br>
* **Subscription:** `default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Virtual network gateway route propagation:** `Disabled`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/39.png?st=2019-09-17T12%3A18%3A19Z&se=2025-09-18T12%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ekMLJ3%2BdHNymBxSZt8hcrc%2BtNoC5Hxskfb3b%2BakVy5U%3D)	

5.	In the Azure portal, navigate to the **az1000402-rt1** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/40.png?st=2019-09-17T12%3A18%3A59Z&se=2025-09-18T12%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=A%2BTzQFo2nTlpR6CpL47Oc%2BoITn46H0Ui%2BCmn5RT0xJg%3D)	

6.	From the **az1000402-rt1** blade, display its **Routes** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/41.png?st=2019-09-17T12%3A19%3A25Z&se=2025-09-18T12%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eGP%2Bwd%2BrDVbEE4ciHSqnLKpXr1q%2B3x4q4mjrg4Nfdxw%3D)	

7.	From the **az1000402-rt1 - Routes** blade, add to the route table a route with the following settings:	

* **Route name:** `custom-route-to-az1000401-vnet1` <br>
* **Address prefix:** `10.104.0.0/16` <br>
* **Next hop type:** `Virtual appliance` <br>
* **Next hop address:** `10.104.1.4`	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/42.png?st=2019-09-17T12%3A19%3A47Z&se=2026-09-18T12%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YGFW3NFo114ALxH8MI9tKcKCtf988nU17W6NmTk%2Bc4s%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/43.png?st=2019-09-17T12%3A20%3A12Z&se=2025-09-18T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Bp9qOINy2voN1VvbX0ocDu%2BfISXe9ehwCHCTLMueO3w%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/44.png?st=2019-09-17T12%3A20%3A31Z&se=2025-09-18T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fD4jcqdiLRIzlLmRDd4Xa15Lm77qMtWCqscxxn6njWc%3D)	

**Note:** *10.104.1.4 is the IP address of the network interface of az1000401-vm2, which will provide service chaining between the two virtual networks.*	

8.	From the **az1000402-rt1** blade, display its **Subnets** blade.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/45.png?st=2019-09-17T12%3A20%3A55Z&se=2025-09-18T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SbIej%2BlrZOcmXcUACSYdc1S4Hn4txyjja5kscf5Yo68%3D)	

9.	From the **az1000402-rt1 - Subnets** blade, associate the route table **az1000402-rt1** with **subnet0** of **az1000402-vnet2**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/46.png?st=2019-09-17T12%3A21%3A17Z&se=2025-09-18T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jb5zIo9P1OpZRfkwD6P5AcSK%2F5lDFwEp0NUbXVxxs08%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/47.png?st=2019-09-17T12%3A21%3A41Z&se=2025-09-18T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mvwIJtxEzb2M32QD4dyPyQVqZ%2FxkXgJDdLHyFDsiluo%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/48.png?st=2019-09-17T12%3A22%3A01Z&se=2025-09-18T12%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pdmI86GdMw1SXH47St4A41PT7HpUbu%2Fo%2BG91BZzlxTc%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/49.png?st=2019-09-17T12%3A22%3A19Z&se=2025-09-18T12%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LHw%2BGzoq4e%2B30PmjOuPlIwL8GxVKDzRm5Vfebo0XdAA%3D)	

### Task 3: Configure routing in an Azure VM running Windows Server 2016	

-	**Remote Desktop**	

Remote desktop is a program or an operating system feature that allows a user to connect to a computer in another location, see that computer's desktop and interact with it as if it were local.	

People use remote desktop access capabilities to do a variety of things, including the following:	

*	Access a workplace computer from home or when traveling.	

*	Access a home computer from other locations.	

*	Fix a computer problem.	

*	Perform administrative tasks.	

*	Demonstrate something, such as a process or a software application	

1.	In the Azure portal, navigate to the blade of the **az1000401-vm2** Azure VM.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/50.png?st=2019-09-17T12%3A22%3A50Z&se=2025-09-18T12%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9sIXJirvyP9ddMCZRYxwXjhSf0f7qi4bAnpnGstaqig%3D)	

2.	From the **Overview** pane of the **az1000401-vm2** blade, copy the Public IP address it to connect to **az1000401-vm2**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/51.png?st=2019-09-17T12%3A23%3A14Z&se=2025-09-18T12%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tZ54u3c4EkDaj%2BLOCLWLc%2Bkj5DVDDVAdt2ShhEHl7H0%3D) 	

From console open the Remote Desktop Connection

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/97.png?st=2019-09-18T07%3A12%3A14Z&se=2025-09-19T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vKUJkZBkDv%2Fzlnia1yVQF9n0%2FRNV2E%2FVIEwbHCqPGX0%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/95.PNG?st=2019-09-18T07%3A12%3A43Z&se=2025-09-19T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z2IP6WWA7DAhz5EsYQnEpA3BS7W%2BHpPAcgtlA2XaYDM%3D)	

3.	When prompted, authenticate by specifying the following credentials:	

```
User name: adminuser	

Password: Password@1234

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/54.png?st=2019-09-17T12%3A24%3A21Z&se=2025-09-18T12%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YVFc8pQySH4fFaiylnEm0MwLI1aSBPtUAlcFY3FCsNI%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/55.png?st=2019-09-17T12%3A24%3A43Z&se=2025-09-18T12%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2v4aLSoK2Euk16YvFdMk8QY51W37F%2FN%2FHhAHESr7%2Bs8%3D)	

4.	Within the Remote Desktop session to **az1000401-vm2**, from **Server Manager**, use the **Add Roles and Features Wizard** to add the **Remote Access** server role with the **Routing** role service and all required features.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/56.png?st=2019-09-17T12%3A25%3A08Z&se=2025-09-18T12%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zvqlgIBlAaTDWyyjZwg2N6E4Vb%2BkOkoZreEIqghRhD4%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/57.png?st=2019-09-17T12%3A25%3A30Z&se=2025-09-18T12%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vA%2B0Rz1H1P8jxPw2fkgreDMnd%2BMn7GxVJ6uUtW7mEmk%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/58.png?st=2019-09-17T12%3A25%3A52Z&se=2025-09-18T12%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gOgpRBhMiIEJdrsivDlGuhNvfQvK8A1pBWIZJ3oNI60%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/59.png?st=2019-09-17T12%3A26%3A13Z&se=2025-09-18T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SkFHQhrexRKroZ79xLOI%2BXZ4pNpVnD%2FJK%2BGXu2fnqaM%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/60.png?st=2019-09-17T12%3A26%3A35Z&se=2025-09-18T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sBSfDtc85Kf8gD0erVljj64RZA9VSqFe4REfCl5FF6Q%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/61.png?st=2019-09-17T12%3A26%3A58Z&se=2025-09-18T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=V6ORXz2Kf7ECULsO63C2ZqzGC8UnmBHSBQD1J%2FADgiQ%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/62.png?st=2019-09-17T12%3A27%3A18Z&se=2025-09-18T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=n44VTs61jcekI8a%2BeadgGoVL9D0waTr75Zv331YCxFA%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/63.png?st=2019-09-17T12%3A27%3A44Z&se=2025-09-18T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=i2KORsNV3Bob5PmPAwQk0klavEw1EYVnNdtNs9cLkGA%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/64.png?st=2019-09-17T12%3A28%3A05Z&se=2025-09-18T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SOomFZLtucqsfdA3Cwcs6wcfdQBhY4UjRIPg36JHSgo%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/65.png?st=2019-09-17T12%3A28%3A26Z&se=2025-09-18T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=49f%2FUWEC6AFt3Fl6cY%2BcDbEplUoya6bU%2F6Q%2FXXkTCxQ%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/66.png?st=2019-09-17T12%3A28%3A47Z&se=2025-09-18T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QZw5rNIc3YnM%2BQAZG58MDFHPCRZFdOGeBczUsEliN2A%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/67.png?st=2019-09-17T12%3A29%3A56Z&se=2025-09-18T12%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qBVvB3YLvO9aRRUCHICRyDhLMeHINfhg9opsQz5azAo%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/68.png?st=2019-09-17T12%3A30%3A18Z&se=2025-09-18T12%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zFFo9DLymSOzaFGhL6WbBal6kk2Uc%2Fv%2BV2gEycAS38A%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/69.png?st=2019-09-17T12%3A30%3A36Z&se=2025-09-18T12%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fA30LYH4DYI07Ea5MRMKRyWb6cLunlNQEdUdPi%2BI4uk%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/70.png?st=2019-09-17T12%3A30%3A58Z&se=2025-09-18T12%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KjNkW65n%2Bp1w0kutmSyKFRlDN4vVGIf4TIetWxAa1Bg%3D)	


**Note:** If you receive an error message **There may be a version mismatch between this computer and the destination server or VHD** once you select the **Remote Access** checkbox on the **Server Roles** page of the **Add Roles and Features Wizard**, clear the checkbox, click **Next**, click **Previous** and select the **Remote Access** checkbox again.	

5.	Within the Remote Desktop session to **az1000401-vm2**, from Server Manager, start the **Routing and Remote Access** console.	

6.	In the **Routing and Remote Access** console, run **Routing and Remote Access Server Setup Wizard**, use the **Custom configuration** option, enable **LAN routing**, and start **Routing and Remote Access** service.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/71.png?st=2019-09-17T12%3A31%3A17Z&se=2025-09-18T12%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KUH27h7rQ72U%2B%2FObj1OGbIkeQXSq3%2FZvYNMtytB5VNA%3D) 	

7.	Within the Remote Desktop session to **az1000401-vm2**, start the **Windows Firewall with Advanced Security** console and enable **File and Printer Sharing (Echo Request - ICMPv4-In)** inbound rule for all profiles.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/72.png?st=2019-09-17T12%3A31%3A46Z&se=2025-09-18T12%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=afgdJhxnEkxBXt7zhOx%2BJlpQaRdn1q3ukinwCYm%2BCCQ%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/73.png?st=2019-09-17T12%3A32%3A12Z&se=2025-09-18T12%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=efVtgXSTR1V3lEfbL75nNYM1d6wFOR%2F68zaWH6QLXsc%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/74.png?st=2019-09-17T12%3A32%3A43Z&se=2025-09-18T12%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kDQkG6%2BQiJsvWpOq5eJFAF1kE%2BYafPx6X%2Fouv6MvO9k%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/75.png?st=2019-09-17T12%3A33%3A04Z&se=2025-09-18T12%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vtCgmm62dtKU140Shu06zjC0AMtniPSP0yKrwE8QW8c%3D) 	

**Result**: After completing this exercise, you have implemented custom routing between peered Azure virtual networks.	

## Exercise 4: Validating service chaining	

The main tasks for this exercise are as follows:	

1.	Configure Windows Firewall with Advanced Security on the target Azure VM	

2.	Test service chaining between peered virtual networks	

### Task 1: Configure Windows Firewall with Advanced Security on the target Azure VM	

1.	In the Azure portal, navigate to the blade of the **az1000401-vm1** Azure VM.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/76.png?st=2019-09-17T12%3A33%3A23Z&se=2025-09-18T12%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nVoipPSn6XhkbDZrRA6tkW3UunCAbBIaUyGdfgFWEww%3D)	

2.	From the **Overview** pane of the **az1000401-vm1** blade, copy Public IP address use it to connect to **az1000401-vm1**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/77.png?st=2019-09-17T12%3A33%3A48Z&se=2025-09-18T12%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xUJngenjTTohoPBkXSEGTqFSMhP7pFroSLOsbaCitFE%3D)	

From console open the Remote Desktop Connection

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/97.png?st=2019-09-18T07%3A12%3A14Z&se=2025-09-19T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vKUJkZBkDv%2Fzlnia1yVQF9n0%2FRNV2E%2FVIEwbHCqPGX0%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/96.PNG?st=2019-09-18T07%3A14%3A38Z&se=2025-09-19T07%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sEH3awtONDU3rW5GtvcvE%2F8kCFDC8vEWHfMEzIOGRnU%3D)	

3.	When prompted, authenticate by specifying the following credentials:	

```

User name: adminuser	

Password: Password@1234

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/79.png?st=2019-09-17T12%3A34%3A35Z&se=2025-09-18T12%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Aswq6OQZ5Vv%2FYKkJftUVgKYihkYWiRNx%2FgZPTAESGhA%3D)	

4.	Within the Remote Desktop session to **az1000401-vm1**, open the **Windows Firewall with Advanced Security** console and enable **File and Printer Sharing (Echo Request - ICMPv4-In)** inbound rule for all profiles.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/80.png?st=2019-09-17T12%3A34%3A54Z&se=2025-09-18T12%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cyYSPuciXMDkoxTlPGSBLzJFQgCb2KfOc7Ur5eA96XU%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/81.png?st=2019-09-17T12%3A35%3A16Z&se=2025-09-18T12%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EuE5LPcATkVn3t6Rt%2FsoLGhD65UMYmJxknCmKMm9o8g%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/82.png?st=2019-09-17T12%3A35%3A34Z&se=2025-09-18T12%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=A6ErHkpd9Tq6M3R%2FKLunUwQwgoRH0mSvdpT3GeZ%2B5OY%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/83.png?st=2019-09-17T12%3A35%3A53Z&se=2025-09-18T12%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=astO5R8JBIqJVIIFcvMae9HPCQhAaQPl7Ibd1UnAbDk%3D) 	

### Task 2: Test service chaining between peered virtual networks	

1.	In the Azure portal, navigate to the blade of the **az1000402-vm3** Azure VM.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/84.png?st=2019-09-17T12%3A36%3A14Z&se=2025-09-18T12%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gD90hjfq7YQgwXWqWnRVam7gCBSya%2Bxu%2Bo6cvgvDPpw%3D)	

2.	From the **Overview** pane of the **az1000402-vm3** blade, generate an RDP file and use it to connect to **az1000402-vm3**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/85.png?st=2019-09-17T12%3A36%3A34Z&se=2025-09-18T12%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=q%2BMvkPDXffmzg94pd9jdXvql3vjAQCFpiVWREEkJj08%3D)	

3.	When prompted, authenticate by specifying the following credentials:

```

User name: adminuser	

Password: Password@1234

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/86.png?st=2019-09-17T12%3A36%3A56Z&se=2025-09-18T12%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hF%2BD7Aa7hFs1ZoJd5wlDsheElGqNmxD4X8dqg8aRhzY%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/87.png?st=2019-09-17T12%3A37%3A20Z&se=2025-09-18T12%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3G6VeLSKgzkvhWf%2Be%2F1%2ByJX9WJx8dyapREMtDbv%2B4Ew%3D)	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/88.png?st=2019-09-17T12%3A37%3A49Z&se=2025-09-18T12%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nDe5m%2B8UKtbXNtItbiBzS96fUVAlLdb4umVX7%2B7OIs4%3D)	

4.	Once you are connected to **az1-1000402-vm3** via the Remote Desktop session, start **Windows PowerShell**.	

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/89.png?st=2019-09-17T12%3A38%3A20Z&se=2025-09-18T12%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7DLWIfN%2FMU%2B3VqnpTH5tMwVVgmwiWFA2oIqc3%2FxP90M%3D)	

5.	In the **Windows PowerShell** window, run the following:	

`Test-NetConnection -ComputerName 10.104.0.4 -TraceRoute`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/lab5/90.png?st=2019-09-17T12%3A38%3A47Z&se=2025-09-18T12%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=N9ZiWJBVqKEyx2TcMUH3vbIUbiqMNoP3XDClSw5J%2Fug%3D)	

**Note: 10.104.0.4** is the IP address of the network interface of the first Azure VM **az1000401-vm1**	

6.	Verify that test is successful and note that the connection was routed over **10.104.1.4**	

**Note:** Without custom routing in place, the traffic would flow directly between the two Azure VMs.	

> **Result:** After you completed this exercise, you have validated service chaining between peered Azure virtual networks.	
