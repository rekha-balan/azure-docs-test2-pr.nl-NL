---
title: 'Tutorial: Azure Active Directory integration with InsideView | Microsoft Docs'
description: Learn how to use InsideView with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 10934b34a9884a9c71e33894ec1eff9de0b07d4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552703"
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a>Tutorial: Azure Active Directory integration with InsideView
The objective of this tutorial is to show the integration of Azure and InsideView.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A InsideView tenant

After completing this tutorial, the Azure AD users you have assigned to InsideView will be able to single sign into the application at your InsideView company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for InsideView
* Configuring single sign-on
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794128.png "Scenario")

## <a name="enable-the-application-integration-for-insideview"></a>Enable the application integration for InsideView
The objective of this section is to outline how to enable the application integration for InsideView.

**To enable the application integration for InsideView, perform the following steps:**
 
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **InsideView**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794129.png "Application Gallery")
7. In the results pane, select **InsideView**, and then click **Complete** to add the application.
   
   ![InsideView](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794130.png "InsideView")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to InsideView with their account in Azure AD using federation based on the SAML protocol.  
 
As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **InsideView** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794131.png "Configure Single SignOn")
2. On the **How would you like users to sign on to InsideView** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794132.png "Configure Single SignOn")
3. On the **Configure App URL** page, in the **InsideView Reply URL** textbox, type your InsideView SSO URL (e.g.: `https://my.insideview.com/iv/<STS Name>/login.iv`), and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794133.png "Configure App URL")
4. On the **Configure single sign-on at InsideView** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794134.png "Configure Single SignOn")
5. In a different web browser window, log into your InsideView company site as an administrator.
6. In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.
   
   ![SAML Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794135.png "SAML Single Sign On Settings")
7. In the **Add a New SAML** section, perform the following steps:
   
   ![Add a New SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794136.png "Add a New SAML")
   
   1. In the **STS Name** textbox, type a name for your configuration.
   2. In the Azure classic portal, on the **Configure single sign-on at InsideView** dialog page, copy the **Service Provider (SP) Initiated Endpoint** value, and then paste it into the **SamlP/WS-Fed Unsolicated EndPoint** textbox.
   3. Create a **base-64 encoded** file from your downloaded certificate.      

     >[!TIP]
     >For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o). 
     >
   4. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox
   5. Complete the following:
    * In the **Crm User Id Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.
    * In the **Crm Email Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.
    * In the **Crm First Name Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
    * In the **Crm lastName Mapping** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.
   9. Click **Save**.
8. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794137.png "Configure Single SignOn")
   
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into InsideView, they must be provisioned into InsideView. In the case of InsideView, provisioning is a manual task.

To get users or contacts created in InsideView, contact your customer success manager or send email to **support@insideview.com**

>[!NOTE]
>You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.
>  

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to InsideView, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **InsideView** application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC794138.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insideview-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

















