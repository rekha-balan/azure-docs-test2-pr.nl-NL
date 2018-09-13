---
title: 'Tutorial: Azure Active Directory integration with Work.com | Microsoft Docs'
description: Learn how to use Work.com with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 6a1be66c7dd3b6f807c0219e0bb0b5cdbc5a7b95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554981"
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a>Tutorial: Azure Active Directory integration with Work.com
The objective of this tutorial is to show the integration of Azure and Work.com.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Work.com single sign-on enabled subscription

After completing this tutorial, the AAD users to whom you have assign Work.com access will be able to single sign into the application at your Work.com company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Work.com
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794105.png "Scenario")

## <a name="enabling-the-application-integration-for-workcom"></a>Enabling the application integration for Work.com
The objective of this section is to outline how to enable the application integration for Work.com.

### <a name="to-enable-the-application-integration-for-workcom-perform-the-following-steps"></a>To enable the application integration for Work.com, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **Work.com**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794106.png "Application Gallery")

7. In the results pane, select **Work.com**, and then click **Complete** to add the application.
   
    ![Work.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794107.png "Work.com")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to Work.com with their account in Azure AD using federation based on the SAML protocol.  
As part of this procedure, you are required to upload a certificate to Work.com.com.

> [!NOTE]
> To configure single sign-on, you need to setup a custom Work.com domain name yet. You need to define at least a domain name, test your domain name, and deploy it to your entire organization.
> 
> 

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. Log in to your Work.com tenant as administrator.
2. Go to **Setup**.
   
    ![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")

3. On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page. 
   
    ![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767825.png "My Domain")

4. To verify that your domain has been setup correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.
   
    ![Doman Deployed to User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784377.png "Doman Deployed to User")

5. In a different web browser window, log in to your Azure classic portal.

6. On the **Work.com **application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794109.png "Configure Single Sign-On")

7. On the **How would you like users to sign on to Work.com** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794110.png "Configure Single Sign-On")

8. On the **Configure App URL** page, in the **Work.com Sign On URL** textbox, type the URL used by your users to sign on to your Work.com application (e.g.:” *http://company.my.salesforce.com*”), and then click **Next**: 
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794111.png "Configure App URL")

9. On the **Configure single sign-on at Work.com** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794112.png "Configure Single Sign-On")

10. Log in to your Work.com tenant.

11. Go to **Setup**.
    
    ![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")

12. Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.
    
    ![Single Sign-On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794113.png "Single Sign-On Settings")

13. On the **Single Sign-On Settings** dialog page, perform the following steps:
    
    ![SAML Enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC781026.png "SAML Enabled")
    
    a. Select **SAML Enabled**.
    
    b. Click **New**.

14. In the **SAML Single Sign-On Settings** section, perform the following steps:
    
    ![SAML Single Sign-On Setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794114.png "SAML Single Sign-On Setting")
    
    a. In the **Name** textbox, type a name for your configuration.  
       
    > [!NOTE]
    > Providing a value for **Name** does automatically populate the **API Name** textbox.
    > 
    > 
    
    b. In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.
    
    c. To upload the downloaded certificate, click **Browse**.
    
    d. In the **Entity Id** textbox, type **https://salesforce-work.com**.
    
    e. As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.
    
    f. As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.
    
    g. In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.
    
    h. In the Azure classic portal, on the **Configure single sign-on at Work.com** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Identity Provider Logout URL** textbox.
    
    i. As **Service Provider Initiated Request Binding**, select **HTTP Post**.
    
    j. Click **Save**.

15. In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page. 
    
    ![My Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794115.png "My Domain")

16. On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.
    
    ![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767826.png "Login Page Branding")

17. On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed. Select it, and then click **Save**.
    
    ![Login Page Branding](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784366.png "Login Page Branding")

18. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794116.png "Configure Single Sign-On")

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.  
In the case of Work.com, provisioning is a manual task.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>To configure user provisioning, perform the following steps:
1. Sign on to your Work.com company site as an administrator.

2. Go to **Setup**.
   
    ![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")
3. Go to **Manage Users \> Users**.
   
    ![Manage Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")

4. Click **New User**.
   
    ![All Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")

5. In the User Edit section, perform the following steps:
   
    ![User Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794118.png "User Edit")
   
    a. Type the **Last Name**, **Alias**, **Email**, **Username** and **Nickname** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.
   
    b. Select **Role**, **User License** and **Profile**.
   
    c. Click **Save**.  
      
    > [!NOTE]
    > The Azure Active Directory account holder will get an email including a link to confirm the account before it becomes active.
    > 
    > 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-workcom-perform-the-following-steps"></a>To assign users to Work.com, perform the following steps:
1. In the Azure classic portal, create a test account.

2. On the Work.com application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC794119.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-work-com-tutorial/IC767830.png "Yes")

You should now wait for 10 minutes and verify that the account has been synchronized to Work.com.com.

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).





























