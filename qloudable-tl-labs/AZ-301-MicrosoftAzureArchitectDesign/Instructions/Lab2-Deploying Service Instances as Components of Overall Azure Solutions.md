# Lab 2: Deploying Service Instances as Components of Overall Azure Solutions

## Table of Contents 

[Overview](#overview)

[Pre-requisites](#pre-requisites)

[Exercise 1: Deploy Function App and Cognitive Service using ARM Template](#Exercise-1-deploy-function-app-and-cognitive-service-using-ARM-template)

[Exercise 2: Create a Logic App that uses a Function App](#Exercise-2-create-a-logic-app-that-uses-a-function-app)

## Overview

The aim of this lab is to deploy service instances as components of overall Azure solutions.

### Scenario & Objective

To Integrate SaaS Services Available on the Azure Platform 
 
After completing this lab, you will be able to:
  
*	Deploy a Function App and Cognitive Services using ARM Template.

*	Create a Logic App that uses a Function App.

*	Configure the Logic App.

## Pre-requisites

*	Visual Studio Code

*	Microsoft Azure Storage Explorer

*	Bash on Ubuntu on Windows

## Exercise 1: Deploy Function App and Cognitive Service using ARM Template

### Task 1: Connecting to the Azure portal

1. Using the Chrome browser, login into Azure portal with the below details.

```

Azure Username: {{ Azure Portal Username }}

Azure Password: {{ Azure Portal Password }}

```
    
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/1.png?st=2019-09-05T10%3A30%3A54Z&se=2021-09-06T10%3A30%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wqkoSsjnWGEMmARWgXaTiUgI8pAQV%2BsF7Q%2FL4XVBPMg%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/2.png?st=2019-09-05T10%3A33%3A48Z&se=2021-09-06T10%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ayh3i1OYwooNh0Zux9AK4Lv2PBJGp2GJ%2FkCaKtACBcg%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.png?st=2019-09-05T10%3A34%3A13Z&se=2021-09-06T10%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Pxk3NjVqKDBaA%2BmQzzdkD84ew%2BwYo1WMFmeZrsONJKE%3D) 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az103/Lab2-Implement%20VirtualMachines%20and%20ScaleSets/3.1.png?st=2019-09-05T11%3A21%3A41Z&se=2021-09-06T11%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ujcp3ZNYYg4q%2BzC3hDB6M6OVvYDsus9wxpME1coauRw%3D)

### Task 2: Deploy Cognitive Service using an Azure Resource Manager template

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Template Deployment** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/1.png?st=2019-09-19T07%3A02%3A39Z&se=2022-09-20T07%3A02%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=z8oUtf8mKkXjZc5dpVED0nv8%2BrvtOINYw9OgEIAX5ZQ%3D)

3. On the **Everything** blade, in the search results, click **Template Deployment (deploy using custom templates)**.

4. On the **Template deployment (deploy using custom templates)** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/2.png?st=2019-09-19T06%3A22%3A20Z&se=2022-09-20T06%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GMQZYSLIZmcIcUBR66X%2Fq8i4winiEGVCWPDej4D2%2Fk8%3D)

5. On the **Custom deployment** blade, click the **Build your own template in the editor** link.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/3.png?st=2019-09-19T06%3A21%3A34Z&se=2022-09-20T06%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=wE5YjdtyPb5YoysGNRH7ROiThOK2cxqOvQr2yb88ups%3D)

6. On the **Edit template** blade,

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/4.png?st=2019-09-19T06%3A23%3A12Z&se=2022-09-20T06%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=6Rya5EF4LH8V4xpWBE2Xwb14SMEskDqdqc8kNfTHDWc%3D)

To load the file **cognitive-template.json** into the azure portal copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

