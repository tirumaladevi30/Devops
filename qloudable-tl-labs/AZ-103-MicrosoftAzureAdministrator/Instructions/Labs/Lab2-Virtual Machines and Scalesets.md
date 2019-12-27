# Virtual Machines and Scale Sets

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Prepare the Lab Environment](#exercise-1-prepare-the-lab-environment)

[Exercise 2: Configure Compute and Storage Resources of Azure VMs](#exercise-2-configure-compute-and-storage-resources-of-azure-VMs)

[Exercise 3: Configure Compute and Storage Resources of Azure VM Scale Sets](#exercise-3-configure-compute-and-storage-resources-of-azure-vm-scale-sets)


## Overview

The Aim of this Lab is about Deploying Azure Windows VM, Performing Scaling Operation on VM using Azure Portal and ARM Template. Also attaching Data disks and Configuring data volumes with in an Azure VM.

Deploying VM Scale Sets using Azure Portal and ARM Template. Performing Horizontal and Vertical Scaling operation on VM Scale Sets, attaching Data disks and Configuring data volumes in the Azure VM Scale Set.

### Scenario and Objective

**XYZ** Training Labs Corporation wants to scale Compute and Storage resources for workloads running on Azure VMs and Azure VM Scale Sets.

After completing this lab, you will be able to:

- Deploy Azure VMs and Azure VM Scale Sets by using Azure Resource Manager Templates

- Configure Compute and Storage resources of Azure VMs

- Configure Compute and Storage resources of Azure VM Scale Sets

## Pre-requisites

 - ARM Templates

 - PowerShell/CloudShell session

All tasks in this lab are performed from the Azure Portal (including a PowerShell Cloud Shell session)

**NOTE:** When not using Cloud Shell, the lab Virtual Machine must have the Azure PowerShell 1.2.0 module (or newer) installed https://docs.microsoft.com/en-us/powershell/azure/install-az-ps

## Exercise 1: Prepare the Lab Environment

The main tasks for this exercise are as follows:

1. Deploy an Azure VM by using an Azure Resource Manager Template

2. Deploy an Azure VM Scale Set by using an Azure Resource Manager Template

**VM Scale Sets**

Azure Virtual Machine Scale Sets let you create and manage a group of identical, load balanced VMs. The number of VM instances can automatically increase or decrease in response to demand or a defined schedule. Scale Sets provide high availability to your applications, and allow you to centrally manage, configure, and update many VMs.

1. Easy to create and manage multiple VMs

2. Provides high availability and application resiliency

3. Allows your application to automatically scale as resource demand changes

**ARM Templates**

Azure Resource Manager allows you to provision your applications using a declarative Template. In a single Template, you can deploy multiple services along with their dependencies. The Template consists of JSON and expressions that you can use to construct values for your deployment. Resource Manager provides a consistent management layer to perform tasks through Azure PowerShell, Azure CLI, Azure Portal, REST API, and client SDKs. 

Resource manager provides the following features:

* Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.

* Repeatedly deploy your solution through the development lifecycle and your resources are deployed in a consistent state.

* Manage your infrastructure through declarative Templates rather than scripts.

* Define the dependencies between resources so they're deployed in the correct order.

* Apply access control to all services in your resource group because Role-Based Access Control (RBAC) is natively integrated into the management platform.

* Apply tags to resources to logically organize all the resources in your subscription.

### Task 1: Deploy an Azure VM by using an Azure Resource Manager Template

1. From the lab after the chrome is opened and coonected then browse to the Azure Portal at http://portal.azure.com and sign in by using a Microsoft Account that has the Owner role in the Azure subscription you intend to use in this lab.

Using the Chrome browser, login into Azure Portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/1.png?st=2019-09-05T10%3A30%3A54Z&se=2021-09-06T10%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wqkoSsjnWGEMmARWgXaTiUgI8pAQV%2BsF7Q%2FL4XVBPMg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/2.png?st=2019-09-05T10%3A33%3A48Z&se=2021-09-06T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ayh3i1OYwooNh0Zux9AK4Lv2PBJGp2GJ%2FkCaKtACBcg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.png?st=2019-09-05T10%3A34%3A13Z&se=2021-09-06T10%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pxk3NjVqKDBaA%2BmQzzdkD84ew%2BwYo1WMFmeZrsONJKE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.1.png?st=2019-09-05T11%3A21%3A41Z&se=2021-09-06T11%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ujcp3ZNYYg4q%2BzC3hDB6M6OVvYDsus9wxpME1coauRw%3D)

2. In the Azure Portal, navigate to the Create a resource blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/4.png?st=2019-09-05T11%3A20%3A53Z&se=2021-09-06T11%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YRGl5kBFZ7qlcDogA0AdngSbtmk2tqE7uUkK5GIjaRA%3D) 

3. From the **Create a resource** blade, search Azure Marketplace for **Template deployment**, then select **Template deployment (deploy using customer Templates)**.
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/5.png?st=2019-09-05T11%3A25%3A48Z&se=2021-09-06T11%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hX5jO2wZNAEBB9fqzA8Quv48LQei8bwu0IevtoZraNY%3D) 

