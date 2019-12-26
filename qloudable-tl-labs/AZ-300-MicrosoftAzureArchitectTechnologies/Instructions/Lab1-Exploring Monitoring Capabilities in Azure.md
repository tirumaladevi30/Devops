# Lab 1: Exploring Monitoring Capabilities in Azure

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites) 

[Exercise 1: Deploy Azure VM scale sets](#exercise-1-deploy-azure-vm-scale-sets)

[Exercise 2: Implementing monitoring and alerting by using Azure Monitor](#exercise-2-implementing-monitoring-and-alerting-by-using-azure-monitor)

## Overview

The aim of this lab is about Managing Azure Subscriptions, Resources and Exploring Monitoring capabilities in Azure.

### Scenario and Objectives

XYZ Training Labs Corporation wants to explore monitoring capabilities in Azure.

After completing this lab, you will be able to:

* Deploy Azure VM scale sets

* Implement monitoring and alerting by using Azure Monitor

## Pre-requisites

* Familiarity with Azure portal 

* Azure Power shell 

* Azure CLI 

* ARM Template

***Note:*** *Azure Cloud Shell is a part of Azure Portal.*

***Note:*** *ARM Template is provided as a part of this lab*.

## Exercise 1: Deploy Azure VM scale sets

The main tasks for this exercise are as follows:

1. Deploy an Azure VM scale set by using an Azure QuickStart template

2. Review autoscaling settings of the Azure VM scale set

### Task 1: Deploy an Azure VM scale set by using an Azure QuickStart template

1. Using the Chrome browser, login to Azure Portal with the below details:

**Azure login_ID:** {{azure-login-id}} <br>

**Azure login_Password:** {{azure-login-password}}<br>

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/portal1.png?st=2019-08-27T10%3A39%3A53Z&se=2022-08-28T10%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=R2HBA53jbkSmAa%2BAH3U2sZhK%2Fn38%2Fu7zoE%2BTukbA97E%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/portal2.png?st=2019-08-27T10%3A40%3A09Z&se=2022-08-28T10%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JRIqS1LNSiLzlVhjfsRtmTr9vzJPguIgR6xLLmH307w%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/portal3.png?st=2019-08-27T10%3A40%3A24Z&se=2022-08-28T10%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PyjFzxvrSXrQo94D2zJ9tSpbZn33MoNbp%2BwixLUVBP4%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/portal4.png?st=2019-08-27T10%3A40%3A40Z&se=2022-08-28T08%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4wR%2FgFkgg59%2FF2g1k8zCLk52fxhKm%2FJQO4JsTw2ML2A%3D)

2. From Azure Portal, click on Cloud Shell icon and start a **PowerShell** session within the Cloud Shell.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/1.png?st=2019-08-27T10%3A41%3A05Z&se=2022-08-28T10%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PAOklgl%2BtiQCmFeARXIT5ymWdtey7fkqrxhi2zn5k6w%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/2.png?st=2019-08-27T10%3A41%3A21Z&se=2022-08-28T10%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DD2MYxv246ij4mi9aaLSMMq%2FY6PRk1ferlzChrZ4tYU%3D)

3. If you are presented with the **You have no storage mounted** message, click **Show Advanced Settings** and then configure storage using the following settings:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/3new.png?st=2019-08-27T10%3A41%3A47Z&se=2022-08-28T10%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=HmuXvbAwLKUUDfXZn0vKtsoo3ermpNIN6zDsJmHzo8A%3D)


**Subsciption**: Select as default from the dropdown

**Cloud Shell region**: {{location}} <br>

Note: If the above specified location is not available in drop-down then select another location from drop-down.

**Resource group**: {{resource-group-name}} <br>

**Storage account**: A name of a new storage account (between 3 and 24 characters consisting of lower case letters and digits)

**File share**: A name of a new file share


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/4new.png?st=2019-08-27T10%3A42%3A08Z&se=2022-08-28T10%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=hX71yKM4TGGIB1gYmQLl3ax%2FwrGaiyxEZRPq2O%2B%2FXLY%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/5new.png?st=2019-08-27T10%3A42%3A24Z&se=2022-08-28T10%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=yr6TwOSgilCrStLufj9eL1gaE%2FV35PihFvClTshXHkA%3D)

4. From the Cloud Shell pane, run the following command to identify a unique DNS domain name (substitute the placeholder `<custom-label>` with any alphanumeric string starting with a letter and no longer than 9 characters, which is likely to be unique and the placeholder `<location>` with the name of the Azure region into which you intend to deploy resources in this lab):

