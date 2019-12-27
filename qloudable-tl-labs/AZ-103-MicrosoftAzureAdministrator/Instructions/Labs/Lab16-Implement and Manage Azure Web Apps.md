# Lab 16: Implement and Manage Azure Web Apps

## Table of content

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Implement Azure web apps](#exercise-1-implement-azure-web-apps)

[Exercise 2: Manage scalability and performance of Azure web apps](#exercise-2-manage-scalability-and-performance-of-azure-web-apps)


## Overview

The aim of this lab is about implementation, management, scalability and performance of Azure Web Apps.

### Scenario and objective

Xyz training labs Corporation wants to implement Azure web apps and configure them for scalability and performance.

After completing this lab, you will be able to:

*	Implement Azure web apps

*	Manage scalability and performance of Azure web apps

All tasks in this lab are performed from the Azure portal (including a PowerShell Cloud Shell session)

## Pre-Requisites

1.	Knowledge on Azure cloud shell

2.	Azure PowerShell Module with 1.2.0 version(if you are not using Azure cloud shell)

**Note:** When not using Cloud Shell, the lab virtual machine must have the Azure PowerShell 1.2.0 module (or newer) installed https://docs.microsoft.com/en-us/powershell/azure/install-az-ps

## Exercise 1: Implement Azure web apps

The main tasks for this exercise are as follows:

1.	Create an Azure web app
2.	Configure web app deployment settings.
3.	Create a staging deployment slot
4.	Deploy code to the staging deployment slot and perform slot swap

**Azure App Service**

Azure App Service enables you to build and host web apps, mobile back ends, and RESTful APIs in the programming language of your choice without managing infrastructure. It offers auto-scaling and high availability, supports both Windows and Linux, and enables automated deployments from GitHub, Azure DevOps, or any Git repo.

**Azure Web Apps**

A Web application (Web app) is an application program that is stored on a remote server and delivered over the Internet through a browser interface.

Azure Web Apps enables you to build and host web applications in the programming language of your choice without managing infrastructure. It offers auto-scaling and high availability, supports both Windows and Linux, and enables automated deployments from GitHub, Visual Studio Team Services, or any Git repo.

Web Apps not only adds the power of Microsoft Azure to your application, such as security, load balancing, auto scaling, and automated management. You can also take advantage of its DevOps capabilities, such as continuous deployment from VSTS, GitHub, Docker Hub, and other sources, package management, staging environments, custom domain, and SSL certificates.

**Auto-scaling**

Autoscaling is the process of dynamically allocating resources to match performance requirements. As the volume of work grows, an application may need additional resources to maintain the desired performance levels and satisfy service-level agreements (SLAs). As demand slackens and the additional resources are no longer needed, they can be de-allocated to minimize costs.

### Task 1: Create an Azure web app

1.	Using the Chrome browser, login into Azure portal with the below details.

 **Azure login_ID:** {{azure-login-id}} <br>
 **Azure login_Password:** {{azure-login-password}} 
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/1.png?st=2019-09-05T10%3A30%3A54Z&se=2021-09-06T10%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wqkoSsjnWGEMmARWgXaTiUgI8pAQV%2BsF7Q%2FL4XVBPMg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/2.png?st=2019-09-05T10%3A33%3A48Z&se=2021-09-06T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ayh3i1OYwooNh0Zux9AK4Lv2PBJGp2GJ%2FkCaKtACBcg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.png?st=2019-09-05T10%3A34%3A13Z&se=2021-09-06T10%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pxk3NjVqKDBaA%2BmQzzdkD84ew%2BwYo1WMFmeZrsONJKE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.1.png?st=2019-09-05T11%3A21%3A41Z&se=2021-09-06T11%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ujcp3ZNYYg4q%2BzC3hDB6M6OVvYDsus9wxpME1coauRw%3D)
 
2.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/4.png?st=2019-09-17T09%3A07%3A43Z&se=2021-09-18T09%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=iu%2FVjGsDzSGjLltj86IXPIzVWxpJtHBKgq7ytmxRa5o%3D)
 
