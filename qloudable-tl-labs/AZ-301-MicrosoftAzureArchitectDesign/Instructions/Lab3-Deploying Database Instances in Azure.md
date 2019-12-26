
# Deploying Database Instances in Azure

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Deploy a Cosmos DB database](#exercise-1-deploy-a-cosmos-db-database)

[Exercise 2: Deploy Application using Cosmos DB](#exercise-2-deploy-application-using-cosmos-db)

[Exercise 3: Connect Cosmos DB to Azure Search](#exercise-3-connect-cosmos-db-to-azure-search)

## Overview

The aim of this lab is to deploy a cosmos DB instance, insert data into collections and deploy an application.

### Scenario and Objectives

To Compare Database Options in Azure

* Deploy a Cosmos DB Instance and insert data.

* Deploy an Application using the Cosmos DB.

* Connect Cosmos DB to Azure Search.

## Pre-Requisites

* Azure Portal

* Powershell

## Exercise 1: Deploy a Cosmos DB database

### Task 1: Open the Azure Portal

From the lab, after the chrome is opened and connected then browse to the Azure portal at http://portal.azure.com

Using the Chrome browser, login into Azure portal with the below details.

```

Azure Email: {{ Azure Portal Email }}

Azure Password: {{ Azure Portal Password }}

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/71.png?st=2019-09-19T08%3A50%3A37Z&se=2022-09-20T08%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DR52RdEteYbRbPbrApQIOJIkzEPIqr7SwFw4kbQKaTw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/72.png?st=2019-09-19T08%3A52%3A00Z&se=2022-09-20T08%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Jlm049jj6aSAHbtMGkcra54gHQ%2B2llUF4Bu%2FVRJKm6E%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/73.png?st=2019-09-19T08%3A52%3A25Z&se=2022-09-20T08%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BhzVyZKZWvCmoSMWyBP85eMQh%2F02MqEXi7K%2BoDc0PSg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/74.png?st=2019-09-19T08%3A52%3A48Z&se=2022-09-20T08%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JntxSYbUn4eJ7Px5AFI0lOvSRiwrDG0IQ1WNqtwdw5g%3D)


### Task 2: Create a Cosmos DB database and collection

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Cosmos DB** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/1.png?st=2019-09-18T09%3A47%3A30Z&se=2022-09-19T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xH0WP5gbPMNxZb9vuQ62CrbD3cQKryDLQNmAtSDtOAc%3D)

4. On the **Azure Cosmos DB** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/3.png?st=2019-09-18T09%3A48%3A41Z&se=2022-09-19T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pz%2FPq5YMnZ6BHi4iBgwDDwDyGyLzhH80mNNI5Ai4%2B9A%3D)

5. On the new **Azure Cosmos DB** blade, perform the following tasks:

```

     Subscription: Select the default

     Resource group: {{ ResourceGroup }}

     Account Name: Type a globally unique value.

     API: Core (SQL)

     Location: {{ Location }}

     Leave all remaining settings with their default values.  
    
 ```
 
6. Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/4.png?st=2019-09-18T09%3A49%3A22Z&se=2022-09-19T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gdZSCAVyRAmIo3bLzfR6hGBixhAf80JbVs7NIKPHTH4%3D)

7. Wait for the provisioning to complete before you proceed to the next step.

   **Note**: The deployment should take less than 5 minutes.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/5.png?st=2019-09-18T09%3A49%3A46Z&se=2022-09-19T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=B55No6xgXxWeDR7RklhaJ6VnmEk5subV7m1CeMe4ztM%3D)

8. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

    **Note**: The **Cloud Shell** icon is a symbol that is constructed of the combination of the *greater than* and *underscore* characters.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/6.png?st=2019-09-18T09%3A50%3A16Z&se=2022-09-19T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kWDsJD0sqnsmyK7BJV84zXrb9fMsbrDXrMknCl5wdaQ%3D)

8. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/59.PNG?st=2019-09-19T09%3A03%3A58Z&se=2022-09-20T09%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gLCU2is6U0%2BltLaNOxijnqObgmPHjUGJET0ow9iyHlQ%3D)

  **Note**: If you do not see the configuration options for **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. If so, proceed directly to the next task. 

9. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

```

    Subscription: Select the default

    Cloud Shell Region: {{ Location }}

    Resource group: {{ ResourceGroup }}

    Storage account: type a unique name consisting of a combination of between 3 and 24 characters and digits. 

    File share: type cloudshell
    
 ```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/60.PNG?st=2019-09-19T09%3A04%3A52Z&se=2022-09-20T09%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RmRV1T2SzGkeU2j%2FnDfHnjKRxWMRJHyPWBk4OboazHM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/61.PNG?st=2019-09-19T09%3A07%3A34Z&se=2022-09-20T09%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BPrp5NwfpzLDngHEh5T%2BBdwYCz9XQPoZRvisF4rz2yU%3D)

10. Click the **Create storage** button.

11. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

12. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the resource group that contains the Azure Cosmos DB account you deployed earlier in this task:

    ```
    RESOURCE_GROUP='{{ ResourceGroup }}'
    ```

12. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the name of the CosmosDB account you created earlier in this task:

    ```
    
    COSMOSDB_NAME=$(az cosmosdb list --resource-group $RESOURCE_GROUP --query "[0].name" --output tsv)
    
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/7.png?st=2019-09-18T09%3A50%3A43Z&se=2022-09-19T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=db%2FbUaQP%2BfKz7d0vmTfNuBTxPsWrWbdggHhJE35eqDE%3D)

13. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the primary key of the CosmosDB account you created earlier in this task:

    ```
    
    PRIMARY_KEY=$(az cosmosdb keys list --resource-group $RESOURCE_GROUP --name $COSMOSDB_NAME --output json | jq -r '.primaryMasterKey')
    
    ```

14. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a variable which value designates the URI of the CosmosDB account you created earlier in this task:

    ```
    
    URI="https://$COSMOSDB_NAME.documents.azure.com:443/"
    
    ```

15. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new CosmosDB database named **FinancialClubDatabase**:

    ```
    
    az cosmosdb database create --url-connection $URI --key $PRIMARY_KEY --db-name 'FinancialClubDatabase'
    
    ```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/8.png?st=2019-09-18T09%3A51%3A12Z&se=2022-09-19T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=c08L5GjtyVTFACAiuAop6vpnJWILxTGm9p5eD4byJHA%3D)

16. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a fixed collection named **MemberCollection** in the newly created database:

    ```
    
    az cosmosdb collection create --url-connection $URI --key $PRIMARY_KEY --db-name 'FinancialClubDatabase' --collection-name 'MemberCollection' --throughput 400
    
    ```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/9.png?st=2019-09-18T09%3A51%3A33Z&se=2022-09-19T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d8Sv%2BN0x2YhMJVP6EEOREYNVAe7Dmi1XH2Mm%2B%2FX3ZAs%3D)

17. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to display the value of the PRIMARY_KEY variable:

    ```
    
    echo $PRIMARY_KEY
    
    ```
    
18. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to display the value of the URI variable:

    ```
    
    echo $URI
    
    ```
  **Note: Take a note of these Primary Key and URI values - you will need them in the next exercise.**
   

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/10.png?st=2019-09-18T09%3A51%3A55Z&se=2022-09-19T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FP1MMPW46woZh8yeEP05TSL3MKvbAjTzvDNQA8PC30s%3D)

### Task 3: Create and query documents in Cosmos DB

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the Resource groups blade, click **{{ ResourceGroup }}**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/62.PNG?st=2019-09-19T09%3A27%3A47Z&se=2022-09-20T09%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uNd9Hd9M%2FePrwLaXCGwTnFKqt%2B1U44VKOQIuyzCJeQY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/63.PNG?st=2019-09-19T09%3A28%3A58Z&se=2022-09-20T09%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bhTWYcudUfgw34NFzaoveXqNgR0SSyVxk2XwOmWqhv8%3D)

3. On the left side of the Azure Cosmos DB account blade, click **Data Explorer**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/11.png?st=2019-09-18T09%3A52%3A16Z&se=2022-09-19T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2mPwLIIAj6AfkztoFBFJROgHHO%2F3kfG9sKYwT52g8oQ%3D)

4. In the **Data Explorer** pane, click the **MemberCollection** child node of the **FinancialClubDatabase** node.

5. Click the **New SQL Query** button at the top of the **Data Explorer** pane.

