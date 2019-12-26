# Lab: Building Azure IaaS-Based Server Applications by using Azure Resource Manager Templates and Azure Building Blocks.

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Deploy an Azure VM by using Azure Resource Manager templates with PowerShell Desired State Configuration extension from the Azure portal](#exercise-1-deploy-an-azure-vm-by-using-azure-resource-manager-templates-with-powershell-desired-state-configuration-extension-from-the-azure-portal)

[Exercise 2: Deploy an Azure Virtual Machine Scale Set by using Azure Resource Manager templates with PowerShell Desired State Configuration extension from the Azure portal](#exercise-2-deploy-an-azure-virtual-machine-scale-set-by-using-azure-resource-manager-templates-with-powershell-desired-state-configuration-extension-from-the-azure-portal)

[Exercise 3: Deploy Azure VMs running Windows Server 2016 and Linux by using Azure Building Blocks with PowerShell Desired State Configuration extension from the Azure Cloud Shell](#exercise-3-deploy-azure-vms-running-windows-server-2016-and-linux-by-using-azure-building-blocks-with-powershell-desired-state-configuration-extension-from-the-azure-cloud-shell)

## Overview

 * Deploy the Windows server 2016 and Virtual Machine Scale Set with PowerShell Desired State Configuration (DSC) extension from the Azure portal.

 * Windows Server 2016 and Linux by using Azure Building Blocks with PowerShell Desired State Configuration (DSC) extension from the Azure Cloud Shell.

### Scenario and Objectives

XYZ training labs wants to Deploy IaaS-Based Server Applications

After completing this lab, you will be able to:

* Create a Windows server 2016.

* Create a Azure storage Account.

* Upload data to the Azure Storage.

* Create ARM template with PowerShell DSC extension 

* Create Virtual machine scale set with with PowerShell Desired State Configuration (DSC) extension from the Azure portal.

* Deploy  Windows Server 2016 and Linux by using Azure Building Blocks with PowerShell Desired State Configuration (DSC) extension from the Azure Cloud Shell.

## Pre-Requisites

* Azure Portal

* ARM Template

* Cloud Shell


## Exercise 1: Deploy an Azure VM by using Azure Resource Manager templates with PowerShell Desired State Configuration extension from the Azure portal

* ARM template

Azure Resource Manager (ARM) allows you to provision your applications using a declarative template. In a single template, you can deploy multiple services along with their dependencies. You use the same template to repeatedly deploy your application during every stage of the application life cycle. 

* Cloud Shell

Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources. Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.

* Desired State Configuration (DSC)

Desired State Configuration (DSC) is an essential part of the configuration, management and maintenance of Windows-based servers. It allows a PowerShell script to specify the configuration of the machine using a declarative model in a simple standard way that is easy to maintain and understand.

### Task 1: Open the Azure Portal

1. From the lab, after the chrome is opened and connected then browse to the Azure portal at http://portal.azure.com

Using the Chrome browser, login into Azure portal with the below details.

```

Azure Email: {{ Azure Portal Email }}

Azure Password: {{ Azure Portal Password }}

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/1.png?st=2019-09-20T05%3A31%3A27Z&se=2022-09-21T05%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TgTX8xshdKnRjeC%2FHZmJBNPV%2BjFooxBQyMkv4q0R5Mc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/2.png?st=2019-09-20T05%3A31%3A59Z&se=2022-09-21T05%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uSM1mICzhHj78cr2QZYyLHtbBsjO89j5hC5i5zxYqQ0%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/a1.png?st=2019-09-23T07%3A13%3A29Z&se=2022-09-24T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UgNVuBHtVulRYcSYFnMzwJDpTXhOikr%2FlHjkyBjdTUM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/a2.png?st=2019-09-23T07%3A14%3A32Z&se=2022-09-24T07%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BxNbm6dLdcavFsx6TM1%2F2Ra782T5lGw5zlzKjx2au9s%3D)

### Task 2: Create an Azure VM running Windows Server 2016 Datacenter.

1. In the upper left corner of the Azure portal, click **Create a resource**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/3.png?st=2019-09-20T05%3A32%3A22Z&se=2022-09-21T05%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=B3tXWyz1n3kfOfmfs5TFjcN7Cj0nZkH4JiG%2FcVA3XsM%3D)

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Windows Server** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Windows Server**.

4. On the **Windows Server** blade, select the **[smalldisk] Windows Server 2016 Datacenter** software plan, then click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/4.png?st=2019-09-20T05%3A32%3A43Z&se=2022-09-21T05%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zi34RW2kcFbE54ykAt0%2FhHqzhQPla9yNHseI7SPJsxw%3D)

5. On the **Basics** tab, perform the following tasks:

```

   Subscription: Select the default
    
   Resource group: {{ ResourceGroup }}
      
   Virtual Machine Name: lab03vm0

   Region: {{ Location }}
    
   Availability options: drop-down list, select Availability set

   In the **Availability set** section, click **Create new**, box, enter the value **lab03avset0**, set **Fault domains** to the maximum value, leave **Update domains** with its default value, and click **OK**.

    Image: drop-down list set to its default value.

    Size: Standard DS1 v2

    Username: Student

    Password: Password@1234
    
    Confirm Password: Password@1234
   
    Inbound port rules: select Allow selected ports option

    Select inbound ports: Http

    Already have a Windows license: No
    
```
    
  Click **Next: Disks >**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/5.png?st=2019-09-20T05%3A33%3A24Z&se=2022-09-21T05%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=feMcVA55PAHdntRcA8ZXAJY7e5Y0vhnWwxhFdgTy%2Bi4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/6.png?st=2019-09-20T05%3A33%3A44Z&se=2022-09-21T05%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nWP7ytuJ4kgkcLu0rnUc4GezvkdBgoN5pe68yZUS%2B4g%3D)

6. On the **Disks** tab, perform the following tasks:

```

     OS disk type:Standard HDD
     
```

   Click **Next: Networking >**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/7.png?st=2019-09-20T05%3A34%3A04Z&se=2022-09-21T05%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Qj5ObmfVBND7KVSuTAeZroOHJ1MZek3PcXY%2BBTaHn1E%3D)

7. On the **Networking** tab, perform the following tasks:

```

    Virtual network section, click Create new 
    
    - On the **Create virtual network** blade, specify the following settings and click **OK**:

     Name: lab03vnet0

     Address range: 10.3.0.0/16

     Subnet name: subnet-0

     Subnet address range: 10.3.0.0/24 and click OK

     Public IP:  entry set to its default value
    
     NIC network security group: Basic
    
     Public inbound ports: Allow selected ports
    
     inbound ports: HTTP

     Accelerated networking: entry set to its default value
    
```

   Click **Next: Management >**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/8.png?st=2019-09-20T05%3A34%3A32Z&se=2022-09-21T05%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yUZlzrC%2FcnI1mq6Shfy7FELs6kraLzZxUs2yw7N78cY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/9.png?st=2019-09-20T05%3A34%3A49Z&se=2022-09-21T05%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QiTJ9lm0NuCbmmKc4rmxgtb7cBePdctXiYNw2YIRZYQ%3D)

8. On the **Management** tab, perform the following tasks:

```

    Boot diagnostics: set to its default value.

    OS guest diagnostics: set to its default value.

    Diagnostics storage account: entry set to its default value.
    
    System assigned managed identity: option set to its default value.
    
    Enable auto-shutdown: option set to its default value.

    Enable backup: option set to its default value.
    
```

  Click the **Review + create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/10.png?st=2019-09-20T05%3A35%3A10Z&se=2022-09-21T05%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=b74g4Im1OYMvEPRuFhsvyJ5%2BZ%2B8oa2IQgser2YNuTls%3D)

9. On the **Create a virtual machine** blade, review the settings of your new virtual machine and click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/11.png?st=2019-09-20T05%3A35%3A27Z&se=2022-09-21T05%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IQRFbrVElRpNZoNV8D0Tth3C1y%2Be%2FQre6LEHXrdDz%2Fw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/12.png?st=2019-09-20T05%3A35%3A45Z&se=2022-09-21T05%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HL5riCC%2B%2BIb6UeOckvYrCiZltdx%2FQejnAFALbqD6k0M%3D)

10. Do not wait for the deployment to complete and proceed to the next task.

### Task 3: View DSC configuration

1. Open the below link in the Chrome, save it in folder and view the IISWebServer.zip.

```

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_02/LabFiles/Starter/IISWebServer.zip?st=2019-09-23T06%3A32%3A56Z&se=2022-09-24T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5ht%2BTU8GYL6I6Hd69Nb%2BRtGXXhc7N42liJbP08srDI0%3D

```

### Task 4: Create an Azure Storage account

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Storage account** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Storage account**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/13.png?st=2019-09-20T05%3A36%3A05Z&se=2022-09-21T05%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OatLN5rAmV8mckLtxrMvqu0rddLxyI95CM%2FBoQRah%2Bs%3D)

4. On the **Storage account** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/14.png?st=2019-09-20T05%3A36%3A25Z&se=2022-09-21T05%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6tLzaVhQ6zgoRr3ZcyPrgc7%2F6udyQ0%2BYKNU7q6qzvJE%3D)

5. On the **Create storage account** blade, perform the following tasks:

```

    Subscription: Select the default
    
    Resource group: {{ ResourceGroup }}

    Storage Account Name: type a unique name consisting of a combination of between 3 and 24 characters and digits.
    
    Location: {{ Location }}
    
    Performance: Standard
       
    Account kind: Storage (general purpose v1)
    
    Replication: Locally-redundant storage (LRS)
    
```

   Click the **Review + Create** button, and then click **Create**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/15.png?st=2019-09-20T05%3A36%3A43Z&se=2022-09-21T05%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=D6BbAL5v9ORKajKxnGBbN5%2F%2BL%2Fvdk9iAf12h%2FUA6tbY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/16.png?st=2019-09-20T05%3A37%3A02Z&se=2022-09-21T05%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EQ4%2F%2FHxnUZHH9%2B8ExkQTDPpE21CztxU8U8buRAd9Xbc%3D)

6. Wait for the deployment to complete before you proceed to the next task.


  **Note**: This operation can take about 2 minutes.

### Task 5: Upload DSC configuration to Azure Storage

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the resource group into which you deployed the storage account.

3. On the **{{ ResourceGroup }}** blade, click the entry representing the newly created storage account.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/17.png?st=2019-09-20T05%3A37%3A20Z&se=2022-09-21T05%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SEDkBLNlYcXB10L8ky7aosj6lvPnajxMaMCKyZve01E%3D)

4. With the **Overview** selection active, on the storage account blade, click **Blobs**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/18.png?st=2019-09-20T05%3A37%3A40Z&se=2022-09-21T05%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2L04c32oNNw2XxVBOK6%2Bcwhm4kvISTHBzakSZDitIfY%3D)

5. Click the **Container** button at the top of the blade.

6. In the **New container** pane that appears, specify the following settings and click **OK**:

  *  In the **Name** text box, enter the value **config**.

  * In the **Public access level** list, select the **Blob (anonymous read access for blobs only)** option.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/19.png?st=2019-09-20T05%3A38%3A02Z&se=2022-09-21T05%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dVBurhD5%2Bc4xy2AgZiW8huvYoal3TwO8lBhEzO413qo%3D)

7. Back on the **Blob service** blade, click the entry representing the new **config** container.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/20.png?st=2019-09-20T05%3A38%3A19Z&se=2022-09-20T18%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qeeyWsIo30wylpfOgqsTpx3YxXaM4ZrMOY7D%2FX9%2FekM%3D)

 8. open the below link in chrome and save it in folder

```

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_02/LabFiles/Starter/IISWebServer.zip?st=2019-09-23T06%3A32%3A56Z&se=2022-09-24T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5ht%2BTU8GYL6I6Hd69Nb%2BRtGXXhc7N42liJbP08srDI0%3D

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/76.PNG?st=2019-09-24T08%3A54%3A29Z&se=2022-09-25T08%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WSixpOD8AS5PyDj7cDQwEvqE7w6BtjtLB1elpskn0mQ%3D)

9. On the **config** blade, click the **Upload** button at the top of the blade.

10. In the **Upload blob** pane, perform the following tasks:


  * In the **Files** field, click the blue folder button to the right of the field.

  *  Select the **IISWebServer.zip** file.

  *  Click the **Open** button to close the dialog box and return to the **Upload blob** popup.

   *  Click the **Upload** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/21.png?st=2019-09-20T05%3A38%3A49Z&se=2022-09-21T05%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2j3D61XsVlZWqEvtke7bCpb1KyArS%2FS%2BrM44wUZ9bJM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/77.PNG?st=2019-09-24T08%3A58%3A31Z&se=2022-09-25T08%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jOuCL7urVYBTyAcg2bmutpy%2FR%2BmgXzQ3oVeqsf58fgY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/23.png?st=2019-09-20T05%3A39%3A24Z&se=2022-09-21T05%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HnqpTkK156v03E1Ia3gV2%2Fs%2FnB21QqThy4fPG5%2Be9gk%3D)

10. Navigate to the **config** blade and click the entry representing the **IISWebServer.zip** blob.

11. In the **Blob properties** popup that appears, locate and record the value of the **URL** property. This URL will be used later in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/24.png?st=2019-09-20T05%3A39%3A46Z&se=2022-09-21T05%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7lArt67BLZDg6knsN0lNDhs5Cak5QTvdma5hFYMfCKY%3D)

