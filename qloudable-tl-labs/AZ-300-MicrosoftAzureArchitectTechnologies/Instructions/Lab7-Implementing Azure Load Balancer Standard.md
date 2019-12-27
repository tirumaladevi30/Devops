
# Lab: Implementing Azure Load Balancer Standard

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Implement inbound load balancing and NAT by using Azure Load Balancer Standard](#exercise-1-implement-inbound-load-balancing-and-nat-by-using-azure-load-balancer-standard)

[Exercise 2: Configure outbound SNAT traffic by using Azure Load Balancer Standard](#exercise-2-configure-outbound-snat-traffic-by-using-azure-load-balancer-standard)


## Overview

The aim of this lab is about implementing and deploying Azure load balancer by adding backend pools, load balancing rules, Health probes and Inbound NAT rules by using load balancer standards. Also configuring Outbound SNAT traffic by using Azure Load Balancer standards.

### Scenario and Objectives

XYZ training labs Corporation wants to implement Azure Load Balancer Standard to direct inbound and outbound traffic of Azure VMs.

After completing this lab, you will be able to:

* Implement inbound load balancing by using Azure Load Balancer Standard

* Configure outbound SNAT traffic by using Azure Load Balancer Standard

## Pre-Requisites

* Familiarity with ARM template

* Familiarity with Azure cloud shell

* RDP session

**Note:** Azure Portal & Remote Desktop is part of the Lab environment

## Exercise 1: Implement inbound load balancing and NAT by using Azure Load Balancer Standard 
  
The main tasks for this exercise are as follows:

1. Deploy Azure VMs in an availability set by using an Azure Resource Manager template

2. Create an instance of Azure Load Balancer Standard

3. Create a load balancing rule of Azure Load Balancer Standard

4. Create a NAT rule of Azure Load Balancer Standard

5. Test functionality of Azure Load Balancer Standard

### Task 1: Deploy Azure VMs in an availability set by using an Azure Resource Manager template

1. Using the Chrome browser, login into Azure portal with the below details.

**Azure login_ID:** {{azure-login-id}} <br>

**Azure login_Password:** {{azure-login-password}}<br>


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal1.png?st=2019-08-22T11%3A08%3A20Z&se=2020-08-23T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fm%2BDTeOkr2f0%2BS344uOTMlPzHxDsCisvhsf4Jo1LzmY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal2.png?st=2019-08-22T11%3A09%3A36Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ONwSsJE%2B5ENkff6wqI098VfdvzB77ezY7PxjamtqBgQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal3.png?st=2019-08-22T11%3A09%3A59Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5JhMvyxOF4PJSrB3u4M9KLit%2B9IqG6MrVjUObzyLaGg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal4.png?st=2019-08-22T11%3A10%3A23Z&se=2020-08-23T11%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QKaTSjnXbhdQ1wkIajvEAwwAJvuUfoQn7NBkmBQa2C4%3D)

2. In the Azure portal,start a **Bash** session within the **Cloud Shell**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/cloudshell.png?st=2019-08-26T11%3A57%3A58Z&se=2021-08-27T11%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=q%2BMoyi6FM4zfA9sqVV612tfvloiyKo7l8%2Fafd%2FT%2FI%2BU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/5.png?st=2019-08-26T11%3A00%3A03Z&se=2021-08-27T11%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vNtWvhbHOFYB%2BCrdjpyeXARPO8HI0z%2FR9MtzhLZqDvg%3D)

3. If you are presented with the **You have no storage mounted** message, configure storage using the following settings:


Subsciption: Select the default
    
Note: choose advanced option to provide the below properties

**Cloud Shell region**: the name of the Azure region that is available in your subscription and which is closest to the lab location

**Resource group**: {{resource-group-name}} <br>

**Storage account**: a name of a new storage account

**File share**: a name of a new file share


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-1.png?st=2019-08-26T12%3A06%3A35Z&se=2021-08-27T12%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ReXVfoia2Va2kUZD9Es5HfmsF3MFmqWGM9Wx%2FUgnYgQ%3D)