6. In the **Query 1** tab that opened, view the default query:

    ```
    SELECT * FROM c
    ```

5. Click the **Execute Query** button at the top of the query editor.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/12.png?st=2019-09-18T09%3A52%3A37Z&se=2022-09-19T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6zlIbrOn1T8jB5FsihkW6z8z59wtwWfGU%2BwS%2FhctB2Y%3D)

6. In the left pane of the Data Explorer, expand the **MemberCollection** node.

7. Click the **Items** child node within the **MemberCollection** node.

8. In the new **Items** tab that opened, click the **New Item** button at the top of the tab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/13.png?st=2019-09-18T09%3A52%3A58Z&se=2022-09-19T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZZQVfpwawpJkxECGxsuvPPwWQuuJQVy11Z6OXReBRXw%3D)

9. In the **Items** tab, replace the existing document with the following document:

    ```
    {
        "firstName": "Pennington",
        "lastName": "Oneal",
        "age": 26,
        "salary": 90000.00,
        "company": "Veraq",
        "isVested": false
    }
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/14.png?st=2019-09-18T09%3A53%3A19Z&se=2022-09-19T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OeLVGZLbnERikEMJKVfBkl6xC6uY4QuwfE8jwzMgkwc%3D)

10. Click the **Save** button at the top of the **Items** tab.

11. In the **Items** tab, click the **New Item** button at the top of the tab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/15.png?st=2019-09-18T09%3A53%3A38Z&se=2022-09-19T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qQwZyXDYRZeiIkTdTRGkhbd2Y9QkvUCYuj5i0ACFsNM%3D)

12. In the **Items** tab, replace the existing document with the following document:

    ```
    {
        "firstName": "Suzanne",
        "lastName": "Oneal",
        "company": "Veraq"
    }
    ```

13. Click the **Save** button at the top of the **Items** tab.

14. Switch back to the **Query 1** tab, re-run the default query `SELECT * FROM c` by clicking the **Execute Query** button at the top of the query editor, and review the results.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/16.png?st=2019-09-18T09%3A53%3A59Z&se=2022-09-19T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eHp0J5biFiFxYg6LSITWIVAYSpIlccVTtrn8NOhkLWM%3D)

15. In the query editor, replace the default query with the following query:

    ```
    SELECT 
        c.id, 
        c.firstName, 
        c.lastName,
        c.isVested,
        c.company
    FROM 
        c
    WHERE
        IS_DEFINED(c.isVested)
    ```

16. Click the **Execute Query** button at the top of the query editor and review the results.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/17.png?st=2019-09-18T09%3A54%3A20Z&se=2022-09-19T09%3A54%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FLdu0JQl7Nxr4vWgt64Z%2F9zQVspjz07KUDzBmsK%2BAxI%3D)

17. In the query editor, replace the existing query with the following query:

    ```
    SELECT 
        c.id, 
        c.firstName, 
        c.lastName,
        c.age
    FROM 
        c
    WHERE
        c.age > 20
    ```

18. Click the **Execute Query** button at the top of the query editor and review the results.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/18.png?st=2019-09-18T09%3A57%3A02Z&se=2022-09-19T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WMhnRfTC5gwcmISHAVQRnKHxDR7hjm8HD62LSz8geJs%3D)

19. In the query editor, replace the existing query with the following query:

    ```
    SELECT VALUE 
        c.id 
    FROM
        c
    ```

20. Click the **Execute Query** button at the top of the query editor and review the results.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/19.png?st=2019-09-18T09%3A57%3A40Z&se=2022-09-19T09%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bADqXDkzPx%2F8Xm1ovoGI1gv%2FnD0TjrD4TlO4eW%2ForFQ%3D)

21. In the query editor, replace the existing query with the following query:

    ```
    SELECT VALUE { 
        "badgeNumber": SUBSTRING(c.id, 0, 8),
        "company": c.company,
        "fullName": CONCAT(c.firstName, " ", c.lastName)
    } FROM c
    ```

22. Click the **Execute Query** button at the top of the query editor and review the results.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/20.png?st=2019-09-18T09%3A58%3A01Z&se=2022-09-19T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C1r27yBQXIjLB5kfxBC6oQmL4A6sZnNUSUnxZ4KUDOI%3D)

**Review**: In this exercise, you created a new Cosmos DB account, database, and collection, added sample items to the collection, and run sample queries targeting these items.

## Exercise 2: Deploy Application using Cosmos DB

### Task 1: Deploy API App code using Azure Resource Manager templates and GitHub

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/21.png?st=2019-09-18T09%3A58%3A21Z&se=2022-09-19T09%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=G5wfobTybzFRyjlbWxh1RpB%2Bvi5ackGaU9goPdRsnqc%3D)

4. On the **Template deployment** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/23.png?st=2019-09-18T09%3A59%3A00Z&se=2022-09-19T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8W1Bolpv8KIhM0V8ECbSJ6rvnjXEHvfaRyIr1R%2FI%2Bto%3D)

5. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/24.png?st=2019-09-18T09%3A59%3A19Z&se=2022-09-19T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fHwg8ZLFwAdarLmDrG%2BlzT%2FyI8zlGdJMxEyRZrXQGbw%3D)

7. Open the below link in Chrome, Copy the data and paste it in **Edit template** blade

**Note: Delete the default data.**

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T02/Module_02/LabFiles/Starter/api.json?st=2019-09-19T09%3A42%3A07Z&se=2022-09-20T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z84kKOvZsNtw%2FRLSZ1m19Uw8sdSkxl7Nh8fK7mLGZ8s%3D

```