### Task 6: Deploy an Azure VM by using an Azure Resource Manager template with PowerShell DSC extension from the Azure portal.

1. In the upper left corner of the Azure portal, click **Create a resourcetemplate**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Template deployment**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/25.png?st=2019-09-20T05%3A40%3A07Z&se=2022-09-21T05%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9VoyD9aJrDUM7B9N7bLbkMy1o4dlgs2Ffpn%2BwAB3wVA%3D)

4. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/26.png?st=2019-09-20T05%3A40%3A26Z&se=2022-09-21T05%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l6K%2BfVB2QdwpyDA26fFxo9NRiVdKzsNToOfp6MlACpE%3D)

5. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/27.png?st=2019-09-20T05%3A40%3A43Z&se=2022-09-21T05%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IoFXoLvIwJv12DcZCynfV9%2FsO%2FPicc%2FXpeFerO2jRuw%3D)

6. From the Edit template blade, load the template file **dsc-extension-template.json.**

To load the file **dsc-extension-template.json** into the azure portal copy the below URL and paste it in the Chrome Browser and click Enter.

Now copy the Content in the URL and paste it in the Edit template blade.

```

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_02/LabFiles/Starter/dsc-extension-template.json?st=2019-09-23T06%3A35%3A30Z&se=2022-09-24T06%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0DXRvxJEt%2Fsxbu3E562BNk18OxWsEdj36pIFsLX%2B988%3D

```