3.	From the **Create a resource** blade, search Azure Marketplace for **Web app**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/5.png?st=2019-09-17T09%3A08%3A04Z&se=2021-09-18T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=E6eA1E2RvJ8n6NrR2q3JMW3NzgFM9nIwadiTk6PGA7g%3D)
 
4.	Use the list of search results to navigate to the **Web App Create** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/6.png?st=2019-09-17T09%3A08%3A24Z&se=2021-09-18T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eg0bN3r4zhl%2FrxGIJ46nIHULlTr4mbFKyymJtpJyxMY%3D)
 
5.	From the **Web App Create** blade, create a new web app with the following settings:

* **App name:** `any unique, valid name` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Subscription:** `Select the default` <br>
* **OS:** `Windows` <br>
* **Publish:** `Code` <br>
* **App Service plan/Location:** a new App Service plan with the following settings (For creating new appservice plan follow the below screens to choose the appservice plan) <br>
* **Name:** `az1010201-AppServicePlan1`
* **Location:** `{{location}}` <br>
* **Pricing tier:** `S1 Standard`


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/7.png?st=2019-09-17T09%3A08%3A44Z&se=2021-09-18T09%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nCsCazIn56CwhPP9qGdeX%2BXb7XXLSSzXTzYqO2aO6rA%3D)

**Note**:For creating new appservice plan follow the below screen shorts to create and choose the size/sku of the appservice plan.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/54.PNG?st=2019-09-18T05%3A05%3A55Z&se=2021-09-19T05%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2tuNri2aD9Viodtn7n5Yj%2FJdDGZwQJhPlCPCez9eAOY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/53.PNG?st=2019-09-18T05%3A05%3A21Z&se=2021-09-19T05%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nfE2mEWz0%2FZBUiDg6A1P8KrSCdX0Rn83bIQWZAe7ZhQ%3D)

``` 
Application Insights: Off

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/8.png?st=2019-09-17T09%3A09%3A01Z&se=2021-09-18T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2F8JyVMiJqgfSkYCMCO669w4UOWsXwgbTmIS4RwMk%2FRA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/9.png?st=2019-09-17T09%3A09%3A16Z&se=2021-09-18T09%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2Fpj2zTWtzLO7hcKY74E%2Fu3ME4pXncCcCyPFi4atoAqo%3D)
 
>   **Note:** The green check mark in the **App name** text box will indicate whether the name you typed in is valid and unique.

>   **Note:** To identify Azure regions where you can provision Azure web apps, refer to https://azure.microsoft.com/en-us/regions/offers/

>   **Note:** Wait until the web app is created before you proceed to the next task. This should take about a minute.

### Task 2: Create a staging deployment slot

1.	In the Azure portal, navigate to the blade of the newly provisioned web app.
2.	On the web app blade, use the **Browse** toolbar icon to open a new browser tab displaying the default App Service home page.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/10.png?st=2019-09-17T09%3A10%3A10Z&se=2021-09-18T09%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Sn45t9%2FSOn9s9LaJK8z4cwNlElAea1Jd7QmRmUbHx%2BU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/11.png?st=2019-09-17T09%3A10%3A29Z&se=2021-09-18T09%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9%2BMtce1gDooGQdLznc1RYZl1JPGywRrM%2BE%2Bbhzr2feU%3D)
 
3.	Close the browser tab displaying the default App Service home page.
4.	In the Azure portal, from the web app blade, display its **Deployment slots** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/12.png?st=2019-09-17T09%3A11%3A14Z&se=2021-09-18T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=C6UhFKs%2Fc8qi5ml1PQoYTyel9no4Jv%2B24Ctt%2B1rE6yc%3D)

5.	From the **Deployment slots** blade, add a slot with the following settings:

```
    Name: staging
    Configuration Source: Don't clone configuration from an existing slot
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/13.png?st=2019-09-17T09%3A11%3A34Z&se=2021-09-18T09%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mzo0%2FqSO1XXgPmcAFoaNNPckNtCETCxSyk4szTQJ1bM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/14.png?st=2019-09-17T09%3A12%3A15Z&se=2021-09-18T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sRUk1LQHi5PQNbVZU97M4Fxibci9TI4sM%2BcNoQN2VfU%3D)
 