5. From the Cloud Shell pane, upload the Azure Resource Manager template **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0801.json?st=2019-08-23T07%3A36%3A43Z&se=2020-08-24T07%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h%2BiTIfndEhYCHy2LXODgxmWhIRjHk2T037S2m0G6tR0%3D** into the home directory.

use the below command to download the Azure resource manager template into the Cloud Shell pane home directory.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0801.json?st=2019-08-23T07%3A36%3A43Z&se=2020-08-24T07%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h%2BiTIfndEhYCHy2LXODgxmWhIRjHk2T037S2m0G6tR0%3D"

```
6. From the Cloud Shell pane, upload the parameter file **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0801.parameters.json?st=2019-08-23T07%3A37%3A19Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yDXZRsjP4IjkdCrIV1P2OMZg%2FxGmUXoXQvOadDueumc%3D** into the home directory.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0801.parameters.json?st=2019-08-23T07%3A37%3A19Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yDXZRsjP4IjkdCrIV1P2OMZg%2FxGmUXoXQvOadDueumc%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/8.png?st=2019-08-26T11%3A01%3A22Z&se=2021-08-27T11%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2J%2B59K6pIryhZoxDOz%2FYITSVWK1%2F%2BZmRGv%2BiTfFDeh0%3D)


Run the below command to change the file names after downloading.

```
mv "azuredeploy0801.json?st=2019-08-23T07%3A36%3A43Z&se=2020-08-24T07%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h%2BiTIfndEhYCHy2LXODgxmWhIRjHk2T037S2m0G6tR0%3D" azuredeploy0801.json

mv "azuredeploy0801.parameters.json?st=2019-08-23T07%3A37%3A19Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yDXZRsjP4IjkdCrIV1P2OMZg%2FxGmUXoXQvOadDueumc%3D" azuredeploy0801.parameters.json

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/mv.png?st=2019-08-26T12%3A21%3A01Z&se=2021-08-27T12%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rkmFmDMmtrL9sYlKJ8rX9Ly9m8in6F%2FT2l1C64vT%2BWY%3D)


7. From the Cloud Shell pane, deploy a pair of Azure VMs hosting Windows Server 2016 Datacenter by running the following command:


az group deployment create --resource-group {{resource-group-name}} <br> --template-file azuredeploy0801.json --parameters @azuredeploy0801.parameters.json


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/9.png?st=2019-08-26T11%3A03%3A24Z&se=2021-08-27T11%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Fcxzu%2F2xer1qLGgMm8l2FW8TIKkTQuH068hWPdURY48%3D)

   > **Note**: Wait for the deployment before you proceed to the next task. This might take about 10 minutes.

8. In the Azure portal, close the Cloud Shell pane.

### Task 2: Create an instance of Azure Load Balancer Standard

1. In the Azure portal, create a new Azure Load Balancer with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/10.png?st=2019-08-26T11%3A04%3A18Z&se=2021-08-27T11%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0YAGYoOF0JFCZ34rROuLXTFs0Rr7RsZ5VJaYSkBvRTI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-2.png?st=2019-08-26T12%3A07%3A52Z&se=2021-08-27T12%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QqgbyG%2F9zEujM9URsxapvZcamubi6551B1Xog7VjwGg%3D)


**Subsciption**: Select the default

**Resource group**: {{resource-group-name}} <br>
    
**Name**: az3000801-lb

**Region**: {{location}} <br>
    
**Type**: Public

**SKU**: Standard

**Public IP address**: Create new named az3000801-lb-pip01

**Availability zone**: Zone-redundant    



![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-3.png?st=2019-08-26T12%3A08%3A24Z&se=2021-08-27T12%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4EvsjZikkcjgLv7l%2B5zjpcC4qca0SoJwfi%2Bax%2BX%2Bu8Y%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-4.png?st=2019-08-26T12%3A08%3A42Z&se=2021-08-27T12%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Gic1AxFVk05MDSIBSOmPGFx8PTNMJnrPmj5txJwCGRs%3D)

### Task 3: Create a load balancing rule of Azure Load Balancer Standard

