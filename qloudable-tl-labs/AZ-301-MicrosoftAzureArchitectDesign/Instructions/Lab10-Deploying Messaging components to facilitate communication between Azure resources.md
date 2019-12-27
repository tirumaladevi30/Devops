# Lab: Deploying Messaging components to facilitate communication between Azure resources

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites) 

[Exercise 1: Deploy a Service Bus namespace](#exercise-1-deploy-a-service-bus-namespace)

[Exercise 2: Create a logic app](#exercise-2-create-a-logic-app)

## Overview

The aim of this lab is, Deploying Messaging components to facilitate communication between Azure resources. for this you have create service bus, storage account and logic app in azure portal.

In this lab excersice1 you have to create a new Service Bus namespace and record a connection string to access queues in the namespace. In this lab exercise2, you have create a logic app that is triggered by messages from a queue in a Service Bus namespace.

### Scenario and Objectives

XYZ Training Corporation wants to take advantage of Integrating Azure Solution Components using Messaging Services.

After completing this lab, you will be able to:

* Deploy a Service Bus namespace 

* Create a logic app

## Pre-Requisites

* Familiarity with azure portal

## Exercise 1: Deploy a Service Bus namespace

### Task 1: Open the Azure portal

1. Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Portal Usermail }}

Azure Password: {{ Portal Password }}

```

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/1.png?st=2019-09-20T09%3A39%3A57Z&se=2026-09-21T09%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iQGKKrn1CFjVBuJ2HhPHP1hWOjdhNFs%2BwwcaOHqFJ0E%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/l2.png?st=2019-09-20T09%3A40%3A17Z&se=2026-09-21T09%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=446LHvJn4ufi6BKwPHFKC3Hkk1qYbZkvpdC229cxQDM%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/l3.png?st=2019-09-20T09%3A40%3A54Z&se=2026-09-21T09%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=206owzkQ%2FbCUaVgRVBSw4qpdeq0u8kcVh1l1IH901EM%3D" alt="image-alt-text" >

<img src="https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/l4.png?st=2019-09-20T09%3A41%3A13Z&se=2025-09-21T09%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KUBBpi4lthsKJdgSkl4dGoZOg4mpveHjWCmdPQ906Ts%3D" alt="image-alt-text" >	

### Task 2: Create a Service Bus namespace

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Service Bus** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/2.png?st=2019-09-20T09%3A41%3A46Z&se=2025-09-21T09%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DK34UHOYeX5LtoXR4KpJSJu9BbqFtYMySzXkd1fq3EM%3D)

3. On the **Everything** blade, in the search results, click **Service Bus**.

4. On the **Service Bus** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/3.png?st=2019-09-20T09%3A42%3A08Z&se=2026-09-21T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Nk1dzWuKakFzFpaT1mHLARoOqr5cNZAdQBTr6ug4Vy8%3D)

5. On the **Create namespace** blade, perform the following tasks:

```

Name: enter a globally unique name.

Pricing tier: drop-down list, select the Basic option.

Subscription: default

Resource group: {{ ResourceGroup }}

Location: {{ location }}

