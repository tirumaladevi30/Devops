# Lab 10: Azure AD Identity Protection

## Table of Contents

[Overview](#overview)

[Pre-requisites](#pre-requisites) 

[Exercise 1: Prepare the lab environment](#exercise-1-prepare-the-lab-environment)

[Exercise 2: Implement Azure MFA](#exercise-2-implement-azure-mfa)

[Exercise 3: Implement Azure AD Identity Protection](#exercise-3-implement-azure-ad-identity-protection)

[Exercise 4: Remove lab resources](#exercise-3-remove-lab-resources)

## Overview:

The aim of this lab is to Create a new Azure AD tenant, Create Azure AD users and groups. In this lab we are Assign Azure AD Premium v2 licenses to Azure AD users. We are configure azure MFA(Multi Factor Authentication) settings and Validate MFA configuration.
After you completed this lab, you have enabled Azure AD Identity Protection, configured user risk policy and sign-in risk policy, as well as validated Azure AD Identity Protection configuration by simulating risk events.

### Scenario and Objective

**XYZ Training Corporation** wants to take advantage of Azure AD Premium features for Identity Protection.

After completing this lab, you will be able to:
*	Deploy an Azure VM by using an Azure Resource Manager template
*	Implement Azure MFA (Multi Factor Authentication)
*	Implement Azure AD Identity Protection

## Pre-requisites:

1.	Familiarity Azure portal 

2.	Familiarity with Remote Desktop Connection

3.	Familiarity ARM Templates

4.	Familiarity Azure virtual machine
Lab files:
*	https://github.com/sysgain/qloudable-tl-labs/blob/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Allfiles/Labfiles/Module_10/Azure_AD_Identity_Protection/az-101-04b_azuredeploy.json
*	https://github.com/sysgain/qloudable-tl-labs/blob/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Allfiles/Labfiles/Module_10/Azure_AD_Identity_Protection/az-101-04b_azuredeploy.parameters.json

## Exercise 1: Prepare the lab environment

The main tasks for this exercise are as follows:
1.	Deploy an Azure VM by using an Azure Resource Manager template

### Task 1: Deploy an Azure VM by using an Azure Resource Manager template

1.	From the lab virtual machine, start Microsoft Edge, browse to the Azure portal at **http://portal.azure.com** and sign in by using a Microsoft account that has the Owner role in the Azure subscription you intend to use in this lab.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-1.png) 

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-2.png) 

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-3.png) 

2.	In the Azure portal, navigate to the **Create a resource** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-4.png) 
 
3.	From the **Create a resource** blade, search Azure Marketplace for **Template deployment**, then select **Template deployment (deploy using customer templates)**.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-5.png) 
 
4.	Click Create.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-6.png) 
 
5.	On the **Custom deployment** blade, click the **Build your own template in the editor** link. If you do not see this link, click **Edit template** instead.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-7.png) 

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-8.png) 

6.	From the **Edit template** blade, load the template file **az-101-04b_azuredeploy.json**.

> **Note**: Review the content of the template and note that it defines deployment of an Azure VM hosting Windows Server 2016 Datacenter.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-9.png) 
 
7.	Save the template and return to the **Custom deployment** blade.

8.	From the **Custom deployment** blade, navigate to the **Edit parameters** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-10.png) 
 
9.	From the **Edit parameters** blade, load the parameters file **az-101-04b_azuredeploy.parameters.json**.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-11.png) 

10.	Save the parameters and return to the **Custom deployment** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-12.png) 
 
11.	From the **Custom deployment** blade, initiate a template deployment with the following settings:

	- Subscription: the name of the subscription you are using in this lab

	- Resource group: the name of a new resource group **az1010401b-RG**

	- Location: the name of the Azure region which is closest to the lab location and where you can provision Azure VMs

	- Vm Size: **Standard_DS1_v2**

	- Vm Name: **az1010401b-vm1**

	- Admin Username: **Student**

    - Admin Password: **Password@1234**

	- Virtual Network Name: **az1010401b-vnet1**

> **Note**: To identify Azure regions where you can provision Azure VMs, refer to **https://azure.microsoft.com/en-us/regions/offers/**

> **Note**: Do not wait for the deployment to complete but proceed to the next exercise. You will use the virtual machine included in this deployment in the last exercise of this lab.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-13.png) 

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-14.png) 
 
**Result**: After you completed this exercise, you have initiated a template deployment of an Azure VM az1010401b-vm1that you will use in the next exercise of this lab.

## Exercise 2: Implement Azure MFA

The main tasks for this exercise are as follows:

1.	Create a new Azure AD tenant
2.	Activate Azure AD Premium v2 trial
3.	Create Azure AD users and groups
4.	Assign Azure AD Premium v2 licenses to Azure AD users
5.	Configure Azure MFA settings, including fraud alert, trusted IPs, and app passwords
6.	Validate MFA configuration

### Task 1: Create a new Azure AD tenant

1.	In the Azure portal, navigate to the **New** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-15.png) 

2.	From the **New** blade, search Azure Marketplace for **Azure Active Directory**.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-16.png) 

3.	Use the list of search results to navigate to the **Create directory** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-17.png) 
 
4.	From the **Create directory** blade, create a new Azure AD tenant with the following settings:

*	Organization name: **AdatumLab101-4b**

*	Initial domain name: a unique name consisting of a combination of letters and digits.

*	Country or region: **United States**

> **Note**: Take a note of the initial domain name. You will need it later in this lab.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-18.png) 

### Task 2: Activate Azure AD Premium v2 trial

1.	In the Azure portal, set the **Directory + subscription** filter to the newly created Azure AD tenant.

> **Note**: The Directory + subscription filter appears to the right of the Cloud Shell icon in the toolbar of the Azure portal

> **Note**: You might need to refresh the browser window if the AdatumLab101-4b entry does not appear in the Directory + subscription filter list.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-19.png) 
 
2.	In the Azure portal, navigate to the **AdatumLab101-4b - Overview** blade by click on it.

3.	From the **AdatumLab101-4b - Overview** blade, navigate to the **Licenses - Overview** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-20.png) 
 
4.	From the **Licenses - Overview** blade, navigate to the **Licenses - All products** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-21.png) 

5.	From the **Licenses - All products** blade, navigate to the Activate blade and activate **Azure AD Premium P2** free trial.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-22.png) 
 
### Task 3: Create Azure AD users and groups.

1.	In the Azure portal, navigate to the **Users - All users** blade of the AdatumLab101-4b Azure AD tenant.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-23.png)
 
2.	From the **Users - All users** blade, create a new user with the following settings:
 
    - Name: **aaduser1**

	-  User name: **aaduser1@<DNS-domain-name>.onmicrosoft.com** where <DNS-domain-name> represents the initial domain name you specified in the first task of this exercise.

    - Profile: **Not Configured**
	
    - Properties: **Default**

	- Groups: **0 groups selected**

	- Directory role: **User**

	- Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.

> **Note**: Take a note of this user name. You will need it later in this lab.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-24.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-25.png)
 
3.	From the Users - All users blade, create a new user with the following settings:
  	
    - Name: **aaduser2**

    - User name: **aaduser2@<DNS-domain-name>.onmicrosoft.com** where <DNS-domain-name> represents the initial domain name you specified in the first task of this exercise.
	
    - Profile: **Default**

	- Properties: **Default**

	- Groups: **0 groups selected**

	- Directory role: **User**

	- Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.
 
> **Note**: Take a note of this user name. You will need it later in this lab.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-26.png)

### Task 4: Assign Azure AD Premium v2 licenses to Azure AD users

> **Note**: In order to assign Azure AD Premium v2 licenses to Azure AD users, you first have to set their location attribute.

1.	From the **Users - All users** blade, navigate to the **aaduser1 - Profile** blade and set the **Usage location** to **United States**.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-27.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-28.png)
 
2.	From the **aaduser1 - Profile** blade, navigate to the **aaduser1 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-29.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-30.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-31.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-32.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-33.png)
 
3.	Return to the **Users - All users** blade, navigate to the **aaduser2 - Profile** blade, and set the **Usage location** to **United States**.

4.	From the **aaduser2 - Profile** blade, navigate to the **aaduser2 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-34.png)
 
5.	Return to the **Users - All users** blade, navigate to the Profile entry of your user account and set the **Usage location** to **United States**.

6.	Navigate to **Licenses** blade of your user account and assign to it an Azure Active Directory Premium P2 license with all licensing options enabled.

7.	Sign out from the portal and sign back in using the same account you are using for this lab.

> **Note**: This step is necessary in order for the license assignment to take effect.

### Task 5: Configure Azure MFA settings

1.	In the Azure portal, navigate to the **Users - All users** blade of the AdatumLab101-4b Azure AD tenant.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-35.png)
 
2.	From the **Users - All users** blade of the AdatumLab101-4b Azure AD tenant, use the **Multi-Factor Authentication** link to open the **multi-factor authentication** portal.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-36.png)
 
3.	On the **multi-factor authentication** portal, display to the **service settings** tab, review its settings, and the **verification options**, including **Text message to phone**, **Notification through mobile app**, and **Verification code from mobile app or hardware token** are enabled.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-37.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-38.png)

4.	On the **multi-factor authentication** portal, switch to the **users** tab, select **aaduser1** entry, and enable its multi-factor authentication status.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-39.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-40.png)