1. In the Azure portal, navigate to the blade displaying the properties of the newly deployed Azure Load Balancer **{{ ResourceGroup }}**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/12.png?st=2019-08-26T11%3A05%3A00Z&se=2022-08-27T11%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iVDaI%2FmVfxzLtswxYV%2FDKkjJ%2BbKvtXkZ%2BT%2BvzzUp4vA%3D)

2. On the **az3000801-lb** blade, click **Backend pools**.

3. On the **az3000801-lb - Backend pools** blade, click **+ Add**.

4. On the **Add backend pool** blade, specify the following settings and click **Add**:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/13.png?st=2019-08-26T11%3A05%3A21Z&se=2021-08-27T11%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rVBAxZIfvDVAFmkQBVefJQWN4%2B9pYvP5yA7RXyZfvEg%3D)

```
Name: az3000801-bepool

Virtual network: az3000801-vnet (2 VM)

VIRTUAL MACHINE: az3000801-vm0  IP ADDRESS: ipconfig1 (10.0.0.4) or ipconfig1 (10.0.0.5)

VIRTUAL MACHINE: az3000801-vm1  IP ADDRESS: ipconfig1 (10.0.0.5) or ipconfig1 (10.0.0.4)

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/14.png?st=2019-08-26T11%3A05%3A43Z&se=2021-08-27T11%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EZjeaaUoUV86Ufda6mCCM3YzmrAGVp9OLPKcxrD0fcE%3D)


   > **Note**: It is possible that the IP addresses of virtual machines are asssigned in the reversed order. 

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

5. Back on the **az3000801-lb - Backend pools** blade, click **Health probes**.

6. On the **az3000801-lb - Health probes** blade, click **+ Add**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/15.png?st=2019-08-26T11%3A06%3A08Z&se=2021-08-27T11%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=u%2Bk%2BWY2fT0f07VePFWCi8qJgcMcOOvmvDb2yu0FMn3g%3D)

7. On the **Add health probe** blade, specify the following settings and click **OK**:

```
Name: az3000801-healthprobe

Protocol: TCP

Port: 80

Interval: 5

Unhealthy threshold: 2

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/16.png?st=2019-08-26T11%3A06%3A34Z&se=2021-08-27T11%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2rCzx%2FEUbKAb%2BclPhSdpYESZAjdCvqRvPLP0FHlvm3k%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

8. Back on the **az3000801-lb - Health probes** blade, click **Load balancing rules**.

9. On the **az3000801-lb - Load balancing rules** blade, click **+ Add**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/17.png?st=2019-08-26T11%3A07%3A24Z&se=2021-08-27T11%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bWEWbh3%2B1qGjtUGRDS5%2BBoqdVJxOUGVMAi6dDS4khE4%3D)

10. On the **Add load balancing rule** blade, specify the following settings and click **OK**:

```
Name: az3000801-lbrule01

IP Version: IPv4

Frontend IP address: select the public IP address assigned to the LoadBalancedFrontEnd from the drop-down list

Protocol: TCP

Port: 80

Backend port: 80

Backend pool: az3000801-bepool (2 virtual machines)

Health probe: az3000801-healthprobe (TCP:80)

Session persistence: None

Idle timeout (minutes): 4

Floating IP (direct server return): Disabled

``` 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/18.png?st=2019-08-26T11%3A07%3A46Z&se=2021-08-27T11%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BMvvL8lQTv%2FCRSlpxLZR5ev%2Fj%2FQilkT5GceFsDrhFVM%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

### Task 4: Create a NAT rule of Azure Load Balancer Standard

1. In the Azure portal, on the **az3000801-lb** blade, click **Inbound NAT rules**.

2. On the **az3000801-lb - Inbound NAT rules** blade, click **+ Add**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/19.png?st=2019-08-26T11%3A08%3A09Z&se=2021-08-27T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=01l3tQl077HOrAmiJgwSE87pa2aGe%2BUrsCSYAagbKk8%3D)

3. On the **Add inbound NAT rule** blade, specify the following settings and click **OK**:

```
Name: az3000801-vm0-RDP

Frontend IP address: select the public IP address assigned to the **LoadBalancedFrontEnd** from the drop-down list

IP Version: IPv4

Service: RDP

Protocol: TCP

Port: 33890

Target virtual machine: az3000801-vm0

Network IP configuration: ipconfig1 (10.0.0.4) or ipconfig1 (10.0.0.5)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/20.png?st=2019-08-26T11%3A08%3A32Z&se=2021-08-27T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gDuhoiNSM0uqWOhVduOnit9TFjL7bgpnnnQ7jfPmVgs%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

4. Back on the **az3000801-lb - Inbound NAT rules** blade, click **+ Add**.

5. On the **Add inbound NAT rule** blade, specify the following settings and click **OK**:

```

Name: az3000801-vm1-RDP

Frontend IP address: select the public IP address assigned to the LoadBalancedFrontEnd from the drop-down list

IP Version: IPv4

Service: RDP

Protocol: TCP

Port: 33891

Target virtual machine: az3000801-vm1

Network IP configuration: ipconfig1 (10.0.0.5) or ipconfig1 (10.0.0.4)

Port mapping: Custom

Floating IP (direct server return): Disabled

Target port: 3389

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/21.png?st=2019-08-26T11%3A08%3A49Z&se=2021-08-27T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=M8rroQaUxfVHkjeovP%2BykGUKi2GBH62N%2F1TU5OLg6T8%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

### Task 5: Test functionality of Azure Load Balancer Standard

1. In the Azure portal, navigate to the **az3000801-lb** blade and note the value of the **Public IP address** entry.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/22.png?st=2019-08-26T11%3A09%3A13Z&se=2021-08-27T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CmLiu%2BMsMOq9jo3U1roZGdm0jaBK3fdnjFdSojD3Xv8%3D)

2. Open Chrome browser's new tab and paste the IP address you identified in the previous step.

3. Verify that you are presented with the default **Internet Information Services Welcome** page. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/23.png?st=2019-08-26T11%3A09%3A36Z&se=2021-08-27T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FANRMAcxZoYIWYlYyl0GHbAniN1wvpEzoXXidcGf%2BzE%3D)

4. On the lab computer, click on  **Start**, select **Remote Desktop client**, and paste the public IP address you identified earlier in this task with the port 33890 like as shown below):

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-6.png?st=2019-08-26T12%3A00%3A47Z&se=2021-08-27T12%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JTTbPxhcdx9nUdTF5Vln%2Fgo4%2FeQrte4PH7PM8Z44peM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-7.png?st=2019-08-26T12%3A01%3A09Z&se=2021-08-27T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=b2%2FcvcFXYCsCbfRQwTnImloFWJz4j0H23nuxbO2hc%2BQ%3D)

```
ex: <IP address>:33890
```

![alt text](![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-8.png?st=2019-08-27T04%3A07%3A48Z&se=2021-08-28T04%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XJ2ju4mQPMyuhlm18SnbvmcWoeGn%2BIY5xHe1e%2F9bGFU%3D))


5. When prompted, authenticate by specifying the following values:

```
User name: adminuser

Password: Password@1234

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-9.png?st=2019-08-26T12%3A01%3A58Z&se=2021-08-27T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3BKJMcrIYK44CxDYEXB1EE0EkxfDmFYndHlQyxKYZdY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-10.png?st=2019-08-26T12%3A02%3A54Z&se=2021-08-27T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OhEBcfJBWMN1k8ub%2Fu1EgtJtQgRTl7gri%2BE41ppjOf0%3D)

6. Within the Remote Desktop session, switch to the **Local Server** view in the Server Manager window and verify that you are connected to **az3000801-vm0** Azure VM.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/26.png?st=2019-08-26T11%3A10%3A49Z&se=2021-08-27T11%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QrruAiQ6bpvZQW2uHlZdHw4qjCWzqzDXwxGIdUs4PrY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/27.png?st=2019-08-26T11%3A11%3A08Z&se=2021-08-27T11%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3qadrwbxwRE0V%2BjPcKO%2B9oK68a17fKacSPXkqXulI%2BY%3D)

7. On the lab computer, click on  **Start**, select **Remote Desktop client**, and paste the public IP address you identified earlier in this task with the port 33890 like as shown below):

```
Ex: <IP address>:33891

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-6.png?st=2019-08-26T12%3A00%3A47Z&se=2021-08-27T12%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JTTbPxhcdx9nUdTF5Vln%2Fgo4%2FeQrte4PH7PM8Z44peM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-7.png?st=2019-08-26T12%3A01%3A09Z&se=2021-08-27T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=b2%2FcvcFXYCsCbfRQwTnImloFWJz4j0H23nuxbO2hc%2BQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-16.png?st=2019-08-27T04%3A09%3A45Z&se=2021-08-28T04%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jzQQFUfHjKYe%2FXMnhDiC8sn06zN%2F2VDt0kdZpiW934E%3D)


8. When prompted, authenticate by specifying the following values:

```
User name: adminuser

Password: Password@1234

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-9.png?st=2019-08-26T12%3A01%3A58Z&se=2021-08-27T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3BKJMcrIYK44CxDYEXB1EE0EkxfDmFYndHlQyxKYZdY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-10.png?st=2019-08-26T12%3A02%3A54Z&se=2021-08-27T12%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OhEBcfJBWMN1k8ub%2Fu1EgtJtQgRTl7gri%2BE41ppjOf0%3D)


9. Within the Remote Desktop session, switch to the **Local Server** view in the Server Manager window and verify that you are connected to **az3000801-vm1** Azure VM.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/29.png?st=2019-08-26T11%3A11%3A46Z&se=2021-08-27T11%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3U5d0Alys78ald2akajeS96J3TZMnLe9h6%2F55Nsdwdk%3D)

10. Within the Remote Desktop session, start a Windows PowerShell session and run the following to determine your current public IP address:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/30.png?st=2019-08-26T11%3A12%3A06Z&se=2021-08-27T11%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gghscDsv58%2BDvwIlr58dExtLmj9%2BlECVd0nG8VAChEE%3D)

```pwsh
Invoke-RestMethod http://ipinfo.io/json 

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/31.png?st=2019-08-26T11%3A12%3A42Z&se=2021-08-27T11%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cVsiu4pCFzfFSsaEY1H9%2FIxlTaGoRf1BIFAAnk3XNX8%3D)

11. Review the output of the cmdlet and verify that the IP address entry matches the public IP address you identified earlier in this task.

12. Leave the Remote Desktop sessions open. You will use them in the next exercise.

**Result**: After you completed this exercise, you have implemented and tested Azure Load Balancer Standard inbound load balancing and NAT rules

## Exercise 2: Configure outbound SNAT traffic by using Azure Load Balancer Standard
  
The main tasks for this exercise are as follows:

1. Deploy Azure VMs into an existing virtual network by using an Azure Resource Manager template

2. Create an Azure Standard Load Balancer and configure outbound SNAT rules

3. Test outbound rules of Azure Standard Load Balancer

### Task 1: Deploy Azure VMs into an existing virtual network by using an Azure Resource Manager template

1. In the Azure portal,start a **Bash** session within the **Cloud Shell**. 

2. From the Cloud Shell pane, upload the Azure Resource Manager template **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0802.json?st=2019-08-23T07%3A37%3A46Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VWmko0en%2FZxT6ytUZE5e0uhDGasg6ZmeK1XxEPMwyng%3D** into the home directory.

3. From the Cloud Shell pane, upload the parameter file **https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0802.parameters.json?st=2019-08-23T07%3A38%3A16Z&se=2020-08-24T07%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tyHRP7L2nRyeRfKEC1gCu%2F8%2FBoXdTVJSQutuC6CXT9c%3D** into the home directory.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0802.json?st=2019-08-23T07%3A37%3A46Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VWmko0en%2FZxT6ytUZE5e0uhDGasg6ZmeK1XxEPMwyng%3D"

wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/allfiles/AZ-300T03/Module_03/azuredeploy0802.parameters.json?st=2019-08-23T07%3A38%3A16Z&se=2020-08-24T07%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tyHRP7L2nRyeRfKEC1gCu%2F8%2FBoXdTVJSQutuC6CXT9c%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/32.png?st=2019-08-26T11%3A13%3A16Z&se=2021-08-27T11%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BU8VjxT5WIUzakHxzv3babr2nIyg%2B%2Fb4sxAUQbi%2BjC4%3D)

```
mv "azuredeploy0802.json?st=2019-08-23T07%3A37%3A46Z&se=2020-08-24T07%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VWmko0en%2FZxT6ytUZE5e0uhDGasg6ZmeK1XxEPMwyng%3D" azuredeploy0802.json

mv "azuredeploy0802.parameters.json?st=2019-08-23T07%3A38%3A16Z&se=2020-08-24T07%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tyHRP7L2nRyeRfKEC1gCu%2F8%2FBoXdTVJSQutuC6CXT9c%3D" azuredeploy0802.parameters.json

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-11.png?st=2019-08-26T12%3A20%3A32Z&se=2021-08-27T12%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JbooNa%2B26bZYPf6rzt6nDN%2Bvv7PmK8hO6mVNGv19YJA%3D)


4. From the Cloud Shell pane, deploy a pair of Azure VMs hosting Windows Server 2016 Datacenter by running:


az group deployment create --resource-group {{resource-group-name}} <br> --template-file azuredeploy0802.json --parameters @azuredeploy0802.parameters.json


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/33.png?st=2019-08-26T11%3A13%3A47Z&se=2021-08-27T11%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZcyV9cJWxARGUyM6b5NhcZ6QUGL1LKFZl%2BK6A8XlgZg%3D)

  > **Note**: Wait for the deployment before you proceed to the next task. This might take about 5 minutes.

5. In the Azure portal, close the Cloud Shell pane.

### Task 2: Create an Azure Standard Load Balancer and configure outbound SNAT rules

1. In the Azure portal,start a **Bash** session within the **Cloud Shell**. 

2. In the Azure portal, from the Cloud Shell pane, run the following to create an outbound public IP address of the load balancer:


az network public-ip create --resource-group {{resource-group-name}} <br> --name az3000802-lb-pip01 --sku standard
   

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/34.png?st=2019-08-26T11%3A14%3A08Z&se=2021-08-27T11%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RsdHoGb9DJ6Z58tB9ospQ%2BTlJbrAPiuSKz%2B7%2BYHt734%3D)

3. In the Azure portal, from the Cloud Shell pane, run the following to create an Azure Load Balancer Standard:


LOCATION=$(az group show --name {{resource-group-name}} <br> --query location --out tsv)

az network lb create --resource-group {{resource-group-name}} <br> --name az3000802-lb --sku standard --backend-pool-name az3000802-bepool --frontend-ip-name loadBalancedFrontEndOutbound --location $LOCATION --public-ip-address az3000802-lb-pip01


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/35.png?st=2019-08-26T11%3A14%3A52Z&se=2021-08-27T11%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qCCPSC3YZQ4%2FmbBNBUNMOv6bAhCweFJQDKhiO0QY6sI%3D)

4. From the Cloud Shell pane, run the following to create an outbound rule:


az network lb outbound-rule create --resource-group {{resource-group-name}} <br> --lb-name az3000802-lb --name outboundRuleaz30000802 --frontend-ip-configs loadBalancedFrontEndOutbound --protocol All --idle-timeout 15 --outbound-ports 10000 --address-pool az3000802-bepool


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/36.png?st=2019-08-26T11%3A15%3A14Z&se=2021-08-27T11%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YUG%2BJ9yNYJ6Vhgpq5S2CJKzk30JHs6VicmRiemX5opU%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

5. Close the Cloud Shell pane.

6. In the Azure portal, navigate to the blade displaying the properties of the Azure Load Balancer **az3000802-lb**.

7. On the **az3000802-lb** blade, click **Backend pools**.

8. On the **az3000802-lb - Backend pools** blade, click **az3000802-bepool**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/38.png?st=2019-08-26T11%3A15%3A36Z&se=2021-08-27T11%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=76XTXbdU6tZOpuh1olliiAw9BmQsC%2FOnKSIkAUP%2F4rk%3D)

9. On the **az3000802-bepool** blade, specify the following settings and click **Save**:

```

