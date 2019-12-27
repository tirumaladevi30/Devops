# Lab 4: Configure Azure DNS

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Configure Azure DNS for Public Domains](#exercise-1-configure-azure-dns-for-public-domains)

[Exercise 2: Configure Azure DNS for Private Domains](#exercise-2-configure-azure-dns-for-private-domains)

## Overview

The Aim of this Lab is Configuring Azure DNS for Public and Private Domains. Creating Azure DNS Zones and records from Azure Portal validating the DNS-based name resolution for the Public Cloud. Also creating Private DNS Zone and Deploying VM's into the Networks using PowerShell.

### Scenario and Objective

XYZ Training Labs Corporation wants to Implement Public and Private DNS Service in Azure without having to deploy its own DNS Servers.

After Completing this Lab, you will be able to:

* Configure Azure DNS for Public Domains

* Configure Azure DNS for Private Domains

**DNS Zone:**

A DNS Zone is a portion of the DNS namespace that is managed by an Organization or Administrator. It serves as an Administrative space with granular control of DNS components and records, such as authoritative nameservers. There is a common misconception that a DNS zone associates only with a single domain name or a single DNS server. In actuality, a DNS Zone can contain multiple domain and subdomains. Multiple zones can also exist on the same server.  Information stored for a DNS zone lives within a text file called a DNS zone file or records.

* **Public DNS** are generally provided to your business by your ISP.  A Public DNS maintains a record of Publicly available domain names reachable from any device with internet access.

* **Private DNS** resides behind a company firewall and maintains records of internal sites. Employees of the company use the Private DNS to access internal sites and services without having to remember IP addresses.

## Pre-Requisites

1. Knowledge on ARM templates deployment

2. Familiar with Azure cloud shell

3. PowerShell

## Exercise 1: Configure Azure DNS for Public Domains

The main tasks for this exercise are as follows:

1. Create a Public DNS zone

2. Create a DNS record in the Public DNS zone

3. Validate Azure DNS-based name resolution for the Public domain

### Task 1: Create a Public DNS zone

1. Using the Chrome browser, login to Azure Portal with the below details:

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal1.png?st=2019-09-05T09%3A42%3A02Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=igNCmxkgy8jEIHJZ6PyjEF9C7%2F%2BIhh1f4y6NOSGhtXM%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal2.png?st=2019-09-05T09%3A42%3A23Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZZUZvHB8wU%2B4qcb5%2FEgwvsWym5BZwrxY0ra%2B8RRjfcg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal3.png?st=2019-09-05T09%3A42%3A40Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wFt6UDhop3gbP%2BwBKG2NA%2FD3u22gYcMYduh8uPmXVZ4%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal4.png?st=2019-09-05T09%3A42%3A55Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gq%2F0iEKqyyV%2F%2FkE%2Fm4OcKfQ4hBKHYowLNbrIUVdSqak%3D) 
 
2. In the Azure Portal, navigate to the Create a resource blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-4.png?st=2019-09-05T09%3A43%3A16Z&se=2022-09-06T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vFssZzNoJS8XJX4jq7VagdKE6m%2BwWCkTDuC4wV7tcT8%3D) 
 
3. From the Create a resource blade, search Azure Marketplace for DNS zone.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-5.png?st=2019-09-05T09%3A43%3A32Z&se=2022-09-06T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5r1T6ZYqNM7NZ9%2FgKJpWdmpuqYEwWJr1rfDB4tH%2FsnY%3D) 
 
4. Select DNS Zone, and then click Create.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-6.png?st=2019-09-05T09%3A43%3A50Z&se=2022-09-06T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cKu6ngajNHv0NcI%2B88sg1Iw3clS0ingDH%2BlIPjXftRM%3D) 
 
5. From the to Create DNS zone blade, create a new DNS zone with the following settings:

* **Subscription:** `Select as default from the dropdown` <br>
* **Resource group:** `{{resource-group-name}}` <br>
* **Name:** any unique, valid DNS domain name in the .com namespace <br>
* **Resource group location:** `{{location}}`

 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/1.PNG?st=2019-09-05T09%3A44%3A13Z&se=2022-09-06T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1CpZ%2B%2BTTHhPytaO174B7NtE9ptjN3WQLoNgzb4GXPQY%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/2.PNG?st=2019-09-05T09%3A44%3A29Z&se=2022-09-06T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9FWx2dORhIE36L8a%2Fvgni1ze9Zb%2FYAy2Qjs3v2h4F4Y%3D) 