4. Click **Create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/6.png?st=2019-09-05T11%3A26%3A09Z&se=2021-09-06T11%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Z3VSy8ooaXVIrRDz9TWOHNquCQRrg5x8%2FyEk1C1%2F8SA%3D) 

5. On the **Custom deployment** blade, click the **Build your own Template in the editor** link. If you do not see this link, **click Edit Template** instead.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/7.png?st=2019-09-05T11%3A26%3A31Z&se=2021-09-06T11%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VvscnGBUTGZvoANedQSGWamL5SSROBL7nd6h85DYi8E%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/8.png?st=2019-09-05T11%3A26%3A54Z&se=2021-09-06T11%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J7BtzjiSyZ1Ef0c3dvj9U2FerRTEDOCEde%2Bqb8%2F22U4%3D) 

6. From the **Edit Template** blade, load the Template file **az-100-03b_01_azuredeploy.json**.

To load the file **az-100-03b_01_azuredeploy.json** into the Azure Portal copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

Now copy the Content in the URL and paste it in the **Edit Template** blade.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Virtual_Machines_and_Scale_Sets/az-100-03b_01_azuredeploy.json?st=2019-09-05T12%3A44%3A56Z&se=2021-09-06T12%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ewz3Rx2tLN740HqyzVfjFZ8Lfpq3EuaAEV2e0v%2Fz9iI%3D

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/9.png?st=2019-09-05T11%3A27%3A36Z&se=2021-09-06T11%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hRe%2FCF1%2FLq2IOQUfQNprrGgKiCrSzvOWjZqL%2F%2BYxGGw%3D) 

**Note:** Review the content of the Template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.

7. Save the Template and return to the **Custom deployment** blade.

8. From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/10.png?st=2019-09-05T11%3A28%3A25Z&se=2021-09-06T11%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0pXsf9CPiV2pITwIPjYu9YsroDjpXEyFLUcXTOwudVM%3D) 

9. From the **Edit parameters** blade, load the parameters file **az-100-03b_01_azuredeploy.parameters.json**.

To load the file **az-100-03b_01_azuredeploy.parameters.json** into the Azure Portal copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

Now copy the Content in the URL and paste it in the **Edit parameters** blade.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Virtual_Machines_and_Scale_Sets/az-100-03b_01_azuredeploy.parameters.json?st=2019-09-05T12%3A45%3A28Z&se=2021-09-06T12%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dOHoNkJMsdbeCJnfPCyUETsB1liGsITZ%2FsRZ1odZlfw%3D

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/11.png?st=2019-09-05T11%3A36%3A47Z&se=2021-09-06T11%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dO1eM6G3mFaX1zzDZUDedRDBazqtmzxlztBJnbktWbo%3D) 

10. Save the parameters and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/12.png?st=2019-09-05T11%3A36%3A08Z&se=2021-09-06T11%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rguh0Wut8UOayZrHZk8yz6TARwrq%2BtT1X6DJKqZWbL0%3D) 

11. From the **Custom deployment** blade, initiate a Template deployment with the following settings:

* **Subscription:** `select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Region:** `{{location}}` <br>
* **Vm Name:** `az1000301b-vm1` <br>
* **Vm Size:** `Standard_DS1_v2` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/13.png?st=2019-09-05T11%3A38%3A03Z&se=2021-09-06T11%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ifGj%2Fe5JlIHJTkbA1g2mqgWfeM50%2BhVlwN7Y8sWH%2F5g%3D) 

**Note:** To identify Azure regions where you can provision Azure VMs, refer to https://azure.microsoft.com/en-us/regions/offers/

**Note:** Do not wait for the deployment to complete but proceed to the next task of this exercise. You will use the Virtual Machine included in this deployment in the next exercise of this lab.

### Task 2: Deploy an Azure VM Scale Set by using an Azure Resource Manager Template

1. On the lab Virtual Machine, in the Azure Portal, navigate to the Create a resource blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/15.png?st=2019-09-05T11%3A39%3A17Z&se=2021-09-06T11%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cz7rt%2FFLcMiiGcZ%2FK%2F%2F6XynhnvxTYc2E74mOfGsitPA%3D) 

2. From the **Create a resource** blade, search Azure Marketplace for **Template deployment**, then select **Template deployment (deploy using customer Templates)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/16.png?st=2019-09-05T11%3A39%3A41Z&se=2021-09-06T11%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UCrOa%2Bzcn3p70Nx1eLdWx31gkmOszN3NQezl1zFSC38%3D) 

3. Click **Create**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/17.png?st=2019-09-05T11%3A39%3A59Z&se=2021-09-06T11%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JytwcDF499OxTXajEPd5GL%2FydTvpHiM3L9BdsmHlsXo%3D) 

4. On the **Custom deployment** blade, click the **Build your own Template in the editor** link. If you do not see this link, click **Edit Template** instead.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/18.png?st=2019-09-05T11%3A40%3A35Z&se=2021-09-06T11%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PTxO%2FFc5CcNlzVUj3w7wFD7ugQNH%2FBK7rjHt44mKzlA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/19.png?st=2019-09-05T11%3A40%3A57Z&se=2021-09-06T11%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IepfH56R%2FGYLbzOzSU5vSPkbaUK3fEM%2FyN0PDh7FAyo%3D) 

5. From the **Edit Template** blade, load the Template file **az-100-03b_02_azuredeploy.json**.

To load the file **az-100-03b_02_azuredeploy.json** into the Azure Portal copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

Now copy the Content in the URL and paste it in the **Edit Template** blade.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Virtual_Machines_and_Scale_Sets/az-100-03b_02_azuredeploy.json?st=2019-09-05T12%3A45%3A46Z&se=2021-09-06T12%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PN9hri1fiFL0vQruYgcZ0eZ10fGuMCK54sQHY%2F3inIQ%3D

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/20.png?st=2019-09-05T11%3A42%3A16Z&se=2021-09-06T11%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4C8NGXbQ6%2B7VsltdYKMG%2FWsAWoGYaSs%2FJsMDzeWc0iU%3D) 

**Note:** Review the content of the Template and note that it defines deployment of an Azure VM Scale Set hosting Windows Server 2016 Datacenter.

6. Save the Template and return to the **Custom deployment** blade.

7. From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/21.png?st=2019-09-05T11%3A43%3A09Z&se=2021-09-06T11%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BSjdrmWz1ji%2BHeu11HCbYwKrCChuZQmvGU%2Fs%2BD%2B52hM%3D) 

8. From the **Edit parameters** blade, load the parameters **file az-100-03b_02_azuredeploy.parameters.json**.

To load the file **az-100-03b_02_azuredeploy.parameters.json** into the Azure Portal copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

Now copy the Content in the URL and paste it in the **Edit parameters** blade.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_02/Virtual_Machines_and_Scale_Sets/az-100-03b_02_azuredeploy.parameters.json?st=2019-09-05T12%3A46%3A06Z&se=2021-09-06T12%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FzgflVEUuXLNvGM6%2FMw7khbQdsMtrvQWppBy15j6gc0%3D

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/22.png?st=2019-09-05T11%3A43%3A27Z&se=2021-09-06T11%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tGuc%2FqE0BTFas9opBc7wyz9vqdRxVxQps6I2pJNK6Ik%3D) 

9. Save the parameters and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/23.png?st=2019-09-05T11%3A43%3A46Z&se=2021-09-06T11%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Vi%2BpU0NOV6YNLlPI3avMHxDQLgWijDsFIvxLKYeY5Rc%3D) 

10. From the **Custom deployment** blade, initiate a Template deployment with the following settings:

* **Subscription:** `select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vmss Name:** `az1000302bvmss1` <br>
* **Vm Size:** `Standard_DS1_v2` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234` <br>
* **Instance Count:** `1`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/24.png?st=2019-09-05T11%3A44%3A08Z&se=2021-09-06T11%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OSSQefuPZhwJJXelg%2FWwFmrB12QUbQlH%2F5DE1ruBv6k%3D) 

**Note:** Do not wait for the deployment to complete but proceed to the next exercise. You will use the Virtual Machine Scale Set included in this deployment in the last exercise of this lab.

**Result:** After you completed this exercise, you have initiated a Template deployment of an Azure VM **az1000301b-vm1** and an Azure VM Scale Set **az1000302bvmss1** that you will use in the next exercise of this lab.

## Exercise 2: Configure Compute and Storage Resources of Azure VMs

The main tasks for this exercise are as follows:

1. Scale Vertically Compute resources of the Azure VM by using the Azure Portal

2. Scale Vertically Compute resources of the Azure VM by using an ARM Template

3. Attach data disks to the Azure VM

4. Configure data volumes within an Azure VM

### Task 1: Scale Vertically Compute resources of the Azure VM by using the Azure Portal

1. From the lab Virtual Machine, in the Azure Portal, navigate to the **ResurceGroup** resource group blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/25.png?st=2019-09-05T11%3A44%3A47Z&se=2021-09-06T11%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xl0FiTKOvUiP0GWjULkKX4WgnSlusL18NPrnmO9EMX0%3D) 

2. From the {{resource-group-name}} resource group blade, navigate to the **az1000301b-vm1** Virtual Machine blade

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/26.png?st=2019-09-05T11%3A46%3A17Z&se=2021-09-06T11%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xayF%2B%2ByT40Qx0biEnpNp1M%2FMr38T1KyLxPbVykhJbNU%3D) 

3. From the **az1000301b-vm1** Virtual Machine blade, navigate to the **Size** Virtual Machine blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/27.png?st=2019-09-05T11%3A46%3A41Z&se=2021-09-06T11%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KhVd803ttb1PD1mVi5yavwuhyxSeDfWQflZcXDvmqLM%3D) 

4. From the **az1000301b-vm1 - Size** Virtual Machine blade, increase the size of the Virtual Machine to **DS3_v2 Standard**, and then click **Resize**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/28.png?st=2019-09-05T11%3A47%3A13Z&se=2021-09-06T11%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xXRgj9q4KMAnKbDGQe7PnWQ8YNMVdDvw9rOoP7t7v5M%3D) 

**Note:** If this size is not available, choose another size. To identify Azure VM sizes that you can choose from, refer to https://azure.microsoft.com/en-us/global-infrastructure/services/

**Note:** Keep in mind that resizing an Azure VM requires restarting its operating system.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/29.png?st=2019-09-05T11%3A48%3A19Z&se=2021-09-06T11%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2UtsAF9xh5H5aw7q%2B%2Fdi5wCtUYJdUsBBx%2FWh%2FnhcXnk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/30.png?st=2019-09-05T11%3A48%3A39Z&se=2021-09-06T11%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6JtxxdkQizrQCLjCx1SpvRx%2FDBw19WdP9ClEAkUTTSY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/31.png?st=2019-09-05T11%3A48%3A51Z&se=2021-09-06T11%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=26Ls0zrAmllSmrXKxVflGKJuq9zK2dwmZZTDmjgC3lI%3D)

### Task 2: Scale Vertically Compute resources of the Azure VM by using an ARM Template

1. From the lab Virtual Machine, in the Azure Portal, navigate to the **ResourceGroup** resource group blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/25.png?st=2019-09-05T11%3A44%3A47Z&se=2021-09-06T11%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xl0FiTKOvUiP0GWjULkKX4WgnSlusL18NPrnmO9EMX0%3D) 

2. From the {{resource-group-name}} resource group blade, navigate to the **{{resource-group-name}} - Deployments** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/32.png?st=2019-09-05T11%3A54%3A34Z&se=2021-09-06T11%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9%2Fa4YtmnWkJDu40vxLaqmowhGE3LuUsWxyGYJEwSopk%3D) 

3. From the **{{resource-group-name}} - Deployments** blade, navigate to the **Microsoft.Template - Overview** blade showing the most recent successful deployment.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/33.png?st=2019-09-05T11%3A55%3A13Z&se=2021-09-06T11%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OXAE6jbDWolLIJEg76HdJU60mCtXYKLq6SotXaxRgH8%3D) 

4. On the **{{resource-group-name}} - Deployments** blade, use the **Redeploy** option to navigate to the **Custom deployment** blade.

5. From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/34.png?st=2019-09-05T11%3A56%3A57Z&se=2021-09-06T11%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F9XbvzKnSC5MmCWs%2FaoapVlPfXWzJ35H3zjFlxEhN0I%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/35.png?st=2019-09-05T11%3A57%3A37Z&se=2021-09-06T11%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aZd0QAd4qEkXQrPZVN9YN6i4MJ%2BothvmH3tbBcL%2FQ4Q%3D) 

6. On the **Edit parameters** blade, review the values of the original parameters used for the most recent successful deployment.

**Note:** The value of the **adminPassword** parameter is null because that parameter has the **securestring** data type.

7. Save the parameters and return to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/34.0.png?st=2019-09-05T12%3A00%3A12Z&se=2021-09-06T12%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sxFjlk5xvgD3twyxxBzDDVC0qa5Vinnplcb7iiGRlg0%3D) 

8. From the **Custom deployment** blade, initiate a Template deployment with the following settings:

* **Subscription:** `select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vm Name:** `az1000301b-vm1` <br>
* **Vm Size:** `Standard_DS2_v2` <br>
* **Admin Username:** `adminuser` <br>
* **Admin Password:** `Password@1234`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/36.png?st=2019-09-05T12%3A02%3A05Z&se=2021-09-06T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lQw2t%2BRcpfiuUTom8CsMB%2BPRoImgxZxaQGfmwQ8SMuA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/37.png?st=2019-09-05T12%3A03%3A48Z&se=2021-09-06T12%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5DC3NHI7VwcFnUBl7tMsSX8OiJ2Db5bDp6SWZqZcQkk%3D)