Virtual network: az3000801-vnet (4 VM)

VIRTUAL MACHINE: az3000802-vm0  IP ADDRESS: ipconfig1 (10.0.1.4) or ipconfig1 (10.0.1.5)

VIRTUAL MACHINE: az3000802-vm1  IP ADDRESS: ipconfig1 (10.0.1.5) or ipconfig1 (10.0.1.4)

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/39.png?st=2019-08-26T11%3A16%3A08Z&se=2021-08-27T11%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yqO%2BF4AkNfARcwRc9Mw8W1hpRpJQyR5PYtDLui4KUrY%3D)

   > **Note**: Wait for the operation to complete. This should not take more than 1 minute.

### Task 3: Verify that the outbound rule took effect
 
1. In the Azure portal, navigate to the **az3000802-lb** blade and note the value of the **Public IP address** entry.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/40.png?st=2019-08-26T11%3A16%3A27Z&se=2021-08-27T11%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cLqFrpaug5rKgyd0jYk5Jy%2B2XAzSbAMMW32Zi06r5xI%3D)

2. On the lab computer, from the Remote Desktop session of **az3000801-vm0**, start a Remote Desktop session to **az3000802-vm0**.

To view the RDP session of **az3000801-vm0** click on switch windows icon on the lab computer.If the Remote session was exipred then relogin into the **az3000801-vm0** using the **az3000801-lb** IPAddress with the port number 33890 as shown like in the previous section.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-300-MicrosoftAzureArchitectTechnologies/Instructions/Lab7-Implementing%20Azure%20Load%20Balancer%20Standard.md?token=AHM6QYAONPWKQVJMNJTV3J25NXVQE)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-14.png?st=2019-08-26T12%3A30%3A24Z&se=2021-08-27T12%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bWKLj1F%2BekJ2%2FNTptduyZH%2FCYMP3DHLdarN%2FiznmTmU%3D)

```
az3000802-vm0

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-15.png?st=2019-08-27T04%3A00%3A43Z&se=2021-08-28T04%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=e15cPerWdVxXMRA2sR5PEr5C%2B6AzDG7w6%2BlZwTxnamE%3D)


3. When prompted, authenticate by specifying the following values:
    
```

User name: adminuser

Password: Password@1234

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-9.png?st=2019-08-26T12%3A01%3A58Z&se=2021-08-27T12%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3BKJMcrIYK44CxDYEXB1EE0EkxfDmFYndHlQyxKYZdY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/42.png?st=2019-08-26T11%3A17%3A05Z&se=2021-08-27T11%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aiX842j%2FPDDESLHkOv1HmD97qd05Y8C%2Fcjt0hA%2FBWc4%3D)

4. Within the Remote Desktop session to **az3000802-vm0**, start a Windows PowerShell session and run the following to determine your current public IP address:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-13.png?st=2019-08-26T12%3A26%3A26Z&se=2021-08-27T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c2%2FCwcCDpU%2BkhxjwrT2zIyGbIrZobM9N5GahuwrNVN8%3D)

Run the below command

```pwsh
Invoke-RestMethod http://ipinfo.io/json 
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab7%20-%20Implementing%20Azure%20Load%20Balancer%20Standard/lb7-12.png?st=2019-08-26T12%3A31%3A35Z&se=2021-08-27T12%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TdW8MQnrD3Ym1QuPQU7jPA7L0WRBLVrXUtej4Df8mHo%3D)

5. Review the output of the cmdlet and verify that the IP address entry matches the public IP address you identified earlier in this task.

**Result**: After you completed this exercise, you have configured and tested Azure Load Balancer Standard outbound rules 
