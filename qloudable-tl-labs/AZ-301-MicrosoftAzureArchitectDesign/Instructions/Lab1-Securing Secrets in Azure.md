# Lab-1: Managing Security and Identity for Azure Solutions 

## Table of Contents 

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Deploy Key Vault resources](#exercise-1-deploy-key-vault-resources)

[Exercise 2: Deploy Azure VM using Key Vault secret](#exercise-2-deploy-azure-vm-using-key-vault-secret)

## Overview

The aim of this Lab is to add secrets in Azure Key Vault by deploying Key Vault resource in Azure portal and deploy the Azure VM using Key Vault secret.

### Scenario & Objective

To manage security and identity for Azure solutions
 
After completing this lab, you will be able to:
  
* Deploy Key Vault resources

* Deploy Azure VM using Key Vault secret

## Pre-requisites

* Familiarity with Azure Portal

* Familiarity Azure CLoud Shell

* Familiarity with ARM Templates deployment

* Chrome browser

> **Note:** Azure Portal and Chrome browser are provided with the Lab virtual machine.

> **Note:** Azure CLoud Shell is a part of Azure Portal.

> **Note:** ARM Template is provided as a part of this lab.

## Exercise 1: Deploy Key Vault resources

### Task 1: Open the Azure Portal

Using the Chrome browser, login to Azure Portal with the below details:

**Azure login_ID:** {{azure-login-id}} <br>

**Azure login_Password:** {{azure-login-password}}<br>

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/1.png?st=2019-09-18T06%3A41%3A03Z&se=2022-09-19T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EOgRmsvFhVmwkDY2aP3retuCcySv9Al8%2F3kX1sTzmvM%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/2.png?st=2019-09-18T06%3A41%3A22Z&se=2022-09-19T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jQ4sb5utUq95ckItjfcuJ7PpULPsibcv%2FQBilRWS8iE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/3.png?st=2019-09-18T06%3A42%3A03Z&se=2022-09-19T06%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Geu1F4yvlme4FZsGavMRyEc%2BF1Ve5mBVb4wwnvAn%2B4w%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/4.png?st=2019-09-18T06%3A42%3A21Z&se=2022-09-19T06%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lxEqmcP9Uc0WC68%2FZUwP3GM0ufMQRs5ijgplBjJ9dbQ%3D)

### Task 2: Deploy a key vault

1. In the upper left corner of the Azure portal, click **Create a resource**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/5.1.png?st=2019-09-18T06%3A43%3A05Z&se=2022-09-19T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HHHNvweYGyLO%2Fv5X27sa%2FNMo1FN80RUfTiAlD8Ji3YA%3D)

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Key Vault** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/5.2.png?st=2019-09-18T06%3A43%3A26Z&se=2022-09-19T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dbG0%2FL6mf7bgY7WTz9izJ13t4ukl60aGpu4nQCtF3cM%3D)

3. On the **Everything** blade, in the search results, click **Key Vault**.

4. On the **Key Vault** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/5.PNG?st=2019-09-18T06%3A43%3A47Z&se=2022-09-19T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hzSTCt2oy3%2B8%2FESBP4Gt%2BTu4Z8gA9oKnIz9fPer4Wjk%3D)

5. On the **Create key vault** blade, perform the following tasks:

 `Subscription`: select the default value.

 `Resource group`: {{resource-group-name}} <br>

 `Key vault name`: type a globally unique value.

 `Location`: {{location}} <br>

 `Pricing tier`: Standard
 
6. Then click Select and leave all remaining settings with their default values. Click the Create button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/6.PNG?st=2019-09-18T06%3A44%3A07Z&se=2022-09-19T06%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=usJMuRI%2BkPRk5XPNEOM7AYNhUkM0tKVgzqvelvMhjII%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/7.PNG?st=2019-09-18T06%3A44%3A22Z&se=2022-09-19T06%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=p1nbVeal3J3lis8KLRcLtfISRZrsxxq4GbqDCl7hjLA%3D)

7. Wait for the provisioning to complete before you proceed to the next task.

### Task 3: Add a secret to a key vault by using the Azure portal

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click on {{resource-group-name}} <br>.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/8.PNG?st=2019-09-18T06%3A44%3A38Z&se=2022-09-19T06%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6fC5bgSxBqmnduAYglJDG1BiQ0urwEQgi3RzCkF28fk%3D)

