---
title: 'Tutorial: Azure Active Directory integration with AppDynamics | Microsoft Docs'
description: Learn how to use AppDynamics with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 64b802c60502c347fd3fd4a3eb8ff44e371fb08e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551633"
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a>Tutorial: Azure Active Directory integration with AppDynamics
The objective of this tutorial is to show the integration of Azure and AppDynamics. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* An AppDynamics single sign-on (SSO) enabled subscription

After completing this tutorial, the Azure AD users you have assigned to AppDynamics will be able to single sign into the application at your AppDynamics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for AppDynamics
* Configuring single sign-on (SSO)
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790209.png "Scenario")

## <a name="enabling-the-application-integration-for-appdynamics"></a>Enabling the application integration for AppDynamics
The objective of this section is to outline how to enable the application integration for AppDynamics.

**To enable the application integration for AppDynamics, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **AppDynamics**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790210.png "Application Gallery")
7. In the results pane, select **AppDynamics**, and then click **Complete** to add the application.
   
   ![AppDynamics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790211.png "AppDynamics")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to AppDynamics with their account in Azure AD using federation based on the SAML protocol.  

As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **AppDynamics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790212.png "Configure Single SignOn")
2. On the **How would you like users to sign on to AppDynamics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790213.png "Configure Single SignOn")
3. On the **Configure App URL** page, in the **AppDynamics Sign On URL** textbox, type your URL used by your users to sign-on to AppDynamics ("*https://companyname.saas.appdynamics.com*"), and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790214.png "Configure App URL")
4. On the **Configure single sign-on at AppDynamics** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790215.png "Configure Single SignOn")
5. In a different web browser window, log into your AppDynamics company site as an administrator.
6. In the toolbar on the top, click **Settings**, and then click **Administration**.
   
   ![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790216.png "Administration")
7. Click the **Authentication Provider** tab.
   
   ![Authentication Provider](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790224.png "Authentication Provider")
8. In the **Authentication Provider** section, perform the following steps:
   
   ![SAML Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790225.png "SAML Configuration")   
   1. As **Authentication Provider**, select **SAML**.
   2. In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.
   3. In the Azure classic portal, on the **Configure single sign-on at AppDynamics** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.
   4. Create a **base-64 encoded** file from your downloaded certificate.  
   
      >[!TIP]
      >For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).
      > 
   5. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox
   6. Click **Save**.

     ![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC777673.png "Save")
9. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790226.png "Configure Single SignOn")
   
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into AppDynamics, they must be provisioned into AppDynamics.  
In the case of AppDynamics, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Log into your AppDynamics company site as an administrator.
2. Go to **Users**, and then click **+** to open the **Create User** dialog.
   
   ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790229.png "Users")
3. In the **Create User** section, perform the following steps:
   
   ![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790230.png "Create User")
   
   1. Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.
   2. Click **Save**.

>[!NOTE]
>You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.
> 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to AppDynamics, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **AppDynamics** application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC790231.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appdynamics-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).





















