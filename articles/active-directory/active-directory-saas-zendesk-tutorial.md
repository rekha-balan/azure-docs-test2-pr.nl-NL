---
title: 'Tutorial: Azure Active Directory integration with Zendesk | Microsoft Docs'
description: Learn how to use Zendesk with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: d8112df1f6290e719b6ecbd647c8da5c45ab81a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564318"
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Tutorial: Azure Active Directory integration with Zendesk
The objective of this tutorial is to show the integration of Azure and Zendesk.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Zendesk tenant

After completing this tutorial, the Azure AD users you have assigned to Zendesk will be able to single sign into the application at your Zendesk company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Zendesk
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773083.png "Scenario")

## <a name="enabling-the-application-integration-for-zendesk"></a>Enabling the application integration for Zendesk
The objective of this section is to outline how to enable the application integration for Zendesk.

### <a name="to-enable-the-application-integration-for-zendesk-perform-the-following-steps"></a>To enable the application integration for Zendesk, perform the following steps:
1. In the Azure Management Portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **Zendesk**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773084.png "Application Gallery")

7. In the results pane, select **Zendesk**, and then click **Complete** to add the application.
   
    ![Zendesk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773085.png "Zendesk")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to Zendesk with their account in Azure AD using federation based on the SAML protocol.  
Configuring single sign-on for Zendesk requires you to retrieve a thumbprint value from a certificate.  
If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. In the Azure AD portal, on the **Zendesk** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
    ![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773086.png "Single sign-on")

2. On the **How would you like users to sign on to Zendesk** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773087.png "Configure single sign-on")

3. On the **Configure App URL** page, perform the following steps:
   
    ![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773088.png "Configure app URL")
   
    a. In the **Zendesk Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.zendesk.com`
   
    b. Click **Next**.

4. On the **Configure single sign-on at Zendesk** page, click **Download certificate**, and then save the certificate file locally on your compiter.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC777534.png "Configure single sign-on")

5. In a different web browser window, log into your Zendesk company site as an administrator.

6. Click **Admin**.

7. In the left navigation pane, click **Settings**, and then click **Security**.
   
    ![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773089.png "Security")

8. On the **Security** page, click the **Admin & Agents** tab.

9. Select **Single sign-on (SSO) and SAML**, and then select **SAML**.

10. In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **SAML SSO URL** value, and then paste it into the **SAML SSO URL** textbox.

11. In the Azure AD portal, on the **Configure single sign-on at Zendesk** page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.
    
    ![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773090.png "Single sign-on")

12. Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Certificate Fingerprint** textbox.
    
    > [!TIP]
    > For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)
    > 
    > 

13. Click **Save**.

14. On the Azure AD portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773093.png "Configure single sign-on")

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
In order to enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.  
In the case of **Zendesk**, provisioning is a manual task.

### <a name="to-provision-a-user-account-to-zendesk-perform-the-following-steps"></a>To provision a user account to Zendesk, perform the following steps:
1. Log in to your **Zendesk** tenant.

2. Select the **Customer List** tab.

3. Select the **User** tab, and click **Add**.
   
    ![Add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773632.png "Add user")
4. Type the email address of an existing Azure AD account you want to provision, and then click **Save**.
   
    ![New user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773633.png "New user")

> [!NOTE]
> You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.
> 
> 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-zendesk-perform-the-following-steps"></a>To assign users to Zendesk, perform the following steps:
1. In the Azure AD portal, create a test account.

2. On the **Zendesk **application integration page, click **Assign users**.
   
    ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC773094.png "Assign users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-zendesk-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).



