3. On the {{resource-group-name}} <br> blade, click the entry representing the newly created key vault.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/9.PNG?st=2019-09-18T06%3A45%3A01Z&se=2022-09-19T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YaJ1XAYH2f1Tg%2B7a7krizyhXxHdcBDTzkIQ%2FpnMYUK8%3D)

4. On the key vault blade, click **Secrets**.

5. On the key vault secrets blade, click the **Generate/Import** button at the top of the pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/10.PNG?st=2019-09-18T06%3A45%3A20Z&se=2022-09-19T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Q2uO4aPAa97nY3r84BgjGqOZ5z1ne%2FP%2Bkda4qtro%2B5U%3D)

6. On the **Create a secret** blade, perform the following tasks:

```
 Upload options: Manual

 Name: thirdPartyKey

 Value: 56d95961e597ed0f04b76e58

```
7. Leave all remaining settings with their default values and click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/11.PNG?st=2019-09-18T06%3A45%3A42Z&se=2022-09-19T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Y8IayYOwoWDDHCdIxcgORZPXNej2E62qXE7dQTjmLqI%3D)

### Task 4: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/12.PNG?st=2019-09-18T06%3A45%3A58Z&se=2022-09-19T06%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3yfaFRdhsWiQaZEvn1Nefdu4O4WQtn4hh94GoPzo2L4%3D)

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/13.PNG?st=2019-09-18T06%3A46%3A13Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cVRxzy1bUmzuNfi6teAMUtOamRnxHysWYJRQihauX5g%3D)

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/14.PNG?st=2019-09-18T06%3A46%3A29Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QSZxJLQZLtQZN7R2fSNyQUruIBNpGhQBwh0Q%2BlPLUTU%3D)


 `Subscription`: select the default value.

 `Cloud Shell region`: {{location}} <br>

 `Resource group`: {{resource-group-name}} <br>

 `Storage account`: a name of a new storage account

 `File share`: a name of a new file share


4. Click the **Create storage** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/15.PNG?st=2019-09-18T06%3A46%3A46Z&se=2022-09-19T06%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OcXDEJVzXf11bcrm0BYy6zd4rodd%2B3F6oDlwfdLySBA%3D)

5. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

### Task 5: Add a secret to a key vault using the CLI

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that contains the Azure key vault you deployed earlier in this exercise:


**RESOURCE_GROUP='{{resource-group-name}} <br>'**
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/16.PNG?st=2019-09-18T06%3A47%3A10Z&se=2022-09-19T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Q%2BZKEWxZmgeAI8Ur8U1Y5syUyQrhFvyvxTGypRSvNHE%3D)

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to retrieve the name of the Azure key vault you created earlier in this exercise:

    ```
    KEY_VAULT_NAME=$(az keyvault list --resource-group $RESOURCE_GROUP --query "[0].name" --output tsv)
    ```

3. At the **Cloud Shell** command prompt, type in the following command, and press **Enter** to list secrets in the key vault:

    ```
    az keyvault secret list --vault-name $KEY_VAULT_NAME --output json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/17.PNG?st=2019-09-18T06%3A47%3A28Z&se=2022-09-19T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tSrWICXCv64sypP%2BHOfzFuUeLZUKmlWuqwccV%2BRnjIA%3D)

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to display the value of the **thirdPartyKey** secret:

    ```
    az keyvault secret show --vault-name $KEY_VAULT_NAME --name thirdPartyKey --query value --output tsv
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/18.PNG?st=2019-09-18T06%3A47%3A42Z&se=2022-09-19T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Yr92xmMrSg6QNyTuKGTroZ9Q1SI%2FYJTTf5sE6LVbB60%3D)

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to add a new secret to your key vault:

    ```
    az keyvault secret set --vault-name $KEY_VAULT_NAME --name firstPartyKey --value 56f8a55119845511c81de488
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/19.PNG?st=2019-09-18T06%3A47%3A57Z&se=2022-09-19T06%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FWRN64l9x0uOvklQc0n%2BiMGp4pYXUrHZgsD7wp95ooE%3D)

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list secrets in the key vault:

    ```
    az keyvault secret list --vault-name $KEY_VAULT_NAME --query "[*].{Id:id,Created:attributes.created}" --out table
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/20.PNG?st=2019-09-18T06%3A48%3A13Z&se=2022-09-19T06%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yb7j8XbnylWspjRlnJawk1iaNmY8XaIDjMpbnXuKy08%3D)

