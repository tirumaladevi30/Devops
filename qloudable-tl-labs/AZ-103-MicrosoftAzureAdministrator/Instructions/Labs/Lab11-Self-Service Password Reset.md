# Lab 11: Self-Service Password Reset

## Table of Contents

  [Overview](#overview)

  [Pre-requisites](#pre-requisites)

  [Exercise 1: Manage Azure AD users and groups](#exercise-1-manage-azure-ad-users-and-groups)

  [Task 1: Create a new Azure AD tenant](#task-1-create-a-new-azure-ad-tenant)

  [Task 2: Activate Azure AD Premium v2 trial](#task-2-activate-azure-ad-premium-v2-trial)

  [Task 3: Create and configure Azure AD users](#task-3-create-and-configure-azure-ad-users)

  [Task 4: Assign Azure AD Premium v2 licenses to Azure AD users](#task-4-assign-azure-ad-premium-v2-licenses-to-azure-ad-users)

  [Task 5: Manage Azure AD group membership](#task-5-manage-azure-ad-group-membership)

  [Task 6: Configure self-service password reset functionality](#task-6-configure-self-service-password-reset-functionality)

  [Task 7: Validate self-service password reset functionality](#task-7-validate-self-service-password-reset-functionality)

  [Exercise 2: Manage Azure AD-integrated SaaS applications](#exercise-2-manage-azure-ad-integrated-saas-applications)

  [Task 1: Add an application from the Azure AD gallery](#task-1-add-an-application-from-the-azure-ad-gallery)

  [Task 2: Configure the application for a single sign-on](#task-2-configure-the-application-for-a-single-sign-on)

  [Task 3: Assign users to the application](#task-3-assign-users-to-the-application)

  [Task 4: Validate single sign-on for the application](#task-4-validate-single-sign-on-for-the-application)

## Overview:

The aim of this lab is, you have created a new Azure AD tenant, activated Azure AD Premium v2 trial, created and configured Azure AD users, assigned Azure AD Premium v2 licenses to Azure AD users, managed Azure AD group membership, as well as configured and validated self-service password reset functionality.

After you completed this lab exercise2, you have added an application from the Azure AD gallery, configured the application for a single sign-on, assigned users to the application, and validated single sign-on for the application.

**Scenario& Objectives**

XYZ Training Corporation wants to take advantage of Azure AD Premium features.

After completing this lab, you will be able to:

-	Manage Azure AD users and groups
-	Manage Azure AD-integrated SaaS applications

## Pre-requisites: 

-	Familiarity with azure portal

All tasks in this lab are performed from the Azure portal.

## Exercise 1: Manage Azure AD users and groups

The main tasks for this exercise are as follows:

1.	Create a new Azure AD tenant

2.	Activate Azure AD Premium v2 trial

3.	Create and configure Azure AD users

4.	Assign Azure AD Premium v2 licenses to Azure AD users

5.	Manage Azure AD group membership

6.	Configure self-service password reset functionality

7.	Validate self-service password reset functionality

### Task 1: Create a new Azure AD tenant

1.	From the lab virtual machine, start Microsoft Edge, browse to the Azure portal at **http://portal.azure.com** and sign in by using a Microsoft account that has the Owner role in the Azure subscription you intend to use in this lab.
   
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/1.png?token=AEMYGFP5SIM2BPLULFSP4UK5LIPUU) 
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/2.png?token=AEMYGFMZRTSEX4B5CWCJ3BK5LIP2C)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/3.png?token=AEMYGFMNCPMVVOXIBIP2QG25LIP4W)

2.	In the Azure portal, navigate to the **New** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/4.png?token=AEMYGFMFXNL5K6JAGPOYQRS5LIP7Y)
 
3.	From the **New** blade, search Azure Marketplace for **Azure Active Directory**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/5.png?token=AEMYGFJQC44MKCWSDR6WUMK5LIQDQ)
 
4.	Use the list of search results to navigate to the **Create directory** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/6.png?token=AEMYGFLIFN6LRLHYWEKYN6C5LIQGA)
 
5.	From the **Create directory** blade, create a new Azure AD tenant with the following settings:

-	Organization name: **AdatumLab100-5b**
-	Initial domain name: a unique name consisting of a combination of letters and digits.
-	Country or region: **United States**

**Note**: *Take a note of the initial domain name. You will need it later in this lab.*
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/7.png?token=AEMYGFLL3DP56V76GQJZSWK5LIQLE)

### Task 2: Activate Azure AD Premium v2 trial

1.	In the Azure portal, set the **Directory + subscription** filter to the newly created Azure AD tenant.

**Note:** *The Directory + subscription filter appears to the right of the Cloud Shell icon in the toolbar of the Azure portal*

**Note:** *You might need to refresh the browser window if the AdatumLab100-5b entry does not appear in the Directory + subscription filter list.*

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/8.png?token=AEMYGFLM26WXUBZCOHG24QC5LIQQE)

2.	In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade.

3.	From the **AdatumLab100-5b - Overview** blade, navigate to the **Licenses - Overview** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/9.png?token=AEMYGFLE4IUTNVLGB4HTDAK5LIQUK)
 
4.	From the **Licenses - Overview** blade, navigate to the **Products** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/10.png?token=AEMYGFI7E52GJXMJAV3BFU25LIQXC)
 
5.	From the **Products** blade, navigate to the **Activate** blade and activate **Azure AD Premium P2** free trial.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/11.png?token=AEMYGFO6RTKF3GIAMYSNVLS5LIZUA) 
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/12.png?token=AEMYGFINJIQ5KW2X4GEWPIS5LIZVA)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/13.png?token=AEMYGFNH3SR2OD6H77LVLOC5LIZWA)
    
### Task 3: Create and configure Azure AD users

1.	In the Azure portal, navigate to the **Users - All users** blade of the AdatumLab100-5b Azure AD tenant.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/14.png?token=AEMYGFOR7Y5UXTFQYGZ45M25LIZQY)
 
2.	From the **Users - All users** blade, create a new user with the following settings:

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/15.png?token=AEMYGFKUZNM5WOFDUGZ63X25LIZOU)
  