10. Click the **Save** button to persist the template.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/26.png?st=2019-09-18T09%3A59%3A59Z&se=2022-09-19T09%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mgb4M9qCnKmK1jsggImoJInZKtw4vX6RnCxBVJYG8dw%3D)

11. Back on the **Custom deployment** blade, perform the following tasks:

```
     Subscription: Select the default

     Resource group: {{ ResourceGroup }}
     
```

 * In the **Terms and Conditions** section, click the **I agree to the terms and conditions stated above** checkbox.

 * Click the **Purchase button.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/27.png?st=2019-09-18T10%3A00%3A17Z&se=2022-09-19T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yAsGFRx5X2PfzQfnuOvZ1uo8u6xlCu0TQucJkwDVp2c%3D)

12. Wait for the deployment to complete before you proceed to the next task.

    **Note**: Deployment from source control can take up to 10 minutes.

### Task 2: Validate API App

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/28.png?st=2019-09-18T10%3A00%3A34Z&se=2022-09-19T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wz461%2FIyUoAY9Hl%2Bf7WwvychpBq07Odm8c3t9lXHnmQ%3D)

3. On the **{{ ResourceGroup }}** blade, click the entry representing the newly created App Service API app.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/29.png?st=2019-09-18T10%3A00%3A54Z&se=2022-09-19T10%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=e7tCZaSge61AwU%2Blt7D0qZeIcDtoQQ5fxMzS9mrwqV4%3D)

4. On the API app blade, under **Settings**, click **Configuration**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/30.png?st=2019-09-18T10%3A01%3A13Z&se=2022-09-19T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vNWkBAqNfLrqHVdwJcX80ScLcICCqHWGRX%2BMyFHai24%3D)

5. On the Application Settings blade, scroll down to the **Application settings** section and perform the following tasks:


 *  Set the value of the **CosmosDB:AuthorizationKey** setting to the value of the **PRIMARY KEY** setting of the **Cosmos DB** account you created earlier in this lab.

 *  Update the value of the **CosmosDB:EndpointUrl** setting to the value of the **URI** setting of the **Cosmos DB** instance you created earlier in this lab.
   
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/65.PNG?st=2019-09-19T10%3A10%3A46Z&se=2022-09-20T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=SAk9MifddbVBdQu96%2BCxchwV9bDSyUD3bIOArSwfaIY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/66.PNG?st=2019-09-20T04%3A27%3A54Z&se=2022-09-21T04%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AO7QHJE5yM%2FHeOVn9pNKFmcsUwp32TO2zMKxZ1hAH6o%3D)


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/31.png?st=2019-09-18T10%3A01%3A33Z&se=2022-09-19T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=59kGkeelqB2WJrenoncc3Dg3FDQYNg9ke22gNcUxdoY%3D)

6. Click the **Save** button at the top of the pane.

7. On the left-side of the API app blade, click **Overview**.