### Task 2: Create a DNS record in the Public DNS zone

1. From the Azure Portal, start a PowerShell session in the Cloud Shell.

> **Note**: If this is the first time you are launching the Cloud Shell in the current Azure Subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, click on **Show advanced settings** and choose already existing Resource group enter the details, which will result in creation of a storage account in already existing Resource group.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-9.png?st=2019-09-05T09%3A44%3A52Z&se=2022-09-06T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lKGIFjYD7y6Ajkeuy1P37P8kKHPVqkdWfzUiG%2FW3WhA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-10.png?st=2019-09-05T09%3A45%3A14Z&se=2022-09-06T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=K%2BtTEy94TU0m2F18MDCEPYbmYFXqfRtubHoWq4prTFQ%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/3.PNG?st=2019-09-05T09%3A45%3A37Z&se=2022-09-06T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Tbcln9OgD3KLdgbprzwVV5A%2BN7S4wSWAOVL426Kdltk%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/4.PNG?st=2019-09-05T09%3A45%3A57Z&se=2022-09-06T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YMehBtP4civYvz22GFXhVn1mQrwNqrW77FcjwMxmgxo%3D) 

2. In the Cloud Shell pane, run the following in order to identify the Public IP address of your lab computer:

```
Invoke-RestMethod http://ipinfo.io/json | Select-Object -ExpandProperty IP
```

> **Note**: Take a note of this IP address. You will use it later in this task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/5.PNG?st=2019-09-05T09%3A46%3A14Z&se=2022-09-06T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=12NAntn7rsmcxgvrjFG7aV%2Bm3BiGfkLlan3M17X%2BzlE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/5.1.png?st=2019-09-05T09%3A46%3A28Z&se=2022-09-06T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vXYJqQjxN3aA6%2F6vk4y2B3KiH0Pd0qWAiRifAnIxe84%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/6.PNG?st=2019-09-05T09%3A46%3A47Z&se=2022-09-06T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FAl1T1O6%2BNKDSZ18%2Buhg6GY4AJzGa1747DtPkSOitmQ%3D) 
 
Here the example IP is 168.61.21.45

3. In the Cloud Shell pane, run the following in order to create a Public IP address resource:

```
$rg = Get-AzResourceGroup -Name {{resource-group-name}}

New-AzPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -Sku Basic -AllocationMethod Static -Name az1000401b-pip -Location $rg.Location
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/7.PNG?st=2019-09-05T09%3A47%3A06Z&se=2022-09-06T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=di8ObO8Rk5HpL3SOWDK9Gl5imlOsiai5Wii8IwXrjWM%3D) 
 
4. In the Azure Portal, navigate to the {{resource-group-name}} resource group blade.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/8.PNG?st=2019-09-05T10%3A09%3A42Z&se=2022-09-06T10%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8TzMdIXbHMw5lKxfNI6Y2ZRmBH%2FWga2LP%2F1TUeywBrA%3D) 

5. From the {{resource-group-name}} resource group blade, navigate to the blade displaying newly created Public DNS zone.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/9.PNG?st=2019-09-05T10%3A10%3A09Z&se=2022-09-06T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MwTEa3brHp3MdzPzeKifC3f9BWe69AVYjbD4DsKZeZg%3D) 
 
6. From the DNS zone blade, click **+ Record set** to navigate to the **Add record set** blade

7. Create a DNS record with the following settings:

```
Name: mylabvmpip

Type: A

Alias record set: No

TTL: 1

TTL unit: Hours

IP ADDRESS: the Public IP address of your lab computer you identified earlier in this task
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/10.PNG?st=2019-09-05T10%3A10%3A41Z&se=2022-09-06T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=78dREDnCPzCdiajg0Dtoa8o15le%2FDlAU%2FDJiilkdQWc%3D) 