-	Name: **aaduser1**
-	User name: **aaduser1@<DNS-domain-name>.onmicrosoft.com** where <DNS-domain-name> represents the initial domain name you specified in the first task of this exercise.

**Note:** *Take a note of this user name. You will need it later in this lab.*

-	Profile:

*	Department: **Sales**

-	Properties: **Default**
-	Groups: **0 groups selected**
-	Directory role: **User**
-	Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/16.png?token=AEMYGFKKEDHT3HRBLQFCYLS5LIREY)

3.	From the **Users - All users** blade, create a new user with the following settings:

-	Name: **aaduser2**
-	User name: **aaduser2@<DNS-domain-name>.onmicrosoft.com** where <DNS-domain-name> represents the initial domain name you specified in the first task of this exercise.

**Note:** *Take a note of this user name. You will need it later in this lab.*

-	Profile:

*	Department: **Finance**

-	Properties: **Default**
-	Groups: **0 groups selected**
-	Directory role: **User**
-	Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/17.png?token=AEMYGFN2JOTK6CBOSLTT3TC5LIZAG)

### Task 4: Assign Azure AD Premium v2 licenses to Azure AD users

**Note:** *In order to assign Azure AD Premium v2 licenses to Azure AD users, you first have to set their location attribute.*

1.	From the **Users - All users** blade, navigate to the **aaduser1 - Profile** blade and set the **Usage location to United States**.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/18.png?token=AEMYGFPR7ETDTU5Q5OQKC225LISK2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/19.png?token=AEMYGFPY52FPVQ6FESD42L25LISIE)

2.	From the **aaduser1 - Profile** blade, navigate to the **aaduser1 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/20.png?token=AEMYGFNVW6H2MWMLZC73DNC5LISTG) 
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/21.png?token=AEMYGFNSJEGADJQGO3FFE4K5LISUO) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/22.png?token=AEMYGFNGP7VEY3WIXBQT5LS5LISWM) 

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/23.png?token=AEMYGFKKOJPVZQY62OZLZ6S5LISYK)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/24.png?token=AEMYGFO3LZCWN4E2Q4GATM25LIS2U)

3.	Return to the **Users - All users** blade, navigate to the **aaduser2 - Profile** blade, and set the **Usage location to United States**.

4.	From the **aaduser2 - Profile** blade, navigate to the **aaduser2 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/25.png?token=AEMYGFIM76EZSVJWGKHTTWK5LITAI)