**Note:** Wait for the deployment to complete before you proceed to the next task of this exercise. The deployment will change the size of the Azure VM back to its original value, effectively scaling it down

### Task 3: Attach data disks to the Azure VM

1. In the Azure Portal, navigate to the **az1000301b-vm1** Virtual Machine blade.

2. From the **az1000301b-vm1** Virtual Machine blade, navigate to the Disks blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/38.png?st=2019-09-05T12%3A04%3A12Z&se=2021-09-06T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OXkvrnLE8MpljGeJP9Tvp7Q41yD6cJX3Uy6KQVKpyeU%3D) 

3. From the **az1000301b-vm1 - Disks** blade, use the **+ Add data disk** then Under **Name** there you have a dropdown option to choose **Create disk**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/39.png?st=2019-09-05T12%3A04%3A55Z&se=2021-09-06T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ziu%2FMT0ulrSe4NnzqISGuE1dQdcj62Mo5EA3jllTxOA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/40.png?st=2019-09-05T12%3A05%3A27Z&se=2021-09-06T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3vS%2FmAnT8yuH7gpD3IkpZs6TYVrza9f9NG5IibYyhaI%3D) 

4.	From the **Create managed disk** blade, create a new data disk with the following settings

* **Name:** `az1000301b-vm1-DataDisk0` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Account type:** `Standard HDD` <br>
* **Source type:** `None (empty disk)` <br>
* **Size (GiB):** `1023`

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/41.png?st=2019-09-05T12%3A05%3A56Z&se=2021-09-06T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rkbtsjYJiHBRENs1O1%2FGM2JbPK1tNC8vYU4wy58TctQ%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/42.png?st=2019-09-05T12%3A06%3A23Z&se=2021-09-06T12%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wEIBSy1Xr5JY3YwtCOlTovC%2FIJjQiFq5xMgcx0jr1mc%3D)

