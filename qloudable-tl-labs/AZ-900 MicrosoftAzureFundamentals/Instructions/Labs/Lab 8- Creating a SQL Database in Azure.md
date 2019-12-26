# Lab 8: Creating a SQL Database in Azure

## Table of Contents

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Creating a new Azure SQL database in Azure and configuring SQL Server firewall rules](#exercise-1-creating-a-new-azure-sql-database-in-azure-and-configuring-sql-server-firewall-rules)

[Exercise 2: Managing content of an Azure SQL database by using SQL Server Management Studio](#exercise-2-managing-content-of-an-azure-sql-database-by-using-sql-server-management-studio)


## Overview

The aim of this lab is to Create SQL Database in Azure.

### Scenario and Objectives

To accommodate a steadily increasing volume of internet-based customers, Adatum Corporation has decided to store its marketing data in a dedicated database hosted in Microsoft Azure. You are considering using Azure SQL Database for this purpose and have decided to test its capabilities.

After completing this lab, students will be able to:

* Create an Azure SQL database.
* Create a table in an Azure SQL database.
* Add data to a table in an Azure SQL database.
* Query the content of a table in an Azure SQL database.
  
**Note:** *The lab steps for this course change frequently due to updates to Microsoft Azure. Microsoft Learning updates the lab steps frequently, so they are not available in this manual. Your instructor will provide you with the lab documentation.*


## Pre-Requisites

* Azure portal subscription. 
* SQL Server Management Studio

### Azure portal subscription

These EAs provide discounts on Azure pricing and allow users to migrate software licenses from on-premises servers to Azure. Users with an EA also have access to the Azure Enterprise Portal, which provides billing and subscription management features.

### SQL Server Management Studio

SQL Server Management Studio (SSMS) is a software application first launched with Microsoft SQL Server 2005 that is used for configuring, managing, and administering all components within Microsoft SQL Server. It's the successor to the Enterprise Manager in SQL 2000 or before. The tool includes both script editors and graphical tools which work with objects and features of the server.

## Exercise 1: Creating a new Azure SQL database in Azure and configuring SQL Server firewall rules

### Scenario

You start your tests by creating a test database to which you will subsequently add some test tables. You will then populate the tables with sample data.

The main tasks for this exercise are as follows:

1.	Create a new Azure SQL database by using the Azure Portal

2.	Configure an Azure SQL Server firewall rule by using Azure Portal

### Task 1: Create a new Azure SQL database by using the Azure Portal

1.	 Using the Chrome browser, login into Azure portal with the below details.


**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/1.png?st=2019-08-26T09%3A00%3A41Z&se=2025-08-27T09%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PSQHgANo3LDC0kTP9cIoUbrj0I6rid3jHCxs83zzuBQ%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/2.png?st=2019-08-26T09%3A01%3A09Z&se=2025-08-27T09%3A01%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ktSNI7qckR8AzvPmolB6KCGKGdiugSQ%2F3IWaWYj4OM8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab6%20-%20Configure%20Azure%20Storage/3.png?st=2019-08-23T09%3A56%3A53Z&se=2025-08-24T09%3A56%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dmPL2LoX8Py2afBo5wbZF14IBfsX%2B%2ByjwjvfWlrD3CM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/4.png?st=2019-08-26T09%3A04%3A11Z&se=2025-08-27T09%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tRFXHLRfyULGRgXd6MpZvbo0QVC3ehWjCiZajybzBZI%3D)

2. Create a new SQL database by specifying the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/5.png?st=2019-08-26T09%3A33%3A21Z&se=2025-08-27T09%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CCUh7LBBv612sAbgbkc778jJBiqbroQN4E5QdU2K9vM%3D)

 **ResourceGroup:** {{resource-group-name}}

 **Region:** {{Location}}
 
 ```
 Subscription: {{subscriptionId}}

 Database name: 10979E0602-db

 Server name: any valid, unique name

 Server admin login: Student

 Password: Password@1234

 Confirm password: Password@1234

 Want to use SQL elastic pool?:  No

 ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/6.png?st=2019-08-26T09%3A36%3A12Z&se=2025-08-27T09%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FbVUvByiZ%2ByokJHzLlnQnhXi0n0xQSx5WKFgALeuANA%3D)

 ```
 Select source: Blank database

 Pricing tier: Basic

 Collation: SQL_Latin1_General_CP1_CI_AS

 ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/7.png?st=2019-08-26T09%3A36%3A45Z&se=2025-08-27T09%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ADbfOTU19q2JCfIaRr0P1d6oDadkHW0jYPZsPuJZKRs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/8.png?st=2019-08-26T09%3A37%3A09Z&se=2025-08-27T09%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FHFhVVvFu7rqqEGRsVegoOgkX9zxyV05foOEeR%2FbzbU%3D)

### Task 2: Configure an Azure SQL Server firewall rule by using Azure Portal

1.	In the Azure portal, navigate to the **10979E0602-db** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/9.png?st=2019-08-26T09%3A38%3A00Z&se=2025-08-27T09%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2B%2F7qqboR3rscPNWWE%2BCtaij3lOd0SoY1f6l9VZ495jw%3D)


2.	From the **10979E0602-db** blade, navigate to the **Firewall settings** of the server hosting the newly created Azure SQL database.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/10.png?st=2019-08-26T09%3A55%3A04Z&se=2025-08-27T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7KXsQvCEYMg0uOzwE5lA4yH%2FsLn%2F5IbaIC2JwrdCouM%3D)

3.	Add a firewall rule representing the **client IP** to the list of firewall rules.