8. From the Overview blade, click **+ Record set**, and create another record with the following settings:


```
Name: myazurepip

Type: A

Alias record set: Yes

Alias type: Azure resource

Choose a subscription: the name of the Azure subscription you are using in this lab

Azure resource: az1000401b-pip

TTL: 1

TTL unit: Hours

```


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/11.PNG?st=2019-09-05T10%3A11%3A02Z&se=2022-09-06T10%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AP02yMGZhQoW2woAZK7cHvCa%2F0mC3ge3d%2Ff0l6%2BAGZ0%3D) 

### Task 3: Validate Azure DNS-based name resolution for the Public domain

1. On the DNS zone blade, note the list of the name servers that host the zone you created. You will use the first of them named in the next step.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/12.PNG?st=2019-09-05T10%3A11%3A20Z&se=2022-09-06T10%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GOzomvL%2BTS70dzfCk6cLDnAF2k7BFyE5%2BwPVoH67UEU%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/13.PNG?st=2019-09-05T09%3A49%3A13Z&se=2022-09-06T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kEHisUz1fLpTxa3u0nCjVTq8o3b25gRmS%2BkzOW%2FniyY%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/14.PNG?st=2019-09-05T09%3A49%3A27Z&se=2022-09-06T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g2ojCMz9mxgNHhJjkAMCMKrWc9j3mDa1CeVDMO3wNdw%3D) 
 
2. Verify that the IP addresses returned match those you identified earlier in this task.

3. From the lab virtual machine, start **Git Bash** and run the following to validate the name resolution of the two newly created DNS records (where `<custom_DNS_domain>` represents the custom DNS domain you created in the first task of this exercise and `<name_server>` represents the name of the DNS name server you identified in the previous step)


```
nslookup mylabvmpip.<custom_DNS_domain> <name_server>
   
nslookup myazurepip.<custom_DNS_domain> <name_server>
```


**Ex:**  nslookup mylabvmpip.az103dns.com ns1-02.azure-dns.com.

**Ex:** nslookup myazurepip.az103dns.com ns1-02.azure-dns.com.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/17.PNG?st=2019-09-05T09%3A49%3A44Z&se=2022-09-06T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=f5oLxaHTqr06WrWCXjLiiao6ad1G0fAENGYTk2yC%2Fw4%3D) 

> **Result**: After you completed this exercise, you have created a Public DNS zone, created a DNS record in the Public DNS zone, and validated Azure DNS-based name resolution for the Public domain.

## Exercise 2: Configure Azure DNS for Private Domains

The main tasks for this exercise are as follows:

1. Provision a multi-virtual network environment

2. Create a Private DNS zone

3. Deploy Azure VMs into virtual networks

4. Validate Azure DNS-based name reservation and resolution for the Private domain

### Task 1: Provision a multi-virtual network environment

1. From the Azure Portal, start a PowerShell session in the Cloud Shell.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/18.PNG?st=2019-09-05T09%3A50%3A29Z&se=2022-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rnftJx70MZSLNcvdFrNT3CT1Fu57WItydcvypCl4vn8%3D)

2. In the Cloud Shell pane, run the following in order to create a resource group:


```
$rg1 = Get-AzResourceGroup -Name '{{resource-group-name}}'

```


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/19.PNG?st=2019-09-05T09%3A50%3A45Z&se=2022-09-06T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HDALJR6UDVQW9OYyWv3YXwYraXEqH8LsniK9E%2BZSavM%3D) 
	 
3. In the Cloud Shell pane, run the following in order to create two Azure virtual networks:

```
$subnet1 = New-AzVirtualNetworkSubnetConfig -Name subnet1 -AddressPrefix '10.104.0.0/24'
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/20.PNG?st=2019-09-05T09%3A51%3A00Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HSHOi4iSN87Tza2NS0SdaLgvZU3E%2BWiZKruez3OFfEw%3D) 

```
$vnet1 = New-AzVirtualNetwork -ResourceGroupName $rg1.ResourceGroupName -Location $rg1.Location -Name az1000402b-vnet1 -AddressPrefix 10.104.0.0/16 -Subnet $subnet1
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/21.PNG?st=2019-09-05T09%3A51%3A15Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0wenhia2QXhxSWWIY0vUm0vbY3UOn4klLzmLxKVbiyo%3D) 

