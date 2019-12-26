# Lab: Deploying Network Infrastructure for Use in Azure Solutions

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Configure the lab environment](#exercise-1-configure-the-lab-environment)

[Exercise 2: Review the Hub-spoke topology](#exercise-2-review-the-hub-spoke-topology)


## Overview

The aim of this Lab is to design Hub and Spoke topology by using the Azure Cloud Shell.Configure Vnet Peering and Routing to the Hub and Spoke Design and Reviewing the Hub-spoke topology.

### Scenario and Objectives

Xyz training labs wants to Deploying Network Infrastructure for Use in Azure Solution.

*	Install the Azure Building Blocks npm package in Azure Cloud Shell

*	Implement the hub component of the Hub and Spoke design

*	Implement the spoke components of the Hub and Spoke design

*	Configure the VNet peering of the Hub and Spoke design

*	Configure routing of the Hub and Spoke design

*	Review the Hub-spoke topology

    * 	Examine Peering and routing Configuration
    * 	Verify connectivity between spokes

## Pre-Requisites

*	Knowledge on Azure cloud shell

* 	Knowledge on Azure portal

*	Azure portal Access

**Note** : Azure portal access is provided as part of the lab environment.

## Exercise 1: Configure the lab environment

* Hub Vnet

Azure VNet used as the hub in the hub-spoke topology. The hub is the central point of connectivity to your on-premises network, and a place to host services that can be consumed by the different workloads hosted in the spoke VNets.

* Spoke Vnet

One or more Azure VNets that are used as spokes in the hub-spoke topology. Spokes can be used to isolate workloads in their own VNets, managed separately from other spokes. Each workload might include multiple tiers, with multiple subnets connected through Azure load balancers.

* Vnet Peering

Two VNets can be connected using a peering connection. Peering connections are non-transitive, low latency connections between VNets. Once peered, the VNets exchange traffic by using the Azure backbone, without the need for a router. In a hub-spoke network topology, you use VNet peering to connect the hub to each spoke. You can peer virtual networks in the same region, or different regions

* Routing

Routing is the process of selecting a path for traffic in a network or between or across multiple networks. 

### Task 1: Open the Azure Portal

1. Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Azure Portal Username }}

Azure Password: {{ Azure Portal Password }}

```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/1.png?st=2019-09-05T10%3A30%3A54Z&se=2021-09-06T10%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wqkoSsjnWGEMmARWgXaTiUgI8pAQV%2BsF7Q%2FL4XVBPMg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/2.png?st=2019-09-05T10%3A33%3A48Z&se=2021-09-06T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ayh3i1OYwooNh0Zux9AK4Lv2PBJGp2GJ%2FkCaKtACBcg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.png?st=2019-09-05T10%3A34%3A13Z&se=2021-09-06T10%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pxk3NjVqKDBaA%2BmQzzdkD84ew%2BwYo1WMFmeZrsONJKE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.1.png?st=2019-09-05T11%3A21%3A41Z&se=2021-09-06T11%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ujcp3ZNYYg4q%2BzC3hDB6M6OVvYDsus9wxpME1coauRw%3D)

### Task 2: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

> **Note**: The **Cloud Shell** icon is a symbol that is constructed of the combination of the *greater than* and *underscore* characters.

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/1.png?st=2019-09-20T09%3A44%3A48Z&se=2022-09-21T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=M8AHTIJ5QWCQnilNL5cj0JmmScxheYtp3qmUiGCM8Zw%3D)

> **Note**: If you do not see the configuration options for **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. If so, proceed directly to the next task. 

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/2.png?st=2019-09-20T09%3A45%3A14Z&se=2022-09-21T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=L3gFs1t12yxrGxwI7alzv6DNq4LoPvT%2Fiodk0dFFp2o%3D)

```
Subscription : set to its default value

Cloud Shell region : {{ Location }}

Resource group : {{ ResourceGroup }}

Storage account : ensure that the Create new option is selected and then, in the text box below, type a unique name consisting of a combination of between 3 and 24 characters and digits. 

File share : ensure that the Create new option is selected and then, in the text box below, type cloudshell.

Click the Create storage button.

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/3.png?st=2019-09-20T09%3A46%3A30Z&se=2022-09-21T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9Pg08cfz6dmfoyMBNrf3DvJ%2FMV6ZXDGChC%2BWcGZmhc0%3D)

4. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/4.png?st=2019-09-20T09%3A48%3A04Z&se=2022-09-21T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l30cAEnFvXORD5dPTVujx61z5WcEmlGbG8wz4MhcOxM%3D)

### Task 3: Install the Azure Building Blocks npm package in Azure Cloud Shell

1. At the **Cloud Shell** command prompt at the bottom of the portal, type in the following command and press **Enter** to create a local directory to install the Azure Building Blocks npm package:

```
    mkdir ~/.npm-global
```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to update the npm configuration to include the new local directory:

```
    npm config set prefix '~/.npm-global'
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to open the ~./bashrc configuration file for editing:

```
    vi ~/.bashrc
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/5.png?st=2019-09-20T09%3A48%3A45Z&se=2022-09-21T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FzozNWQmGH6PhXSn72R2EQCK0%2FRkQVNDFYo81%2Bv80%2BU%3D)

4. At the **Cloud Shell** command prompt, in the vi editor interface, scroll down to the bottom of the file (or type **G**), scroll to the right to the right-most character on the last line (or type **$**), type **a** to initiate the **INSERT** mode, press **Enter** to start a new line, and then type the following to add the newly created directory to the system path:

```
    export PATH="$HOME/.npm-global/bin:$PATH"
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/6.png?st=2019-09-20T09%3A49%3A03Z&se=2022-09-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2B0tPEX7uOqw4uZRN8uibqFHvMaGM6DS8n1aJTKRo93M%3D)

5. At the **Cloud Shell** command prompt, in the vi editor interface, to save your changes and close the file, press **Esc**, press **:**, type **wq!** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/7.png?st=2019-09-20T09%3A49%3A21Z&se=2022-09-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XIPfI7zUlsy1Om2MunIpwonKKcy4m26KT490escJTak%3D)

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to install the Azure Building Blocks npm package:

```
    npm install -g @mspnp/azure-building-blocks

```

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to exit the shell:

```
    exit
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/8.png?st=2019-09-20T09%3A50%3A00Z&se=2022-09-21T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5O3lnTj8niSTgLtBHcrpn00GJDKq2WAxNl9H3h7UAlI%3D)

8. In the **Cloud Shell timed out** pane, click **Reconnect**. 

	> **Note**: You need to restart Cloud Shell for the installation of the Buliding Blocks npm package to take effect.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/9.png?st=2019-09-20T09%3A50%3A20Z&se=2022-09-21T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pa1SEXJz2X%2BcBkWL4tqKrFJIkyj9xD0JmAaNKh%2FzycM%3D)

### Task 3: Prepare Building Blocks Hub and Spoke parameter files
1. In the **Cloud Shell** pane, **run** the below command to download the following files.

```
    wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_03/LabFiles/Starter/hub-nva.json?st=2019-09-20T05%3A16%3A39Z&se=2022-09-21T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FhyuoCQZU2TiJkNvT0nTWIIAh4zEvV3ssvFHhYGXxD8%3D"

    wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_03/LabFiles/Starter/hub-vnet-peering.json?st=2019-09-20T05%3A17%3A31Z&se=2022-09-21T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w%2BXj2wtL%2F%2F2HV8Y63%2BGPxmwv5Z%2BMCDYy7hpqjMZ92y8%3D"

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/10.png?st=2019-09-20T09%3A50%3A54Z&se=2022-09-21T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JnfbBBAsLqM91McpSS9lycbKcrlYPlAko%2FEv60SXNDs%3D)

```
    wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_03/LabFiles/Starter/hub-vnet.json?st=2019-09-20T05%3A17%3A46Z&se=2022-09-21T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3K2cGLEMkXgbS84wQNedRf02x%2B4ecRbsuDLXRzTDrr4%3D"

    wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_03/LabFiles/Starter/spoke1.json?st=2019-09-20T05%3A18%3A01Z&se=2022-09-21T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RIDpPZAgQfuATBxrHD6%2FtRD3WqthFELSOVrq0fKkeBE%3D"
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/11.png?st=2019-09-20T09%3A51%3A09Z&se=2022-09-21T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=O%2FKcVEXtsCWvd6VR0H7i1esHwMp3cwKea0ZeX3RZFIA%3D)