5.	Return to the **Users - All** users blade, navigate to the Profile entry of your user account and set the **Usage location to United States**.

6.	Navigate to **Licenses** blade of your user account and assign to it an Azure Active Directory Premium P2 license with all licensing options enabled.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/26.png?token=AEMYGFOFTL6YV6MZRLPHZL25LITPU)

7.	Sign out from the portal and sign back in using the same account you are using for this lab.

**Note:** *This step is necessary in order for the license assignment to take effect.*

### Task 5: Manage Azure AD group membership

1.	In the Azure portal, navigate to the **Groups - All groups** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/27.png?token=AEMYGFKAGZHK2LVNK6FGLZK5LITTW)
 
2.	From the **Groups - All groups** blade, navigate to the **Group** blade and create a new group with the following settings:

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/28.png?token=AEMYGFI6O4AIHAEWCCWVJ625LITWQ)
 
-	Group type: **Security**
-	Group name: **Sales**
-	Group description: **All users in the Sales department**
-	Membership type: **Dynamic User**
-	Dynamic user members:

*	Simple rule

*	Add users where: **department Equals Sales**
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/29.png?token=AEMYGFOXBG3BR2AMYDPFRX25LIT6U)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/30.png?token=AEMYGFN2OMH7SSA2P2ZF3725LIUAG)

3.	From the **Groups - All groups** blade, navigate to the **Group** blade and create a new group with the following settings:

-	Group type: **Security**
-	Group name: **Sales and Finance**
-	Group description: **All users in the Sales and Finance departments**
-	Membership type: **Dynamic User**
-	Dynamic user members:

*	Advanced rule: (**user.department -eq "Sales"**) -or (**user.department -eq "Finance"**)
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/31.png?token=AEMYGFLPQ5YHDTF33Z4ZL4S5LIUJG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/32.png?token=AEMYGFLSZJNROZUQJ4K6CEK5LIUKY)

4.	From the **Groups - All groups** blade, navigate to the blades of **Sales** and **Sales** and **Finance groups**, and note that the group membership evaluation is in progress. Wait until the evalution completes, then navigate to the Members blade, and verify that the group membership is correct.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/33.png?token=AEMYGFK7HOKOGT6JDBWSXZ25LIUPA) 
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/34.png?token=AEMYGFJ3PK3G3HCLKXKKFS25LIURK)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/35.png?token=AEMYGFOQDM3UQLDFWBSAGTS5LIUS4)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/36.png?token=AEMYGFLYKPKSYEOXG6G3WHS5LIUVG)

### Task 6: Configure self-service password reset functionality

1.	In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade.

2.	From the **AdatumLab100-5b - Overview** blade, navigate to the **Password reset - Properties** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/37.png?token=AEMYGFIMD5KNMRDBTW3UDNC5LIUZW)
 
3.	On the **Password reset - Properties** blade, configure the following settings:

-	Self service password reset enabled: **Selected**
-	Selected group: **Sales**
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/38.png?token=AEMYGFO3Q5Z6S6KLUOIDZHS5LIU64)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/39.png?token=AEMYGFINOUSONDWIL7USYPS5LIVAI)


4.	From the **Password reset - Properties** blade, navigate to the **Password reset - Auhentication methods** blade and configure the following settings:

-	Number of methods required to reset: 1
-	Methods available to users:

*	**Email**

*	**Mobile phone**

*	**Office phone**

*	**Security questions**

*	Number of security questions required to register: **3**

*	Number of security questions required to reset: **3**

*	Select security questions: select **Predefined** and add any combination of 5 predefined security questions
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/40.png?token=AEMYGFJDPY7EAPFJS3EVCK25LIVJG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/41.png?token=AEMYGFND325FOS2BORY6X3C5LIVK2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/42.png?token=AEMYGFN63BFGJE2WL6JHTUS5LIVMG)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/43.png?token=AEMYGFJLASJY7ZE7VTV27US5LIVOE)
 
5.	From the **Password reset - Authentication methods** blade, navigate to the **Password reset - Registration** blade, and ensure that the following settings are configured:

-	Require users to register when signing in?: **Yes**
-	Number of days before users are asked to re-confirm their authentication information: **180**

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/44.png?token=AEMYGFNND7AM62WS42W47FK5LIVTY)
  