5. Back on the **az1000301b-vm1 - Disks** blade, configure the following settings for the newly created disk:

```
LUN: 0
HOST CACHING: None

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/43.png?st=2019-09-05T12%3A06%3A52Z&se=2021-09-06T12%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1IVS0Vj4e5myEBqN4tC4wZ4dPke5MeBs1sjmZx19Ruk%3D) 

6. From the **az1000301b-vm1 - Disks** blade, use the **+ Add data disk** option then click **Create disk**.

7. From the **Create managed disk** blade, create a new data disk with the following settings:

Do the same procedure as mentioned in point No 4 and 5.

* **Name:** `az1000301b-vm1-DataDisk1` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Account type:** `Standard HDD` <br>
* **Source type:** `None (empty disk)` <br>
* **Size (GiB):** `1023`

8. Back on the **az1000301b-vm1 - Disks** blade, configure the following settings for the newly created disk:

```
LUN: 1
HOST CACHING: None

```

Click **Save**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/44.png?st=2019-09-05T12%3A07%3A56Z&se=2021-09-06T12%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dGtv54UA1Qrmo6plJwGsaA1s0QFtuPuTAr1jL%2BcJmps%3D) 

### Task 4: Configure data volumes within an Azure VM

1. In the Azure Portal, navigate to the **az1000301b-vm1** blade.
2. From the **az1000301b-vm1** blade, connect to the Azure VM via the RDP protocol and, when prompted to sign in, provide the following credentials:

```
Admin Username: adminuser
Admin Password: Password@1234 

```

Open RDP from the search box of the lab Virtual Machine.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/46.png?st=2019-09-05T12%3A10%3A27Z&se=2021-09-06T12%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tJ1o3E79eUYv7D%2Fk89sF6YR93lZqDXT7FpMY1lmffpk%3D) 

Copy the **az1000301b-vm1** public-ip from Azure Portal and paste it in the RDP prompt under Computer property then click **connect**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/45.png?st=2019-09-05T12%3A09%3A56Z&se=2021-09-06T12%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hs2koYEwKf4RuIoNIGFhKY9j7gbv%2BRuK5gxdWyG6WRg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/47.png?st=2019-09-05T12%3A11%3A01Z&se=2021-09-06T12%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LZ1HqT38W%2FP9CM7cnusP8k5oTdOM1k6Xxdqc1uU5Lqw%3D) 

Provide the **Username** and **Password** of the **az1000301b-vm1** and click **OK**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/48.png?st=2019-09-05T12%3A11%3A49Z&se=2021-09-06T12%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h3wGzdOxZ4jf3lnKs25CIrWEMRC84Xs%2FTrzLz%2Bbtkhw%3D) 

Click **Yes**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/49.png?st=2019-09-05T12%3A12%3A04Z&se=2021-09-06T12%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Di7ub321vZJYmOn1b8de2Et9GHzDnZiR9RVad0sF5iE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/50.png?st=2019-09-05T12%3A12%3A27Z&se=2021-09-06T12%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Qw9TOO9dwfTPte9mUAPsQnJhZqwtvXj8qMKlyXSIQCY%3D)
 
3. Within the RDP session, in Server Manager, navigate to **File and Storage Services**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/51.png?st=2019-09-05T12%3A13%3A07Z&se=2021-09-06T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s5HwsxkAIX7DFhthyuvap6j8kvDhFUG4Et1lWyjMjFo%3D) 

4. Cick **Storage Pools**, then right-click the **Primordial** Storage, and click New **Storage Pool**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/52.png?st=2019-09-05T12%3A13%3A37Z&se=2021-09-06T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dc3lskfubVRq%2FA%2FnyKQVc2D%2BT7DK1wZB7RhqHg2U8j0%3D) 

5. Use the New Storage Pool Wizard to create a new Storage pool named **StoragePool1** consisting of two disks you attached in the previous task

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/53.png?st=2019-09-05T12%3A13%3A58Z&se=2021-09-06T12%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xQT1fDY9Xyu5mS26RapgzPqtE0WluRF5jTFiGJGfNQs%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/54.png?st=2019-09-05T12%3A14%3A15Z&se=2021-09-06T12%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2fzz6wxN1xZsA%2BcJJ%2BYfcYqshDP4DRwMJIctVxs3VL0%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/55.png?st=2019-09-05T12%3A14%3A33Z&se=2021-09-06T12%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Xm4V7wiONZvTmqWFewqIaCjwfi7wskxg%2BotZyHHvTuw%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/56.png?st=2019-09-05T12%3A14%3A54Z&se=2021-09-06T12%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PgikBqCD2gH0ELzlGBIoeOOAe6cvYLtFWE5R6Ygo3Js%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/57.png?st=2019-09-05T12%3A15%3A09Z&se=2021-09-06T12%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3OrYyTFZrhS4ctJSFP06BO7rVVGKmNax6dPD1lPB2cQ%3D) 

6. On the **Results** page, place a checkmark next to **Create a virtual disk when this wizard closes**, and then click **Close**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/58.png?st=2019-09-05T12%3A15%3A47Z&se=2021-09-06T12%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LyMcibthahFEagyw0ymUfaY4Fs6gS2PegYZBoWhFh%2FU%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/59.png?st=2019-09-05T12%3A16%3A03Z&se=2021-09-06T12%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1%2BXbMLmJ10DG3OXOI9VTkADbYOSzZPl%2FD4NpFimLpFM%3D) 

7.	Use the New Virtual Disk Wizard to create a new virtual disk named **VirtualDisk1** with the following settings:

```
Enclosure Awareness: Disabled
Storage layout: Simple
Provisioning: Fixed
Size: Maximum size

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/60.png?st=2019-09-05T12%3A16%3A24Z&se=2021-09-06T12%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RVzhqUWmO%2FMgbhRAyllf9wWM2cuDIWVf07utI0Qh%2FHk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/61.png?st=2019-09-05T12%3A17%3A00Z&se=2021-09-06T12%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Xyoc3aIEkv9JkiUtowjU40lwcrEMVA3rPQZeaHn8eG0%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/62.png?st=2019-09-05T12%3A17%3A16Z&se=2021-09-06T12%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VzLyHghtbQyTlViviaJxwqf0aIp5N1EJKJDosqkavzM%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/63.png?st=2019-09-05T12%3A17%3A34Z&se=2021-09-06T12%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RD%2BIDlKnPlcWmcy%2FBEE7Z%2BSsZSSDn%2FzV0Ubm%2FSooUm8%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/64.png?st=2019-09-05T12%3A17%3A51Z&se=2021-09-06T12%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ee3rb2y8IDyCKENPRvIiLo8uzNPOZZmqxGzeOf501Bw%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/65.png?st=2019-09-05T12%3A18%3A07Z&se=2021-09-06T12%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=N6n0Xy0Y5F1JSo4FH1G02qhcMB02No9WIBKKxNqLv7I%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/66.png?st=2019-09-05T12%3A18%3A25Z&se=2021-09-06T12%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hE0rXuBP5vVX4I%2B7FTxdzEo%2Bnhpq9LQNnIV%2BgD6zfpg%3D) 