```
    wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T04/Module_03/LabFiles/Starter/spoke2.json?st=2019-09-20T05%3A18%3A16Z&se=2022-09-21T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Lkwtrd9uimhe2tbmJdwniWwCX4ggPsp%2FaqSNCGEZtjg%3D"
    
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/12.png?st=2019-09-20T09%3A51%3A24Z&se=2022-09-21T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CpppfChE0XDWg%2Fv92Xd7t1AyHsRmu%2BS2XbmA4Xj00ig%3D)

2. Use the below command to change the file names.(If you get any token related if not don’t run this commands)

```

    mv "hub-nva.json?st=2019-09-20T05%3A16%3A39Z&se=2022-09-21T05%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FhyuoCQZU2TiJkNvT0nTWIIAh4zEvV3ssvFHhYGXxD8%3D" hub-nva.json

	mv "hub-vnet-peering.json?st=2019-09-20T05%3A17%3A31Z&se=2022-09-21T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=w%2BXj2wtL%2F%2F2HV8Y63%2BGPxmwv5Z%2BMCDYy7hpqjMZ92y8%3D" hub-vnet-peering.json

	mv "hub-vnet.json?st=2019-09-20T05%3A17%3A46Z&se=2022-09-21T05%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3K2cGLEMkXgbS84wQNedRf02x%2B4ecRbsuDLXRzTDrr4%3D" hub-vnet.json

	mv "spoke1.json?st=2019-09-20T05%3A18%3A01Z&se=2022-09-21T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RIDpPZAgQfuATBxrHD6%2FtRD3WqthFELSOVrq0fKkeBE%3D" spoke1.json

	mv "spoke2.json?st=2019-09-20T05%3A18%3A16Z&se=2022-09-21T05%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Lkwtrd9uimhe2tbmJdwniWwCX4ggPsp%2FaqSNCGEZtjg%3D" spoke2.json

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/13.png?st=2019-09-20T09%3A52%3A51Z&se=2022-09-21T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z%2B90ZeUYk2R3azFYuT0vZ68029K1JU7Q331tdTj4L90%3D)

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the **hub-vnet.json** Building Blocks parameter file:

```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ~/hub-vnet.json
```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminPassword** parameter with the value **Pa55w.rd1234** in the **hub-vnet.json** Building Blocks parameter file:

```
    sed -i.bak2 's/"adminPassword": ""/"adminPassword": "Pa55w.rd1234"/' ~/hub-vnet.json
```

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the **hub-vnet.json** Building Blocks parameter file:

```
    cat ~/hub-vnet.json
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/14.png?st=2019-09-20T09%3A53%3A09Z&se=2022-09-21T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l9wZel2la5%2FeIM9Z8SBIw7nUbWEaT4F9ANpMWIS2z1c%3D)

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the **hub-nva.json** Building Blocks parameter file:

```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ~/hub-nva.json
```

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminPassword** parameter with the value **Pa55w.rd1234** in the **hub-nva.json** Building Blocks parameter file:

```
    sed -i.bak2 's/"adminPassword": ""/"adminPassword": "Pa55w.rd1234"/' ~/hub-nva.json
```

8. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the **hub-nva.json** Building Blocks parameter file:

```
    cat ~/hub-nva.json
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/15.png?st=2019-09-20T09%3A53%3A39Z&se=2022-09-21T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LaPVFAZM0krzMFy3yK4J%2FPQJPlHsct5qviYJj8SEOMQ%3D)

9. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the **spoke1.json** Building Blocks parameter file:

```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ~/spoke1.json
```

10. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminPassword** parameter with the value **Pa55w.rd1234** in **spoke1.json** the Building Blocks parameter file:

```
    sed -i.bak2 's/"adminPassword": ""/"adminPassword": "Pa55w.rd1234"/' ~/spoke1.json
```

11. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the **spoke1.json** Building Blocks parameter file:

```
    cat ~/spoke1.json
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/16.png?st=2019-09-20T09%3A54%3A11Z&se=2022-09-21T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xb8PUOLsTpJDLqHh5w0TBEpGJamhX1HVh1pgovFvf2A%3D)

12. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminUsername** parameter with the value **Student** in the **spoke2.json** Building Blocks parameter file:

```
    sed -i.bak1 's/"adminUsername": ""/"adminUsername": "Student"/' ~/spoke2.json