### Task 7: Validate self-service password reset functionality

1.	Open an InPrivate Microsoft Edge window.

2.	In the new browser window, navigate to the Azure portal and sign in using the **aaduser1** user account. When prompted, change the password to a new value.

**Note:** *You will need to provide a fully qualified name of the aaduser1 user account, including the Azure AD tenant DNS domain name, as noted earlier in this lab.*
       
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/45.png?token=AEMYGFMB55XKN33UIQNHF3S5LIVY4)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/46.png?token=AEMYGFM354GHPCGO3GJS4RC5LIVZ2)           
      
3.	When prompted with the **More information required** message, continue to the **don't lose access to your account** page.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/47.png?token=AEMYGFP4PIMGS63BDIKO2LK5LIV42)
   
4.	On the **don't lose access to your account** page, note that you need to set up at least one of the following options:

-	**Office phone**
-	**Authentication Phone**
-	**Authentication Email**
-	**Security Questions**

5.	From the **don't lose access to your account** page, configure answers to 5 security questions you selected in the previous task
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/48.png?token=AEMYGFIXVCZ7PQTN7RHHK225LIWCO)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/49.png?token=AEMYGFKCBF6OMHLXJEE4OLC5LIWDM)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/50.png?token=AEMYGFONN2AVKXBAQW5FLFK5LIWEQ)         
 
6.	Verify that you successfully signed in to the Azure portal.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/51.png?token=AEMYGFIXW4ELNGMQBMEDMFK5LIWGS)
 
7.	Sign out as **aaduser1** and close the InPrivate browser window.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/52.png?token=AEMYGFPABJCN2XMIRLUMFA25LIWI4)
 
8.	Open an InPrivate Microsoft Edge window.

9.	In the new browser window, navigate to the Azure portal and, on the **Pick an account** page, type in the **aaduser1** user account name.

10.	On the **Enter password** page, click the **Forgot my password** link.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/53.png?token=AEMYGFJQPP63A4VGTHZQHYS5LIWNE)
 
11.	On the **Get back into your account** page, verify the **User ID**, enter the characters in the picture or the words in the audio, and proceed to the next page.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/54.png?token=AEMYGFJIOYWGWWZ253DDA5S5LIWQQ)

12.	On the next page, provide answers to thre security questions using answers you specified in the previous task.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/55.png?token=AEMYGFNM7EFJ3DYACVVKXHS5LIWSY)

13.	On the next page, enter twice a new password and complete the password reset process.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/56.png?token=AEMYGFKWUHEGBPYADBNPRXC5LIWVK)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/57.png?token=AEMYGFJUAI6PK6FQS5HDF625LIWWO)

14.	Verify that you can sign in to the Azure portal by using the newly reset password.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/58.png?token=AEMYGFJU2WJMQCGSG2GRLQK5LIWYU) 

**Result:** *After you completed this exercise, you have created a new Azure AD tenant, activated Azure AD Premium v2 trial, created and configured Azure AD users, assigned Azure AD Premium v2 licenses to Azure AD users, managed Azure AD group membership, as well as configured and validated self-service password reset functionality*

## Exercise 2: Manage Azure AD-integrated SaaS applications

The main tasks for this exercise are as follows:

1.	Add an application from the Azure AD gallery

2.	Configure the application for a single sign-on

3.	Assign users to the application

4.	Validate single sign-on for the application

### Task 1: Add an application from the Azure AD gallery

1.	In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade.

2.	From the **AdatumLab100-5b - Overview** blade, navigate to the **Enterprise applications - All applications** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/59.png?token=AEMYGFMPN54AEVRTVZSYKIK5LIW7G)
 
3.	From the **Enterprise applications - All applications** blade, navigate to the **Add an application** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/60.png?token=AEMYGFJUP5KJTUZTPOQZLUC5LIXCG)
 
4.	On the **Add an application** blade, search the application gallery for the **Microsoft OneDrive**.

5.	Use the list of search results to navigate to the **Microsoft OneDrive** add app blade and add the app.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/61.png?token=AEMYGFMJVFXNMCXGKMGLRZC5LIXG4)
       
### Task 2: Configure the application for a single sign-on