Now copy the Content in the URL and paste it in the **Edit template** blade.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_02/LabFiles/Starter/cognitive-template.json?st=2019-09-18T06%3A55%3A12Z&se=2021-09-19T06%3A55%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=gq4v1MkCUiFd5uPNj4PKWNqJzFpJrSuhJmtHi51AX%2BY%3D

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/5.png?st=2019-09-19T06%3A26%3A53Z&se=2022-09-20T06%3A26%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ZYp1qh5MXepFNIjtSH%2BAMVtqA1nkRyqs9S3VmYpbpYE%3D)

8. Click the **Save** button to persist the template.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/6.png?st=2019-09-19T06%3A27%3A25Z&se=2022-09-20T06%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OfavuH0EFxUYtxPNnF00QwktW3FU0DzWhxspIhcAphg%3D)

9. Back on the **Custom deployment** blade, perform the following tasks:

```
	Subscription:select the its default value.

	Resource group : {{ ResourceGroup }}

	Location : {{ Location }}

```

In the **Terms and Conditions** section, select the **I agree to the terms and conditions stated above** checkbox.

Click the **Purchase** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/7.png?st=2019-09-19T06%3A27%3A53Z&se=2022-09-20T06%3A27%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=W7bkcVwHBC9Ow87j1bMOAmvUJMtxisZuAlvxMZjEOAk%3D)

10. Wait for the deployment to complete before you proceed to the next step. 

11. In the hub menu of the Azure portal, click **Resource groups**.

12. On the **Resource groups** blade, click {{ resourceGroup }}.

13. On the {{ ResourceGroup }} blade, locate the **Deployments** header at the top of the blade and click the below the **Deployments** label, which indicates the number of successful deployments.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/8.png?st=2019-09-19T06%3A28%3A11Z&se=2022-09-20T06%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=9yT2az7aqZYSiasLNlYW%2FWztcCK%2Bqxx19kln9XuviG8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/9.png?st=2019-09-19T06%3A28%3A45Z&se=2022-09-20T06%3A28%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MagPLNPbefwqJpbP6KPQBC2BUfv%2F6Yrfg8Qvc2eH5LI%3D)

14. Click on the successful deployments.

15. Click **Microsoft.Template** and click **Outputs** on the deployment blade.

16. On the **Microsoft.Template - Outputs** blade, identify the values of **cognitiveEndpointUrl** and **cognitiveEndpointKey** outputs. Record these values, since you will need them later in the lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/10.png?st=2019-09-19T06%3A29%3A41Z&se=2022-09-20T06%3A29%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=snGYp7Uzxggmx1Apa0Nunzlbp5kc9MTDOyDLlucnpZs%3D)

### Task 3: Deploy a function app

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Function App** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/11.png?st=2019-09-19T07%3A03%3A10Z&se=2022-09-20T07%3A03%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=VyfYccXiQ1eturStd%2BqASWWvD7qvpAIG4RCRRzRgYCg%3D)

3. On the **Everything** blade, in the search results, click **Function App**.

4. On the **Function App** blade, click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/12.png?st=2019-09-19T06%3A31%3A10Z&se=2022-09-20T06%3A31%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Nn%2BYTi0F3h4SdJiHyoaSEdQpdsWigzQNgwarI49u3OA%3D)


5. On the next **Function App** blade, perform the following tasks:

```
	App name: Type a globally unique name.
    
	Subscription : set to its default value.

	Resource group : click use existing to select {{ ResourceGroup }}

	OS  : Windows

	Hosting Plan : Consumption Plan entry is selected.

	Location : {{ Location }}

	Runtime Stack : .NET Core

	Storage : ensure that the Create new option is selected and accept the default value of the Storage Account name. 

	Application Insights : set the option to Disabled.

```

Click the **Create** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/13.png?st=2019-09-19T06%3A32%3A31Z&se=2022-09-20T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=uEvsO2kVgnfgFCg%2BP2hIrBO2H9v6k5c7Mg3DMx3tBZs%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/14.png?st=2019-09-19T06%3A32%3A55Z&se=2022-09-20T06%3A32%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Ap26B%2FPRu1mEO1p%2FOqM0sKSdywtApKJycx6aQ62Z7DA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/15.png?st=2019-09-19T06%3A33%3A38Z&se=2022-09-20T06%3A33%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=GPoXDohFgx3WGNAAz677yIC2CPKN0qK4jzNKCmrsm3U%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/16.png?st=2019-09-19T06%3A34%3A00Z&se=2022-09-20T06%3A34%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=B5uCvs4i6rf0EWVLIZqI3P7a6zgfxFXxLlcZxWSO8WU%3D)


