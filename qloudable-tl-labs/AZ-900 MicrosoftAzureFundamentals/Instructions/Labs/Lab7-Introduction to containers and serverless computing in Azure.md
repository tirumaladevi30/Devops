# Lab 7: Introduction to containers on Azure using Docker

## Table of content

[Overview](#overview)

[Pre-Requisites](#pre-requisites)

[Exercise 1: Implementing Docker hosts on Azure VMs](#exercise-1-implementing-docker-hosts-on-azure-vms)

[Exercise 2: Deploying containers to Azure VMs](#exercise-2-deploying-containers-to-azure-vms)

[Exercise 3: Deploying multicontainer applications to Azure VMs with Docker Compose](#exercise-3-deploying-multicontainer-applications-to-azure-vms-with-docker-compose)

## Overview

The aim of this lab is to provision Docker Host on Azure using the ARM template and run the Docker containers on the deployed Docker Engine. Run the Docker Compose file on the Docker Engine.

### Scenario and Objectives

XYZ Training Labs Corporation plans to implement some of its applications as Docker containers on Azure VMs. To optimize this implementation, you intend to combine multiple containers by using Docker Compose.

XYZ Training Labs Corporation would also like to deploy its own private Docker registry in Azure to store containerized images. Your task is to test the functionality of tools that facilitate deployment of Docker hosts and Docker containers.

After completing this lab, students will be able to:

* Implement Docker hosts on Azure VMs.

* Deploy containers to Azure VMs.

* Deploy multicontainer applications with Docker Compose.

## Pre-Requisites

* Azure Cloud Shell

* ARM template

**Note:** 1. Azure Cloud Shell is a part of Azure Portal.

**Note:** 2. ARM Template is provided as a part of this lab.

## Exercise 1: Implementing Docker hosts on Azure VMs

**Scenario**

To test the planned deployment, you must identify the methods that would allow you to deploy Docker hosts to Azure VMs.

The main tasks for this exercise are as follows:

1. Connect to Azure Cloud Shell.

2. Create a new Azure VM running Docker.

3. Connect to an Azure VM running Docker

**Azure Cloud Shell**

Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work. Linux users can opt for a Bash experience, while Windows users can opt for PowerShell. 

**ARM template**

Azure Resource Manager is the deployment and management service for Azure. It provides a consistent management layer that enables you to create, update, and delete resources in your Azure subscription.

Azure Resource Manager (ARM) allows you to provision your applications using a declarative template. In a single template, you can deploy multiple services along with their dependencies. You can use the same template to repeatedly deploy your application during every stage of the application life cycle.

**Docker**

Docker is a Containerization platform which packages your application & all its dependencies together in the form of Containers, to ensure that your application works seamlessly in any environment be it Development/Test/Production.

**Docker Container**

A Docker container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and 
reliably from one computing environment to another.

**Docker Compose**

Docker compose is used to run multi-container application. Each container will run a stand-alone application and it can communicate with other containers present in the same host.

**Ex:** MEAN Stack Application [MongoDB, ExpressJS, Angular & NodeJS] using different containers.

### Task 1: Connect to Azure Cloud Shell.

1. Using the Chrome browser, login to Azure Portal with the below details:

**Azure login_ID:** {{azure-login-id}}

**Azure login_Password:** {{azure-login-password}}

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/portal1.png?st=2019-08-26T06%3A14%3A13Z&se=2022-08-27T06%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=cbuq12fZbgQRuE%2Bo3zt7dbQhKXNOr9SV8Xq60fshiQQ%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/portal2.png?st=2019-08-26T06%3A14%3A48Z&se=2022-08-27T06%3A14%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9KH%2FQbyyCfPFZE68%2BQY7BVjX4%2BPaSO9DqT1kVsaaoZ8%3D)
 
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/portal3.png?st=2019-08-26T06%3A15%3A07Z&se=2022-08-27T06%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=nTp1DIgr5LA6LsasBT4hZJmB1LPXTOpvP72hQQbqBSA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/portal4.png?st=2019-08-26T06%3A15%3A29Z&se=2022-08-27T06%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NPVqicWLLVxnpW3NtBA8F5vqgwLoWMaYiUKdlY0IqqE%3D)

2. From Azure Portal, click on Cloud Shell icon. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/3.png?st=2019-08-26T06%3A15%3A50Z&se=2022-08-27T06%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YAR6NInd9HfNlvs%2B4tyDdsGNuIF9MnkXn3foQ6Qo3hU%3D)

3. Start the **Bash shell** in Azure Cloud Shell.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/4.png?st=2019-08-26T06%3A16%3A09Z&se=2022-08-27T06%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vhZEoYulMChcttbIjWxo0NQG36msXZZPyZJlvesmbNE%3D)
 
4. If you are presented with you have **no storage mounted** message, configure storage using the following settings:

> Settings

**ResourceGroup:** {{resource-group-name}}

**Cloud Shell region:** {{Location}}

```
Subscription: Select as default from the dropdown

Cloud Shell region: {{ Location }}

Storage account: a name of a new storage account

File share: a name of a new file share
 
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/5.png?st=2019-08-26T06%3A16%3A30Z&se=2022-08-27T06%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pl1mwpQFBONUdSCE9onPyRIMiYf44537D0SgwW5YICs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/6.png?st=2019-08-26T06%3A16%3A46Z&se=2022-08-27T06%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=FEKO62CDeRI7xvHQR4RcYPggjAvI1ZVxins25E3RCgc%3D)

5. Wait for the deployment to complete.

*Note: The deployment might take a couple of minutes.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/7.png?st=2019-08-26T06%3A17%3A02Z&se=2022-08-27T06%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Z%2FDAclNF13M%2BJYVhBYYmNVCAUzQ7rl1uS42VKSq5J0s%3D)

### Task 2: Create a new Azure VM running Docker

1. In the new Chrome tab, browse to https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu. 

2. On the **Simple deployment of an Ubuntu VM with Docker page**, click on **Deploy to Azure** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/9.png?st=2019-08-26T06%3A17%3A34Z&se=2022-08-27T06%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MfauATrusWEdHsmhZMWgaw%2FaD4J1n6oc%2B6nx6IvWfuc%3D)
 
3. On the **Deploy an Ubuntu VM with Docker Engine** blade, specify the following settings and click **Purchase:**

**ResourceGroup:** {{resource-group-name}}

**Region:** {{Location}}

```
Subscription: select the default from the dropdown

Admin Username: adminuser

Dns Name for Public IP: any valid, unique name consisting of lowercase letters and digits EX: xyztraining

Vm Size: Standard_F1

Ubuntu OS Version: 16.04.0-LTS from the dropdown select the value

Authentication Type: password

Admin Password or Key: Password@1234

```
4. Click on **I agree to the terms and conditions stated above** and select **purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/10.png?st=2019-08-26T06%3A17%3A57Z&se=2022-08-27T06%3A17%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5XVcmCAYeGolrbDJMH2uFx31%2BJS5Xz8E%2Bd42q0HW4mU%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/11.png?st=2019-08-26T06%3A18%3A24Z&se=2022-08-27T06%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Whw9Fvq7L75k0XoMMVWlvETLkA4kzZCXWIHdd%2FJ48gs%3D)
  
5. Wait for the deployment to complete.

*Note: The deployment might take a couple of minutes.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/12.png?st=2019-08-26T06%3A18%3A45Z&se=2022-08-27T06%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=eupT3jShnHWYKA6yM5xKY%2Bmyy7Tbsu6kUcj5zma3IpY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/13.png?st=2019-08-26T06%3A19%3A04Z&se=2022-08-27T06%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=LnWj%2FIcr6ywDOmL7ej1WbWZ047zijh6qrK7fDLGjXlw%3D)

## Exercise 2: Deploying containers to Azure VMs

**Scenario**

After deploying the Docker host VM, you intend to verify that the Docker host is operational. To accomplish this, you want to run a sample containerized nginx web server, available from Docker Hub.

The main tasks for this exercise are as follows:

1. Connect to an Azure VM running Docker

2. Deploy a container to a Docker host running on an Azure VM

### Task 1: Connect to an Azure VM running Docker

1. In the Azure portal, in the Cloud Shell pane, identify the fully qualified domain name of the Azure VM you deployed in the previous exercise by using the **az vm show** command and storing the results in a variable named **$fqdn**
```
az vm show -g {{resource-group-name}} -n MyDockerVM -d
```
**EX: az vm show -g tl-stq-xxxxxxxxxxxxx -n MyDockerVM -d**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/14.png?st=2019-08-26T06%3A19%3A23Z&se=2022-08-27T06%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=1QikvKfiMeb2azjKSN1plh4eRmkycrkHqn8gOqIoW2c%3D)
 
2.	From the Cloud Shell pane, identify the fully qualified domain name via which you can access the Azure VM. 

*Note: Copy the **fqdns** from the above step and note it in Notepad.*

3.	From the Cloud Shell pane, establish an SSH session to the Azure VM as **adminuser** by using the fully qualified domain name you identified in the previous step.

4.	When prompted, authenticate by using the password **Password@1234**. You should be presented with the **adminuser@MyDockerVM** prompt.

```
ssh username@fqdns
```
**Ex: ssh adminuser@xyztraining.westus2.cloudapp.azure.com**

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/15.png?st=2019-08-26T06%3A19%3A41Z&se=2022-08-27T06%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=t%2F6qAQKK%2F7aRxiK0B53W5mZx1PyNO19MPAd1To27kGk%3D)
 
### Task 2: Deploy a container to a Docker host running on an Azure VM

1. Within the SSH session to the Linux Azure VM Docker host, within the Cloud Shell pane, use the **docker run** command to start an **nginx** container from the Docker Hub, making it available via TCP port 80.

```
docker run -itd --name docker-nginx -p 80:80 nginx

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/16.png?st=2019-08-26T06%3A19%3A59Z&se=2022-08-27T06%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=7uw9x3fXuSxGe5GhvS738hYsNsxVus1BpycLuOOf8Ww%3D)
 