7. Close the **Cloud Shell** pane.

### Task 6: Add secrets to a key vault by using Azure Resource Manager templates

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Template Deployment**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/21.PNG?st=2019-09-18T06%3A49%3A38Z&se=2022-09-19T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZwkXBJD3x3ZFidOrK0t6kZN3c4bY0WbcHjomRo6uVJ0%3D)

4. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/22.PNG?st=2019-09-18T06%3A49%3A53Z&se=2022-09-19T06%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KxcTS0WcTGyVMv7%2FglnrzT2XwLkJ%2Bwoy8Gf0KQQFxxM%3D)

5. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/23.PNG?st=2019-09-18T06%3A50%3A10Z&se=2022-09-19T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pw1FLVWan2NM4B2u1WmHk%2FWQi%2BYSQv%2FC7goA8LtiL4k%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/24.PNG?st=2019-09-18T06%3A50%3A25Z&se=2022-09-19T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GLPjquHOPDfZgyKdJZs%2BZZAK4jUMaqF4dTwFxIiNcMw%3D)

6. Copy the below link and paste it in New Chrome browser. 

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_01/LabFiles/Starter/secret-template.json?st=2019-09-17T11%3A54%3A42Z&se=2022-09-18T11%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0oi5pkM9yWSoT5eiOSW6xu75owo2jX9AKzIr%2BCxh2mE%3D**

7. Selct the content and paste it in **Edit template** blade.

    ```
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "vaultName": {
                "type": "string"
            }
        },
        "variables": {
            "secretName": "vmPassword"
        },
        "resources": [
            {
                "apiVersion": "2016-10-01",
                "type": "Microsoft.KeyVault/vaults/secrets",
                "name": "[concat(parameters('vaultName'), '/', variables('secretName'))]",
                "properties": {
                    "contentType": "text/plain",
                    "value": "StudentPa$$w.rd"
                }
            }
        ]
    }
    ```

8. Click the **Save** button to persist the template.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/25.PNG?st=2019-09-18T06%3A50%3A45Z&se=2022-09-19T06%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fo%2Fw3OuvlMyImUon34S2KtbWYl3wB48mTCkhiDdAshM%3D)

9. Back on the **Custom deployment** blade, perform the following tasks:


 `Subscription`: select the default value.

 `Resource group`: : {{resource-group-name}} <br>

 `Vault Name`: type the name of the key vault you created earlier in this exercise.


10. In the Terms and Conditions section, select the I agree to the terms and conditions stated above checkbox and click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/26.PNG?st=2019-09-18T06%3A51%3A00Z&se=2022-09-19T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wWCjUscIuUi89okuquL8I6H1r6XCJg0Em0j3mnpT7aA%3D)

11. Do not wait for the deployment to complete but proceed to the next step.

12. In the upper left corner of the Azure portal, click **Create a resource**.

13. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

14. On the **Everything** blade, in the search results, click **Template Deployment**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/27.PNG?st=2019-09-18T06%3A51%3A17Z&se=2022-09-19T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UurG7iFIOYNe9WTNtoHmj3QDqJ7WxuaT4EltWxqhKpQ%3D)

15. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/28.PNG?st=2019-09-18T06%3A51%3A35Z&se=2022-09-19T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fOoIolyrcCvVsS9swjJuTkSLgLYkCAChx0ZrUPA2104%3D)

16. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/29.PNG?st=2019-09-18T06%3A51%3A50Z&se=2022-09-19T06%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=UrweHGKOwWDH4LdK6o21%2BUTisi9Hu5As3uVh%2BeZ5owE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/30.PNG?st=2019-09-18T06%3A52%3A06Z&se=2022-09-19T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kw6PC8C6lNqrd9tnpzxW3j9pw28dOV7ZbTZpedb0vL4%3D)

17. Copy the below link and paste it in New Chrome browser.

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_01/LabFiles/Starter/storage-template.json?st=2019-09-17T11%3A59%3A18Z&se=2022-09-18T11%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3m%2Fcs30Mduib%2FEncIiGmGRf%2BC0YMk%2BWh%2BzpvGt5GM2U%3D**