8. Click the **Save** button to persist the template.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/28.png?st=2019-09-20T05%3A41%3A03Z&se=2022-09-21T05%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FZxQm25C3x7nYh1iUAzYdMNDggzPgo%2BFjeCwSYA1%2Fxg%3D)

9. Back on the **Custom deployment** blade, perform the following tasks:

```

   Subscription: Select the default 

   Resource group: {{ ResourceGroup }}

   Location: {{ Location }}

   Virtual Machine Name: lab03vm0

   Configuration Module Url: enter the URL value that you recorded in the previous task.

   Extension Function: IISWebServer.ps1\\IISWebServer
    
```
 * In the **Terms and Conditions** section, select the **I agree to the terms and conditions stated above** checkbox.

 *  Click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/29.png?st=2019-09-20T05%3A41%3A24Z&se=2022-09-21T05%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QU%2Bua8VvUcakoo0ays5EZi%2BC%2FFgfdOB0U6%2FPNVKc6cc%3D)

10. Wait for the deployment of the DSC configuration to complete before you proceed to the next task.

   **Note**: DSC configuration deployment can take up to ten minutes.

### Task 7: Validate that the Azure VM is serving web content

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the {{ ResourceGroup }} into which you deployed the virtual machine.

3. On the resource group blade, click the entry representing the **Virtual Machine** you deployed.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/30.png?st=2019-09-20T05%3A41%3A42Z&se=2022-09-21T05%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eyn6ORplGtpbHBrgl5ky3%2FYeXMGCyv%2B3e1oYvzze8OY%3D)