6. Wait for the provisioning of the function app to complete before you proceed to the next step. 

7. In the hub menu of the Azure portal, click **Resource groups**.

8. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/17.png?st=2019-09-19T06%3A35%3A27Z&se=2022-09-20T06%3A35%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ymYpqu%2BEjZWqZKmAs3LUtrFk8NQV1uMEvDcneMxdmO8%3D)

9. On the **{{ ResourceGroup }}** blade, in the list of resources, click the newly provisioned function app.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/18.png?st=2019-09-19T06%3A36%3A57Z&se=2022-09-20T06%3A36%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=RET9xZB2bENeIy%2FSaFq49qffVHOH1HFt8ql3cRKMXSY%3D)

10. On the function app blade, click the **Platform features** tab at the top of the blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/19.png?st=2019-09-19T06%3A37%3A35Z&se=2022-09-20T06%3A37%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=OmGYBtaL%2BoLgNTZL15VXd0ik76bHlnzkKXw2YvqtdxU%3D)

11. On the **Platform features** tab, click the **Configuration** link in the **General Settings** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/20.png?st=2019-09-19T06%3A38%3A03Z&se=2022-09-20T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Zoawsd2utYAMPOhK3DU8PysXvV8Fig7bpAB3BRk9jyw%3D)

12. On the **Application settings** tab, locate the **Application Settings** section. Click the **+ New application setting** link and perform the following tasks:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/21.png?st=2019-09-19T06%3A38%3A48Z&se=2022-09-20T06%3A38%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=vOO5HJb7p%2FDPFSwX%2Fo19YsSXD2FW5NYhJqzy4AN9l1s%3D)

```
	Name: Type the EndpointUrl

	Value :  enter the value of cognitiveEndpointUrl you identified earlier.

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/22.png?st=2019-09-19T06%3A39%3A14Z&se=2022-09-20T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=%2BcbJWY96%2FXfGswXz8FHk2YB6%2BSVuVxLypZCTG%2F%2FUIsc%3D)

13. In the **Application Settings** section, click the **Add new setting** link again and pferform the following tasks:

```
	Name : Type EndpointKey.

	value: Type the value of cognitiveEndpointKey you identified earlier.

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/23.png?st=2019-09-19T06%3A39%3A33Z&se=2022-09-20T06%3A39%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=enVF259sQpAhxdSi4d55teNABEqA1jkcXCU0Lzzee7s%3D)


14. Click the **Save** button at the top of the **Application settings** tab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/24.png?st=2019-09-19T06%3A40%3A15Z&se=2022-09-20T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=37wqJjKFVHIcR3OPVmpTPEgBt%2Fq8NKbYyTPlJss7fEc%3D)

15. Navigate back on the function app blade, click the **Platform features** tab at the top of the blade

16.	In the **Platform features tab**, click the **Deployment Center** link in the **Code Deployment** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/25.png?st=2019-09-19T06%3A40%3A54Z&se=2022-09-20T06%3A40%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=F33hOKehD7dozAg8ZpvZjWzst%2BZs%2BdG7lcb5evpze8s%3D)
   
17. On the **Deployment Center** blade that appears, scroll down and click the External button and then click Continue.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/26.png?st=2019-09-19T06%3A42%3A08Z&se=2022-09-20T06%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=EZa97lKCUhbWxOGM6c8KE%2FpCu6n0ceOmBHiPpYbr3Wo%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/27.png?st=2019-09-19T06%3A41%3A32Z&se=2022-09-20T06%3A41%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BvgIT1BYfpzIPaP70D3lxld%2FMb5NEWcAs%2FBlK19GY1A%3D)

