---
title: 'Tutorial: Azure Active Directory Integration with Citrix ShareFile | Microsoft Docs'
description: Learn how to use Citrix ShareFile with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 75add885cb636f4bc667de91bcd2b7015c94cbea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563450"
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Tutorial: Azure Active Directory Integration with Citrix ShareFile
The objective of this tutorial is to show the integration of Azure and Citrix ShareFile.  

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Citrix ShareFile tenant

After completing this tutorial, the Azure AD users you have assigned to Citrix ShareFile will be able to single sign into the application at your Citrix ShareFile company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Citrix ShareFile
* Configuring single sign-on (SSO)
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773620.png "Scenario")

## <a name="enable-the-application-integration-for-citrix-sharefile"></a>Enable the application integration for Citrix ShareFile
The objective of this section is to outline how to enable the application integration for Citrix ShareFile.

**To enable the application integration for Citrix ShareFile, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
=   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **Citrix ShareFile**.
   
   ![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773621.png "Application gallery")
7. In the results pane, select **Citrix ShareFile**, and then click **Complete** to add the application.
   
   ![Citrix ShareFile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773622.png "Citrix ShareFile")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Citrix ShareFile with their account in Azure AD using federation based on the SAML protocol.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Citrix ShareFile** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773623.png "Enable single sign-on")
2. On the **How would you like users to sign on to Citrix ShareFile** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773624.png "Configure Single Sign-On")
3. On the **Configure App URL** page, in the **Citrix ShareFile Sign On URL** textbox, type your URL using the following pattern `https://<tenant-name>.shareFile.com`, and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773625.png "Configure App URL")
4. On the **Configure single sign-on at Citrix ShareFile** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.
   
   ![ConfigureSingle Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773626.png "ConfigureSingle Sign-On")
5. In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.
6. In the toolbar on the top, click **Admin**.
7. In the left navigation pane, select **Configure Single Sign-On**.
   
   ![Account Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773627.png "Account Administration")
8. On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:
   
   ![Single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773628.png "Single sign-on")
   1. Click **Enable SAML**.
   2. In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Entity ID** value, and then paste it into the **Your IDP Issuer/ Entity ID** textbox.
   3. In the Azure classic portal, on the **Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.
   4. In the Azure classic portal, on **the Configure single sign-on at Citrix ShareFile** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.
   5. Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure AD classic portal. 
   
      ![Basic Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773629.png "Basic Settings")
9. Click **Save** on the Citrix ShareFile management portal.
10. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773630.png "Configure single sign-on")
    
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.  

* In the case of Citrix ShareFile, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Log in to your **Citrix ShareFile** tenant.
2. Click **Manage Users \> Manage Users Home \> + Create Employee**.
   
   ![Create Employee](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC781050.png "Create Employee")
3. Enter the **Email**, **First name** and **Last name** of a valid Azure AD account you want to provision.
   
   ![Basic Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC799951.png "Basic Information")
4. Click **Add User**.
   >[!NOTE]
   >The AAD account holder will receive an email and follow a link to confirm their account before it becomes active. 
   > 

>[!NOTE]
>You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision AAD user accounts.
>  

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Citrix ShareFile, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Citrix ShareFile** application integration page, click **Assign users**.
   
   ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC773631.png "Assign users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-citrix-sharefile-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).




