4. On the **Virtual machine** blade, locate the **Public IP address** entry, and identify its value.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/31.png?st=2019-09-20T05%3A42%3A00Z&se=2022-09-21T05%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4u8RLEQSKMGISs3zmiNRo%2BHgw0rPmGXZJ%2FR7Lj2J1NA%3D)

5. Open a new Chrome tab and navigate to the IP address you identified in the previous step.

6. Verify that you are able to access the default Internet Information Services webpage.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/32.png?st=2019-09-20T05%3A42%3A33Z&se=2022-09-21T05%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6J4YH%2FTJphMYBpvRl4WZSegj%2F%2B45ZRFzaHCzbV20lN8%3D)

7. Close the new browser tab.

**Review**: In this exercise, you deployed an **Virtual Machine** from the Azure portal and then used the **PowerShell DSC** extension to apply changes to the virtual machine in an unattended manner.

## Exercise 2: Deploy an Azure Virtual Machine Scale Set by using Azure Resource Manager templates with PowerShell Desired State Configuration extension from the Azure portal

### Task 1: View an Azure Resource Manager template.

1. Open the below link in Chrome.

```

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_02/LabFiles/Starter/vmss-template.json?st=2019-09-23T06%3A37%3A22Z&se=2022-09-24T06%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ihowgK5q%2BjjQSyFQ%2FzW4eH88YheeTsSjhgXHR2XtvbY%3D

```

