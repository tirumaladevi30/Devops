# Lab: Getting Started with Azure Resource Manager Templates and Azure Building Blocks

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Deploy core Azure resources by using an Azure Resource Manager Template from the Azure portal](#exercise-1-deploy-core-azure-resources-by-using-an-azure-resource-manager-template-from-the-azure-portal)

[Exercise 2: Deploy core Azure resources by using Azure Building Blocks from the Azure Cloud Shell](#exercise-2-deploy-core-azure-resources-by-using-azure-building-blocks-from-the-azure-cloud-shell)


## Overview

The aim of this Lab is to deploy core Azure resources using an ARM Template from Azure Portal and Cloud Shell. 

### Scenario and Objectives

After completing this lab, you will be able to:

* Deploying Azure resources using ARM Template from the Azure Portal.

* Deploy Azure resources using ARM Template from the Cloud Shell.

## Pre-Requisites

* Visual Studio Code

* Microsoft Azure Storage Explorer

* Bash on Ubuntu on Windows

* Microsoft Edge

* File Explorer

* Windows PowerShell

> **Note**: You can also find shortcuts to these applications in the **Start Menu**.

## Exercise 1: Deploy core Azure resources by using an Azure Resource Manager Template from the Azure portal

### Task 1: Open the Azure Portal

1. Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Portal Usermail }}

Azure Password: {{ Portal Password }}

```

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/1.png?st=2019-09-18T10%3A06%3A01Z&se=2025-09-19T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XZGeH1jGfqDUwPC78XLyLgTzimoonqiXajPSC2OGSao%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/2.png?st=2019-09-18T10%3A06%3A23Z&se=2025-09-19T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=auyaEFgG5GJgHO7IMAlfdR1pxyeVzhdrpaplc8GLSTs%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/3.png?st=2019-09-18T10%3A06%3A44Z&se=2025-09-19T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BFlxbmlSHHBw%2FNca9EPoSaTDVLO55FZBJMcUkaIQCmE%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/4.png?st=2019-09-18T10%3A07%3A01Z&se=2025-09-19T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xavoBQG6FzWVH%2BvwqWfS4XL0Q0jl33WI2Maa%2B%2FalMMk%3D" alt="image-alt-text" >	


### Task 2: Deploy an Azure virtual network from the Azure portal by using an Azure Resource Manager template

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/5.png?st=2019-09-18T10%3A27%3A58Z&se=2025-09-19T10%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FJd91mJ5JrbG2FGzwqyFRR%2BtRmwTyiue2oYAZOw8FbA%3D)

3. On the **Everything** blade, in the search results, click **Template deployment**.

4. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/6.png?st=2019-09-18T10%3A28%3A33Z&se=2025-09-19T10%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TgFsxoNjFsOiid%2FE2g543YpTixSyA2waxBilPztYyhs%3D)

5. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/7.png?st=2019-09-18T10%3A28%3A52Z&se=2025-09-19T10%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FMvM5t%2F61UXs6nN1ljiRTg2O9CD8AINYklizLubjMks%3D)

6. On the **Edit template** blade, From the **Edit template** blade, clear the existing content, Copy and paste the below url in chrome new window copy the entire content display in that page paste it in template file.

https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/vnet-simple-template.json?st=2019-09-18T10%3A29%3A46Z&se=2025-09-19T10%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ljwCRSOT%2FWZviYHEQQTVYPDM0xAmoEQPnBWCzoFYwL4%3D

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/8.png?st=2019-09-18T10%3A35%3A23Z&se=2025-09-19T10%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hNtZcTPmhIaamrLAkz%2BYi5FFXaIDixkY8S6r0tmVUOA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/9.PNG?st=2019-09-19T09%3A02%3A13Z&se=2025-09-20T09%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tk8IdCZtWzdgx43RSoMn9QAndKvybGXs%2FwAL%2Fvs3yjo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/10.PNG?st=2019-09-19T09%3A03%3A21Z&se=2025-09-20T09%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fT2TTQ9y6OtW6znIiwdDH710A4cWjFRC%2B3qKuM66Bd8%3D)

7. Click the **Save** button to persist the template.

8. Back on the **Custom deployment** blade, perform the following tasks:

```