4.	In the **START IP** column of the newly added firewall rule, replace the last two numbers separated by a period with **0.0.**

5.	In the **END IP** column of the newly added firewall rule, replace the last two numbers separated by a period with **255.255.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/11.png?st=2019-08-26T09%3A55%3A28Z&se=2025-08-27T09%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gHjo%2FRoq6tgx3IcxxB5b9NIDQkjF1SweMnfK0KLviDw%3D)

6.	Click **Save.**

**Note:** It might take up to five minutes for this change to take effect.

**Result:** After you completed this exercise, you have created a Microsoft Azure SQL database. You have also configured Server firewall rules to allow connectivity from your lab computer.


## Exercise 2: Managing content of an Azure SQL database by using SQL Server Management Studio

### Scenario

You created a test database. Now it is time to create a test table, populate it with sample data, and verify that data has been added by using SQL Server Management Studio.

The main tasks for this exercise are as follows:

1.	Add a table to an Azure SQL Database by using SQL Server Management Studio
2.	Add data to a table of a SQL database in Azure by using SQL Server Management Studio.
3.	Query a table of an Azure SQL database in Azure by using SQL Server Management Studio
4.	Prepare for the next module

### Task 1: Add a table to an Azure SQL Database by using SQL Server Management Studio

1.	On App Stream, start SQL Server Management Studio.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/20.png?st=2019-11-08T11%3A06%3A11Z&se=2022-11-09T11%3A06%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=m%2B%2BWSC2GMOIdM6tZVj6DU0C1sBrkSy2Gdy%2Byp5iKVlo%3D)

2.	From SQL Server Management Studio, connect to SQL Server in Azure by specifying the following information (replace **server_name** with the unique name you specified when creating your SQL Database server in the previous exercise):

 ```
 Server type: Database Engine

 Server name: server_name.database.windows.net

 Authentication: SQL Server Authentication

 Login: Student

 Password: Password@1234

 ```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/12.png?st=2019-08-26T10%3A14%3A34Z&se=2025-08-27T10%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IVRlge6yAK%2FvA4%2F6C%2FJKliVuM3ElFHGcZ3MvlF%2Bj9F8%3D)

3.	If the connection attempt fails indicating that the client IP address is not allowed to access the server, note the IP address in the error message. Switch to Chrome and, on the **Firewall settings blade**, create a new rule by specifying the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/13.png?st=2019-08-26T10%3A15%3A12Z&se=2025-08-27T10%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z0YSRuByWUBaCfLfskUiHRa0XXg%2FHb8YwW5Cui7J%2FVw%3D)

* RULE NAME: **allowLabVM**
* START IP: the IP address that you noted in the error message
* END IP: the IP address that you noted in the error message
  
**Note:** *Note that it might take up to five minutes for this change to take effect.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/14.png?st=2019-08-26T10%3A15%3A38Z&se=2025-08-27T10%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E%2BRDGAjRF5ic4uk4QdHVnBGu49tab75DG%2FzI7P%2FLpdI%3D)

4.	Create a new table in the **10979E0602-db** SQL database in Azure by running the following T-SQL command from SQL Server Management Studio, and then click **Execute.**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/21.png?st=2019-08-26T10%3A22%3A54Z&se=2025-08-27T10%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wsvH6tOiVxmo5tNdOIKr5CWXZB3k0Vi3kPK6l%2Bf8vHE%3D)

5.	In Object Explorer, expand the **10979E0602-db** node, expand the **Tables** folder and verify that **dbo.testTable** is listed (if not, refresh the Tables view).

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/15.png?st=2019-08-26T10%3A16%3A06Z&se=2025-08-27T10%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=J50sB%2FXPhkL4wvs71krRctbIFH36x1TH8L93g7R8x6A%3D)

6.	Leave the SQL Server Management Studio open for the next task

### Task 2: Add data to a table of a SQL database in Azure by using SQL Server Management Studio.

1.	Populate the content of the newly created table by running the following T-SQL command from SQL Server Management Studio, and then click **Execute:**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/19.png?st=2019-08-26T10%3A18%3A04Z&se=2025-08-27T10%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rg%2BvGIV2d1KiBTCCetwclbdsVmfX9RDGx2YNTj5JU7M%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/16.png?st=2019-08-26T10%3A16%3A33Z&se=2025-08-27T10%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FLmt%2FHlARWPqAGgnz6RMg70U%2BuweoNngs6vqt%2FziwKQ%3D)

2.	Leave the SQL Server Management Studio open for the next task.

### Task 3: Query a table of an Azure SQL database in Azure by using SQL Server Management Studio

1.	In Object Explorer, right-click **dbo.testTable**, in the context menu click **Script Table** as, click **SELECT To**, and then click **New Query Editor Window.** This generates a Transact-SQL query that retrieves data from the table.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/17.png?st=2019-08-26T10%3A24%3A20Z&se=2025-08-27T10%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wfVf3JN%2FILry9QdKSCkPJMAgX8Ca3KMYcLcDgrtuQSU%3D)

2.	Execute the newly created query.

3.	View the query results and verify that a table of **id** and **dataval** values is returned.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/lab8-Creating%20a%20SQL%20Database%20in%20Azure/18.png?st=2019-08-26T10%3A23%3A56Z&se=2025-08-27T10%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7Viteuq3dcGfxlAfcxJdhujrrMFd7tIBLE0LiwBcMZ8%3D)

**Result:** After you completed this exercise, you have created a test table in an Azure SQL Database instance, populated it with sample data, and queried its content.