```
$subnet2 = New-AzVirtualNetworkSubnetConfig -Name subnet1 -AddressPrefix '10.204.0.0/24'
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/22.PNG?st=2019-09-05T09%3A51%3A30Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=32NwNsLnHnRmCBnq47AYQ1bTawoQZXhECNp0u0KKY64%3D) 

```
$vnet2 = New-AzVirtualNetwork -ResourceGroupName $rg1.ResourceGroupName -Location $rg1.Location -Name az1000402b-vnet2 -AddressPrefix 10.204.0.0/16 -Subnet $subnet2
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/23.PNG?st=2019-09-05T09%3A51%3A47Z&se=2022-09-06T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BXwLAZUB2%2Fn3OEh04THrxLsynGH4h%2FLmiIl8oFwfCwQ%3D) 
 
### Task 2: Create a Private DNS zone

1. In the Cloud Shell pane, run the following in order to create a Private DNS zone with the first virtual network supporting registration and the second virtual network supporting resolution:

```
$vnet1 = Get-AzVirtualNetwork -Name az1000402b-vnet1

$vnet2 = Get-AzVirtualNetwork -name az1000402b-vnet2

New-AzDnsZone -Name adatum.local -ResourceGroupName $rg1.ResourceGroupName -ZoneType private -RegistrationVirtualNetworkId @($vnet1.Id) -ResolutionVirtualNetworkId @($vnet2.Id)
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/24.PNG?st=2019-09-05T09%3A52%3A04Z&se=2022-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wTCtB6hh7EE6uQKGDUmQ8QMzJNnQkmlRzzIngU7AFm4%3D) 

> **Note**: Virtual networks that you assign to an Azure DNS zone cannot contain any resources.

2. In the Cloud Shell pane, run the following in order to verify that the Private DNS zone was successfully created:

```
Get-AzDnsZone -ResourceGroupName $rg1.ResourceGroupName
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/25.PNG?st=2019-09-05T09%3A52%3A21Z&se=2022-09-06T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yf3c%2FGBGOI5bLvGnEVyn94THEHHADHzi7n%2F5iaopEq8%3D) 
 
### Task 3: Deploy Azure VMs into virtual networks

**Lab files:**

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04b_01_azuredeploy.json?st=2019-09-05T08%3A55%3A37Z&se=2022-09-06T08%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UiJX%2F0EsNKGBYZuiP7b1gclWsFAQTSKfrAWn9j6bjv0%3D**

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04b_02_azuredeploy.json?st=2019-09-05T08%3A58%3A40Z&se=2022-09-06T08%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2roPFGKtrZ45mZz%2BLPM9B7Cq6HrqfTlnJTvvRu1G9Is%3D**

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04_azuredeploy.parameters.json?st=2019-09-05T08%3A59%3A02Z&se=2022-09-06T08%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ytyxog%2FU4z16U2dBr5MwIMHR%2BW0UH1IXDwWiWZWF7Sg%3D**

1. Download **az-100-04b_01_azuredeploy.json**, **az-100-04b_02_azuredeploy.json**,and **az-100-04_azuredeploy.parameters.json** Azure resource manager template files into Cloud Shell home directory.

To download the above files into the cloud shell, run the following commands.