6.	From the **Deployment slots** blade, navigate to the **staging** blade displaying the properties of the newly created deployment slot.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/15.png?st=2019-09-17T09%3A12%3A31Z&se=2021-09-18T09%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hKrXdonyQqmktvBQtbcSQFeNzdyExJjawb9a2f3NXzw%3D)
 
7.	On the **staging** blade, use the **Browse** toolbar icon to open a new browser tab displaying the default App Service home page.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/16.png?st=2019-09-17T09%3A13%3A22Z&se=2021-09-18T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DQrjEecdrsdo8zqSO%2BkxixKJ0gAPB57MvJOAWvq7zMA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/17.png?st=2019-09-17T09%3A13%3A42Z&se=2021-09-18T09%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dxVwYJgTRLpNnKcI6bMBnv9D%2Bdsk0vM1bV4JrXh16cw%3D)

8.	Close the browser tab displaying the default App Service home page in the staging deployment slot.


### Task 3: Configure web app deployment settings.

1.	In the Azure portal, from the **staging blade**, display the **staging - Deployment Center** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/18.png?st=2019-09-17T09%3A14%3A04Z&se=2021-09-18T09%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Y8qc1hUTQmGwi3aO0zirmRGyshC0yg6nsieAmkg%2Bk5o%3D)
 
2.	On the **staging - Deployment Center** blade, configure the following settings:

```
    Source control: Local Git
    Build provider: App Service Kudu build server
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/19.png?st=2019-09-17T09%3A14%3A48Z&se=2021-09-18T09%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bMv2Jz%2BnPe4i1C9SqVRny6ACtrT54GC1TlHYQVxciPA%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/20.png?st=2019-09-17T09%3A15%3A06Z&se=2021-09-18T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sAmhqX0oPp1h7IEj2sbBLL58yUOp%2BsPIWubtSsohsqU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/21.png?st=2019-09-17T09%3A15%3A23Z&se=2021-09-18T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Q4sEfIam%2FqQSmhcr8n2xSpFfvMW%2BI07fvwm4yUAK7RE%3D)
 
3.	Note the resulting **Git Clone Url**. You will need in the next task of this exercise.

4.	From the **Deployment Center** blade, use the **Deployment Credentials** toolbar icon to display **User Credentials** pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/22.png?st=2019-09-17T09%3A15%3A45Z&se=2021-09-18T09%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=xf8gEmMZeJ1rIBHMdHf1n%2BUpwjHD2%2FxW2FY7f06IXeg%3D)
 
5.	In the **User Credentials** pane, set the password to any valid, complex string and save the newly set credentials.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/23.png?st=2019-09-17T09%3A16%3A01Z&se=2021-09-18T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kRphPWuzpOGXyL006baBJetNORyFX8mwMHKznOYv5a8%3D)
 
### Task 4: Deploy code to the staging deployment slot and perform a slot swap

1.	From the Azure Portal, start a PowerShell session in the Cloud Shell pane.

**Note:** If this is the first time you are launching the Cloud Shell in the current Azure subscription, you will be asked to create an Azure file share to persist Cloud Shell files. If so, accept the defaults, which will result in creation of a storage account in an automatically generated resource group.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/24.png?st=2019-09-17T09%3A16%3A18Z&se=2021-09-18T09%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BchGgL%2FCVb1eQUBRRDnGIJkovuipewMYxuNmkFcFE%2FE%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/25.png?st=2019-09-17T09%3A19%3A27Z&se=2021-09-18T09%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=P5SZddk%2FBu5w4ls3KisKKz%2FJAvehvXChbh%2FQltBwHJQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/26.png?st=2019-09-17T09%3A20%3A00Z&se=2021-09-18T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=TJXNDeOlzhDVWwrJ9fclxCgyCH%2BiC%2Bodj3UP2QGepMY%3D)

2.	In the Cloud Shell pane, run the following command:

```
git clone https://github.com/Azure-Samples/php-docs-hello-world