8. Click the **Restart** button at the top of the blade and, when prompted to confirm, click **Yes**. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/32.png?st=2019-09-18T10%3A01%3A54Z&se=2022-09-19T10%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0wmiS0s5aRykNFakCC7Xwt0oeVpnpcL92Gl70Ee%2BswM%3D)

9. Click the **Browse** button at the top of the blade. This will open a new browser tab displaying the **Swagger UI** homepage.

  **Note**: If you click the **Browse** button before the API app has fully restarted, you may not be able to follow the remaining steps in this task. If this happens, refresh your browser until the API app is running again.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/33.png?st=2019-09-18T10%3A02%3A12Z&se=2022-09-19T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=K%2FIrNPdWoTm89p4tduwchh87NgTn8g4OxLAp5Znwkug%3D)

10. On the **Swagger UI** homepage, click **GET/Documents**.

11. Click the **Try it out!** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/34.png?st=2019-09-18T10%3A02%3A33Z&se=2022-09-19T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=s1WYx48TKmzVZIUzsu2dX9ADXqfdJFUIZ3CTe9cmods%3D)

11. Review the results of the request.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/35.png?st=2019-09-18T10%3A02%3A50Z&se=2022-09-19T10%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jyAEYSKzkG9gfjz%2FGYAbV5Qfcc%2F1jBTK%2Brla5KikjNQ%3D)

12. Back on the **Swagger UI** homepage, click **POST/Populate**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/36.png?st=2019-09-18T10%3A03%3A10Z&se=2022-09-19T10%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Z2SKlm%2FHxolAFGPzA2M%2F4DElGKu6Kh3JJCQAlB3wHac%3D)

13. In the **Parameters** section, in the **Value** field for the **options** parameter, paste in the following JSON content:

    ```
    {
        "quantity": 50
    }
    ```

14. In the **Response Messages** section, click the **Try it out!** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/37.png?st=2019-09-18T10%3A03%3A28Z&se=2022-09-19T10%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Bpqv7aYwVMcKvBLosKa2zopIVBDeNJubE7SJxDhhpfM%3D)

15. Review the results of the request.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/38.png?st=2019-09-18T10%3A03%3A53Z&se=2022-09-19T10%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=24%2F48wf7ItTOmfkfCK6mlRItv8X9ttBxdQCBiUsTpEw%3D)

16. Back on the **Swagger UI** homepage, click **GET/Documents**.

17. Locate the **Response Messages** section. Click the **Try it out!** button.

18. Review the results of the request.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/39.png?st=2019-09-18T10%3A04%3A15Z&se=2022-09-19T10%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hkDi4FQwKKUTQ7lkvwkYd9CZUkU%2BAgHveXcxyGZxYbM%3D)

19. Close the new browser tab and return to the browser tab displaying the Azure portal.

**Review**: In this exercise, you created a new API App that uses the .NET Core DocumentDB SDK to connect to Azure Cosmos DB collection and manage its documents.

## Exercise 3: Connect Cosmos DB to Azure Search

### Task 1: Create Azure Search Instance

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Search** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/40.png?st=2019-09-18T10%3A04%3A37Z&se=2022-09-19T10%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d5x3MGJqirsWUZLP5qLmq9vQTicHE1F6Xn8pfJ4Pv70%3D)

4. On the **Azure Search** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/42.png?st=2019-09-18T10%3A05%3A16Z&se=2022-09-19T10%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IwD43LIdBFtsVdQyrD8hk0eJwKpHhXzd28rJgcvimbk%3D)

5. On the **New Search Service** blade, perform the following tasks:

```
     Subscription: Select the default
     
     Resource group: {{ ResourceGroup }}
     
     URL: Enter a globally unique name. Record its value. You will use it later in this lab.
     
     Location: {{ Location }}
     
     Pricing Tier: Free
     
 ```

  Click the **Review + Create** button, review the settings then click **Create**.
    

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/43.png?st=2019-09-18T10%3A05%3A37Z&se=2022-09-19T10%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d6aJMhwc1dDELElEY4GvNQU6KHnafpZKUcraP7T5R%2FQ%3D)

6. Wait for the provisioning to complete before you proceed to the next step.

7. In the hub menu in the Azure portal, click **Resource groups**.

8. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

