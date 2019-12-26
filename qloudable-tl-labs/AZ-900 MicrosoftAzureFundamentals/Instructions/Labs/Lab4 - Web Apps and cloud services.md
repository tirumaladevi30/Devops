# Lab 4: Web Apps and Cloud Services

## Table of Contents 

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Creating and configuring a WordPress web app](#exercise-1-creating-and-configuring-a-wordpress-web-app)
 
## Overview

The main aim of this lab is to create and configure an Azure web app to support WordPress blogs.

### Scenario and Objectives

You were asked to deploy a web app for the XYZ Training Labs Corporation public relations team. You have decided to use the Web Apps feature of Azure App Service for this purpose.

After completing this lab, you will be able to:

*	Create and configure a web app.

## Pre-Requisites

* Azure Portal access

* Familiar with WebApp

* Familiar with Wordpress

**Note:** Azure Portal access is provided as part of the Lab environment

## Exercise 1: Creating and configuring a WordPress web app

**WordPress:** 

WordPress is a open source software, you can use to create a beautiful website or blog. It is the easiest and most flexible blogging and website content management system (CMS) based PHP and MySQL.

**Scenario**

You have decided to host this website on Azure. In this exercise, you will create a website to host WordPress blogs and then test the website by posting articles to the site.

The main tasks for this exercise are as follows:

1.	Create a web app

2.	Install WordPress

3.	Create a blog post

### Task 1: Create a web app

1.	From Virtual Machine, start Chrome, browse to http://portal.azure.com and, if prompted, sign in by using the Microsoft account that is the Service Administrator of your Azure subscription.

Using the Chrome browser, login into Azure portal with the below details.


**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal1.png?st=2019-08-22T11%3A08%3A20Z&se=2020-08-23T11%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=fm%2BDTeOkr2f0%2BS344uOTMlPzHxDsCisvhsf4Jo1LzmY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal2.png?st=2019-08-22T11%3A09%3A36Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ONwSsJE%2B5ENkff6wqI098VfdvzB77ezY7PxjamtqBgQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal3.png?st=2019-08-22T11%3A09%3A59Z&se=2020-08-23T11%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5JhMvyxOF4PJSrB3u4M9KLit%2B9IqG6MrVjUObzyLaGg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/portal4.png?st=2019-08-22T11%3A10%3A23Z&se=2020-08-23T11%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QKaTSjnXbhdQ1wkIajvEAwwAJvuUfoQn7NBkmBQa2C4%3D)

 
2.	From the Azure portal, create a new **WordPress** website based on the Azure Marketplace offering from **WordPress** with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/5.png?st=2019-08-22T11%3A12%3A28Z&se=2020-08-23T11%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZGLiSxHQTGnHOajuDP5LOvXsU3sxdxTPVxlkJSLD5lA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/6.png?st=2019-08-22T11%3A13%3A01Z&se=2020-08-23T11%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0u07I5H6th%2Bnp1Fmm1GRGij%2B6ftKcb0S3TGzpLnpXeA%3D) 

 
 **Resource Group:** {{resource-group-name}}
 

 ```

App name: AzureWeb-Test1

Subscription: Select the default

Database Provider: Azure Database for MySQL 

Note: From the drop ensure that Azure Database for MySQL is selected

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/10.png?st=2019-08-22T11%3A13%3A26Z&se=2020-08-23T11%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RQ99LEZSkh3x0H9CerXVM%2FGreWZwvz53H2QfXecEFPw%3D)

> Create a new App Service plan by selecting **App Service plan/Loction**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/11.png?st=2019-08-22T11%3A13%3A46Z&se=2020-08-23T11%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2FNJTnGTQfUenbi22utDszlxul6rPtuV%2FWAUEniOm4n0%3D)


**Location:** {{Location}}

```

App Service plan: 10979E0401-sp
 
Pricing tier: S1 Standard

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/12.png?st=2019-08-22T11%3A14%3A18Z&se=2020-08-23T11%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9g6A3z9qDFBEMAVC9gg%2BSdNKdiDFFW3hR%2FYI4xYsAzg%3D)

click **OK**

> Configure database settings by selecting **Database**

```

Database server name: accept the default value

Server admin login name: student

Password: Pa55w.rd1234

Confirm password: Pa55w.rd1234

Version: 5.7

Note: Don't make any changes to other settings, leave them as is.

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/dbsimage.PNG?st=2019-08-23T05%3A45%3A01Z&se=2020-08-24T05%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NnFuUY5S%2FbSHMJjocJ9rSeSkxSrbJWMv56kuWrqu3JQ%3D)


**MySQL Location:** {{Location}}


> Configure Application Insights settings by selecting Application Insights 

```

Application Insights: Disable

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/15.png?st=2019-08-22T11%3A15%3A25Z&se=2020-08-23T11%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eKY74nroFI3TgmgQZllvQhb8CPx%2B9f1Tfc%2BO6HOLCgU%3D)