2. In the **Chrome** window that appears, review the content of the JSON file.

### Task 2: Deploy a VMSS using ARM

1. In the hub menu of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Template deployment**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/33.png?st=2019-09-20T05%3A43%3A02Z&se=2022-09-21T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Vhe0N4MH%2FeneJFDF4nXvOBkOrJz1QoHve6iSPlPY%2B6Q%3D)

4. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/34.png?st=2019-09-20T05%3A43%3A20Z&se=2022-09-21T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sKLMSgdgbVNZw1dCpZh0DGK5%2FpwqMIl6PV2jaW%2B73nk%3D)

5. On the **Custom deployment** blade, click **Build your own template in the editor**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/35.png?st=2019-09-20T05%3A43%3A38Z&se=2022-09-21T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IkoHanAGiexIxIntzZ%2BGVVeePMokm9P94wu9oWqkR10%3D)

6. From the Edit template blade, load the template file **vmss-template.json**.

To load the file **vmss-template.json** into the azure portal copy the below URL and paste it in the Chrome Browser and click Enter.

Now copy the Content in the URL and paste it in the Edit template blade.

```

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_02/LabFiles/Starter/vmss-template.json?st=2019-09-25T05%3A45%3A48Z&se=2022-09-26T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9iEwE6Qh8RpILZQ7y9ZskVoCeiaIHKcloDpk1zU8FhM%3D

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/36.png?st=2019-09-20T05%3A43%3A56Z&se=2022-09-21T05%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8o%2FWndHnlF1OPzm%2FBlJHGxjDFaEdAsYG9l4jV8tsuMQ%3D)

7. Save the template and return to the **Custom deployment blade**.

8.. Back on the **Custom deployment** blade, perform the following tasks:

```

    Subscription: Select the default

    Resource group: {{ ResourceGroup }}

    Location: {{ Location }} 

    Admin User Name: Student

    Admin Password: Password@1234

   Instance Count: 2

   Overprovision: true

   Configuration Module Url: text box, enter the URL that you recorded for the uploaded blob in the previous exercise of this lab.
   