2.	Monitor the progress of the container deployment. Verify the successful outcome, by running the **docker ps** command.

```
docker ps

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/17.png?st=2019-08-26T06%3A20%3A17Z&se=2022-08-27T06%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=utWS2cAQqv8sUOMrHTOD%2Bu0plSQHRx%2BlZcNkhp6EmW0%3D)
 
3.	Using Chrome browser new tab, browse to the fully qualified DNS name you obtained in the previous task. Verify that web page displays the **Welcome to nginx!**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/18.png?st=2019-08-26T06%3A20%3A38Z&se=2022-08-27T06%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=bwR7iXHC%2BSJS50Jaeo7ROw8JO3yQFzisiHs6%2FpMkp8Y%3D)
 
**Result:** Once you completed this exercise, you have successfully ran a sample containerized web server nginx on the Docker host Azure VM.

## Exercise 3: Deploying multicontainer applications to Azure VMs with Docker Compose

**Scenario**

You intend to implement wordpress application using multiple containers. To accomplish this, you will test the deployment of multicontainer images using Docker Compose.

The main tasks for this exercise are as follows:

1.	Create a compose file

2.	Deploy the containers on Docker Host using docker-compose

### Task 1: Create a compose file

1. In the Cloud Shell pane, within the SSH session to the Azure VM Docker host, create a new file named docker-compose.yml with the following content:

```yaml
version: "2"
services:
  wordpress:
    image: wordpress
    links:
       - db:mysql
    ports:
       - 8080:80
  db:
    image: mariadb
    environment:
        MYSQL_ROOT_PASSWORD: 'Pa55w.rd'