Subscription: default

Resource group: {{ ResourceGroup }}

Location: {{ location }}

vnetNamePrefix: vnet-

vnetIPPrefix: 10.2.0.0/16

subnetNamePrefix: subnet-

subnetIPPrefix: 10.2.0.0/24

```

In the **Terms and Conditions** section, select the **I agree to the terms and conditions stated above** checkbox.

Click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/11.png?st=2019-09-19T09%3A03%3A47Z&se=2025-09-20T09%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gsE%2FsjO1Y0EIIs7cw2k8e9jWvDiiOmF16DKUAlgfZGA%3D)

9. Wait for the deployment to complete before you proceed to the next task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/12.png?st=2019-09-19T09%3A04%3A13Z&se=2025-09-20T09%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=v3Yqim32%2FqEz2TZt7UkUadRfpX1ZbVNqqR1u%2FWStM7Y%3D)

### Task 3: View deployment metadata

1. In the hub menu of the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click the entry representing the resource group to which you deployed the template in the previous task.

3. With the **Overview** selection active, on the resource group blade, click the **Deployments** link. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/13.png?st=2019-09-19T09%3A04%3A55Z&se=2025-09-20T09%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ePTvlsjSZ0JpKWCX9n1zJFr3mNBRJZU9am2BaZxBEy4%3D)

4. On the resulting blade, click the latest deployment to view its metadata in a new blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/14.png?st=2019-09-19T09%3A05%3A17Z&se=2025-09-20T09%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DonUgsR%2FET%2BCPGimCcYofGp5bpw0tVuS7DAjIqqPhMk%3D)

5. Within the deployment blade, observe the information displayed in the **Operation details** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/15.png?st=2019-09-19T09%3A05%3A33Z&se=2025-09-20T09%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PZeH6R9p4B%2FGS2WKJu5qoxsu44wvPXEZ3%2B00bj%2BppGw%3D)

> **Review**: In this exercise, you deployed an Azure virtual network by using an Azure Resource Manager template from the Azure portal

## Exercise 2: Deploy core Azure resources by using Azure Building Blocks from the Azure Cloud Shell

### Task 1: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

    > **Note**: The **Cloud Shell** icon is a symbol that is constructed of the combination of the *greater than* and *underscore* characters.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/16.png?st=2019-09-19T09%3A06%3A01Z&se=2025-09-20T09%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t8Q6DD%2FZz298QH3qSM5FEa66Ob9Z05Euo8XnWbJP4bs%3D)

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

    > **Note**: If you do not see the configuration options for **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. If so, proceed directly to the next task. 

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

```

Subscription: default

Resource group: {{ ResourceGroup }}

Location: {{ location }}

Storage account: In the Storage account section, ensure that the Create new option is selected and then, in the text box below type a unique name consisting of a combination of between 3 and 24 characters and digits. 

File share: ensure that the Create new option is selected and then, in the text box below, type cloudshell

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/17.png?st=2019-09-19T10%3A02%3A00Z&se=2025-09-20T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OC%2Bf%2FCQ8kE3oif3kA9cN68lcVAf1mycos2mUvrsLX8g%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/18.png?st=2019-09-19T09%3A07%3A33Z&se=2025-09-20T09%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h%2BnydtlmNXy%2B%2FrHB3t1DigxhMAX2Mp2kAhKGK7AZYA4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/19.PNG?st=2019-09-19T09%3A08%3A39Z&se=2025-09-20T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TuK%2FQ7fGpLPFUWmsYV8LXFI9jh5v8EWfYJCJjtnRQkE%3D)

Click the **Create storage** button.


4. Wait for the **Cloud Shell** to finish its first-time setup procedures before you continue to the next task.

### Task 2: Install the Azure Building Blocks npm package in Azure Cloud Shell

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
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/20.png?st=2019-09-19T09%3A11%3A07Z&se=2025-09-20T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2RwSvufRpRhNxwSYWKEdKwZzlfsdhY8QXpxvWDeAv7M%3D)

