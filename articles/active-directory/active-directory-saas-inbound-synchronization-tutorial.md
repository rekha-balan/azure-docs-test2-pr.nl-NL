---
title: 'Tutorial: Configure Workday for Inbound Synchronization | Microsoft Docs'
description: Learn how to use Inbound Synchronization with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8fe96f0a-f142-4d66-b53d-3ac3eb41a661
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 1e97b830e457b4e029bc75964a1e6fae20030b94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540647"
---
# <a name="tutorial-configure-workday-for-inbound-synchronization"></a>Tutorial: Configure Workday for Inbound Synchronization

The objective of this tutorial is to show you the steps you need to perform in Workday and Microsoft Azure AD to import people from Workday to Microsoft Azure AD.    

>[!NOTE]
>Azure Active Directory (AD) Premium is available for customers in China using the worldwide instance of Azure AD. Azure AD Premium is not currently supported in the Microsoft Azure service operated by 21Vianet in China.    
> 
> 

The scenario outlined in this tutorial assumes that you already have the following items:  

* A valid Azure subscription  
* A tenant in Workday  

The scenario outlined in this tutorial consists of the following building blocks:  

1. Enabling the application integration for Workday  
2. Creating an integration system user  
3. Creating a security group  
4. Assigning the integration system user to the security group  
5. Configuring security group options  
6. Activating security policy changes  
7. Configuring user import in Microsoft Azure AD  

## <a name="enable-the-application-integration-for-workday"></a>Enable the application integration for Workday
The objective of this section is to outline how to enable the application integration for Salesforce.    

**To enable the application integration for Workday, perform the following steps:**

1. In the Azure Management Portal, on the left navigation pane, click **Active Directory**.    
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700993.png "Active Directory")  
2. From the **Directory** list, select the directory for which you want to enable directory integration.    
3. To open the applications view, in the directory view, click **Applications** in the top menu.    
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700994.png "Applications")  
4. To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.    
   
   ![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC700995.png "What do you want to do?")  
5. In the **search box**, type **Workday**.    
   
   ![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701021.png "Workday")  
6. In the results pane, select **Workday**, and then click **Complete** to add the application.    
   
   ![Workday](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC701022.png "Workday")  

## <a name="create-an-integration-system-user"></a>Create an integration system user
1. In the **Workday Workbench**, enter **create user** in the search box, and then click on the link, **Create Integration System User**.     
   
   ![create user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750979.png "create user")  
2. Complete the Create Integration System User task by supplying a user name and password for a new Integration System User.  
 * Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.    
 * Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.    
   
   ![Create Integration System User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750980.png "Create Integration System User")  

## <a name="create-a-security-group"></a>Create a security group
For the scenario outlined in this tutorial, you need to create an unconstrained integration system security group and assign the user to it.    

1. Enter create security group in the search box, and then click on the link, Create Security Group.     
   
   ![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750981.png "CreateSecurity Group")  
2. Complete the Create Security Group task.  Select Integration System Security Group—Unconstrained from the Type of Tenanted Security Group dropdown, to create a security group to which members will be explicitly added.     
   
   ![CreateSecurity Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750982.png "CreateSecurity Group")  

## <a name="assign-the-integration-system-user-to-the-security-group"></a>Assign the integration system user to the security group
1. Enter edit security group in the search box, and then click on the link,  **Edit Security Group**.     
   
   ![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750983.png "Edit Security Group")  
2. Search for, and select the new integration security group by name.    
   
   ![Edit Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750984.png "Edit Security Group")  
3. Add the new integration system user to the new security group.       
   
   ![System Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750985.png "System Security Group")  

## <a name="configure-security-group-options"></a>Configure security group options
In this step, you grant to the new security group permissions for Get and Put operations on the objects secured by the following domain security policies:  

* External Account Provisioning  
* Worker Data: Public Worker Reports  
* Worker Data: All Positions  
* Worker Data: Current Staffing Information  
* Worker Data: Business Title on Worker Profile  

1. Enter domain security policies in the search box, and then click on the link, Domain Security Policies for Functional Area.     
   
   ![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750986.png "Domain Security Policies")  
2. Search for system and select the System functional area.  Click on the button labelled, OK.     
   
   ![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750987.png "Domain Security Policies")  
3. In the list of security policies for the System functional area, expand Security Administration and select the domain security policy, External Account Provisioning.     
   
   ![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750988.png "Domain Security Policies")  
4. Click on the Edit Permissions button, and then, on the Edit Permissions screen, add the new security group to the list of security groups with Get and Put integration permissions.     
   
   ![Edit Permission](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750989.png "Edit Permission")  
5. Repeat step 1, above, to return to the screen for selecting functional areas, and this time, search for staffing, select the Staffing functional area, and click on the button labelled, OK.    
   
   ![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750990.png "Domain Security Policies")  
6. In the list of security policies for the Staffing functional area, expand Worker Data: Staffing, and repeat step 4 above for each of these remaining security policies:    
   
   * Worker Data: Public Worker Reports  
   * Worker Data: All Positions  
   * Worker Data: Current Staffing Information  
   * Worker Data: Business Title on Worker Profile    
   
   ![Domain Security Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750991.png "Domain Security Policies")  

## <a name="activate-security-policy-changes"></a>Activate security policy changes
1. Enter activate in the search box, and then click on the link,Activate Pending Security Policy Changes.    
   
   ![Activate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750992.png "Activate")  
2. Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then clicking on the button labelled, OK.      
   
   ![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750993.png "Activate Pending Security")  
3. Complete the task on the next screen by checking the checkbox labelled Confirm and clicking on the button labelled, OK.     
   
   ![Activate Pending Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750994.png "Activate Pending Security")  

## <a name="configure-user-import-in-microsoft-azure-ad"></a>Configure user import in Microsoft Azure AD
The objective of this section is to outline how Microsoft Azure AD to import people from Workday.    

**To configure user import in Microsoft Azure AD, perform the following steps:**

1. On the **Workday** application integration page, click **Configure user import** to open the **Configure Provisioning** dialog.    
2. On the **Settings and admin credentials** page, perform the following steps, and then click Next:    
   
   ![Settings and admin credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750995.png "Settings and admin credentials")    
   
 * In the **Workday admin user name** textbox, type the name of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.    
 * In the **Workday admin password** textbox, type the password of the user you have created in the [Creating an integration system user](https://msdn.microsoft.com/library/azure/Dn762434.aspx#BKMK_CreateUser) section.    
 * In the **Workday tenant URL** textbox, type the URL or your Workday tenant.    
3. On the **Test connection** page, click **Start test** to confirm connectivity, and then click **Next**.    
   
   ![Test connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750996.png "Test connection")  
4. On the **Provisioning options** page, click **Next**.    
   
   ![Provisioning options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750997.png "Provisioning options")  
5. On the **Start provisioning** dialog, click **Complete**.    
   
   ![Start provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inbound-synchronization-tutorial/IC750998.png "Start provisioning")  

You can now go to the **Users** section and check whether your Workday user has been imported.    


