```

>   **Note:** This command clones a remote repository containing a sample web app code

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/27.png?st=2019-09-17T09%3A20%3A20Z&se=2021-09-18T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=v22UHy57amSzKY9uZfDeNCxBRSUTT4AscpwNzuUrWYQ%3D)
 
3.	In the Cloud Shell pane, run the following command:

```
Set-Location -Path $HOME/php-docs-hello-world/

```

>   **Note:** This command sets the current location to the newly created clone of the local repository containing the sample web app code

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/28.png?st=2019-09-17T09%3A20%3A47Z&se=2021-09-18T09%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zv%2BURCE8d9sP0ReuVew6fJkWFBqVp4SJ4PdqX8R%2FcTI%3D)
 
4.	In the Cloud Shell pane, run the following command, replacing the <git_clone_url> placeholder with the value of the **Git Clone Url** you identified in the previous task:

```
git remote add azure <webapp local git url>

ex: git remote add azure "https://testappsuiqd-staging.scm.azurewebsites.net:443/testappsuiqd.git"

```

>   **Note:** This command connects the local repo to the Git repo in Azure repos associated with the Azure web app

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/29.png?st=2019-09-17T09%3A21%3A04Z&se=2021-09-18T09%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=o%2F21jfuH48bIExTDz7BIluVUrJZ4yGioAggzpfRx6xs%3D)
 
5.	In the Cloud Shell pane, run the following command:

```
git push azure master

```

6.	When prompted, type the password you set in the previous task.
7.	Close the Cloud Shell pane.

>   Note: This command pushes the sample web app code from the local repository to the Azure web app staging deployment slot

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/30.png?st=2019-09-17T09%3A24%3A03Z&se=2021-09-18T09%3A24%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ACj%2F0Be%2FqyAOzn%2BkkUns31n87trqXbacRCJcU8wXXiI%3D)

8.	In the Azure portal, navigate to the **Overview** section of the **staging** blade.
9.	On the **staging** blade, use the **Browse** toolbar icon to open a new browser tab. Note that the browser displays the **Hello World!** page you just deployed.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/31.png?st=2019-09-17T09%3A26%3A52Z&se=2021-09-18T09%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6Dw52sF242yjzvujOWHS34Z5UrZGtXXTap2e%2FDRuy1U%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/32.png?st=2019-09-17T09%3A27%3A09Z&se=2021-09-18T09%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sjr5%2FZA3%2FJ5UcDp96WRvlQ4cMiLQqsVBFm5zMLxO6T0%3D)
 
10.	Close the browser tab displaying the **Hello World!** page.
11.	On the **staging** blade, use the **Swap** toolbar icon to display the **Swap** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/33.png?st=2019-09-17T09%3A27%3A27Z&se=2021-09-18T09%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6c2F9%2BlpIJd1leCbXf6s7RLThty3YDCZfltVQOWMbf8%3D)
 
12.	On the Swap blade, initiate slot swap with the following settings:

```
    Swap type:  swap
    Source: staging
    Destination: production
    Preview Changes: review the changes that will be applied to the destination slot

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/34.png?st=2019-09-17T09%3A28%3A02Z&se=2021-09-18T09%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yegWuMV22Qa6n%2BeOU%2B3Z3tFqCfBst5zBtloQM%2Bn8DZ4%3D)
 
13.	On the **staging** blade, use the **Browse** toolbar icon to open a new browser tab. Note that the browser displays now the default App Service home page.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/35.png?st=2019-09-17T09%3A28%3A26Z&se=2021-09-18T09%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GbPb23m4y9aZzr2QeZqM6rYemHWuKKlj87UyAaUVoWU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/36.png?st=2019-09-17T09%3A28%3A43Z&se=2021-09-18T09%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=n4CuW1w2WdbBVN%2F6qHhaFnNfYjo4lWGxllkYWMgBrDI%3D)
 
 
14.	Close the browser tab displaying the default App Service home page.
15.	From the **staging** blade, display its **Deployment slots** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/37.png?st=2019-09-17T09%3A29%3A17Z&se=2021-09-18T09%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Mv%2FE7sOyr18al885dQ4Fd5FRY%2FyHgiMpx9FLVktsLNs%3D)
 