18. Click App Service build service and click Continue.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/28.png?st=2019-09-19T06%3A42%3A39Z&se=2022-09-20T06%3A42%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KDtXSPeh8Kl9HoxKgmVJEOr%2FTHFx91h%2FmPtbr7PhFMY%3D)


19. Once the **Code** section is displayed, perform the following tasks

```
	Repository : https://github.com/azure-labs/cognitive-services-function.

	Branch : master.

```
    
> **Note**: The Branch field is case sensitive.

```
	Repository Type : Git
    
	Private Repository : No

```
Click the **Continue** button.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/29.png?st=2019-09-19T06%3A43%3A26Z&se=2022-09-20T06%3A43%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DWJdSdWn4d90aYhSz4zuHXaBZKZa%2BeS1zovsdKMY%2F%2Fg%3D)

20. Click **Finish** and wait for the deployment to complete before you proceed to the next task. 

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/30.png?st=2019-09-19T06%3A44%3A06Z&se=2022-09-20T06%3A44%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0zntFxMzdUAE8rgsaTWj1njblY5WHHHtoWkR5t8XZ5o%3D)

> **Note**: You will be able to determine that the first deployment has completed by monitoring the **Deployments** tab. This tab updates automatically.

### Task 4: Test a function app using Cognitive Services

1. Back on the function app blade, click **Functions** to expand the list of functions.

> **Note**: You may need to click **Functions** twice to refresh the list of functions.

2. Select the **DetermineLanguage** function from the list of functions.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/31.png?st=2019-09-19T06%3A57%3A16Z&se=2022-09-20T06%3A57%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=goL46JNaE0aHvZjIlyAKFD2A7KGP7xc7Db4nupYhuQA%3D)

3. In the **run.csx** pane that opens, click **Test** on the right side of the pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/32.png?st=2019-09-19T06%3A59%3A02Z&se=2022-09-20T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DnracNEDzK1UlWr2loUki4La5YshdKcg0z4wQTzrUpk%3D)

4. In the **Test** pane, perform the following tasks:

*	In the **Request body** text box, type the following:

```
    {
        "text": "I stuffed a shirt or two into my old carpet-bag, tucked it under my arm, and started for Cape Horn and the Pacific."
    }
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/33.png?st=2019-09-19T06%3A59%3A30Z&se=2022-09-20T06%3A59%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Wyrp9GlFdOUgNNlwI8QkwBmZOZB9b892K7wA%2FV9RvzE%3D)

*	Click the **Run** button.

*	Review the output in the **Output** section. The output should identify the language as **en** (English).

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/34.png?st=2019-09-19T07%3A00%3A12Z&se=2022-09-20T07%3A00%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=F82cqI%2BoSUyR6A4AI9fdTpyVRfN8%2FrAI1dmjPmDRXYI%3D)

> **Review**: In this exercise, you created a function app that uses Azure Cognitive Services.


## Exercise 2: Create a Logic App that uses a Function App

### Task 1: Create a logic app

1. In the upper left corner of the Azure portal, click **Create a resource**.

2. At the top of the **New** blade, in the **Search the Marketplace** text box, type **Logic App** and press **Enter**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/36.png?st=2019-09-19T07%3A04%3A20Z&se=2022-09-20T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=N%2Fb3A2zEz3fNIuGGeYU7VVyihKS%2BJKVjt7QAlCVSQJw%3D)

3. On the **Everything** blade, in the search results, click **Logic App**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/37.png?st=2019-09-19T07%3A04%3A41Z&se=2022-09-20T07%3A04%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DFuvHg9pC1uEdXSDIVRXklVC%2FJzEn7cl6zDoOmxp498%3D)

4. On the **Logic App** blade, click the **Create** button.

5. On the **Create logic app** blade, perform the following tasks:

```
	Name :  CognitiveWorkflow.
    
	Subscription : set to its default value.

	Resource group : {{ ResourceGroup }}.

	Location : {{ Location }} 

	Log Analytics : ensure that the Off button is selected.

	Click the Create button.

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/38.png?st=2019-09-19T07%3A05%3A13Z&se=2022-09-20T07%3A05%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=BZXk%2BLCNIJOdgxN1gZVdKuUcfHIcs1mHGS94NMqoYgU%3D)