```

Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/4.png?st=2019-09-20T09%3A42%3A26Z&se=2025-09-21T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2By5uFY4a0Rwwh2aYyMGFvaIyO%2F8cdYy8wnpgYwgXfEM%3D)

6. Wait for the provisioning to complete before you proceed to the next step. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/5.png?st=2019-09-20T09%3A42%3A48Z&se=2025-09-21T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mc%2BkFI6adKXJQ3qYizJOquFD8dIUizF6Gmtz2KVpdxg%3D)

### Task 3: Create a Service Bus Queue

1. In the hub menu of the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{ ResourceGroup }}.

3. On the {{ ResourceGroup }} blade, click the newly created Service Bus namespace.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/6.png?st=2019-09-20T09%3A43%3A05Z&se=2025-09-21T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Yn6B%2F4QEyKb%2BIdO%2FVik%2BPcgjDHE1xcziRry9XYvRwKU%3D)

4. On the Service Bus namespace blade, in the **ENTITIES** section, click **Queues**.

5. On the Service Bus namespace blade, click the **+ Queue** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/7.png?st=2019-09-20T09%3A43%3A21Z&se=2025-09-21T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6%2BuiGYt%2BrSNN8NimsJTxqh19z3MktlZy89PCXu8LP2A%3D)

6. In the **Create queue** pane, perform the following tasks:

    - In the **Name** text box, type **messages**.

    - Leave all remaining settings with their default values.

    - Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/8.png?st=2019-09-20T09%3A43%3A45Z&se=2025-09-21T09%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fudKxCgfFn0L%2BR9sm75iWi03qf8yLCPzd5lhnsQkMPo%3D)

### Task 4: Get Service Bus Connection String

1. Back on the Service Bus namespace blade, click **Shared access policies**.

2. On the Service Bus namespace blade, click the **RootManageSharedAccessKey** policy.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/9.png?st=2019-09-20T09%3A44%3A03Z&se=2025-09-21T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vsCDK6CAXDKbT1pUxzNJuvMHzD8ef10zdJIC3%2BweIjc%3D)

3. In the **SAS Policy: RootManageSharedAccessKey** pane, locate and record the value of the **Primary Connection String** field. You will use this value later in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/10.png?st=2019-09-20T09%3A44%3A28Z&se=2025-09-21T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nvFk8lkdbc9abkMvkBESTTMtgrxmViWPV%2Bzy%2BdUcmyc%3D)

> **Review**: In this exercise, you created a new Service Bus namespace and recorded a connection string to access queues in the namespace.

## Exercise 2: Create a logic app

### Task 1: Create an Azure Storage account

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Storage Account** and press **Enter**.

3. On the **Everything** blade, in the search results, click **Storage Account**.

4. On the **Storage Account** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/11.png?st=2019-09-20T09%3A44%3A47Z&se=2025-09-21T09%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=oPKWrw0Y0f3ekGzntODcjS5I7aOPdl5JY7iP2Cqvvjg%3D)

5. On the **Create storage account** blade, perform the following tasks:

```

Name: type a unique name consisting of a combination of between 3 and 24 characters and digits.

Deployment model: ensure that the Resource manager option is selected.

Account kind: drop-down list, ensure that the Storage (general purpose v1) option is selected.

Location: {{ location }}

Replication: drop-down list, select the Locally-redundant storage (LRS) entry.

Performance: ensure that the Standard option is selected.

Secure transfer required: ensure that the Disabled option is selected. 

Subscription: default

Resource group: {{ ResourceGroup }}

Configure virtual networks: set to its default value.

Hierarchical namespaces: set to its default value.

```
Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/12.png?st=2019-09-20T09%3A45%3A08Z&se=2025-09-21T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=lZf6xzLi3vPo0t5lDhXS12SRCYea5w1psWZNvg0ERDA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/13.png?st=2019-09-20T09%3A45%3A29Z&se=2025-09-21T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MJus6dcX64qDfXWz0XSPq0emUdh4XDHqnFK9CyEEkAI%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/14.png?st=2019-09-20T09%3A45%3A44Z&se=2025-09-21T09%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fbz0B8NERXWZUfmp%2FgTpc59%2Ff%2FgcYqL%2FNcz6lio%2FmFw%3D)

6. Wait for the provisioning to complete before you proceed to the next step.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/15.png?st=2019-09-20T09%3A46%3A16Z&se=2025-09-21T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=I12c%2FDRe8elOky6m6%2Fe7s6KOvSDNdVIFostQx7ZNo%2BU%3D)

7. In the hub menu of the Azure portal, click **Resource groups**.

8. On the **Resource groups** blade, click {{ ResourceGroup }}.

9. On the {{ ResourceGroup }} blade, click the newly created Azure Storage account. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/16.png?st=2019-09-20T09%3A46%3A40Z&se=2025-09-21T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1LuuDPjmdQfbJlirj0FTG5FAaGlG0%2BEoPC0o1GlWirg%3D)

10. On the Storage account blade, click the **Blobs** tile. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/17.png?st=2019-09-20T09%3A46%3A57Z&se=2025-09-21T09%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GtyAXpAwVpcKizGKj3Y51UZ1AnknNYcvp%2FNIJ2z3oos%3D)

11. On the Storage account blade, click the **+ Container** button.

12. In the **New container** pane, perform the following tasks:

    - In the **Name** text box, type **messageoutput**.

    - In the **Public access level** drop-down list, select the **Blob (anonymous read access for blobs only)** option.

    - Click the **OK** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/18.png?st=2019-09-20T09%3A47%3A15Z&se=2026-09-21T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9AvmPorAhqSc9nU%2BkNakRvyZs0wmJDktpvsvztuVHRM%3D)

### Task 2: Create a logic app

1. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Logic App** and press **Enter**.

2. On the **Everything** blade, in the search results, click **Logic App**.

3. On the **Logic App** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/19.png?st=2019-09-20T09%3A47%3A34Z&se=2025-09-21T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hbxEBTqt3b4xRJVyETCG0somXKI9FkL8FlNAG6R%2FDW8%3D)

4. On the **Create logic app** blade, perform the following tasks:

```