pwsh

Test-AzDnsAvailability -DomainNameLabel <custom-label> -Location '{{location}} <br>'


5. Verify that the command returned **True**. If not, rerun the same command with a different value of the `<custom-label>` until the command returns **True**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/6.png?st=2019-08-27T10%3A42%3A42Z&se=2022-08-28T10%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=sSeGnVksgFDPKSTmyRyYdDLW9T2FV%2F1%2FLmxpdrb9AAY%3D)

6. Note the value of the `<custom-label>` that resulted in the successful outcome. You will need it in the next task.

**Ex:** az300dns

7. In the new Chrome tab, browse to [**https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale**](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale).

8. Click **Deploy to Azure** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/7.png?st=2019-08-27T10%3A43%3A02Z&se=2022-08-28T10%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=JGKlLgOT7599m7xFI4bxEElCgmSm3oQ3Qbzon%2F6pea8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/7.5.png?st=2019-08-27T10%3A43%3A18Z&se=2022-08-28T10%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MmuOmjWiBp3Zgt9lU73IPpBU8WqIHwjkn9Tt%2BRhX1fc%3D)


9. In the Azure Portal, on the **Deploy VM Scale Set with Python Bottle server & AutoScale** blade, specify the following settings and initiate the deployment:


**Subscription**: select the default from the dropdown

**Resource group**: {{resource-group-name}} <br>

**Location**: {{location}} <br>

**Vm Sku**: Standard_DS1_v2

**Vmss Name**: the custom label you identified when running `Test-AzDnsAvailability` earlier in this task

**Instance count**: 1

**Admin Username**: adminuser

**Admin Password**: Password@1234


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/8new.png?st=2019-08-27T10%3A43%3A41Z&se=2022-08-28T10%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ElePEKT0yG8I0UeS%2F99pLdLp%2B02RisMeratqkdCQdkw%3D)

10. Place a checkmark next to **I agree to the terms and conditions stated above**, and then click **Purchase**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/9new.png?st=2019-08-27T10%3A43%3A56Z&se=2022-08-28T10%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=mztau12k7ghaEzdRRdPBm7pCWlNBa2%2FqxFKC0wb985k%3D)

11. Wait for the deployment to complete. This will take about 5 minutes.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/10new.png?st=2019-08-27T10%3A44%3A17Z&se=2022-08-28T10%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VayxN47xiCF8aAtg5SLI3h5QSVYELjHXLOGF7YWxVCY%3D)

### Task 2: Review autoscaling settings of the Azure VM scale set

1. In Azure Portal, navigate to the blade representing the newly deployed **Azure VM scale set**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/11new.png?st=2019-08-27T10%3A44%3A37Z&se=2022-08-28T10%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RafODGtWWxxWITOS0oXNMuiANEurSMVUYE%2BRWfm0lQE%3D)

2. From the VM scale set blade, navigate to the its **Scaling** blade.

3. Note that the Azure VM scale set is configured to scale dynamically based on a metric using the following criteria:

```
Scale out: increase instance count by 1 when average percentage of CPU > 60

Scale in: decrease instance count by 1 when average percentage of CPU < 30

Minimum number of instances: 1

Maximum number of instances: 10

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/12.png?st=2019-08-27T10%3A44%3A57Z&se=2022-08-28T10%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wJiUXGBqd8kNfOzuuS0KVKw1IZh2iHmICqD8qbx0vvQ%3D)

4. Modify the maximum number of instances to 3 and **save** your changes.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/13.png?st=2019-08-27T10%3A45%3A12Z&se=2022-08-28T10%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BW2%2B04hWFXNwKjLWniwF2pCNUF%2BE9mKzb%2FCGf3HmHwE%3D)

**Result**: After you completed this exercise, you have deployed an Azure VM scale set and reviewed its autoscaling settings.

## Exercise 2: Implementing monitoring and alerting by using Azure Monitor

The main tasks for this exercise are as follows:

1. Create Azure VM scale set metrics-based alerts

2. Configure Azure VM scale set autoscaling-based notifications

3. Test Azure VM scale set monitoring and alerting.

### Task 1: Create Azure VM scale set metrics-based alerts

1. Navigate to the blade representing Azure VM scale set and, from there, switch to the **Metrics** blade under **Monitoring**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/14.png?st=2019-08-27T10%3A45%3A32Z&se=2022-08-28T10%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Fu5k1vwuqB4fxtIvdYL7yPlYjL9ybvmaLxk6BL1w%2ByI%3D)

2. On the **Metrics** blade, use the filter to display **Percentage CPU** metric with an aggregation value of **Avg** of the VM scale set resource you provisioned in the previous exercise of this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/15.png?st=2019-08-27T10%3A45%3A48Z&se=2022-08-28T10%3A45%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dsi%2FRhhlzBiwg5916PoWL%2BXnOXTx0PixhvETqlM2vEM%3D)

3. Review the resulting chart and note the average percentage CPU within the last few minutes.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/16.png?st=2019-08-27T10%3A46%3A04Z&se=2022-08-28T10%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Do%2FE0L1i87oSE%2FH2NpIXGtspPQxuwQDLGH%2FJY1Qjw6g%3D)

4. Navigate to the **Alerts** blade in the **Monitoring** section.

5. From the **Alerts** blade, navigate to the **Manage actions** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/17.png?st=2019-08-27T10%3A46%3A19Z&se=2022-08-28T10%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=PaMuRRTi5Izog%2BKb%2FdVC1YB%2FY0DnMgd6aFUeejSkdo8%3D)

6. In the **Manage actions** section, click **Add action group**  

> Set the following values in the **Manage actions** section:


**action group name**: az30001 action group

**set short name**: az30001 

**subscription**: {{subscriptionId}} <br>

**resource group**: {{resource-group-name}} <br>

**action name**: az30001-email

**action type**: Email/SMS/Push/Voice


![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/18.png?st=2019-08-27T10%3A46%3A41Z&se=2022-08-28T10%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=8jgmu6UGqHiyYRxQSub8mQr2ld%2FdSCm4TDL%2B9%2FLSMOg%3D)

7. On the **Email/SMS/Push/Voice** blade, set an email address, a mobile phone number, or a phone number that you want to use to receive alerts generated by this rule and then click **OK**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/19.png?st=2019-08-27T10%3A46%3A55Z&se=2022-08-28T10%3A46%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GujItZ%2BWQ9iMEwqb6nUqSaxAeIQBd4rVyG34hAuxxTo%3D)

8. On the Add action group page, click **OK**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/20.png?st=2019-08-27T10%3A47%3A10Z&se=2022-08-28T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Nm4Qq0LIfGbtPwtv%2FMzwmaVDFkEuySgpeQLSNuwcyiY%3D)

9. Navigate to the **Alerts** blade.

10. From the **Alerts** blade, navigate to the **New alert rule** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/21new.png?st=2019-08-27T10%3A47%3A42Z&se=2022-08-28T10%3A47%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RucF%2B1f76Wp8l2qW4flLxILLVD5Zj9Cq5hx0ChM1VU4%3D)

11. In the **Resource** section, select the VM scale set you provisioned in the previous exercise of this lab.

12. In the **Condition** section, click **Add condition**, select the **Percentage CPU** metric, leave the dimension settings and condition type with their default values, set the condition to **Greater than**, set the time aggregation to **Average**, set the threshold to **60**, set the Aggregation granularity (period) to **1 minute**, set the frequency to **Every 1 minute** and click **done**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/22new.png?st=2019-08-27T10%3A48%3A05Z&se=2022-08-28T10%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5q1Lem1CniuEHLIjPIbon9ADfHkuPMBocNqXqN2vD3M%3D)

13. In the **Action** section, click **Select action group**, then select previously created action and click **done**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/25.1.png?st=2019-08-27T10%3A48%3A22Z&se=2022-08-28T10%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=5KOkRxzBUnzhS4%2FRC%2FEV4xs8HugEXA0H8WxLxMD4Kxw%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/25.2.png?st=2019-08-27T10%3A48%3A37Z&se=2022-08-28T10%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=I%2FeWnBgYMGZcu48%2FfbHlFzAYmX1q%2BasiKToWZVM1%2FRg%3D)

14. In the **Alert Details** section, set the alert rule name to **Percentage CPU of the VM scale set is greater than 60 percent**, its description to **Percentage CPU of the VM scale set is greater than 60 percent**, its severity to **Sev 3**, and set enable rule upon creation to **Yes**.

15. Click **Create alert rule**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/25.3.png?st=2019-08-27T10%3A48%3A53Z&se=2022-08-28T10%3A48%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=byzl81z8nPxsPpmnsWjCExDU4Fcd3Nt%2BjE8MJN0EZaY%3D)

   > **Note**: It can take up to 10 minutes for a metric alert rule to become active. 

### Task 2: Configure Azure VM scale set autoscaling-based notifications

1. Navigate to the blade representing Azure VM scale set and, from there, switch to the **Scaling** blade.

2. On the **Scaling** blade, click the **Notify** tab heading, configure the following settings, and **save** your changes:

```
Email administrators: enabled