```

   * In the **Terms and Conditions** section, select the **I agree to the terms and conditions stated above** checkbox.

   * Click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/37.png?st=2019-09-20T05%3A44%3A17Z&se=2022-09-21T05%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=P%2F0LzZ7e2110knz46t3OyiZpCtkrz0iKHFSsr4lc%2BPI%3D)

12. Wait for the deployment to complete before you proceed to the next task.

### Task 3: Validate that VMSS instances are serving web content

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the resource group into which you deployed the virtual machine scale set.

3. On the resource group blade, click the resource of the **Public IP address** type.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/39.png?st=2019-09-20T05%3A45%3A27Z&se=2022-09-21T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uv%2B0XyDhS6fI6pz1l7B6pegnViBxePYKitc36yHvcLY%3D)

4. On the Public IP address resource blade, in the **Essentials** section, identify the value of **IP address** entry.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/40.png?st=2019-09-20T05%3A45%3A57Z&se=2022-09-21T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kGKFApVC3VAh1dGMghjcQHiNzDUDod%2FE0O7s6j0U0L8%3D)

5. Open a new Microsoft Edge tab and navigate to the IP address you identified in the previous step.

6. Verify that you are able to access the default Internet Information Services webpage.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/41.png?st=2019-09-20T05%3A46%3A17Z&se=2022-09-21T05%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lX1X9OZpRnZMsIDQcA4RWwcd8sK9bFxh5XwgF8kjOVg%3D)

7. Close the new browser tab and return to the browser tab with the **Azure Portal** currently active.

**Review**: In this exercise, you created a Virtual Machine scale set and configured the individual instances using PowerShell DSC.

## Exercise 3: Deploy Azure VMs running Windows Server 2016 and Linux by using Azure Building Blocks with PowerShell Desired State Configuration extension from the Azure Cloud Shell

### Task 1: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.
 
3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

  * Leave the **Subscription** drop-down list entry set to its default value.

  * Region: {{ Location }}

  * In the **Resource group** section, ensure that the **Use existing** option is selected and then select **{{ ResourceGroup}}**.

  * In the **Storage account** section, ensure that the **Create new** option is selected and then, in the text box below, type a unique name consisting of a combination of between 3 and 24 characters and digits. 

  * In the **File share** section, ensure that the **Create new** option is selected and then, in the text box below, type **cloudshell**.

  * Click the **Create storage** button.
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/125.png?st=2019-09-25T06%3A00%3A34Z&se=2022-09-26T06%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hUKedQMhSGrLhm%2FQPbrngy2rmiS%2BoqkqcWnZOx4lg50%3D)
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/126.png?st=2019-09-25T05%3A56%3A29Z&se=2022-09-26T05%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=013YIO4LEZMejTgpqQp23lsRuNy5WIqT5Q5RWqLxiAo%3D) 
  
  ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/124.PNG?st=2019-09-25T05%3A55%3A12Z&se=2022-09-26T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3BQ2R6MyDQeXE0Iwss39hKKBE6O8CrbSi4RUIgeWBxg%3D)  

4. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

### Task 2: Install the Azure Building Blocks npm package in Azure Cloud Shell

1. At the **Cloud Shell** command prompt at the bottom of the portal, type in the following command and press **Enter** to create a local directory to install the Azure Building Blocks npm package:

    ```
    mkdir ~/.npm-global
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/43.png?st=2019-09-20T05%3A46%3A56Z&se=2022-09-21T05%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eBV2Wo3A9hm%2FRpHm5LbV2sUZN0yMS%2B%2FBshGt7GA4Xhc%3D)

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to update the npm configuration to include the new local directory:

    ```
    npm config set prefix '~/.npm-global'
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/44.png?st=2019-09-20T05%3A47%3A15Z&se=2022-09-21T05%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=q7g7rDq9aGLVdtbfJ7vQGJ3OTI%2B3AMMO0c45coTDVZ4%3D)

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to open the ~./bashrc configuration file for editing:

    ```
    vi ~/.bashrc
    ```

4. At the **Cloud Shell** command prompt, in the vi editor interface, scroll down to the bottom of the file (or type **G**), scroll to the right to the right-most character on the last line (or type **$**), type **a** to enter the **INSERT** mode, press **Enter** to start a new line, and then type the following to add the newly created directory to the system path:

    ```
    export PATH="$HOME/.npm-global/bin:$PATH"
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/45.png?st=2019-09-20T05%3A47%3A34Z&se=2022-09-21T05%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eMoDhqK1T3moNlDl8lE2TBOmX42juWaBfOeyP1Rbufs%3D)

5. At the **Cloud Shell** command prompt, in the vi editor interface, to save your changes and close the file, press **Esc**, type **:wq!** and press **Enter**.

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to install the Azure Building Blocks npm package:

    ```
    npm install -g @mspnp/azure-building-blocks
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/46.png?st=2019-09-20T05%3A47%3A52Z&se=2022-09-21T05%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RnGALt7fH7jwosw0F7SZmKRQetnYXW%2FeHJOHvPhvy5w%3D)

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to exit the shell:

    ```
    exit
    ```

8. In the **Cloud Shell timed out** pane, click **Reconnect**. 

  **Note**: You need to restart Cloud Shell for the installation of the Buliding Blocks npm package to take effect.

### Task 3: Deploy a Windows Server 2016 Azure VM from Cloud Shell by using Azure Building Blocks

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to download the GitHub repository containing the Azure Building Blocks reference architecture files:

    ```
    git clone https://github.com/mspnp/reference-architectures.git
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/47.png?st=2019-09-20T05%3A48%3A14Z&se=2022-09-21T05%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hJhhgnPVpH57FDa1DBfSQe5%2BnomHAB7RVBzuwLIbA%2FM%3D)