18. Selct the content and paste it in **Edit template** blade.

    ```
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "vaultName": {
                "type": "string"
            }
        },
        "variables": {
            "secretName": "storageConnectionString",
            "storageName": "[concat('stor', uniqueString(resourceGroup().id))]"
        },
        "resources": [
            {
                "apiVersion": "2017-10-01",
                "type": "Microsoft.Storage/storageAccounts",
                "name": "[variables('storageName')]",
                "location": "[resourceGroup().location]",
                "kind": "Storage",
                "sku": {
                    "name": "Standard_LRS"
                },
                "properties": {                
                }
            },
            {
                "apiVersion": "2016-10-01",
                "type": "Microsoft.KeyVault/vaults/secrets",
                "name": "[concat(parameters('vaultName'), '/', variables('secretName'))]",
                "dependsOn": [
                    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageName'))]"
                ],
                "properties": {
                    "contentType": "text/plain",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageName'), ';', 'AccountKey=', listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('storageName')), providers('Microsoft.Storage', 'storageAccounts').apiVersions[0]).keys[0].value, ';')]"
                }
            }
        ]
    }
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/31.PNG?st=2019-09-18T06%3A52%3A25Z&se=2022-09-19T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hhZ7RH1VGKm9tHpqcpDAPV%2BLuwtKv0kTMQd9Jr6xiXI%3D)

19. Click the **Save** button to persist the template.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/32.PNG?st=2019-09-18T06%3A52%3A39Z&se=2022-09-19T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JpLHk84J9tzLDdEagcmtgQPjpNSZAs6RRr7CeC4B67I%3D)

20. Back on the **Custom deployment** blade, perform the following tasks:


 `Subscription`: select its default value.

 `Resource group`: {{resource-group-name}} <br>

 `Vault Name`: type the name of the key vault you created earlier in this exercise.

21. In the Terms and Conditions section, select the I agree to the terms and conditions stated above checkbox. Click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/33.PNG?st=2019-09-18T06%3A52%3A56Z&se=2022-09-19T06%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s7G6CTMGaSphEL66hGn6waLusCZ26TC2Iq2K5OSCNXA%3D)

22. Wait for the deployment to complete before you proceed to the next task.

### Task 7: View key vault secrets

1. In the hub menu of the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{resource-group-name}} <br>.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/34.PNG?st=2019-09-18T06%3A53%3A13Z&se=2022-09-19T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EpGh0D9TS8POCHhULmOp3x0cY%2FDl6wym0kfcO2HjNO0%3D)

3. On the {{resource-group-name}} <br> blade, click the entry representing the key vault you created earlier in this exercise.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/35.PNG?st=2019-09-18T06%3A53%3A27Z&se=2022-09-19T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dfd9d%2FXUNe%2B0oCHP6O76z7OS4KbBzxSSIo2YEv%2FsQYY%3D)

4. On the key vault blade, click **Secrets**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/36.PNG?st=2019-09-18T06%3A53%3A42Z&se=2022-09-19T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WPkIHhKAWjZMZgC%2BuSGmeiTCIUiq0zQPy0Fd128Pvwc%3D)

5. On the key vault secrets blade, review the list of secrets created during this lab.

6. Click the entry representing the **vmPassword** secret.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/37.PNG?st=2019-09-18T06%3A53%3A56Z&se=2022-09-19T06%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1hGhZjfV9AJEPRjBpQljj47P2rFuUSdFeQZJPMx1Bhg%3D)

7. On the **vmPassword** blade, click the entry representing the current version of the secret.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/38.PNG?st=2019-09-18T06%3A54%3A09Z&se=2022-09-19T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QeQtN9s5VsH%2BTbr%2FuNYfgyA1Mb9Fuyxbv0ty2UK6NqY%3D)

8. On the Secret Version blade, click the **Show secret value** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/39.PNG?st=2019-09-18T06%3A54%3A30Z&se=2022-09-19T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ely7fCsczI4Aqr7e%2BzMt3LFyP4yfb%2BlIE1OvAePEVE8%3D)

9. Verify that the value of the secret matches the one included in the template you deployed in the previous task.

> **Result**: In this exercise, you created a **Key Vault** instance and used several different methods to add secrets to the key vault.

## Exercise 2: Deploy Azure VM using Key Vault secret

### Task 1: Retrieve the value of the key vault Resource Id parameter

1. At the top of the portal, click the **Cloud Shell** icon to open a new Clould Shell instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/40.PNG?st=2019-09-18T06%3A54%3A47Z&se=2022-09-19T06%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2PlVS4vYOzquD8l0RM%2F%2B%2FKwY93tFkbvzN5fKeHyU6dk%3D)

2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that will contain the hub virtual network:

    
    RESOURCE_GROUP='{{resource-group-name}} <br>'
    

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to retrieve the resource id of the Azure key vault you created earlier in this exercise:

    ```
    KEY_VAULT_ID=$(az keyvault list --resource-group $RESOURCE_GROUP --query "[0].id" --output tsv)
    ```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the Azure key vault resource id and which takes into account any special character the resource id might include:

    ```
    KEY_VAULT_ID_REGEX="$(echo $KEY_VAULT_ID | sed -e 's/\\/\\\\/g; s/\//\\\//g; s/&/\\\&/g')"
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/41.PNG?st=2019-09-18T06%3A55%3A04Z&se=2022-09-19T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=R%2BO2ukA9%2BdY9ynVWRy6F5HKciK%2BDxaNYxQitcXI6HQc%3D)