```

13. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **adminPassword** parameter with the value **Pa55w.rd1234** in the **spoke2.json** Building Blocks parameter file:

```
    sed -i.bak2 's/"adminPassword": ""/"adminPassword": "Pa55w.rd1234"/' ~/spoke2.json
```

14. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the parameter values were successfully changed in the **spoke2.json** Building Blocks parameter file:

```
    cat ~/spoke2.json
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/17.png?st=2019-09-20T09%3A54%3A55Z&se=2022-09-21T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UVPGKFCP9Ex0MmQoL2u2OSoKWtAVUyf7CpXxUtdvbM0%3D)

### Task 4: Implement the hub component of the Hub and Spoke design

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')
```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that will contain the hub virtual network:

```
    RESOURCE_GROUP_HUB_VNET='{{ ResourceGroup }}'
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment (replace the placeholder `<Azure region>` with the name of the Azure region to which you intend to deploy resources in this lab):

```
    LOCATION='{{ Location }}'

```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the hub component of the Hub-and-Spoke topology by using the Azure Building Blocks:

```
    azbb -g $RESOURCE_GROUP_HUB_VNET -s $SUBSCRIPTION_ID -l $LOCATION -p ~/hub-vnet.json --deploy
    
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/18.png?st=2019-09-20T09%3A55%3A33Z&se=2022-09-21T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QxcvL9BqwVKXww6W%2FfjjieBeWmsP4K0jqxtZsmjMGPs%3D)


### Task 5: Implement the spoke components of the Hub and Spoke design

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')

```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that will contain the first spoke virtual network:

```
    RESOURCE_GROUP_SPOKE1_VNET='{{ ResourceGroup }}'
    
```
3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)
    
```
4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the first spoke component of the Hub-and-Spoke topology by using the Azure Building Blocks:

```
    azbb -g $RESOURCE_GROUP_SPOKE1_VNET -s $SUBSCRIPTION_ID -l $LOCATION -p ~/spoke1.json --deploy

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/19.png?st=2019-09-20T09%3A55%3A59Z&se=2022-09-21T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ozZV%2B5XWjbPy99lZOJFrzplJs0tXw3gzE6N%2FSTWUUTM%3D)

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')

```

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that will contain the second spoke virtual network:

```
    RESOURCE_GROUP_SPOKE2_VNET='{{ ResourceGroup }}'

```

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)

```

8. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the second spoke component of the Hub-and-Spoke topology by using the Azure Building Blocks:

```
    azbb -g $RESOURCE_GROUP_SPOKE2_VNET -s $SUBSCRIPTION_ID -l $LOCATION -p ~/spoke2.json --deploy

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/20.png?st=2019-09-20T09%3A56%3A18Z&se=2022-09-21T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KQ%2B6a8ZATJKVaEr9ToHJbuMLBD9Amgtk5rp1SqjnbVc%3D)

### Task 6: Configure the VNet peering of the Hub and Spoke design

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')

```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that contains the hub virtual network:

```
    RESOURCE_GROUP_HUB_VNET='{{ ResourceGroup }}'

```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)

```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to provision peering of the virtual networks in the Hub-and-Spoke topology by using the Azure Building Blocks:

```
    azbb -g $RESOURCE_GROUP_HUB_VNET -s $SUBSCRIPTION_ID -l $LOCATION -p ~/hub-vnet-peering.json --deploy

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/21.png?st=2019-09-20T09%3A56%3A45Z&se=2022-09-21T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aB1c1OqiKfDq5UaCFqP0WyTekBFtECee%2FUcYumslj2s%3D)

### Task 7: Configure routing of the Hub and Spoke design

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of your Azure subscription:

```
    SUBSCRIPTION_ID=$(az account list --query "[0].id" --output tsv | tr -d '"')

```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that will contain the hub Network Virtual Appliance (NVA) functioning as a router:

```
    RESOURCE_GROUP_HUB_NVA='{{ ResourceGroup }}'

```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
    LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)

```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the NVA component of the Hub-and-Spoke topology by using the Azure Building Blocks:

```
    azbb -g $RESOURCE_GROUP_HUB_NVA -s $SUBSCRIPTION_ID -l $LOCATION -p ~/hub-nva.json --deploy

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/22.png?st=2019-09-20T09%3A57%3A36Z&se=2022-09-21T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KljqYm%2BOh87ENO5WaIiQAw9nPSss0GdCKqdCKXD%2BmjI%3D)

