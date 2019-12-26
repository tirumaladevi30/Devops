# Lab-7: Deploying Serverless Workloads to Azure

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Create Web App](#exercise-1-create-web-app)

[Exercise 2: Deploy Web App code](#exercise-2-deploy-web-app-code)

## Overview

The aim of this lab is about creating an web app Using ARM template and Pushing the application code from GitHub into the webapp using Azure CLI. Also pushing the Application code from the container into the webapp. 

### Scenario and Objectives

Xyz training labs wants to Deploy Serverless Workloads to Azure

After completing this lab, you will be able to:

* Create Web App

* Deploy Web App code

## Pre-Requisites

* Familiar with ARM template 

* Familiar with Azure cloud shell

> **Note:** Azure CLoud Shell is a part of Azure Portal.

> **Note:** ARM Template is provided as a part of this lab.

## Exercise 1: Create Web App

### Task 1: Open the Azure Portal

Using the Chrome browser, login to Azure Portal with the below details:

 Azure Username : {{ Portal Useremail }}

 Azure Password : {{ Portal Password }}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal1.png?st=2019-09-05T09%3A42%3A02Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=igNCmxkgy8jEIHJZ6PyjEF9C7%2F%2BIhh1f4y6NOSGhtXM%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal2.png?st=2019-09-05T09%3A42%3A23Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZZUZvHB8wU%2B4qcb5%2FEgwvsWym5BZwrxY0ra%2B8RRjfcg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal3.png?st=2019-09-05T09%3A42%3A40Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wFt6UDhop3gbP%2BwBKG2NA%2FD3u22gYcMYduh8uPmXVZ4%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab4%20-%20Configure%20Azure%20DNS/portal4.png?st=2019-09-05T09%3A42%3A55Z&se=2022-09-06T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gq%2F0iEKqyyV%2F%2FkE%2Fm4OcKfQ4hBKHYowLNbrIUVdSqak%3D)

### Task 2: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/12.PNG?st=2019-09-18T06%3A45%3A58Z&se=2022-09-19T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3yfaFRdhsWiQaZEvn1Nefdu4O4WQtn4hh94GoPzo2L4%3D)

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/13.PNG?st=2019-09-18T06%3A46%3A13Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cVRxzy1bUmzuNfi6teAMUtOamRnxHysWYJRQihauX5g%3D)

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/14.PNG?st=2019-09-18T06%3A46%3A29Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QSZxJLQZLtQZN7R2fSNyQUruIBNpGhQBwh0Q%2BlPLUTU%3D)

```
 Subscription: Leave the Subscription drop-down list entry set to its default value.

 Cloud Shell region: {{ Location }}

 Resource group: {{ ResourceGroup }}

 Storage account: a name of a new storage account

 File share: a name of a new file share

```

4. Click the **Create storage** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/15.PNG?st=2019-09-18T06%3A46%3A46Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OcXDEJVzXf11bcrm0BYy6zd4rodd%2B3F6oDlwfdLySBA%3D)

5. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

### Task 3: Create an App Service plan

1. At the **Cloud Shell** command prompt at the bottom of the portal, type in the following command and press **Enter** to create a variable which value designates the name of the resource group you will use in this exercise:

```
 RESOURCE_GROUP_APP='{{ ResourceGroup }}'
```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment (Enter the name of the region when prompted):

```
 read -p 'Region: ' LOCATION
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new App Service plan:

```
 az appservice plan create --is-linux --name "AADesignLab0502-$LOCATION" --resource-group $RESOURCE_GROUP_APP --location $LOCATION --sku B2
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/1.PNG?st=2019-09-19T12%3A22%3A59Z&se=2022-09-20T09%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g9xAY0Wia%2BSzJcJQxBvUBUqwpjywo0fm56rjFdwFxzw%3D)

### Task 4: Create a Web App instance

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to view a list of possible runtimes for a Linux-based App Service web app instance: 

```
 az webapp list-runtimes --linux --output tsv
``` 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/2.PNG?st=2019-09-19T12%3A23%3A28Z&se=2022-09-20T12%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uC3BfDfgR04dqP2wPvJv%2B94P4vIwQLE7xLr2T7NouUg%3D)

2. At the **Cloud Shell** command prompt, type the following command and press **Enter** to create a new variable which value is a randomly generated string that you will use as the name of a new web app:

```
 WEBAPPNAME1=webapp05021$RANDOM$RANDOM
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new web app using a unique name:

```
 az webapp create --name $WEBAPPNAME1 --plan AADesignLab0502-$LOCATION --resource-group $RESOURCE_GROUP_APP --runtime "DOTNETCORE|2.1"
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/3.PNG?st=2019-09-19T12%3A23%3A44Z&se=2022-09-20T12%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gCGHtCzIf%2BwV5VBdihaalHeezmRXEOjgKxetfb%2Fdl%2FY%3D)

> **Note**: In case the command fails due to duplicate web app name, re-run the last two steps until the command completes successfully

4. Wait for the deployment to complete before you proceed to the next task.

### Task 5: View deployment results

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{ ResourceGroup }}.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/4.PNG?st=2019-09-19T12%3A23%3A57Z&se=2022-09-20T12%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fba8T0pZrpteh3gi9%2FSC2FVpW4IG37kIJzKQKtJeztM%3D)

3. On the {{ ResourceGroup }} blade, click the entry representing the Azure web app you created earlier in this exercise.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/5.PNG?st=2019-09-19T12%3A24%3A09Z&se=2022-09-20T12%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dvorkU4wJktqNPZuW%2BX0dP1t5ZztT7gphI8Pky2PJQg%3D)

4. On the web app blade, click the **Browse** button at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/6.PNG?st=2019-09-19T12%3A24%3A22Z&se=2022-09-20T12%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dUX09WEjEouyLk%2FJnvLrZYDGjM1SWD7eRfgvbQSbRr0%3D)

5. Result the default page generated by Azure App Service.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/7.PNG?st=2019-09-19T12%3A24%3A37Z&se=2019-09-20T12%3A24%3A37Z&sp=rl&sv=2018-03-28&sr=b&sig=5m2bCHyVXCCF2%2FDIWvJUJylbHGFsOjSUl%2BCfCAsXyT8%3D)

6. Close the new browser tab and return to the browser tab displaying the Azure portal.

> **Result**: In this exercise, you created a Linux-based App Service Plan that contained a blank web app. 

## Exercise 2: Deploy Web App code

### Task 1: Deploy code with a Web App Extension using an Azure Resource Manager template and GitHub

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group you will use in this exercise:

```
 RESOURCE_GROUP_APP='{{ ResourceGroup }}'
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/8.PNG?st=2019-09-19T12%3A24%3A56Z&se=2022-09-20T12%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Q7bErUXW5eEOT8NnAtKZCrk%2FSkm5YsWHDOwj3wzvziY%3D)

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
 LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)
```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new variable which value is a randomly generated string that you will use as the name of a new web app:

```
 WEBAPPNAME2=webapp05022$RANDOM$RANDOM
```

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new web app using a unique name:

```
 az webapp create --name $WEBAPPNAME2 --plan AADesignLab0502-$LOCATION --resource-group $RESOURCE_GROUP_APP --runtime "NODE|9.4"
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/9.PNG?st=2019-09-19T12%3A25%3A17Z&se=2022-09-20T12%3A25%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sOlRtxPQ6zyqFYVKBcnSu8KUXAWbi8KweOOT3CsyED4%3D)

> **Note**: In case the command fails due to duplicate web app name, re-run the last two steps until the command completes successfully

6. In the hub menu in the Azure portal, click **Resource groups**.

7. On the **Resource groups** blade, click {{ ResourceGroup }}.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/10.PNG?st=2019-09-20T06%3A39%3A48Z&se=2022-09-21T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EmKaqmDY2cYL9DCvopf4REVTU%2Bi0AXxnBBFNx3yCvhg%3D)

8. On the {{ ResourceGroup }} blade, click the entry representing the Azure web app you created earlier in this exercise.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/11.PNG?st=2019-09-20T06%3A40%3A05Z&se=2022-09-21T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hPpl4IJvNJfEfU19Qo0ZpWc2u0Qok5i%2BUrAUXBPPGoQ%3D)

9. On the web app blade, click the **Browse** button at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/12.PNG?st=2019-09-20T06%3A40%3A19Z&se=2022-09-21T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lncGnZJ0f0HzWmsKnTt54NCGhxrMf%2FAOForUfaUpbNg%3D)

10. Result the default page generated by Azure App Service.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/13.PNG?st=2019-09-20T06%3A40%3A35Z&se=2022-09-21T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JMe3emQxnvJxdluN82ZGFfvmsgW0oc1VWS4KQbGsWVw%3D)

**Lab files:**

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T03/Module_03/LabFiles/Starter/github.json?st=2019-09-19T12%3A04%3A57Z&se=2022-09-20T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a9qYIBTF98TZ10qxZ7l8%2Fc5XeRGbgSGSEDT1vasRd3I%3D**

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T03/Module_03/LabFiles/Starter/parameters.json?st=2019-09-19T12%3A05%3A30Z&se=2022-09-20T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cm2WqBIN1uaEifWdoJW5dqLpDcdv53anHhcpDtk85oY%3D**

6. Download **github.json** and **parameters.json** Azure resource manager template files into Cloud Shell home directory.

To download the above files into the cloud shell, run the following commands.

```
wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T03/Module_03/LabFiles/Starter/github.json?st=2019-09-19T12%3A04%3A57Z&se=2022-09-20T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a9qYIBTF98TZ10qxZ7l8%2Fc5XeRGbgSGSEDT1vasRd3I%3D"