8. On the **Results** page, place a checkmark next to **Create a volume when this wizard closes**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/67.png?st=2019-09-05T12%3A19%3A01Z&se=2021-09-06T12%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aCUJEVXVjqPW8m2ccQQKXb7jB7ubOFd2YvQRl6Ofutg%3D) 

```
Drive letter: F

File system: NTFS

Allocation unit size: Default

Volume label: Data

```
**Result:** After you completed this exercise, you have scaled Vertically Compute resources of the Azure VM by using the Azure Portal and by using an ARM Template, attached data disks to the Azure VM, and configured data volumes within an Azure VM.  

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/68.png?st=2019-09-05T12%3A20%3A13Z&se=2021-09-06T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oEugE7sq3RcPKVxxCKkJGtb8hAwyA1FF6eni4hpJvpQ%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/69.png?st=2019-09-05T12%3A20%3A57Z&se=2021-09-06T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YKnIyK91yEauqJMz1P0oG%2FmCEi%2FZ7%2FrrqnMi1I3zRmk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/70.png?st=2019-09-05T12%3A21%3A12Z&se=2021-09-06T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SxF8qBSoLDNo32wVAMxc5cezlwJkgQZgOKgZwSoBIUk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/71.png?st=2019-09-05T12%3A21%3A31Z&se=2021-09-06T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Tqz6OqD73UVUBZEWAkx6PpeFCGZ33r2a3QAEPAnSr70%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/72.png?st=2019-09-05T12%3A21%3A46Z&se=2021-09-06T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JpLiYhxsjG1VZZXYUJSSMPcC2D2xgVcFNUS5F1up3d8%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/73.png?st=2019-09-05T12%3A22%3A01Z&se=2021-09-06T12%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6jeJv9Hbuhj3%2BiX%2FPC7wCgk5HHE2g6IDNdkDA67qpvk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/74.png?st=2019-09-05T12%3A22%3A16Z&se=2021-09-06T12%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xsZa1BK0zN5NwrG9G8HU6Cigxy%2Bh8GIQwPc%2FX0lQSI8%3D) 

## Exercise 3: Configure Compute and Storage Resources of Azure VM Scale Sets

The main tasks for this exercise are as follows:

1. Scale Vertically Compute resources of the Azure VM Scale Set by using an Azure Resource Manager Template

2. Attach data disks to the Azure VM Scale Set

3. Configure data volumes in the Azure VM Scale Set

4. Scale Horizontally Compute resources of the Azure VM Scale Set

### Task 1: Scale Vertically Compute resources of the Azure VM Scale Set by using an Azure Resource Manager Template

1. From the lab Virtual Machine, in the Azure Portal, navigate to the **ResourceGroup** resource group blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/25.png?st=2019-09-05T11%3A44%3A47Z&se=2021-09-06T11%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xl0FiTKOvUiP0GWjULkKX4WgnSlusL18NPrnmO9EMX0%3D)

2. From the {{resource-group-name}} resource group blade, navigate to the **{{resource-group-name}} - Deployments** blade.
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/75.png?st=2019-09-05T12%3A26%3A27Z&se=2021-09-06T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IH4haAxn8cxPfD9d4AcULbXl%2BTQBzDGdAXe75Q34yuE%3D) 