5. Wait for the deployment to complete before you proceed to the next task.

    > **Note**: The deployment can take about 10 minutes.

## Exercise 2: Review the Hub-spoke topology

### Task 1: Examine the peering configuration

1. In the hub menu in the Azure portal, click **All services**.

2. In the **All services** menu, in the **Filter** text box, type **Virtual networks** and press **Enter**.

3. In the list of results, click **Virtual networks**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/23.png?st=2019-09-20T09%3A57%3A58Z&se=2022-09-21T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pSgCWGWmBZAbJOPKFDMq35PuMjlFn672d9yme8AECpc%3D)

4. On the **Virtual networks** blade, click **hub-vnet**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/24.png?st=2019-09-20T09%3A58%3A18Z&se=2022-09-21T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bJQWdT8yss%2BKh%2BmEESLWhBsbWAsMB9r5S673GPajTYg%3D)

5. On the **hub-vnet** blade, click **Peerings**.

6. On the **hub-vnet - Peerings** blade, review the list of peerings and their status.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/25.png?st=2019-09-20T09%3A58%3A45Z&se=2022-09-21T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xNxQaKGSnzX1joiKee29J4vqbzyM0e99T17qgHHfgcY%3D)

7. Navigate back to the **Virtual Networks** blade and click **spoke1-vnet**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/26.png?st=2019-09-20T09%3A59%3A04Z&se=2022-09-21T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vszycgmeZaNg7ElTd86Bdx1TRCOJVFTUCbiqELti064%3D)

8. On the **spoke1-vnet** blade, click **Peerings**.

9. On the **spoke1-vnet - Peerings** blade, review the existing peering and its status.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/27.png?st=2019-09-20T09%3A59%3A19Z&se=2022-09-21T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CTGQCAlEiR%2FRGnJ7fDFQVYr48%2BdBYV2ZjRHuYwQtVEw%3D)

10. Navigate back to the **Virtual Networks** blade and click **spoke2-vnet**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/28.png?st=2019-09-20T09%3A59%3A58Z&se=2022-09-21T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zL3j76BFnJavaKY%2FuWrkd7chUxGIrAY6wkaOXBTBV44%3D)

11. On the **spoke2-vnet** blade, click **Peerings**.

12. On the **spoke2-vnet - Peerings** blade, review the existing peering and its status.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/29.png?st=2019-09-20T10%3A00%3A14Z&se=2022-09-21T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=30hZAZKCc3rcltFvyCUEOZFaMq87JgFY4NEQvIng490%3D)

### Task 2: Examine the routing configuration

1. In the **All services** menu, in the **Filter** text box, type **Route tables** and press **Enter**.

2. In the list of results, click **Route tables**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/30.png?st=2019-09-20T10%3A00%3A51Z&se=2022-09-21T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zGsu6SwmNwO5Mzk%2FLGKk2xkJEM2YL0VR77tvaIgNIkY%3D)

3. On the **Route tables** blade, click **spoke1-rt**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/31.png?st=2019-09-20T10%3A01%3A08Z&se=2022-09-21T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iG8anzBZJhyT0AHWyGF9NYsVyR8EKcFeSEz9%2BJvSNWs%3D)

4. On the **spoke1-rt** blade, review the list of routes. Note the **NEXT HOP** entry for the route **toSpoke2**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/32.png?st=2019-09-20T10%3A01%3A29Z&se=2022-09-21T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GIp9Hg75%2FbmL7MPW182GsJGmNFmu2U0ZYCLZMwK%2BsCs%3D)

5. Navigate back to the **Route tables** blade and click **spoke2-rt**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/33.png?st=2019-09-20T10%3A01%3A53Z&se=2022-09-21T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wJAjXWxEiu89aB%2FHEdNokpe0c4vda3GHhQjLenyKp6M%3D)

6. On the **spoke2-rt** blade, review the list of routes. Note the **NEXT HOP** entry for the route **toSpoke1**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab%209%20-%20Deploying%20Network%20Infrastructure%20for%20Use%20in%20Azure%20Solutions/34.png?st=2019-09-20T10%3A02%3A17Z&se=2022-09-21T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HRvWddxKoILodntrVVMyrQfATmjRQH3hlWFuCWFMZvo%3D)