5.	On the **multi-factor authentication** portal, note that the multi-factor authentication status of **aaduser1** changed to Enabled and that, once you select the user entry again, you have the option of changing it to **Enforced**.

> **Note**: Changing the user status from enabled to enforced impacts only legacy, Azure AD integrated apps which do not support Azure MFA and, once the status changes to enforced, require the use of app passwords.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-41.png)
 
6.	On the **multi-factor authentication** portal, with the **aaduser1** entry selected, display the **Manage user settingswindow** and review its options, including:
    - Require selected users to provide contact methods again

	- Delete all existing app passwords generated by the selected users

	- Restore multi-factor authentication on all remembered devices
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-42.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-43.png)
 
7.	Do not make any changes to user settings and switch back to the Azure portal.

8.	From the **Users - All users** blade of the AdatumLab101-4b Azure AD tenant, navigate to the **AdatumLab101-4b - Overview** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-44.png)
 
9.	From the **AdatumLab101-4b - Overview** blade, navigate to the **AdatumLab101-4b - MFA** blade.

10.	From the **AdatumLab101-4b - MFA** blade, navigate to the **Multi-Factor Authentication - Fraud alert** blade and configure the following settings:

	- Allow users to submit fraud alerts: **On**

	- Automatically block users who report fraud: **On**

	- Code to report fraud during initial greeting: **0**

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-45.png)
 
### Task 6: Validate MFA configuration

1.	Open an InPrivate Microsoft Edge window.

2.	In the new browser window, navigate to the Azure portal and sign in using the **aaduser1** user account. When prompted, change the password to a new value.

> **Note**: You will need to provide a fully qualified name of the aaduser1 user account, including the Azure AD tenant DNS domain name, as noted earlier in this lab.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-46.png)
       
3.	When prompted with the **More information required** message, continue to the **Additional security verification** page.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-47.png)
 
4.	On the **How should we contact you?** page, note that you need to set up one of the following options:

	- Authentication phone

	- Mobile app

5.	Select the **Authentication phone** option with the **Send me a code by text message** method.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-48.png)
 
6.	Complete the verification and note the automatically generated app password.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-49.png) 

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-50.png)

7.	When prompted, change the password from the one generated when you created the **aaduser1** account.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-51.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-52.png)

8.	Verify that you successfully signed in to the Azure portal.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-53.png)
 
9.	Sign out as **aaduser1** and close the InPrivate browser window.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-54.png)
 
## Exercise 3: Implement Azure AD Identity Protection:

The main tasks for this exercise are as follows:
1.	Enable Azure AD Identity Protection
2.	Configure user risk policy
3.	Configure sign-in risk policy
4.	Validate Azure AD Identity Protection configuration by simulating risk events

### Task 1: Enable Azure AD Identity Protection

1.	From the lab virtual machine, start Microsoft Edge, browse to the Azure portal at **http://portal.azure.com** and sign in by using the Microsoft account you used to create the **AdatumLab101-4b** Azure AD tenant.

> **Note**: Ensure that you are signed-in to the AdatumLab101-4b Azure AD tenant. You can use the Directory + subscription filter to switch between Azure AD tenants.

2.	In the Azure portal, navigate to the **New** blade.

3.	From the **New** blade, search Azure Marketplace for **Azure AD Identity Protection**.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-55.png)

4.	Select the **Azure AD Identity Protection** in the list of search results and proceed to create an instance of **Azure AD Identity Protection** associated with the **AdatumLab101-4b** Azure AD tenant.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-56.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-57.png)

5.	In the Azure portal, navigate to the **All services** blade and use the search filter to display the **Azure AD Identity Protection** blade.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-58.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-59.png)

### Task 2: Configure user risk policy

1.	From the **Azure AD Identity Protection** blade, navigate to the **Azure AD Identity Protection - User risk policy** blade

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-60.png)
 
2.	On the Azure **AD Identity Protection - User risk policy** blade, configure the **User risk remediation policy** with the following settings:
    - Assignments: 

        - Users: **All users** (be sure to exclude the current admin account to avoid getting locked out of the tenant)

        - Conditions:

            - User risk: **Medium and above**

    - Controls:

        - Access: **Allow access**

        - **Require password change**

    - Enforce Policy: **On**

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-61.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-62.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-63.png)
 
### Task 3: Configure sign-in risk policy

1.	From the **Azure AD Identity Protection - User risk policy** blade, navigate to the **Azure AD Identity Protection - Sign-in risk policy** blade

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-64.png)
 