```

```
mkdir wordpress

cd wordpress

vi docker-compose.yml
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/19.png?st=2019-08-26T06%3A21%3A01Z&se=2022-08-27T06%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vfUgX0ZH%2BX7HdoG%2BRRjajMzpmWauZtjQuJWXiuNifxc%3D)
 
2.	After opening the **docker-compose.yml** file type **Esc and i** to insert the data into the file. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/20.png?st=2019-08-26T06%3A21%3A23Z&se=2022-08-27T06%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Daw6HEqExchcOiBP929rP3xRKD%2BVE9gYmz8f%2FD2jYp8%3D)
 
3.	After inserting the data into the file save and quit by going to **Esc mode** and typing **:wq** then Press **Enter.**

*Note: Be careful when typing the text above. Make sure you include the spaces to the left of the text (each indent should be a multiple of 2 spaces).*

4.	Save the file.

### Task 2: Deploy the containers on Docker Host using docker-compose

1. In the Cloud Shell pane, within the SSH session to the Azure VM Docker host, deploy containers defined in the **docker-compose.yml** file using the below command.

```
docker-compose up -d

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/21.png?st=2019-08-26T06%3A21%3A45Z&se=2022-08-27T06%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=CQC5I1dCF6dupi%2Fwqm9%2FnN3E%2B9KivzOYUqkrx9AiQhM%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/22.png?st=2019-08-26T06%3A22%3A06Z&se=2022-08-27T06%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KOoo2DwdBUfsSyVW6VSfuURoYU9CTTDcbQLnCcGzrMw%3D)
 
2. Monitor the progress of the container deployment. Use the **docker ps** command to verify the successful outcome.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/23.png?st=2019-08-26T06%3A22%3A31Z&se=2022-08-27T06%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yGBZht9xEXREFM28WKDDAHiWtJZ8zI8dR6AtbeF2pgo%3D)
 
3. Navigate to your Chrome browser and browse to the port 8080 on the target host via the same URL you used in the previous exercise. Verify that Chrome browser displays the initial Wordpress setup page.

*Note: This is possible because the template used to provision the deployment of the Linux Azure VM Docker host included a network security group with a rule that allows inbound traffic on TCP port 8080. If that was not the case, you would need to add this rule.*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/24.png?st=2019-08-26T06%3A32%3A05Z&se=2022-08-27T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KHUGZg%2FherZB7JmlMx2yINqq9hZ6fF%2BtBWxjZI6AF8c%3D)
  
4.	Exit the SSH session and close the Cloud Shell pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az900/Lab7-Introduction%20to%20containers%20and%20serverless%20computing%20in%20Azure/25.png?st=2019-08-26T06%3A41%3A51Z&se=2022-08-27T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=zdD80xFvwb7ptnlsoXK0szaeaeXv%2B8AT%2BmmmI3oIT3s%3D)
  
**Result:** Once you completed this exercise, you have successfully implemented a multi-container application by using Docker Compose.
