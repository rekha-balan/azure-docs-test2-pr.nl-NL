---
title: 'Tutorial: Azure Active Directory integration with TOPdesk - Secure | Microsoft Docs'
description: Learn how to use TOPdesk - Secure with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 51ba2d2e7c2e4d31b27628477c501745be8a50f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548730"
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Tutorial: Azure Active Directory integration with TOPdesk - Secure
The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A TOPdesk - Secure single sign-on enabled subscription

After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for TOPdesk - Secure
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")

## <a name="enabling-the-application-integration-for-topdesk---secure"></a>Enabling the application integration for TOPdesk - Secure
The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a>To enable the application integration for TOPdesk - Secure, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **TOPdesk - Secure**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")

7. In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.
   
    ![TOPdesk - Secure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.  
Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file. To get the icon file, contact the TOPdesk support team.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. Sign on to your **TOPdesk - Secure** company site as an administrator.
2. In the **TOPdesk** menu, click **Settings**.
   
    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")

3. Click **Login Settings**.
   
    ![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")

4. Expand the **Login Settings** menu, and then click **General**.
   
    ![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

5. In the **Secure** section of the **SAML login** configuration section, perform the following steps:
   
    ![Technical Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")
   
    a. Click **Download** to download the public metadata file, and then save it locally on your computer.
   
    b. Open the metadata file, and then locate the **AssertionConsumerService** node.
    
    ![Assertion Consumer Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")
   
    c. Copy the **AssertionConsumerService** value.  
      
    > [!NOTE]
    > You will need the value in the **Configure App URL** section later in this tutorial.
    > 
    > 

6. In a different web browser window, log into your **Azure classic portal** as an administrator.

7. On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")

8. On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")

9. On the **Configure App URL** page, perform the following steps:
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")
   
    a. In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").
   
    b. In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Click **Next**.

10. On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")

11. To create a certificate file, perform the following steps:
    
    ![Certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")
    
    a. Open the downloaded metadata file.
    b. Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.
    c. Copy the value of the **X509Certificate** node.
    d. Save the copied **X509Certificate** value locally on your computer in a file.

12. On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.
    
    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")

13. Click **Login Settings**.
    
    ![Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")

14. Expand the **Login Settings** menu, and then click **General**.
    
    ![General](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")

15. In the **Public** section, click **Add**.
    
    ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")

16. On the **SAML configuration assistant** dialog page, perform the following steps:
    
    ![SAML Configuration Assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")
    
    a. To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.

    b. To upload your certificate file, under **Certificate (RSA)**, click **Browse**.

    c. To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.

    d. In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. In the **Display name** textbox, type a name for your configuration.

    f. Click **Save**.

17. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.  
In the case of TOPdesk - Secure, provisioning is a manual task.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>To configure user provisioning, perform the following steps:
1. Sign on to your **TOPdesk - Secure** company site as administrator.
2. In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.
   
    ![Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")

3. On the **New Operator** dialog, perform the following steps:
   
    ![New Operator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")
   
    a. Click the General tab.
   
    b. In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.
   
    c. Select a **Site** for the account in the **Location** section.
   
    d. In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.
   
    e. Click **Save**.

> [!NOTE]
> You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.
> 
> 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a>To assign users to TOPdesk - Secure, perform the following steps:
1. In the Azure classic portal, create a test account.
2. On the **TOPdesk - Secure **application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).




