2.	On the Azure AD Identity Protection - Sign-in risk policy blade, configure the Sign-in risk remediation policy with the following settings:
    
     - Assignments: 

        - Users: **All users**

        - Conditions:

            - User risk: **Medium and above**

    - Controls:

        - Access: **Allow access**

        - **Require multi-factor authentication**

    - Enforce Policy: **On**
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-65.png)

### Task 4: Validate Azure AD Identity Protection configuration by simulating risk events

> **Note**: Before you start this task, ensure that the template deployment you started in Exercise 0 has completed.

1.	In the Azure portal, set the **Directory + subscription** filter to the default Azure AD tenant.

2.	In the Azure portal, navigate to the **az1010401b-vm1** blade.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-66.png)
 
3.	From the **az1010401b-vm1** blade, connect to the Azure VM via Remote Desktop session and, when prompted to sign in, provide the following credentials:
	
    - Admin Username: Student

	- Admin Password: Password@1234
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-67.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-68.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-69.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-70.png)
 
4.	Within the Remote Desktop session, in Server Manager, click **Local Server** and then click **IE Enhanced Security Configuration**.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-71.png)
 
5.	In the **Internet Explorer Enhanced Security Configuration** dialog box, set both options to **Off** and click **OK**.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-72.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-73.png)
 
6.	Within the Remote Desktop session, open an InPrivate Internet Explorer window.

7.	In the new browser window, navigate to the ToR Browser Project at **https://www.torproject.org/projects/torbrowser.html.en**, download the ToR Browser, and install it with the default options.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-74.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-75.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-76.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-77.png)

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-78.png)
         
8.	Once the installation completes, start the ToR Browser, use the **Connect** option on the initial page, and navigate to the Application Access Panel at **https://myapps.microsoft.com**

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-79.png)
 
9.	When prompted, sign in with the **aaduser2** account you created in the previous exercise.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-80.png)
 
10.	You will be presented with the message **Your sign-in was blocked**. This is expected, since this account is not configured with multi-factor authentiation, which is required due to increased sign-in risk associated with the use of ToR Browser.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-81.png)
 
11.	Use the **Sign out and sign in with a different account option** to sign in as **aaduser1** account you created and configured for multi-factor authentication in the previous exercise.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-82.png)
 
12.	This time, you will be presented with the **Suspicious activity detected** message. Again, this is expected, since this account is configured with multi-factor authentiation. Considering the increased sign-in risk associated with the use of ToR Browser, you will have to use multi-factor authentication, according to the sign-in risk policy you configured in the previous task.

13.	Use the **Verify** option and specify whether you want to verify your identity via text or a call.
 
![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-83.png)

14.	Complete the verification and ensure that you successfully signed in to the Application Access Panel.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-84.png)
 
15.	Sign out as **aaduser1** and close the ToR Browser window.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-85.png)
 
16.	Start Internet Explorer, browse to the Azure portal at **http://portal.azure.com** and sign in by using the Microsoft account you used to create the **AdatumLab101-4b** Azure AD tenant.

17.	In the Azure portal, navigate to the **Azure AD Identity Protection - Risk events** blade and note that the entry representing **Sign-in from anonymous IP address**.

18.	From the **Azure AD Identity Protection - Risk events** blade, navigate to the **Azure AD Identity Protection - Users flagged for risk** blade and note the entry representing **aaduser2**.

> **Result**: After you completed this exercise, you have enabled Azure AD Identity Protection, configured user risk policy and sign-in risk policy, as well as validated Azure AD Identity Protection configuration by simulating risk events

## Exercise 4: Remove lab resources

### Task 1: Open Cloud Shell

1.	At the top of the portal, click the **Cloud Shell** icon to open the Cloud Shell pane.

![alt text](https://github.com/sysgain/qloudable-tl-labs/raw/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab10/lab10-86.png)
 
2.	At the Cloud Shell interface, select **Bash**.

3.	At the **Cloud Shell** command prompt, type in the following command and press **Enter** to list all resource groups you created in this lab:

**az group list --query "[?starts_with(name,'az1010')].name" --output tsv**
       
4.	Verify that the output contains only the resource groups you created in this lab. These groups will be deleted in the next task.

> **Note**: To remove the Azure AD tenant you created in this lab, follow https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-delete-howto

> **Result**: In this exercise, you removed the resources used in this lab.

### Task 2: Delete resource groups

1.	At the **Cloud Shell** command prompt, type in the following command and press **Enter** to delete the resource groups you created in this lab

**az group list --query "[?starts_with(name,'az1010')].name" --output tsv | xargs -L1 bash -c 'az group delete --name $0 --no-wait --yes'**

2.	Close the Cloud Shell prompt at the bottom of the portal.

> **Note**: To remove the Azure AD tenant you created in this lab, follow https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-delete-howto

> **Result**: In this exercise, you removed the resources used in this lab.
