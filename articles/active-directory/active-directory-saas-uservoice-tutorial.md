---
title: 'Tutorial: Azure Active Directory Integration with UserVoice | Microsoft Docs'
description: Learn how to use UserVoice with Azure Active Directory to enable single sign-on, automated provisioning, and more!.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0f38add4a23532366839c7f81b313c646f69e937
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550699"
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Tutorial: Azure Active Directory Integration with UserVoice
The objective of this tutorial is to show the integration of Azure and UserVoice.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A UserVoice tenant

After completing this tutorial, the Azure AD users you have assigned to UserVoice will be able to single sign into the application at your UserVoice company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for UserVoice
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777514.png "Scenario")

## <a name="enabling-the-application-integration-for-uservoice"></a>Enabling the application integration for UserVoice
The objective of this section is to outline how to enable the application integration for UserVoice.

### <a name="to-enable-the-application-integration-for-uservoice-perform-the-following-steps"></a>To enable the application integration for UserVoice, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **UserVoice**.
   
    ![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777513.png "Application gallery")

7. In the results pane, select **UserVoice**, and then click **Complete** to add the application.
   
    ![UserVoice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777810.png "UserVoice")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to UserVoice with their account in Azure AD using federation based on the SAML protocol.  
Configuring single sign-on for UserVoice requires you to retrieve a thumbprint value from a certificate.  
If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. In the Azure classic portal, on the **UserVoice** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777515.png "Configure single sign-on")

2. On the **How would you like users to sign on to UserVoice** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777516.png "Configure single sign-on")

3. On the **Configure App URL** page, in the **UserVoice Sign In URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.UserVoice.com*", and then click **Next**.
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777517.png "Configure App URL")

4. On the **Configure single sign-on at UserVoice** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\UserVoice.cer**.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777518.png "Configure single sign-on")

5. In a different web browser window, log into your UserVoice company site as an administrator.

6. In the toolbar on the top, click Settings, and then select Web portal from the menu.
   
    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777519.png "Settings")

7. On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page
   
    ![Web portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777520.png "Web portal")

8. On the **Edit User Authentication** dialog page, perform the following steps:
   
    ![Edit user authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777521.png "Edit user authentication")
   
    a. Click **Single Sign-On (SSO)**.
 
    b. In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Login URL** value, and then paste it into the **SSO Remote Sign-In** textbox.

    c. In the Azure classic portal, on the **Configure single sign-on at UserVoice** dialog page, copy the **Remote Logout URL** value, and then paste it into the **SSO Remote Sign-Out textbox**.
 
    d. Copy the **Thumbprint** value from the exported certificate, and then paste it into the **Current certificate SHA1 fingerprint** textbox.  
      
    > [!TIP]
    > For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI)
    > 
    > 
  
    e. Click **Save authentication settings**.

9. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777522.png "Configure single sign-on")

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
In order to enable Azure AD users to log into UserVoice, they must be provisioned into UserVoice.  
In the case of UserVoice, provisioning is a manual task.

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a>To provision a user accounts, perform the following steps:
1. Log in to your **UserVoice** tenant.

2. Go to **Settings**.
   
    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777811.png "Settings")

3. Click **General**.

4. Click **Agents and permissions**.
   
    ![Agents and permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777812.png "Agents and permissions")

5. Click **Add admins**.
   
    ![Add admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777813.png "Add admins")

6. On the **Invite admins** dialog, perform the following steps:
   
    ![Invite admins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777814.png "Invite admins")
   
    a. In the Emails texbox, type the email address of the account you want to provision, and then click **Add**.
   
    b. Click **Invite**.

> [!NOTE]
> You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.
> 
> 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-uservoice-perform-the-following-steps"></a>To assign users to UserVoice, perform the following steps:
1. In the Azure classic portal, create a test account.
2. On the **UserVoice **application integration page, click **Assign users**.
   
    ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC777523.png "Assign users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-uservoice-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).






