Email co-administrators: disabled

Additional administrator emails(s): add an email address that you want to use to receive notifications about autoscaling events

```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/26.png?st=2019-08-27T10%3A49%3A11Z&se=2022-08-28T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=R1zTAzvNPwaqo5k3xK9ifmQdNe%2FWwVfI3sjb0XdW1bM%3D)

### Task 3: Test Azure VM scale set monitoring and alerting.

1. In the Azure portal, search for **Load balancers** and navigate to the Load Balancers blade. A load balancer should exist, representing the one created with the scale set you deployed from a template in a previous exercise of this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/27new.png?st=2019-08-27T10%3A49%3A29Z&se=2022-08-28T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Xk4xgobWFRxZXvBFebLsMW8KSyihWK2eAl8r41VKOLs%3D)

2. Identify the value of the **Public IP address** assigned to the front end of the load balancer associated with the VM scale set.

**Ex:** *40.76.197.89*

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/28.png?st=2019-08-27T10%3A49%3A46Z&se=2022-08-28T10%3A49%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XWTZtSSQ%2FlWsB1B0bjJDOmU12lXnl9l16iDzzIZ8UoE%3D)

3. From the lab computer, open new tab in Chrome and browse to **http://<Public IP address>:9000** (where **<Public IP address>** is the IP address you identified in the previous step)

**Ex:** *http://40.76.197.89:9000*

4. On the **Worker interface** page, click the **Start work** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/29.png?st=2019-08-27T10%3A50%3A02Z&se=2022-08-28T10%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vG0RUp%2B%2B%2Fg6UrxK%2B8dMtwaltGmZ6uqfWig%2BCGqeU72U%3D)

5. Use the **CPU (average)** chart on the VM scale set Overview blade to monitor changes to the CPU utilization.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/30.png?st=2019-08-27T10%3A50%3A18Z&se=2022-08-28T10%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GBGP2zilXIdFFFs41gkJX7ZLBM%2BnDn%2FXZZbv8LKWc2o%3D)

   > **Note**: Alternatively, you can navigate back to the **Metrics** blade and use the filter to display **Percentage CPU** metric of the VM scale set resource, and set the time to **Last 30 minutes**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/31.png?st=2019-08-27T10%3A50%3A34Z&se=2022-08-28T10%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=tz8kSqb633JV8l1QU9QBzExsLjfAvvlTWdGXcT31jPs%3D)

   > **Note**: You should receive an alert regarding increased CPU utilization within a couple of minutes

6. Switch to the **Instances** blade of the VM scale set in order to identify the number of its instances.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/32.png?st=2019-08-27T10%3A50%3A50Z&se=2022-08-28T10%3A50%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=NIoCgEEVXxxqQPoFSneGjHBC6S6kQ2KHMZWjwqdv8hY%3D)

   > **Note**: Alternatively, you can navigate back to the **Scaling** blade, in the list of resources capable of autoscaling, click the name of the VM scale set, on the **Autoscale settings** blade, click **Run history**, and then review the list of autoscale events.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/33.png?st=2019-08-27T10%3A51%3A11Z&se=2022-08-28T10%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XWF7KhIzpk5bzsEByTvng3XQPkgVvITGpJr7WnmSab4%3D)

   > **Note**: Autoscaling should be triggered within a couple of minutes.

7. Switch to the chrome browser displaying worker instances page and click the **Stop work** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az300/Lab1-Exploring%20Monitoring%20Capabilities%20in%20Azure/34.png?st=2019-08-27T10%3A51%3A27Z&se=2022-08-28T10%3A51%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0l878IGdhhX65Td4TzGBzXR9RsrwOLE9zhvE5gVkSOE%3D)

8. Monitor decrease in CPU utilization and scaling in events using the same methods that you used when scaling out the VM scale set.

**Result**: After you completed this exercise, you have implemented and tested monitoring and alerting by using Azure Monitor.