3. From the **{{resource-group-name}} - Deployments** blade, navigate to the **Microsoft.Template - Overview** blade showing the most recent successful deployment.
4. On the **{{resource-group-name}} - Deployments** blade, use the **Redeploy** option to navigate to the **Custom deployment** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/76.png?st=2019-09-05T12%3A27%3A08Z&se=2021-09-06T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OVzOCFIxBFg7AuUTBkem8p%2BI3gVLWg%2BokOoHnpS2kb0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/77.png?st=2019-09-05T12%3A27%3A28Z&se=2021-09-06T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AxjuPsN%2BKfJ0x3tTOmQCafXXgnjRfQh%2Fu4PQZd4wc7k%3D) 

5. From the **Custom deployment** blade, initiate a Template deployment with the following settings:

* **Subscription:** `select the default` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Vm Name:** `az1000302bvmss1` <br>
* **Vm Size:** the name of the VM size you used to scale up the Azure VM in the previous exercise of this lab`(Standard_DS3_v2)` <br>
* **Admin Username:** `adminuser` <br>	
* **Admin Password:** `Password@1234`

> **Note:** Wait for the deployment to complete before you proceed to the next task of this exercise. The deployment will increase the size of Azure VM instances of the Azure VM Scale Set.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/78.png?st=2019-09-05T12%3A28%3A02Z&se=2021-09-06T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h3t6XA2OROYRAYEOBPx0B%2FaxXy3GD461nqdpYj9sXLM%3D) 
	 
6. In the Azure Portal, navigate to the **az1000302bvmss1** blade and verify that the size of the VM instances of the VM Scale Set has changed.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/78.0.png?st=2019-09-05T12%3A31%3A08Z&se=2021-09-06T12%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hpIe8ACs1V5LoNpR%2Bwkj%2FswO6NGyr0WHO79tZ7V4ZvM%3D) 

### Task 2: Attach data disks to the Azure VM Scale Set

1. From the Azure Portal, start a PowerShell session in the Cloud Shell.

**Note:** If this is the first time you are launching the Cloud Shell in the current Azure subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a Storage Account in an automatically generated resource group.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/79.png?st=2019-09-05T12%3A31%3A48Z&se=2021-09-06T12%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hAIsFl2ZXBnw6kYK6iplFeKfNFWOe6mUBQneDgHq4IQ%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/80.png?st=2019-09-05T12%3A32%3A23Z&se=2021-09-06T12%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w1mPxCdl5HVVX%2FRfYBlgbApN4LKq7m7FLMg3sfzygrY%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/81.png?st=2019-09-05T12%3A32%3A44Z&se=2021-09-06T12%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Rg2y068LFhO5YazAgfkc5VIoii0ULFsFCt5rkhSkRbE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/81.0.png?st=2019-09-05T12%3A34%3A14Z&se=2021-09-06T12%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FeFMEAKFm4CFCrTXVxpk%2FGeKTA07KC2SW0fnEc5HoBI%3D) 
 
2. In the Cloud Shell pane, run the following in order to attach one 128 GB disk to each VM instance in the VM Scale Set:

```
$vmss = Get-AzVmss -ResourceGroupName '{{ ResourceGroup }}' -VMScaleSetName 'az1000302bvmss1'

Add-AzVmssDataDisk -VirtualMachineScaleSet $vmss -CreateOption Empty -Lun 1 -DiskSizeGB 128 -StorageAccountType 'Standard_LRS'
	
Update-AzVmss -ResourceGroupName $vmss.ResourceGroupName -VirtualMachineScaleSet $vmss -VMScaleSetName $vmss.Name 

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/82.png?st=2019-09-05T12%3A34%3A58Z&se=2021-09-06T12%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Emkj1TzVSYagnsZ2TwBQpZmt%2BUZ3UFKSiGb5f%2B3%2BYQA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/83.png?st=2019-09-05T12%3A35%3A20Z&se=2021-09-06T12%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=x0IfALIGuAomgPviGfxC5IFxfggenOxV9fzrwhBd%2BDw%3D) 

7. In the Azure Portal, navigate to the **Storage** blade of the az1000302bvmss1 Scale Set and verify that the data disk has been added.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/84.png?st=2019-09-05T12%3A36%3A25Z&se=2021-09-06T12%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C0R691cb4H%2B7wZTfZyeNjmjesUYH7x4a%2Bjf2iDFcck4%3D) 

### Task 3: Configure data volumes in the Azure VM Scale Set

1. In the Cloud Shell pane, run the following in order to configure a simple volume on the newly added disk by using Custom Script Extension:

```
$vmss = Get-AzVmss -ResourceGroupName '{{ ResourceGroup }}' -VMScaleSetName 'az1000302bvmss1'

$publicSettings = @{"fileUris" = (,"https://raw.githubusercontent.com/Azure-Samples/compute-automation-configurations/master/prepare_vm_disks.ps1");"commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File prepare_vm_disks.ps1"}

Add-AzVmssExtension -VirtualMachineScaleSet $vmss -Name "customScript" -Publisher "Microsoft.Compute" -Type "CustomScriptExtension" -TypeHandlerVersion 1.8 -Setting $publicSettings  