6. Wait for the provisioning to complete before you proceed to the next task. 

### Task 2: Configure logic app steps

1. In the hub menu in the Azure portal, click **Resource groups**.

2. On the **Resource groups** blade, click **{{ ResourceGroup }}**.

3. On the **{{ ResourceGroup }}** blade, click the entry representing the logic app you created in the previous task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/39.png?st=2019-09-19T07%3A07%3A18Z&se=2022-09-20T07%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=l%2FUrtbmCNQF89dghS7d9cC%2FoV51TiyN6Iy55IEDDeAo%3D)

4. On the **Logic Apps Designer** blade, scroll down and click the **Blank Logic App** tile in the **Templates** section.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/40.png?st=2019-09-19T07%3A07%3A47Z&se=2022-09-20T07%3A07%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=IDBifsCHx7faIGIjVTPTcgcFgW2NUN0ljtAQJ%2BL5Xvs%3D)

5. On the **Logic Apps Designer** blade, click the **Code view** button at the top of the pane.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/41.png?st=2019-09-19T07%3A08%3A44Z&se=2022-09-20T07%3A08%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=4qg33QrtYalBTXy%2FFUiZO0KlmxCSYBBtIK%2BV9pt%2BZ6U%3D)

6. On the **Logic Apps Designer** blade, review the blank Logic App JSON template:

```
    {
        "definition": {
            "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
            "actions": {},
            "contentVersion": "1.0.0.0",
            "outputs": {},
            "parameters": {},
            "triggers": {}
        }
    }
```

7. Replace the default JSON template with the following template that includes an HTTP trigger 

To to that copy the below URL and paste it in the **Chrome Browser** and click **Enter**.

```
https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/allfiles/AZ-301T01/Module_02/LabFiles/Starter/logic-app.json?st=2019-09-18T06%3A58%3A03Z&se=2021-09-19T06%3A58%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QfHoLSiwTblBWlEcXfGh9E3v3bKV3BXRkFXxry4mSZk%3D

```

Now copy the Content in the URL and paste it in the **default JSON template** blade.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/42.png?st=2019-09-19T07%3A09%3A39Z&se=2022-09-20T07%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rmuXe4pdCtS%2Fp8XFIhA8IxwOOq6OxRQq4JaLIT5z%2BZA%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/43.png?st=2019-09-19T07%3A10%3A15Z&se=2022-09-20T07%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0d9xx1J%2Fu%2FHCGceddyU4zxSQ1UcEIPD5IVQFDpufzf4%3D)

8. On the **Logic Apps Designer** blade, click the **Designer** button.

> **Note**: At this point, you should see a single step in the designer. This is the "trigger" step that begins a workflow.

9. Click the **+ New Step** button in the designer.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/44.png?st=2019-09-19T07%3A10%3A54Z&se=2022-09-20T07%3A10%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=YAGEMiStsHqbBQsb0%2BE04S%2FNXuvcHOf%2FJmF4upY7g0A%3D)

10. In the **Choose an action** section, perform the following tasks:

*	In the search text box, type **Azure Functions**.

*	In the search results, select the action named **Choose an Azure function**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/45.png?st=2019-09-19T07%3A11%3A22Z&se=2022-09-20T07%3A11%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Gf9XvaNs2XsG4HuJUQm7fm5ahMMWrQxdO2Wor7GIHWk%3D)


*	In the next set of search results, select the Azure Function instance you created in the previous exercise of this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/46.png?st=2019-09-19T07%3A12%3A11Z&se=2022-09-20T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=ITEi1T2%2FVDiqTMwyaGbQWejrA9Z5scdF7yDQsN7jDH4%3D)