wget "https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T03/Module_03/LabFiles/Starter/parameters.json?st=2019-09-19T12%3A05%3A30Z&se=2022-09-20T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cm2WqBIN1uaEifWdoJW5dqLpDcdv53anHhcpDtk85oY%3D"

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/n1.PNG?st=2019-09-20T06%3A28%3A36Z&se=2022-09-21T06%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lmwRQCo0vdFlSwwBOl13zbhKDwAvtaa67iB4EdfyW3U%3D)

Run the below command to list the uploaded files.

```
ls
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/n2.PNG?st=2019-09-20T06%3A28%3A59Z&se=2022-09-21T06%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Y1YzMiGKfLxxNNTBdOI5WvPbZfjFsVpjdJFW0E83pLc%3D)

Run the below command to change the file names after downloading.

```
mv "github.json?st=2019-09-19T12%3A04%3A57Z&se=2022-09-20T12%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=a9qYIBTF98TZ10qxZ7l8%2Fc5XeRGbgSGSEDT1vasRd3I%3D" github.json

mv "parameters.json?st=2019-09-19T12%3A05%3A30Z&se=2022-09-20T12%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cm2WqBIN1uaEifWdoJW5dqLpDcdv53anHhcpDtk85oY%3D" parameters.json

```

Run the below command to list the uploaded files.

```
ls

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/n3.PNG?st=2019-09-20T06%3A29%3A16Z&se=2022-09-21T06%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Td3bcyfVD6cLCpPpg1cW7R6v8eU1vOLjfRq8X2x6t6A%3D)


10. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the GitHub repository hosting the web app code:

```
 REPOSITORY_URL='https://github.com/Azure-Samples/nodejs-docs-hello-world'
```

11. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the GitHub repository hosting the web app code and which takes into account any special character the URL might include:

```
 REPOSITORY_URL_REGEX="$(echo $REPOSITORY_URL | sed -e 's/\\/\\\\/g; s/\//\\\//g; s/&/\\\&/g')"
```

> **Note**: This is necessary because you will use the **sed** utility to insert this string into the Azure Resource Manager template parameters file. Alternatively, you could simply open the file and enter the URL string directly into the file.

12. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the value of the **webAppName** parameter with the value of the **$WEBAPPNAME2** variable in the parameters file:

```
 sed -i.bak1 's/"$WEBAPPNAME2"/"'"$WEBAPPNAME2"'"/' ~/parameters.json
```

13. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the value of the **repositoryUrl** parameter with the value of the **$REPOSITORY_URL** variable in the parameters file:

```
 sed -i.bak2 's/"$REPOSITORY_URL"/"'"$REPOSITORY_URL_REGEX"'"/' ~/parameters.json
```

14. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the placeholders were successfully replaced in the parameters file:

```
 cat ~/parameters.json
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/14.PNG?st=2019-09-19T12%3A26%3A29Z&se=2022-09-20T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MTurwoxKiujfZpza09yEsKbTu8OYVJexl8wq55yaMmk%3D)

15. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the GitHub-resident web app code by using a local Azure Resource Manager template and a local parameters file:

```
 az group deployment create --resource-group $RESOURCE_GROUP_APP --template-file github.json --parameters @parameters.json
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/15.PNG?st=2019-09-19T12%3A26%3A41Z&se=2022-09-20T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uIQTtXDM6IiPXdPklSvBTp95UMEgSHTv5vB2umg8Zow%3D)