> On**WordPress Create** window/pane, click on **Create** button

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/create.PNG?st=2019-08-22T11%3A15%3A48Z&se=2020-08-23T11%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JLrrCQDsXxkoUgv%2FzgczdAa2CVeHSmjAXSKSVkxCjsc%3D)
 
3.	Wait until the provisioning completes.

**Note**: *The provisioning might take a couple of minutes.*

### Task 2: Install WordPress

1.	Nagivate to newly created WordPress web app, as shown below:
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/16.png?st=2019-08-22T11%3A16%3A16Z&se=2020-08-23T11%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MXYz1a20nyMGqz8VKt4h4vIrWeiIaoRT9kBWWg2T7pg%3D)

Copy the WordPress webapp url and paste it in the chrome browser's new tab.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/17.png?st=2019-08-22T11%3A16%3A32Z&se=2020-08-23T11%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=3SbyQfjNqZAxZX0Ctkw0%2FPHZt0YplXuAw%2FOg6qBAb68%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/wordpress.PNG?st=2019-08-22T11%3A16%3A58Z&se=2020-08-23T11%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZZpMgXQePjC2sFhEsolySKfLzj8cwpbYP96mCDYDOB4%3D)

2.	On the WordPress website, set the language to **English (United States)**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/18.png?st=2019-08-22T11%3A17%3A20Z&se=2020-08-23T11%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kDth%2FxXYSssWGQjUSJXb%2BU6Xakwa%2FZN59svQRajhNdQ%3D)
 
3.	On the Welcome page, complete the **Information needed** section by specifying the following settings


**Site Title:** XYZ Training Blog

**Username:** {{azure-login-id}}

**Password:** Pa55w.rd0401

**Your E-mail:** {{azure-login-id}} 

Search Engine Visibility: Click on check box, as shown in the below image 


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/19.png?st=2019-08-23T04%3A35%3A30Z&se=2020-08-24T04%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9rZeBntikKwxzmtck43EB%2FsHEXNF52mJj4QGmCUfJd4%3D)
 
4.	Complete the installation of WordPress.

**Note**: *This might take a couple of minutes. If your connection to the web app times out, refresh the Chrome window.*

### Task 3: Create a blog post

1.	In Chrome, on the WordPress web app webpage, log in with the following credentials:

**Username:** {{azure-login-id}}

**Password:** Pa55w.rd0401

**Remember Me:** select the check box


**Note**: *If prompted by Chrome to store the password for the website, click No.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/login.PNG?st=2019-08-22T11%3A18%3A24Z&se=2020-08-23T11%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xXyNdSv1xw6sN9%2B2qKSj1r8dTBJleXCweHgxpK8vzeU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/login-ok.PNG?st=2019-08-22T11%3A18%3A45Z&se=2020-08-23T11%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ySCpw3oE88%2B4YLKizX8JZSzufoFn9PdzYicDhRhA3GM%3D)


2.	From the WordPress dashboard, create a new post with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/21.png?st=2019-08-22T11%3A19%3A08Z&se=2020-08-23T11%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=czMhQD%2BqK4QPVmJsqV3NMv%2By1fnVH1RG8DG%2FeJcTNZw%3D)
 
*	Title: **Welcome to the XYZ Training blog**

*	Main text: **Welcome to the XYZ Training blog**

3.	Publish the new post.
 
Copy the title content and paste it in the title box

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/22-1.png?st=2019-08-23T05%3A08%3A33Z&se=2020-08-24T05%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bewqEOokQMvU4PiBAX6ohcnvAnMzc2X14ysM4NJM9vI%3D)

 Copy the main text and paste it in the text editor as shown below.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/22-2.png?st=2019-08-23T05%3A09%3A07Z&se=2020-08-24T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dSuwOQToOKI0Mi1lLDnx730WGM%2BtDgHRyrrz%2BXKDesA%3D)

click on **publish** to publish the newly created post.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/22-3.png?st=2019-08-23T05%3A09%3A30Z&se=2020-08-24T05%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=aRD9yDbPwlYKXM1zw8lJzjEhrlQTz14gocsQNp7bazg%3D)

4.	View the new post.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/23.png?st=2019-08-23T05%3A10%3A17Z&se=2020-08-24T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5MTDGuvstk%2BBxariqznXAwvN1eHXcVzfEAWC33nJtEE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab4-Web%20Apps%20and%20cloud%20services/24.png?st=2019-08-23T05%3A10%3A39Z&se=2020-08-24T05%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9yU7WaGIfZ3QZNF%2B37DtPQRjPa5IOjadUkIIAbRVyv8%3D)
 
5.	Close Chrome.

**Result:** After completing this exercise, you should have successfully created and configured an Azure web app to support WordPress blogs.