9. On the **{{ ResourceGroup }}** blade, click the entry representing the newly created Azure Search instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/44.png?st=2019-09-18T10%3A05%3A59Z&se=2022-09-19T10%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7eOjA%2B3p52bApN2fjeFQPP0kg1I0cVpTRxxVkZ1vH6w%3D)

10. On the Search service blade, click **Keys**.

11. In the **Keys** pane, record the value of **QUERY KEY**. You will use it later in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/45.png?st=2019-09-18T10%3A06%3A20Z&se=2022-09-19T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TXJ87sgMBp%2BsvZEX7M6A2h8WmWsgQ79SgCVNDPNWxjM%3D)

  **Note:** The query key is located below the primary and secondary keys, and does not have a name by default.

### Task 2: Index Cosmos DB Data in Azure Search

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

3. On the **{{ ResourceGroup }}** blade, click the entry representing the Azure Cosmos DB account you created earlier in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/46.png?st=2019-09-18T10%3A06%3A42Z&se=2022-09-19T10%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CWvkeUQOhKxYxPE16qnR78Wi7T92wTeJwp%2FR85T%2BKMQ%3D)

4. On the Azure Cosmos DB account blade, click **Add Azure Search**.

5. On the Select a search service tab, select the Azure Search service that was previously created, then click **Next: Connect to your data**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/47.png?st=2019-09-18T10%3A07%3A04Z&se=2022-09-19T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=u003YLQFWg5E4yprWSIiAHeKWqcw9%2FSNRK6bRjuBeQI%3D)

6. On the **Connect to your data** tab, perform the following tasks:

```

    Name: cosmosdata

    Cosmos DB account: Accept the default entry.

    Database: select the FinancialClubDatabase

    Collection: MemberCollection

    In the **Query** field, enter the following SQL query:

        SELECT c.id, c.firstName, c.lastName, c.age, c.salary, c.company, c.isVested, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
        

    Ensure that the **Query results ordered by _ts** checkbox is selected.
    
```

**Note: If Cosmos DB account default entry is not working, you can take from below path and paste it in that.**

 * In the hub menu in the Azure portal, click **Resource groups**.

 * On the **Resource groups** blade, click **{{ ResourceGroup }}**.

 * On the **{{ ResourceGroup }}** blade, click the Azure **Cosmos DB** then click on **Keys** and take the **PrimaryKey value**
 
 ![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/68.PNG?st=2019-09-20T04%3A39%3A15Z&se=2022-09-21T04%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VK8j%2BoF5gB%2FONIJRlFIHvcPeeV90A3dJLn09781Fvzk%3D)

 7. Click the **Next: Add cognitive search (optional)** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/48.png?st=2019-09-18T10%3A07%3A27Z&se=2022-09-19T10%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qQCNNEgOsfzzNYX3YPoLDgUB76PfhdWUmHp%2FzoWQdRM%3D)

8. On the **Cognitive Search** blade, click the **Skip to: Customize target index** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/49.png?st=2019-09-18T10%3A08%3A03Z&se=2022-09-19T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wFrnnI4UQznmjRTWSa%2FP5oUUApx8ohYfBsBaqNmQDiA%3D)

9. On the **Index** blade, perform the following tasks:

```

    Index name: memberindex

    Key: drop-down list, ensure that the id entry is selected
    
```

   * For the **id** field in the table, ensure that the **RETRIEVABLE**, **FILTERABLE**, and **SORTABLE** checkboxes are selected.

   * For the **firstName** field in the table, ensure that the **RETRIEVABLE**, **SORTABLE**, and **SEARCHABLE** options are selected.

   * For the **lastName** field in the table, ensure that the **RETRIEVABLE**, **SORTABLE**, and **SEARCHABLE** checkboxes are selected.

   * For the **age** field in the table, ensure that the **RETRIEVABLE**, **FILTERABLE**, **SORTABLE**, and **FACETABLE** checkboxes are selected.

   * For the **salary** field in the table, ensure that the **RETRIEVABLE**, **FILTERABLE**, **SORTABLE**, and **FACETABLE** checkboxes are selected.

   * For the **company** field in the table, ensure that the **RETRIEVABLE**, **FACETABLE**, and **SEARCHABLE** checkboxes are selected.

   * For the **isVested** field in the table, ensure that the **RETRIEVABLE**, **FILTERABLE**, **SORTABLE**, **FACETABLE** checkboxes are selected.