*	In the final set of search results, select the **DetermineLanguage** function that will be used for the action.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/47.png?st=2019-09-19T07%3A12%3A29Z&se=2022-09-20T07%3A12%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=214MaqQEHnleB%2FBdoIYaAGz%2Foh9pvtlk7P5PdHbfYc8%3D)

11. In the **DetermineLanguage** step, perform the following tasks:

*	Click the **Show advanced options** link to display all options.

*	In the **Request Body** text box, type **@triggerBody()**.

*	In the **Method** drop-down list, select the **POST** option.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/48.png?st=2019-09-19T07%3A13%3A08Z&se=2022-09-20T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=rZmppJv9TCP8YNck8YDH%2FlGb8vYyPhLGZrcf05AqB40%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/49.png?st=2019-09-19T07%3A13%3A25Z&se=2022-09-20T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=KcfCu%2FFLoG%2F5IbcatyaYurBfHlJ9MvxpxoaojbVOVyc%3D)

12. Click the **+ New Step** button in the designer. Click the **Add an action** button to open the dialog for creating an action.

13. In the **Choose an action** dialog that displays, perform the following tasks:

*	In the search text box, type **Azure Functions**.

*	In the search results, select the action named **Choose an Azure function**.
  
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/50.png?st=2019-09-19T07%3A13%3A57Z&se=2022-09-20T07%3A13%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=odxB%2FqwS7czVxKpq9YKSLD7ZfP7%2F2fMHFC6fMaFOHYA%3D)

*	In the next set of search results, select the Azure Function instance you created in the previous exercise of this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/51.png?st=2019-09-19T07%3A15%3A24Z&se=2022-09-20T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0BPj8ycks1kGXcgLMM9mA1%2FIDogUZ3qk0mTvINZIaB0%3D)

*	In the final set of search results, select the **DetermineKeyPhrases** function that will be used for the action.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/52.png?st=2019-09-19T07%3A15%3A52Z&se=2022-09-20T07%3A15%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=unEtBeMIU5c1HZPZVPWdSS6UxA16rgc8dvcIHeUhtyY%3D)

14. In the **DetermineKeyPhrases** step, perform the following tasks:

*	Click the **Show advanced options** link to display all options.

*	In the **Request Body** text box, enter the value **@body('DetermineLanguage')**.

*	In the **Method** drop-down list, select the **POST** option.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/53.png?st=2019-09-19T07%3A16%3A23Z&se=2022-09-20T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=jF1ka%2BvZxFJzI2mstnEEmajRnYNuUX9ButpKGtdLRO8%3D)

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/54.png?st=2019-09-19T07%3A16%3A48Z&se=2022-09-20T07%3A16%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=apveU7cfO3MXDtichQecb595gKq128nOxNdeHsDslL4%3D)

15. Click the **+ New Step** button in the designer. 

16. In the **Choose an action** dialog that displays, perform the following tasks:

*	In the search text box, type **Response**.

*	In the search results, select the **Action** named **Response Request**.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/55.png?st=2019-09-19T07%3A18%3A23Z&se=2022-09-20T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=DcAwNacpK26fLqbEH4qEYJGOCSwCz0HRf78iJ8Av7x4%3D)

    
17. In the **Response** step, perform the following tasks:

*	In the **Status Code** text box, ensure that the value **200** is specified.

*	In the **Body** text box, type **@body('DetermineKeyPhrases')**.

18. At the top of the **Logic Apps Designer** blade, click the **Save** button to persist your workflow.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/56.png?st=2019-09-19T07%3A18%3A49Z&se=2022-09-20T07%3A18%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=QZJwkByALBI1Ku9gqalVL9MppYqECDimXUy0vuThCVM%3D)

19. Scroll to the top of the **Logic Apps Designer** area and click the **When a HTTP request is received** step.

20. Copy the value of the **HTTP POST URL** text box. This URL will be used later in this lab.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/57.png?st=2019-09-19T07%3A19%3A08Z&se=2022-09-20T07%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=Te1BmnQd6eHNdA5sJXddwg%2BfBmWF2hkOnbeE%2BNtNehg%3D)