Name: type ServiceBusWorkflow.

Subscription: default

Resource group: {{ ResourceGroup }}

Location: {{ location }}

Log Analytics: ensure that the Off button is selected.

```
Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/20.png?st=2019-09-20T09%3A47%3A59Z&se=2026-09-21T09%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ptDhgrmPkY7qaH0ouqjyMBLkeOM83AexvmdwyuF42Vo%3D)

5. Wait for the provisioning to complete before you proceed to the next task. 

### Task 3: Configure logic app steps.

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click {{ ResourceGroup }}.

3. On the {{ ResourceGroup }} blade, click the entry representing the logic app you created in the previous task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/21.png?st=2019-09-20T09%3A48%3A19Z&se=2025-09-21T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ciWctyj7NEGEGHf0fxR9fVeyKPv2QPy4%2Frn0C589t7w%3D)

4. On the **Logic Apps Designer** blade, scroll down and click the **Blank Logic App** tile in the **Templates** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/22.png?st=2019-09-20T09%3A48%3A43Z&se=2025-09-21T09%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=qL3KLNUTeOYKOcFyRbx9XALy6ibV%2BQuGiwovRjPJ6wU%3D)

5. On the **Logic Apps Designer** blade, perform the following tasks:

    - In the **Search connectors and triggers** text box, type **Service Bus**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/23.png?st=2019-09-20T09%3A49%3A02Z&se=2025-09-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5jlxkesLjMvDPYPOvJKFGZV7l0SRMiHNWIajL3sajbk%3D)

In the search results, select the trigger named **When a message is received in a queue (auto-complete) - Service Bus**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/24.png?st=2019-09-20T09%3A49%3A22Z&se=2025-09-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9tNJdKR2FAg0irts97zwHaXDC2%2BYX2zC3tXjtuw%2BVO4%3D)

  - In the **Connection Name** text box, type **ServiceBusConnection**.
    
  - In the list of **Service Bus namespaces**, select the namespace you created earlier in this lab.

  - In the list of policies, select the **RootManageSharedAccessKey** policy.

  - Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/25.png?st=2019-09-20T09%3A49%3A38Z&se=2025-09-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=O7uDub6bORFPyHa%2BQFE6nt1BId1VRJj68cFIyk45T70%3D)

6. In the **When a message is received in a queue (auto-complete)** step, perform the following tasks:

    - In the **Queue name** drop-down list, select the **messages** entry.

    - In the **Interval** text box, type **30**.

    - In the **Frequency** drop-down list, select the **Second** entry.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/26.png?st=2019-09-20T09%3A49%3A58Z&se=2026-01-21T09%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IJhBjGvtwUlXHYsyqFwVzDNkSaeSTJX855KkRoNSR24%3D)

7. On the **Logic Apps Designer** blade, click the **+ New Step** button.

8. On the **Logic Apps Designer** blade, perform the following tasks:

    - In the **Search connectors and actions** text box, type **Storage blob**.

    - In the search results, select the action named **Create blob - Azure Blob Storage**.

    - In the **Connection Name** text box, type **StorageConnection**.
    
    - In the list of *Storage accounts*, select the account you created earlier in this lab.

    - Click the **Create** button.  

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/27.png?st=2019-09-20T09%3A50%3A29Z&se=2025-09-21T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ldx3XBTnWZDtl5ha16CPSqOrz69WIspubshJo9m8bdc%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/28.png?st=2019-09-20T09%3A50%3A51Z&se=2025-09-21T09%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aifFrm1TjHhsObndCwG8tsoPa6aL3nzoHEiOBUNlyU8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/29.png?st=2019-09-20T09%3A51%3A10Z&se=2025-09-21T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=idbVVbZoS%2FlF1vrRh4M4l3q2pL83sIJEVBJ67xUxfcI%3D)

9. In the **Create Blob** step, perform the following tasks:

    - In the **Folder path** text box, type **/messageoutput**.

    - In the **Blob name** text box, type **@concat(triggerBody()?['MessageId'], '.txt')**.

    - In the **Blob content** text box, type **@string(decodeBase64(triggerBody()?['ContentData']))**.

10. At the top of the **Logic Apps Designer** blade, click the **Save** button to persist your workflow.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/30.png?st=2019-09-20T09%3A51%3A33Z&se=2025-09-21T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RmlRlhtm4SQn2O6VXSanpmD58sB4IFTiJXFE5U84%2FdI%3D)

### Task 2: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/31.png?st=2019-09-20T09%3A51%3A54Z&se=2025-09-21T09%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F2P6TBS81Wg%2BIrSrFvcHCW0gBWgnkwZi3GBqlYDJMcs%3D)

 > **Note**: The **Cloud Shell** icon is a symbol that is constructed of the combination of the *greater than* and *underscore* characters.

2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/32.png?st=2019-09-20T09%3A52%3A18Z&se=2025-09-21T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fGiuIGiry%2FWFaQBA0JGbRd37WTpW%2FmfkOwAvYPxnpy8%3D)

   > **Note**: If you do not see the configuration options for **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. If so, proceed directly to the next task. 

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

    - Leave the **Subscription** drop-down list entry set to its default value.

    - In the **Cloud Shell region** drop-down list, select the Azure region matching or near the location where you deployed resources in this lab.

    - In the **Resource group** section, select the **Use existing** option and then, in the drop-down list, select {{ ResourceGroup }}.

    - In the **Storage account** section, ensure that the **Create new** option is selected and then, in the text box below, type a unique name consisting of a combination of between 3 and 24 characters and digits. 

    - In the **File share** section, ensure that the **Create new** option is selected and then, in the text box below, type **cloudshell**.

    - Click the **Create storage** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/33.png?st=2019-09-20T09%3A52%3A37Z&se=2025-09-21T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dafY4XFc936wtk44cVit9AYBiEhV7qfK6fAtAkOQqoU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/34.png?st=2019-09-20T09%3A52%3A59Z&se=2026-09-21T09%3A52%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jQ43c5P2HPMh0f%2FDBjA7UTbZmmEYaRlDGEOmBUY%2FrSo%3D)

4. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

### Task 4: Validate Logic App using Node.js

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

2. At the **Cloud Shell** command prompt at the bottom of the portal, type in the following command and press **Enter** to install the **azure** package using NPM:

```
npm install azure
```

3. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to open the interactive node terminal:

```
node
```

4. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to import the **azure** module in Node:

```
var azure = require('azure');
```
    
> **Note**: The output will show **undefined**. This is expected.
    
5. At the **Cloud Shell** command prompt, type in the following command (replacing the placeholder `<Service Bus namespace connection string>` with the value of your url you recorded earlier in this lab) and press **Enter** to create a new variable for your Service Bus namespace connection string:

```
var connectionString = '<Service Bus namespace connection string>';
```

6. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to create a new client to connect to the Service Bus namespace:

```
var serviceBusService = azure.createServiceBusService(connectionString);
```

7. At the **Cloud Shell** command prompt, type in the following command and press **Enter** to send a message to Service Bus namespace queue using the client.

```
serviceBusService.sendQueueMessage('messages', { body: 'Hello World' }, function(error) { console.log(error) });    
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/35.png?st=2019-09-20T09%3A53%3A19Z&se=2026-09-21T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bu9FZyP4a%2BNtWIn%2Bi%2FqLQ6wnnoza%2BMHTQ9WGXLmN9KY%3D)

8. In the hub menu of the Azure portal, click **Resource groups**.

9. On the **Resource groups** blade, click {{ ResourceGroup }}.

10. On the {{ ResourceGroup }} blade, click the Azure Storage account you created earlier in this lab.

11. On the Storage account blade, click the **Blobs** tile. 

12. On the Storage account container blade, click the **messageoutput** container.

13. Note the newly created blob in your container.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/lab10/36.png?st=2019-09-20T09%3A53%3A39Z&se=2025-09-21T09%3A53%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YkDcGTODqFYTlTOX3JL2ek2hCiJ7z%2B4CDj8sHvqWVfM%3D)

> **Review**: In this exercise, you created a logic app that is triggered by messages from a queue in a Service Bus namespace.