``` 
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04b_01_azuredeploy.json?st=2019-09-05T08%3A55%3A37Z&se=2022-09-06T08%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UiJX%2F0EsNKGBYZuiP7b1gclWsFAQTSKfrAWn9j6bjv0%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n1.PNG?st=2019-09-19T05%3A15%3A46Z&se=2022-09-20T05%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=139TjVRSH4AJlb%2F9sDqy%2FAuaVuY1UW8MigN%2FnsbvwMg%3D) 

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04b_02_azuredeploy.json?st=2019-09-05T08%3A58%3A40Z&se=2022-09-06T08%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2roPFGKtrZ45mZz%2BLPM9B7Cq6HrqfTlnJTvvRu1G9Is%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n2.PNG?st=2019-09-19T05%3A16%3A02Z&se=2022-09-20T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=miTqXis2UycFAiHD9WsuZcltDDOJfeqDZttx6svH%2Bog%3D) 

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Allfiles/Labfiles/Module_04/Configure_Azure_DNS/az-100-04_azuredeploy.parameters.json?st=2019-09-05T08%3A59%3A02Z&se=2022-09-06T08%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ytyxog%2FU4z16U2dBr5MwIMHR%2BW0UH1IXDwWiWZWF7Sg%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n3.PNG?st=2019-09-19T05%3A16%3A19Z&se=2022-09-20T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IR2BpX5xNxJFoiDrJROyonwigHziWtbhB8hQHpt1p4A%3D) 

Run the below command to list the uploaded files.

```
ls 

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n4.PNG?st=2019-09-19T05%3A16%3A35Z&se=2022-09-20T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BnBln4uf89cf8nAbKcqbnEiN6xiDzrPgWj1oXJP3la4%3D) 

Run the below command to change the file names after downloading.

```
mv "az-100-04_azuredeploy.parameters.json?st=2019-09-05T08%3A59%3A02Z&se=2022-09-06T08%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ytyxog%2FU4z16U2dBr5MwIMHR%2BW0UH1IXDwWiWZWF7Sg%3D" az-100-04_azuredeploy.parameters.json

mv "az-100-04b_01_azuredeploy.json?st=2019-09-05T08%3A55%3A37Z&se=2022-09-06T08%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UiJX%2F0EsNKGBYZuiP7b1gclWsFAQTSKfrAWn9j6bjv0%3D" az-100-04b_01_azuredeploy.json

mv "az-100-04b_02_azuredeploy.json?st=2019-09-05T08%3A58%3A40Z&se=2022-09-06T08%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2roPFGKtrZ45mZz%2BLPM9B7Cq6HrqfTlnJTvvRu1G9Is%3D" az-100-04b_02_azuredeploy.json

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n7.PNG?st=2019-09-23T06%3A22%3A53Z&se=2022-09-24T06%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=r2%2BIPZeAuwLHbi3Pxy4P%2Fu%2FSMR777ALKsVtzfvPEzfo%3D)

Run the below command to list the uploaded files.

```
ls 

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/n6.PNG?st=2019-09-19T05%3A17%3A02Z&se=2022-09-20T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KG7%2BFg2vGdJlnC0fSHmx3olkHciUuIo8mwjdmW%2BfOCA%3D)

2. In the Cloud Shell pane, run the following in order to deploy an Azure VM into the first virtual network:

```
cd $home

New-AzResourceGroupDeployment -ResourceGroupName $rg1.ResourceGroupName -TemplateFile "./az-100-04b_01_azuredeploy.json" -TemplateParameterFile "./az-100-04_azuredeploy.parameters.json" -AsJob
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/29.PNG?st=2019-09-05T09%3A53%3A53Z&se=2022-09-06T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YxOZfH015OOZGNCLMo14OXIKRTwnAu5SiaSMGYzfyEo%3D)
	 
3. In the Cloud Shell pane, run the following in order to deploy an Azure VM into the second virtual network:

```
New-AzResourceGroupDeployment -ResourceGroupName $rg1.ResourceGroupName -TemplateFile "./az-100-04b_02_azuredeploy.json" -TemplateParameterFile "./az-100-04_azuredeploy.parameters.json" -AsJob
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/30.PNG?st=2019-09-05T09%3A54%3A10Z&se=2022-09-06T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aKl%2F1ba26KvYOYWW3O7dt2%2F%2BFAkC%2FuphAqyULOMwy24%3D)
 
> **Note**: Wait for both deployments to complete before you proceed to the next task. You can identify the state of the jobs by running the below cmdlet in the Cloud Shell pane.