16. Wait for the deployment to complete before you proceed to the next task.

> **Note**: The deployment should take about a minute.

### Task 2: View deployment results

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{ ResourceGroup }}.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/16.PNG?st=2019-09-19T12%3A26%3A56Z&se=2022-09-20T12%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=y4DSEkbZlzrT81BxKozvJT9vlWNWqLsmfhYOqxb60ug%3D)

3. On the {{ ResourceGroup }} blade, click the entry representing the Azure web app you created in the previous task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/17.PNG?st=2019-09-19T12%3A27%3A10Z&se=2022-09-20T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C7sLFXuTfovXdAvkzmW%2Ff54m1723Sf6P2hiFt%2BmxztE%3D)

4. On the web app blade, click the **Browse** button at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/18.PNG?st=2019-09-19T12%3A27%3A22Z&se=2022-09-20T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6S0vNaFqMxHI3A2sAXJfSmKV%2Bvyy0f3bXqaqIHWTJBE%3D)

5. Review the sample Node.js web application deployed from GitHub.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/19.PNG?st=2019-09-19T12%3A27%3A34Z&se=2022-09-20T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C799lWH3ZW7KJ5Ylgx4NkQs3Ttwo%2BtgIXbBA0rwQBWU%3D)

6. Close the new browser tab and return to the browser tab displaying the Azure portal.

### Task 3: Deploy Code with a Docker Hub container image

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group you will use in this task:

```
 RESOURCE_GROUP_CONTAINER='{{ ResourceGroup }}'
```

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the Azure region you will use for the deployment:

```
 LOCATION=$(az group list --query "[?name == '{{ ResourceGroup }}'].location" --output tsv)
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new variable which value is a randomly generated string that you will use as the name of a new web app:

```
 WEBAPPNAME3=webapp05023$RANDOM$RANDOM
```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new web app using a unique name:

```
 az webapp create --name $WEBAPPNAME3 --plan AADesignLab0502-$LOCATION --resource-group $RESOURCE_GROUP_CONTAINER --deployment-container-image ghost
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/20.PNG?st=2019-09-19T12%3A27%3A49Z&se=2022-09-20T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ac%2FOhtO%2BZT2cOwbo9nuZw9D%2BviiKp6pqACEPGblKosA%3D)

> **Note**: In case the command fails due to duplicate web app name, re-run the last two steps until the command completes successfully

5. Wait for the deployment to complete before you proceed to the next task.

> **Note**: The deployment should take less than a minute.

6. Close the **Cloud Shell** pane.

### Task 4: View deployment results

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{ ResourceGroup }}.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/21.PNG?st=2019-09-19T12%3A28%3A08Z&se=2022-09-20T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4tKtq36Taahe2KHxkQbLyXnCoUqbqHC0c70T%2BlEqdPk%3D)

3. On the {{ ResourceGroup }} blade, click the entry representing the Azure web app you created in the previous task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/22.PNG?st=2019-09-19T12%3A28%3A20Z&se=2022-09-20T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z2N0PgmEvJia02uOvpZ7NqlkdFy%2F49UNVk7CIbgYdUk%3D)

4. On the web app blade, click the **Browse** button at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/23.PNG?st=2019-09-19T12%3A28%3A32Z&se=2022-09-20T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QhB6rXVrl3ZchuP7GgtD%2BtvoEGHK76t7HhqUhXJS9rQ%3D)

> **Note**: If the application does not appear, switch to the web app blade, click **Restart** button at the top of the blade and then click **Browse** again. 

5. Review the blog application deployed from Docker Hub. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab7/24.PNG?st=2019-09-19T12%3A28%3A45Z&se=2022-09-20T12%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dl6%2Bu3TxTcI9xfL6bX%2FCXUi4tF%2BphJLwvE2RDaqVdRk%3D)

6. Close the new browser tab and return to the browser tab displaying the Azure portal.

> **Result**: In this exercise, you deployed code using an Azure Resource Manager template and a Docker Hub image to App Service web apps.