Update-AzVmss -ResourceGroupName $vmss.ResourceGroupName -VirtualMachineScaleSet $vmss -VMScaleSetName $vmss.Name

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/85.png?st=2019-09-05T12%3A38%3A05Z&se=2021-09-06T12%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NuoElggmMrN5jRvj97tIk4mVBhantjyofAI8iQ10O%2F0%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/86.png?st=2019-09-05T12%3A38%3A23Z&se=2021-09-06T12%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2VnqOSPR29AR9eCCFTY5QDogwjn%2BJOCbnPnFMX3I944%3D) 

**Note:** To confirm that the volume has been configured, you will connect to the VM instance in the VM Scale Set via RDP.

8. To identify the public IP address of the Azure load balancer in front of the VM Scale Set, in the Azure Portal, navigate to the **az1000302bvmss1** blade and note the value of the **Public IP address** entry.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/87.png?st=2019-09-05T12%3A38%3A51Z&se=2021-09-06T12%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rIGRJPPzAKW0OfgZ2PDcaHn68vXxii0MUAzdyAI2CMw%3D) 

9. To identify the port on which you should connect, navigate to the {{resource-group-name}} resource group blade.

10. From the {{resource-group-name}} resource group blade, navigate to the **az1000302bvmss1-lb** load balancer blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/88.png?st=2019-09-05T12%3A39%3A07Z&se=2021-09-06T12%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4W1ClYydOda8ZPwQ7b31b1T%2FEIFIVBCFPEsdMjDt%2FAk%3D) 

11. On the **az1000302bvmss1-lb** load balancer blade, note that the value of the **Public IP address** setting matches the value of the IP address used by the VM Scale Set you identified earlier in this task.

12. From the **az1000302bvmss1-lb** load balancer blade, navigate to the **az1000302bvmss1-lb - Inbound NAT rules** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/89.png?st=2019-09-05T12%3A39%3A40Z&se=2021-09-06T12%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Gg3aUrd8LK40EX%2BSsGM4276dFJZO%2BDWFxBYny8D3L3o%3D) 

13. From the **az1000302bvmss1-lb - Inbound NAT rules** blade, navigate to the natpool.0 blade and note that the port mappings start with **50000**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/90.png?st=2019-09-05T12%3A40%3A13Z&se=2021-09-06T12%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pktvg6fRxeV%2FiQw8zYCaapnWPFVdzyPOafcT9vFs%2F6o%3D) 

14. From the lab Computer, initiate the Remote Desktop Connection to the first VM instance in the VM Scale Set by running the following settings.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/91.png?st=2019-09-05T12%3A41%3A45Z&se=2021-09-06T12%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=20QS0oAl6OqwsVuPXR1VsFmgMdHQWgIW07pzXxaKfzk%3D) 
 
16.	When prompted to sign in via RDP to a VM instance of the VM Scale Set, provide the following credentials:

```
Admin Username: adminuser	
Admin Password: Password@1234

```
**Note:** Ignore any messages regarding signing in with temporary profile.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/92.png?st=2019-09-05T12%3A42%3A12Z&se=2021-09-06T12%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mJp11dHStd%2B8fj5JBVy911a4jAyn54KxBR2VFDxEG8U%3D) 

17. Within the RDP session, launch File Explorer and verify that the VM has an extra volume of 127 GB in size with F: drive letter assigned to it.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/93.png?st=2019-09-05T12%3A42%3A56Z&se=2021-09-06T12%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FXK5L0Qt%2BBqA0jsRKc5cefuHAcY%2FJvWgpPEaB5ert9U%3D) 

18. Sign out from the RDP session.

### Task 4: Scale Horizontally Compute resources of the Azure VM Scale Set

1. From the lab Virtual Machine, in the Azure Portal, navigate to the **az1000302bvmss1** VM Scale Set blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/94.png?st=2019-09-05T12%3A43%3A18Z&se=2021-09-06T12%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BUNeV%2BXfDpRATq5DKtdHQK92t23QusyGknXyKlFfNZ4%3D) 

2. From the **az1000302bvmss1** VM Scale Set blade, navigate to the **Scaling** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/95.png?st=2019-09-05T12%3A43%3A34Z&se=2021-09-06T12%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8ieKuT7nB64001JkUcmVuPmHgwzYGtyxT3Bdo%2FnMNog%3D) 
 
3. On the **az1000302bvmss1 - Scaling** blade, use the **Override condition** setting to increase the instance count to 2.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/96.png?st=2019-09-05T12%3A44%3A05Z&se=2021-09-06T12%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0dUhsCIos3fIGk3wa87%2B9hQHKVeyPr1kifAihc%2BHfbA%3D) 

4. Navigate to the **az1000302bvmss1 - Instances** blade and verify that the number of instances has increased to 2.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/97.png?st=2019-09-05T12%3A44%3A20Z&se=2021-09-06T12%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6fiPsp3lIxYN1tE3qAwpCR7wVqQSk7mGhYJiVWbRJPQ%3D) 

**Note:** You might need to refresh the display on the **az1000302bvmss1 - Instances** blade to view the process of provisioning the additional instance.

**Result:** After you completed this exercise, you have scaled Vertically Compute resources of the Azure VM Scale Set by using an Azure Resource Manager Template, attached data disks to the Azure VM Scale Set, configured data volumes in the Azure VM Scale Set, and scaled Horizontally Compute resources of the Azure VM Scale Set.