10.Click the **Next: Create an indexer** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/50.png?st=2019-09-18T10%3A08%3A26Z&se=2022-09-19T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ER0rBgq9tQ3HviIc%2FulsLa9us3w%2FENfDbLJ2bXw1VYs%3D)

11. On the **Create an Indexer** blade, perform the following tasks:

```

    Name: cosmosmemberindexer

    Schedule: select the **Custom** option.

    Interval (minutes): Type 5

    In the Start time (UTC) field, specify the current date and accept the default value of the time entry
    
```

 12. Click the **Submit** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/51.png?st=2019-09-18T10%3A08%3A46Z&se=2022-09-19T10%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iiSY5e8RTcJSDGP5SGKvglqJovIPRS9zowXj6jwZbWk%3D)

### Task 3: Validate API App

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

3. On the **{{ ResourceGroup }}** blade, click the entry representing the App Service API app you created earlier in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/52.png?st=2019-09-18T10%3A09%3A06Z&se=2022-09-19T10%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0NHmVaD9VN7ivj5%2BNq9FjIlMN7%2BJVZjBsMbGig7ahp0%3D)

4. On the API app blade, click **Configuration**.

5. On the Application settings blade, scroll down to the **Application settings** section and perform the following tasks:


  * Set the value of the **Search:AccountName** setting to the name of the Azure Search instance you created earlier in this lab.

  * Set the value of the **Search:QueryKey** setting to the value of the **QUERY KEY** of the Azure Search instance you created earlier in this lab.
    
  * Set the value of the **Search:IndexId** setting to the value **memberindex**. 

   Click the **Save** button at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/76.png?st=2019-09-19T10%3A47%3A29Z&se=2022-09-20T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7C9tUq8%2FDQPsGfdh0MgEpQF6YBF1op%2FdaYZlVJMNMZA%3D)

6. On the API app blade, click **Overview**.

7. Click the **Restart** button at the top of the blade and, when prompted to confirm, click **Yes**. 

8. Click the **Browse** button at the top of the blade. This will open a new browser tab displaying the **Swagger UI** homepage.

  **Note**: If you click the **Browse** button before the API app has fully restarted, you may not be able to follow the remaining steps in this task. If this happens, refresh your browser until the API app is running again.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/54.png?st=2019-09-18T10%3A09%3A46Z&se=2022-09-19T10%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lVSF2ibW1ykuvtTlvmH7s7IPMNh7WkjWmvLupKpYeMo%3D)

9. On the **Swagger UI** homepage, click **Cosmos DB API v.1.0.0** at the top of the page and select the **Cosmos DB API v.2.0.0** option from the drop-down list.

10. Click **GET/Documents/search**.

11. In the **Parameters** section, in the **Value** text box of the **query** parameter, type the following text:

    ```
    Oneal
    ```

12. In the **Response Messages** section, click the **Try it out!** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/55.png?st=2019-09-18T10%3A10%3A04Z&se=2022-09-19T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GMv%2BJaapr5gntdfbDW3PfE%2BamKtgvvgjOZ5SvjD47vU%3D)

13. Review the results of the request.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/56.png?st=2019-09-18T10%3A10%3A28Z&se=2022-09-19T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BpcnYpfAVdNWfKB8gZ5swndBkjxrry1ZyXXIQBv7Vk0%3D)

14. In the **Parameters** section, in the **Value** text box of the **query** parameter, type the following text:

    ```
    penn*
    ```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/57.png?st=2019-09-18T10%3A10%3A47Z&se=2022-09-19T10%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=g32vmElCbqTEb2EVtPJoxLx0FN7%2FLNKglsUIQNgUlkM%3D)

15. In the **Response Messages** section, click the **Try it out!** button.

16. Review the results of the request.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab3-Deploying%20Database%20Instances%20in%20Azure/58.png?st=2019-09-18T10%3A11%3A05Z&se=2022-09-19T10%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tsjBLga3eHXJLD%2BfJ%2FrTWdoqs8aWybTYhTv4kDfLT5k%3D)

17. Close the new browser tab and return to the browser tab displaying the Azure portal.

**Review**: In this exercise, you created an Azure Search instance that uses an indexer to index the documents in Azure Cosmos DB.