2.  At the **Cloud Shell** command prompt, type in the following command and press **Enter** to view the content of the Azure Building Block parameter file you will use for this deployment:

    ```
    cat ./reference-architectures/virtual-machines/single-vm/parameters/windows/single-vm.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/48.png?st=2019-09-20T05%3A48%3A32Z&se=2022-09-21T05%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mw68NrrRs5boNV3TbVEqgWXAPt9BrdqqxsAlhPJ76xU%3D)

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

    ```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')
    ```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/49.png?st=2019-09-20T05%3A48%3A52Z&se=2022-09-21T05%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1U3a9gfqnkKbCHOvAZPJPZ%2BhwXpzJc4zbKRQovmke2o%3D)

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group you created earlier in this exercise:

    ```
    RESOURCE_GROUP='{{ ResourceGroup }}'
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/50.png?st=2019-09-20T05%3A49%3A12Z&se=2022-09-21T05%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g2wrASxJBbNnuEkiCWrDhRAaoyb8GtRAqL4dyxiJfoE%3D)

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

    ```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/51.png?st=2019-09-20T05%3A49%3A29Z&se=2022-09-21T05%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dmR1RQTPnHQT1d48te7vtx51nkuYG9UuFlcbi5Ftvdw%3D)
   

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the Building Blocks parameter file:

    ```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ./reference-architectures/virtual-machines/single-vm/parameters/windows/single-vm.json
    ```

8. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminPassword** parameter with the value **Password@1234** in the Building Blocks parameter file:

    ```
    sed -i.bak2 's/"adminPassword": ""/"adminPassword": "Password@1234"/' ./reference-architectures/virtual-machines/single-vm/parameters/windows/single-vm.json
    ```

9. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the Building Blocks parameter file:

    ```
    cat ./reference-architectures/virtual-machines/single-vm/parameters/windows/single-vm.json
    ```
    
    ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/53.png?st=2019-09-20T05%3A50%3A14Z&se=2022-09-21T05%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7E4Re8hAI3qZQJmNviowDRfUbDIVq%2BQRt4llSf9wVZs%3D)

10. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy a Windows Server 2016 Azure VM by using the Azure Building Blocks:

    ```
    azbb -g $RESOURCE_GROUP -s $SUBSCRIPTION_ID -l $LOCATION -p ./reference-architectures/virtual-machines/single-vm/parameters/windows/single-vm.json --deploy
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/54.png?st=2019-09-20T05%3A50%3A37Z&se=2022-09-21T05%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mRJVo9cXPDG8pXLY%2B3ZjDJFflQqd1NcGbE1a0oJNnPw%3D)

11. Wait for the deployment to complete before you proceed to the next task.

### Task 4: Validate that the Windows Server 2016 Azure VM is serving web content

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the resource group into which you deployed the Windows Server 2016 Datacenter virtual machine earlier in this exercise.

3. On the resource group blade, click the entry representing the virtual machine you deployed.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/56.png?st=2019-09-20T05%3A51%3A20Z&se=2022-09-21T05%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hHQYlJssbhA2Q8umjU2vbqb1QGTYCI4lFF21uoMJ8EM%3D)

4. On the **Virtual machine** blade, locate the **Public IP address** entry, and identify its value.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/57.png?st=2019-09-20T05%3A51%3A36Z&se=2022-09-21T05%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=T1iG2NxAXNfUV2qOSnrzMHnxLNObuRPM1XR%2BhpL2FYg%3D)

5. Open a new Google Chrome tab and navigate to the IP address you identified in the previous step.

6. Verify that you are able to access the default Internet Information Services webpage.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/58.png?st=2019-09-20T05%3A51%3A58Z&se=2022-09-21T05%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4zZkGRiWXkyWpuLsPXOlgTgY5Uq3U1iihaPz12aKhY4%3D)

7. Close the new browser tab.

### Task 5: Deploy a Linux Azure VM from Cloud Shell by using Azure Building Blocks

1.  At the **Cloud Shell** command prompt, type in the following command and press **Enter** to view the content of the Azure Building Block parameter file you will use for this deployment:

    ```
    cat ./reference-architectures/virtual-machines/single-vm/parameters/linux/single-vm.json
    ```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to generate the SSH key pair that you will use to authenticate when accessing the Linux VM:

    ```
    ssh-keygen -t rsa -b 2048
    ```

  * When prompted to enter the file in which to save the key, press **Enter** to accept the default value **(~/.ssh/id_rsa)**.

  * When prompted to enter passphrase, press **Enter** twice.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/59.png?st=2019-09-20T05%3A52%3A16Z&se=2022-09-21T05%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JTfRuUPnt6CoVpMAwHNp5%2FrzD7UydKp7Rysfyd2rim0%3D)

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the public key of the newly generated key pair:

    ```
    PUBLIC_KEY=$(cat ~/.ssh/id_rsa.pub)
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/60.png?st=2019-09-20T05%3A52%3A59Z&se=2022-09-21T05%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5aj8kOeByHTzVAn3BjLk1x2bSgbVwK%2F4hf%2FhGOAO%2BN4%3D)

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the public key of the newly generated key pair and which takes into account any special character the public key might include:

    ```
    PUBLIC_KEY_REGEX="$(echo $PUBLIC_KEY | sed -e 's/\\/\\\\/g; s/\//\\\//g; s/&/\\\&/g')"
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/61.png?st=2019-09-20T05%3A53%3A22Z&se=2022-09-21T05%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jh%2FQhHN1WPmhT0VVKpgRNEbpUqwLLpyeKTRUhpobZxs%3D)

  **Note**: This is necessary because you will use the **sed** utility to insert this string into the Azure Building Blocks parameter file. Alternatively, you could simply open the file and enter the public key string directly into the file.

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

    ```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/62.png?st=2019-09-20T05%3A53%3A41Z&se=2022-09-21T05%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jenUS%2Buxy%2BE7fGul1XHMG3g%2FNMP5ihRU6CLdcLKS2iA%3D)

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group you will use for the deployment:

    ```
    RESOURCE_GROUP='{{ ResourceGroup }}'
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/63.png?st=2019-09-20T05%3A54%3A01Z&se=2022-09-21T05%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F8pK5afDgU0BvjvUNRV37mUciqCEVjkpH5ST6vDAlCk%3D)

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

    ```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/64.png?st=2019-09-20T05%3A54%3A19Z&se=2022-09-21T05%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oOszkVUlMZ8tfnxZ0OY%2B7Wp0t6FBDEM%2BoOV1l5wyUDI%3D)

8. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the Building Blocks parameter file:

    ```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ./reference-architectures/virtual-machines/single-vm/parameters/linux/single-vm.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/65.png?st=2019-09-20T05%3A54%3A39Z&se=2022-09-21T05%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=x1oi4octf1cK9nrI0UX%2BFlgq44wQGcxdLEcFF9pKe1I%3D)

9. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **sshPublicKey** parameter with the value of the **$PUBLIC_KEY_REGEX** variable in the Building Blocks parameter file:

    ```
    sed -i.bak2 's/"sshPublicKey": ""/"sshPublicKey": "'"$PUBLIC_KEY_REGEX"'"/' ./reference-architectures/virtual-machines/single-vm/parameters/linux/single-vm.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/66.png?st=2019-09-20T05%3A55%3A00Z&se=2022-09-21T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TLkAsW%2BYcf%2BMQLdhZ1wj4f9LrH3ybRCcnBC7ayFDrNI%3D)

10. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the Building Blocks parameter file:

    ```
    cat ./reference-architectures/virtual-machines/single-vm/parameters/linux/single-vm.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/67.png?st=2019-09-20T05%3A55%3A19Z&se=2022-09-21T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eMilN%2BMoJHDTx8Hzhp5Vu0sxCOrxBTDDRe6JJPx4EvM%3D)

12. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy a Linux Azure VM by using the Azure Building Blocks:

    ```
    azbb -g $RESOURCE_GROUP -s $SUBSCRIPTION_ID -l $LOCATION -p ./reference-architectures/virtual-machines/single-vm/parameters/linux/single-vm.json --deploy
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/69.png?st=2019-09-20T05%3A55%3A56Z&se=2022-09-21T05%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=caSlzeFTWq3qSGDuJ5Xe%2Brm9EXtU4foxwR%2BxreFuNpM%3D)

13. Wait for the deployment to complete before you proceed to the next task.

### Task 7: Validate that the Linux Azure VM is serving web content

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the resource group into which you deployed the virtual machine.

3. On the resource group blade, click the entry representing the virtual machine you deployed.

4. On the **Virtual machine** blade, locate the **Public IP address** entry, and identify its value.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/71.png?st=2019-09-20T05%3A56%3A35Z&se=2022-09-21T05%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jT7xG%2BJemL6Fs5%2BtnDeElnVHXSPpd740x4j28lbeH3U%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/72.png?st=2019-09-20T05%3A56%3A54Z&se=2022-09-21T05%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5j56FqzlQqYFIrBGn7HvyxXUVVdDHgElr3P4kZ8dfU4%3D)

5. Open a new Chrome tab and navigate to the IP address you identified in the previous step.

6. Verify that you are able to access the default Apache2 Ubuntu webpage.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab8-Building%20Azure%20IaaS-Based%20Server%20Applications%20by%20using%20Azure%20Resource%20Manager%20Templates%20and%20Azure%20Building%20Blocks/73.png?st=2019-09-20T05%3A57%3A12Z&se=2022-09-21T05%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MrDzZyMslIoXIUgEuI0NX2ROTWKVPtJg9pS0TZ3rKdg%3D)

7. Close the new browser tab.

8. Close the **Cloud Shell** pane.

 **Review**: In this exercise, you deployed Azure VMs running Windows Server 2016 Datacenter and Linux from Cloud Shell by using Azure Building Blocks.