### Task 2: Open Cloud Shell

1. At the top of the portal, click the **Cloud Shell** icon to open a new shell instance.

> **Note**: The **Cloud Shell** icon is a symbol that is constructed of the combination of the *greater than* and *underscore* characters.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/58.png?st=2019-09-19T07%3A19%3A33Z&se=2022-09-20T07%3A19%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=0fobukwaRsfTM5Hjr53j15tzkyEIZpJsIjqqltqlzCY%3D)


2. If this is your first time opening the **Cloud Shell** using your subscription, you will see a wizard to configure **Cloud Shell** for first-time usage. When prompted, in the **Welcome to Azure Cloud Shell** pane, click **Bash (Linux)**.

> **Note**: If you do not see the configuration options for **Cloud Shell**, this is most likely because you are using an existing subscription with this course's labs. If so, proceed directly to the next task. 

3. In the **You have no storage mounted** pane, click **Show advanced settings**, perform the following tasks:

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/59.png?st=2019-09-19T07%3A20%3A14Z&se=2022-09-20T07%3A20%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=MCLtHtRTHC0LWZWRwJ7wLnCoYvU3hXCQ%2F267YAwMM7M%3D)

```
Subscription  : set to its default value.

Cloud Shell region : {{ Location }}

Resource group : {{ ResourceGroup }}

Storage account : ensure that the Create new option is selected and then, in the text box below, type a unique name consisting of a combination of between 3 and 24 characters and digits. 

File share : ensure that the **Create new** option is selected and then, in the text box below, type cloudshell.

Click the Create storage button.

```
![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/60.png?st=2019-09-19T07%3A21%3A02Z&se=2022-09-20T07%3A21%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=XZO%2F2UXsz2dH5Z4ktvzJOwwiYkRzxNTgO4yoMKtYQwI%3D)

4. Wait for the **Cloud Shell** to finish its first-time setup procedures before you proceed to the next task.

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/61.png?st=2019-09-19T07%3A22%3A05Z&se=2022-09-20T07%3A22%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=q8r7hVNwGRbZprmAIA3k5kog5Sy1FxEovhpj8FFI6cs%3D)


### Task 3: Validate Logic App using Python

1. At the **Cloud Shell** command prompt at the bottom of the portal, type the following command and press **Enter** to open the interactive **python** terminal:

```
    python
```

2. At the **Cloud Shell** command prompt at the bottom of the portal, type the following command and press **Enter** to import the **requests** library:

```
    import requests
```

3. At the **Cloud Shell** command prompt at the bottom of the portal, type the following command (replacing the placeholder `<logic app POST Url>` with the value of your url recorded earlier in this lab) and press **Enter** to create a variable containing the value of your logic app's url :

```
    url = "<logic app POST Url>"
```
   
4. At the **Cloud Shell** command prompt at the bottom of the portal, type the following command and press **Enter** to send an HTTP POST request to trigger your logic app workflow:

```
    response = requests.post(url, json={'text': 'Circumambulate the city of a dreamy Sabbath afternoon. Go from Corlears Hook to Coenties Slip, and from thence, by Whitehall, northward.'})
```

5. At the **Cloud Shell** command prompt at the bottom of the portal, type the following command and press **Enter** to display the output of the Logic App workflow:

```
    print(response.status_code, response.reason, response.text)
```

![alt text](https://qloudableassets.blob.core.windows.net/microsoft-learning/Az301/Images/Lab2%20-%20Deploying%20Service%20Instances%20as%20Components%20of%20Overall%20Azure%20Solutions/62.png?st=2019-09-19T07%3A23%3A10Z&se=2022-09-20T07%3A23%3A00Z&sp=rl&sv=2018-03-28&sr=b&sig=dpC5Aqjf2O2T1Xsf25XyeA%2BT6R04VZz%2BVUDD2LT72Sg%3D)
    
6.  Close the **Cloud Shell** pane.

> **Review**: In this exercise, you created a logic app that leverages the function app created in the previous exercise of this lab.