4. At the **Cloud Shell** command prompt, in the vi editor interface, scroll down to the bottom of the file (or type **G**), scroll to the right to the right-most character on the last line (or type **$**), type **a** to enter the **INSERT** mode, press **Enter** to start a new line, and then type the following to add the newly created directory to the system path:

```
export PATH="$HOME/.npm-global/bin:$PATH"

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/21.png?st=2019-09-19T09%3A11%3A34Z&se=2025-09-20T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Dnmo0IM8NCK05V%2BWiiv8xyWxNza3he4rFiICa8Vqg%2FI%3D)

5. At the **Cloud Shell** command prompt, in the vi editor interface, to save your changes and close the file, press **Esc**, press **:**, type **wq!** and press **Enter**.

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to install the Azure Building Blocks npm package:

```
npm install -g @mspnp/azure-building-blocks

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/22.png?st=2019-09-19T09%3A11%3A53Z&se=2025-09-20T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=h3EgF571fSazjsMeOC0KI%2FsD2g8899aQ34eDRSEX7fE%3D)

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to exit the shell:

```
exit

```

8. In the **Cloud Shell timed out** pane, click **Reconnect**. 

    > **Note**: You need to restart Cloud Shell for the installation of the Buliding Blocks npm package to take effect.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/23.png?st=2019-09-19T09%3A12%3A23Z&se=2025-09-20T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xorOXMzEDS5rhrOBJtQTVQgdO5ceGOs4UaylflnivP8%3D)

### Task 3: Deploy an Azure virtual network from Cloud Shell by using Azure Building Blocks

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to download the GitHub repository containing the Azure Building Blocks templates:

```
git clone https://github.com/mspnp/template-building-blocks.git

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/24.png?st=2019-09-19T09%3A12%3A44Z&se=2025-09-20T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rkYjxwoLCQ6VUr1YQ2vX7tJC1CZ4%2FK%2BP%2Bnui2uJzo0Y%3D)

2.  At the **Cloud Shell** command prompt, type in the following command and press **Enter** to view the content of the Azure Building Block parameter file you will use for this deployment:

```

cat ./template-building-blocks/scenarios/vnet/vnet-simple.json 
    
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy a virtual network by using the Azure Building Blocks:

```
azbb -g '{{ ResourceGroup }}' -s '{{ subscriptionId }}' -l '{{ location }}' -p ./template-building-blocks/scenarios/vnet/vnet-simple.json --deploy
   
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/25.png?st=2019-09-19T09%3A13%3A13Z&se=2025-09-20T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J3OSphny6TA9A%2FUoQvFoQlHSFNq2LXF6V5Llw2KFaQ8%3D)

4. Wait for the deployment to complete before you proceed to the next task.

### Task 4: View deployment metadata

1. On the left side of the portal, click the **Resource groups** link.

2. On the **Resource groups** blade, click the entry representing the resource group presented earlier in this exercise.

3. With the **Overview** selection active, on the resource group blade, click the **Deployments** link. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/26.png?st=2019-09-19T09%3A13%3A32Z&se=2025-09-20T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UaWJ4ceNUW1h3iw6%2FpTfF%2FNKX8g2AbvLM4K0KWaeVOI%3D)

4. On the resulting blade, click the latest deployment to view its metadata in a new blade.it takes few minutes to display.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/27.png?st=2019-09-19T09%3A13%3A48Z&se=2025-09-20T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Z5eyYbgsiN8F7Z6pOba5CXfk%2FhNSIiAGqJuwjf4h%2FvE%3D)

5. Within the deployment blade, observe the information displayed in the **Operation details** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab5/lab5/28.PNG?st=2019-09-19T09%3A55%3A35Z&se=2025-09-20T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yXkb%2B76f4%2BeVNtts%2Bgx3oeHhK7zQ1Kzw52DC6f%2FBgSE%3D)

6. Close the **Cloud Shell** pane.

> **Review**: In this exercise, you deployed an Azure virtual network by using Azure Building Blocks templates from the cloud shell.