16.	From the **Deployment slots** blade, navigate back to the blade displaying the properties of the production slot of the Azure web app.

17.	On the web app blade, use the **Browse** toolbar icon to open a new browser tab. Note that the browser displays the **Hello World!** page.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/38.png?st=2019-09-17T09%3A29%3A39Z&se=2021-09-18T09%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DpX4wx7XCUzCZ4WyezOKSA2VM2Bib913Hb10U%2BLHoPE%3D)

 
18.	Close the browser tab displaying the **Hello World!** page.

**Result:** After you completed this exercise, you have created an Azure web app, configured web app deployment settings, created a staging deployment slot, deployed code to the staging deployment slot, and performed a slot swap.

## Exercise 2: Manage scalability and performance of Azure web apps

The main tasks for this exercise are as follows:

1.	Configure and test autoscaling of the Azure web app
2.	Configure Content Delivery Network (CDN) for the Azure web app

### Task 1: Configure and test autoscaling of the Azure web app

1.	In the Azure portal, from the web app blade, display the **Scale out (App Service plan)** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/39.png?st=2019-09-17T09%3A29%3A57Z&se=2021-09-18T09%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5IhBiagK2kNp2ykJrpoehZdgCQXXeEJU3eQCzF4OLKk%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/40.png?st=2019-09-17T09%3A32%3A53Z&se=2021-09-18T09%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=is2W0rME7r5syYhX4sf2GzW0Ku0qoHksjz0G2Dm6VDs%3D)

2.	On the web app **Scale out (App Service plan)** blade, enable autoscale with the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/41.png?st=2019-09-17T09%3A33%3A49Z&se=2021-09-18T09%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MGmxLu7osCpbUYgQ6RXvVsmbtYWCJ97BL27XnIcNsOY%3D)

* **Autoscale setting name:** `az1010201-AutoScaling` <br>
* **Resource group Name:** `{{resource-group-name}}` 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/42.png?st=2019-09-17T09%3A35%3A41Z&se=2021-09-18T09%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ksoICa5N8gKV7BY8gQPw9oGxImijALMx5rfVd0Qvvxo%3D)   

```
    Default Auto created scale condition:

    	Scale mode: Scale based on a metric
    	Rules: Scale out
        When:
        	Time aggregation: Average
        	Metric name: Data In
            Time grain statistics: Average
	        Operator: Greater than
        	Threshold: 1048576 bytes
        	Duration: 5 minutes
        	Cool down (minutes): 5
    	Instance limits (Minimum): 1
        Instance limits (Maximum): 2
        Instance limits (Default): 1
```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/43.png?st=2019-09-17T09%3A36%3A01Z&se=2021-09-18T09%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=kT0NoHI3llstQzDrsgQVg2UBUS1%2B7V1ghlbttBhWrok%3D)

Now click on **+Addrule** to create another Scale condition with the following settings as shown like above.

```
	Auto created scale condition 1:

       Scale mode: Scale based on a metric
       Rules: Scale in
    	When:
            Time aggregation: Average
        	Metric name: Data In
        	Time grain statistics: Average
            Operator: Greater than
            Threshold: 1048576 bytes
        	Duration: 5 minutes
        	Cool down (minutes): 5

```

Add below conditions to the newly created Rule and click **+Save**.

``` 
    	Instance limits (Minimum): 1
    	Instance limits (Maximum): 1
    	Instance limits (Default): 1
    	Schedule: Repeat specific days
    	Repeat every: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
    	Timezone: (UTC-5:00) Eastern Time (US & Canada)
    	Start time: 00:00
    	End time: 23:59

```

 ![alt text](![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/44.png?st=2019-09-17T09%3A37%3A17Z&se=2021-09-18T09%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YNss%2FkMvpr2qPW58kQbXtcjCWC6LaPth8RhevcChOow%3D))


3. From the Azure Portal, start a PowerShell session in the Cloud Shell.
4. In the Cloud Shell pane, run the following commands:

```
$resourceGroup = Get-AzResourceGroup -Name '{{resource-group-name}}'

$webapp = Get-AzWebApp -ResourceGroupName $resourceGroup.ResourceGroupName

while ($true) { Invoke-WebRequest -Uri $webapp.DefaultHostName }

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/45.png?st=2019-09-17T09%3A38%3A37Z&se=2021-09-18T09%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=2X6fQ7InfZclPOS18tCPnkEaCSJfWj8vriVfL6XnZic%3D)

 
>  **Note:** These commands submit requests to the Azure web app in a loop in order to trigger autoscaling

5. Minimize the Cloud Shell pane and, from the web app blade, display the **Process explorer** blade. This will allow you to monitor the number of instances and their resource utilization.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/46.png?st=2019-09-17T09%3A40%3A50Z&se=2021-09-18T09%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=pB8E7sYJEnzUnDjALBDUknOCeqqCBePkcNAqZU1bt3o%3D)
 
6. Once you notice that the number of instances has increased to 2, reopen the Cloud Shell pane and terminate the PowerShell script by pressing **Ctrl+C.**

**Note:** It might take about 5 minutes for the number of instances to increase to 2

### Task 2: Configure Content Delivery Network (CDN) for the Azure web app

1. In the Azure portal, navigate to the **Create a resource** blade.

2. From the **Create a resource** blade, search Azure Marketplace for **CDN**.
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/47.png?st=2019-09-17T09%3A41%3A22Z&se=2021-09-18T09%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dOpoKDhFlG30njWi7D0cYh4wHakqzCrDBVV7W690PEg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/48.png?st=2019-09-17T09%3A41%3A38Z&se=2021-09-18T09%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=WcF3%2FiICj3JMMXpKWGIZwjxzLTzHrEBSKVuToX6dvnI%3D)

3. Use the list of search results to navigate to the **CDN profiile** blade.

4. From the **CDN profile** blade, create a CDN profile with the following settings:

* **App name:** `az1010202cdn-profile` <br>
* **Subscription:** `Select the default` <br>
* **Resource group Name:** `{{resource-group-name}}` <br>
* **Location:** `{{location}}` <br>
* **Pricing tier:** `Standard Microsoft` <br>
* **Create a new CDN endpoint now:** `enabled` <br>
* **CDN endpoint name:** any unique, valid name consisting of letters and digits <br>
* **Origin type:** `Web App` <br>
* **Origin hostname:** the fully qualified name of the web app you created in the first exercise <br>


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/49.png?st=2019-09-17T09%3A41%3A57Z&se=2021-09-18T09%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=d90CGwP5NsHl%2FoK8qhXeU6DyXxLMmJ%2FztkdJcftMchM%3D)
 
**Note:** The green check mark in the CDN endpoint name text box will indicate whether the name you typed in is valid and unique.

**Note:** Wait until the CDN endpoint is created before you proceed to the next task. This should take less than a minute.

5. In the Azure portal, navigate to the **az1010202cdn-profile** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/50.png?st=2019-09-17T09%3A42%3A13Z&se=2021-09-18T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QY5aIVBf%2B0EYvmmdrIeqwnSmMJ%2FwI6ubrGtUY0qNrIo%3D)
 
6. From the **az1010202cdn-profile** blade, note the list of endpoints and use it to navigate to the newly created endpoint.

7. From the endpoint blade, note the value of the **Endpoint hostname**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/51.png?st=2019-09-17T09%3A42%3A36Z&se=2021-09-18T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5SZMuWD4B5VyxSvviuIC%2FSsbifcK17TJ9OwewMnDjsQ%3D)
 
8. Open a new tab on the browser  and browse to the URL representing the **Endpoint hostname**. Note that the browser displays the **Hello World!** page you just deployed.

> **Note**: If the browser displays 404 error not found page then wait for 5 to 10 mins and stop and start the CDN profile endpoint.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab16%20-%20Implement%20and%20Manage%20Azure%20Web%20Apps/52.png?st=2019-09-17T09%3A42%3A52Z&se=2021-09-18T09%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=AlBXB2p1qbCM64aI5J4dU3tHRGZkPluI%2ByITOCd3VpM%3D)
 
**Result:** After you completed this exercise, you have configured and tested autoscaling of the Azure web app as well as configured Content Delivery Network (CDN) for the Azure web app.