1.	From the **Microsoft OneDrive - Overview** blade, navigate to the **Microsoft OneDrive - Getting started** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/62.png?token=AEMYGFP737GCBBPZADCN6J25LIXKO)
 
2.	On the **Microsoft OneDrive - Getting started** blade, use the **Configure single sign-on (required)** option to navigate to the **Microsoft OneDrive - Single sign-on** blade.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/63.png?token=AEMYGFPQQGUCXBRSX4Q5DKS5LIXOK)

3.	On the **Microsoft OneDrive - Single sign-on** blade, select the **Password-based** option and save the configuration.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/64.png?token=AEMYGFIHWSJEUIO5BKFRKSK5LIXRI)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/65.png?token=AEMYGFPECFJAGSYVHH4HGUK5LIXSE)

### Task 3: Assign users to the application

1.	Navigate back to the **Microsoft OneDrive - Getting started** blade.

2.	On the **Microsoft OneDrive - Getting started** blade, use the **Assign a user for testing (required)** option to navigate to the **Users and groups** blade for **Microsoft OneDrive**.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/66.png?token=AEMYGFJF2OZSIRGRRPFL7ZC5LIXXO)

3.	From the **Users and groups** blade for **Microsoft OneDrive**, navigate to the **Add Assignment** blade and add the following assignment:

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/67.png?token=AEMYGFJVGH7K7BA6JRRS3C25LIX4E)

-	Users and groups: **Sales and Finance*8
-	Select role: **Default access**

*	Assign Credentials:

*	Assign credentials to be shared among all group members: **Yes**

*	Email Address: the name of the Microsoft Account you are using for this lab

*	Password: the password of the Microsoft Account you are using for this lab
       
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/68.png?token=AEMYGFITALUEBODBML2DBKS5LIYA4)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/69.png?token=AEMYGFPMTLETCL5CUJIG4E25LIYC4)
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/70.png?token=AEMYGFIIGD3JQ2DMIFOWXES5LIYFC)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/71.png?token=AEMYGFOCYMHSAHKXP2IQENS5LIYGW)

4.	Sign out from the Azure portal and close the Microsoft Edge window.

### Task 4: Validate single sign-on for the application

1.	Open a Microsoft Edge window.

2.	In the Microsoft Edge window, navigate to the Application Access Panel at http://myapps.microsoft.com and sign in by using the **aaduser2** user account. When prompted, change the password to a new value.

**Note:** *You will need to provide a fully qualified name of the aaduser2 user account, including the Azure AD tenant DNS domain name, as noted earlier in this lab.*
       
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/72.png?token=AEMYGFLE5KZV6DPHQVKVOF25LIYLY)        
               
3.	On the Access Panel Applications page, click the **Microsoft OneDrive** icon.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/73.png?token=AEMYGFPFP2VIYEPPHMDDXS25LIYQU)
 
4.	When prompted, add the My Apps Secure Sign-in Extension and enable it, including the **Allow for InPrivate browsing** option.
 
![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/74.png?token=AEMYGFIS3WR5KH4ZIKRNT7K5LIYU2)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/75.png?token=AEMYGFLE4OZ6UMH7R3V7ZZK5LIYVU)

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/76.png?token=AEMYGFNFYM6HZ3HCONXN3H25LIYWW)         
 
5.	Navigate again to the Application Access Panel at http://myapps.microsoft.com and sign in by using the **aaduser2user** account.

6.	On the Access Panel Applications page, click the **Microsoft OneDrive** icon.

7.	Verify that you have successfully accessed the Microsoft OneDrive application without having to re-authenticate.

![alt text](https://raw.githubusercontent.com/sysgain/qloudable-tl-labs/MicrosoftLearnings/AZ-103-MicrosoftAzureAdministrator/Images/lab11/77.png?token=AEMYGFPNT7EZG5DSX2U5LVC5LIY2A)
 
8.	Sign out from the Application Access Panel and close the Microsoft Edge window.

**Note:** *Make sure to launch Microsoft Edge again, browse to the Azure portal, sign in by using the Microsoft account that has the Owner role in the Azure subscription you were using in this lab, and use the Directory + subscription filter to switch to your default Azure AD tenant once you complete this lab.*

**Result:** After you completed this exercise, you have added an application from the Azure AD gallery, configured the application for a single sign-on, assigned users to the application, and validated single sign-on for the application.