### Task 2: Prepare the Azure Resource Manager deployment template and parameters files

1. In the **Cloud Shell** pane, type below command to create **vm-template.json**. 

```
vi vm-template.json

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/42.PNG?st=2019-09-18T06%3A55%3A18Z&se=2022-09-19T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fGwouXun9X2vxKyOcmK5UhRNUVWpwwKNhKhlZPQTjMI%3D)

2. Then press i to get into Insert mode.

3. Copy the below link and paste it in new Chrome browser.

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_01/LabFiles/Starter/vm-template.json?st=2019-09-17T12%3A27%3A42Z&se=2022-09-18T12%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bJ8ta5BenXMKlhAmb97nICs8hyFmXWTmJhRQrKAHDI4%3D**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/43.PNG?st=2019-09-18T06%3A55%3A34Z&se=2022-09-19T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4RHGi3wzuj3NmV7E7yaqQWLweAZq49UloSUxNpMFPy4%3D)

4. Copy the content and then insert in vi editor as shown like below. Then press **Esc:wq!** to save and exit.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/44.PNG?st=2019-09-18T06%3A55%3A50Z&se=2022-09-19T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C2B5u%2B3VHYqBUMP%2BHu3KG7mLlw7HJ2%2Bzyok6va4O2O0%3D)

Similarly, type below command to create **vm-template.parameters.json**. 

```
vi vm-template.parameters.json

```
5. Then press i to get into Insert mode.

6. Copy the below link and paste it in new Chrome browser.

**https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_01/LabFiles/Starter/vm-template.parameters.json?st=2019-09-17T12%3A30%3A56Z&se=2022-09-18T12%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9fCwTYUpLzUnAdIn2LrB8dsGlUHkEZatX1%2BptEVhBa0%3D**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/45.PNG?st=2019-09-18T06%3A56%3A05Z&se=2022-09-19T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vCemARa%2BpznY%2Fn0gXIt9iHsXWortcorAkDgI1KHQlro%3D)

7. Copy the content and then insert in vi editor as shown like below. Then press **Esc:wq!** to save and exit.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/46.PNG?st=2019-09-18T06%3A56%3A22Z&se=2022-09-19T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ggSuXe%2FWN4Amfzz9yMbir3c45MdmLBBzeE28PfdEvEw%3D)

Type `ls` to list the created files.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/47.PNG?st=2019-09-18T06%3A56%3A37Z&se=2022-09-19T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ghFT4N0Ux9xdiqATN%2B3HxHTjTZ4WnrTTNnmyYXaVXs4%3D)

8. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to replace the placeholder for the **$KEY_VAULT_ID** parameter in the **vm-template.parameters.json** parameters file with the value of the **$KEY_VAULT_ID** variable:

    ```
    sed -i.bak1 's/"$KEY_VAULT_ID"/"'"$KEY_VAULT_ID_REGEX"'"/' ~/vm-template.parameters.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/48.PNG?st=2019-09-18T06%3A56%3A54Z&se=2022-09-19T06%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WVUPcCst%2F7PqzCPRV1%2F39Od5s%2B0E2Fd%2FlEeDUqYpEEw%3D)

9. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to verify that the placeholder was successfully replaced in the parameters file:

    ```
    cat ~/vm-template.parameters.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/49.PNG?st=2019-09-18T06%3A57%3A08Z&se=2022-09-19T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0aX1nOyP2LfFgbfAcSW30pINeFphixRHSu13e9WZr9Q%3D)

### Task 3: Configure a key vault for deployment of Azure Resource Manager templates

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{resource-group-name}} <br>.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/50.PNG?st=2019-09-18T06%3A57%3A23Z&se=2022-09-19T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g97L8SD%2FPuR6eJ21%2FLEcYswuEj5g%2BZNNx4K%2BieHL290%3D)

3. On the {{resource-group-name}} <br> blade, click the entry representing the key vault you created in the previous exercise.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/51.PNG?st=2019-09-18T06%3A57%3A42Z&se=2022-09-19T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YWbj%2FDXGj%2Fq2vyfs1X5y%2B1PhL3%2BE6Iy2iINw5MwyFQc%3D)

4. On the key vault blade, click **Access policies**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/52.PNG?st=2019-09-18T06%3A57%3A59Z&se=2022-09-19T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=k7mBKeuzRr68OPwQtfrt9Colqf4IHaa2QYBTad4Y8oc%3D)

5. On the **Access policies** blade, under the **Enable access to:** area.

6. Select the  **Enable access to Azure Resource Manager for template deployment**  checkbox.

7. Click the **Save** button at the top of the pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/53.PNG?st=2019-09-18T06%3A58%3A13Z&se=2022-09-19T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Xan%2BcJPWCqy885Ci3IAPpGUOncqtPlLZNxMa%2Brat3yQ%3D)

### Task 4: Deploy a Linux VM with the password parameter set by using a key vault secret.

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to deploy the Azure Resource Manager template with the specified parameters file:

    ```
    az group deployment create --resource-group $RESOURCE_GROUP --template-file ~/vm-template.json --parameters @~/vm-template.parameters.json
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/54.png?st=2019-09-18T06%3A58%3A28Z&se=2022-09-19T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qMLxYiGQ%2BObaWnm%2FP7QW54DkSEvJIlWoLh8eSA2fkjk%3D)

2. Wait for the deployment to complete before you proceed to the next task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/55.png?st=2019-09-18T06%3A58%3A41Z&se=2022-09-19T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0Ood%2BqIpL6KO3s0%2BC8GThjJ8tUQ2wUqh%2BZ5vbq4FYKk%3D)

### Task 5: Verify the outcome of the deployment

1. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that contains the newly deployed Azure VM:


    RESOURCE_GROUP='{{resource-group-name}} <br>'


2. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to retrieve the name of the Azure key vault containing the secret that stores the value of the password of the local Administrator account:

    ```
    KEY_VAULT_NAME=$(az keyvault list --resource-group $RESOURCE_GROUP --query "[0].name" --output tsv)
    ```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to retrieve the value of the secret:

    ```
    az keyvault secret show --vault-name $KEY_VAULT_NAME --name vmPassword --query value --output tsv
    ```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to retrieve the public IP address of the Azure VM you deployed in the previous task:

    ```
    PUBLIC_IP=$(az network public-ip list --resource-group $RESOURCE_GROUP --query "[0].ipAddress" --output tsv)
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/56.png?st=2019-09-18T06%3A58%3A59Z&se=2022-09-19T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TTD%2BDz5IIEEp0LHAYzXoKTaIDJCt4FiUxfDdI4OiLpM%3D)

5. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to connect to the Azure VM via SSH:

    ```
    ssh Student@$PUBLIC_IP
    ```

6. At the **Cloud Shell** command prompt, when prompted whether you want to continue connecting, type `yes` and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/57.png?st=2019-09-18T06%3A59%3A13Z&se=2022-09-19T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XAl8Av5jdSdoVgQ9V7DG%2F5Yp7cRRzQw4WGxQ6Z4ZT8E%3D)

7. At the **Cloud Shell** command prompt, when prompted for password, type the value of the secret you retrieved earlier in this task and press **Enter**.

8. Verify that you successfully authenticated.

9. At the **Cloud Shell** command prompt, type `exit` to log out from the Azure VM.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab1/58.png?st=2019-09-18T06%3A59%3A27Z&se=2022-09-19T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W7rZWFboYM9lFzO2NuypNpAbkkFUx1JTIIzLRQexX0M%3D)

> **Result**: In this exercise, you deployed a Linux VM using a password stored as a key vault secret.