```
Get-Job
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/31.PNG?st=2019-09-05T09%3A54%3A26Z&se=2022-09-06T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t6VrnPt%2BUmgQFqyiaQ7iD%2BjDEeh0yz4WMCewGcgSDTg%3D)

### Task 4: Validate Azure DNS-based name reservation and resolution for the Private domain

1. In the Azure Portal, navigate to the blade of the **az1000402b-vm2** Azure VM.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/32.PNG?st=2019-09-05T10%3A15%3A57Z&se=2022-09-06T10%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HQ9pz%2FeXuLKmrKrDmEB2RE0n4dfoSSRoeN9o2pvGGp8%3D)

2. From the **Overview** pane of the **az1000402b-vm2** blade, Copy the **Public IP address**.

3. Open the **Remote Desktop Client** as shown like below and paste the copied Public IP address to connect to **az1000402b-vm2**.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/33.PNG?st=2019-09-05T10%3A16%3A17Z&se=2022-09-06T10%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YspH9uDmAlMwUCuPCuc06brm1s1XEmKfpcRJgjMgiJo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/34.5.png?st=2019-09-05T09%3A55%3A13Z&se=2022-09-06T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cWzaM2jMxjx18o8SxYnKaDp0nLJOsZJgEwOMol%2FMnSg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/34.PNG?st=2019-09-05T09%3A55%3A26Z&se=2022-09-06T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m7xO1GgLeQFR%2F%2FpCE7gAqkX3M6TjejThmahk5qRfUsw%3D)

3. When prompted, authenticate by specifying the following credentials:

```
User name: adminuser

Password: Password@1234
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/35.PNG?st=2019-09-05T09%3A55%3A43Z&se=2022-09-06T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LgDhIGw8llBRhQmjdEVseeVSVOoSP3aWWR69pmqqpes%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/36.PNG?st=2019-09-05T09%3A56%3A00Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Yaf%2FdFPLNI0eJpwwI61n7epA%2Fuub1wS3vrHdCsUPqP8%3D)

4. Click on **Yes** to continue.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/37.PNG?st=2019-09-05T09%3A56%3A17Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pKvhpBK00wJxU%2BVCaEYJsiJ7ccEqgfbBY8EyQzk919Y%3D)

> **Note**: If the Networks prompted after login to Remote Desktop session, then click **Yes** to continue. If not just ignore the below screen and proceed to next step.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/38.PNG?st=2019-09-05T09%3A56%3A30Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tSVojeEMyFx8BnVnt1DQ5EolCSBw6NSVBsh8aM%2FK8eQ%3D)
 
5. Within the Remote Desktop session to **az1000402b-vm2**, start a Command Prompt window and run the following:


```
nslookup az1000402b-vm1.adatum.local
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/40.PNG?st=2019-09-05T09%3A56%3A47Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DwirkQLGBOuBieE07ENqLJvRyp1qVlzRIUmDYPMbKfg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/41.PNG?st=2019-09-05T09%3A56%3A59Z&se=2022-09-06T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gHkHN3j0ahGV%2Bato3QkGpdP%2F6vq8KOVMaZbMoMrdk2M%3D)


6. Verify that the name is successfully resolved.

7. Switch back to the lab virtual machine and, in the Cloud Shell pane of the / window, run the following in order to create an additional DNS record in the Private DNS zone:

```
$rg1 = Get-AzResourceGroup -Name '{{resource-group-name}}'

New-AzDnsRecordSet -ResourceGroupName $rg1.ResourceGroupName -Name www -RecordType A -ZoneName adatum.local -Ttl 3600 -DnsRecords (New-AzDnsRecordConfig -IPv4Address "10.104.0.4")

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/42.png?st=2019-09-18T05%3A10%3A21Z&se=2022-09-19T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YOgrxVQBQ7AUdM%2FwtnQhcK8RNYFLxVhaur1P9myDugs%3D)
 
8. Switch again to the Remote Desktop session to **az1000402b-vm2** and run the following from the Command Prompt window:

```
nslookup www.adatum.local
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/lab4-45.png?st=2019-09-05T09%3A58%3A30Z&se=2022-09-06T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=T%2B%2Bt6pWITrlluvvhFNp8ChOFwznvZ8UA3mjZEd718Bg%3D)
 
9. Verify that the name is successfully resolved.

> **Result**: After completing this exercise, you have provisioned a multi-virtual network environment, created a Private DNS zone, deployed Azure VMs into virtual networks, and validated Azure DNS-based name reservation and resolution for the Private domain
