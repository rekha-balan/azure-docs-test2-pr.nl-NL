---
title: 'Tutorial: Azure Active Directory integration with Central Desktop | Microsoft Docs'
description: Learn how to use Central Desktop with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9627d2337594eb7c7a67bee08b5860c2dbcee45e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549407"
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Tutorial: Azure Active Directory integration with Central Desktop
The objective of this tutorial is to show the integration of Azure and Central Desktop. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Central desktop single sign on enabled subscription / Central desktop tenant

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Central Desktop
* Configuring single sign-on (SSO)
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")

## <a name="enable-the-application-integration-for-central-desktop"></a>Enable the application integration for Central Desktop
The objective of this section is to outline how to enable the application integration for Central Desktop.

**To enable the application integration for Central Desktop, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **Central Desktop**.
   
   ![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")
7. In the results pane, select **Central Desktop**, and then click **Complete** to add the application.
   
   ![Central Desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.

As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.  
If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")
2. On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")
3. On the **Configure App URL** page, perform the following steps, and then click **Next**: 
   
   1. In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).
   2. In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).
   >  
   
   ![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")
4. On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.
   
  ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")
5. Log in to your **Central Desktop** tenant.
6. Go to **Settings**, click **Advanced**, and then click **Single Sign On**.
   
  ![Setup - Advanced](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")
7. On the **Single Sign On Settings** page, perform the following steps:
   
  ![Single Sign On Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")
   
  1. Select **Enable SAML v2 Single Sign On**.
  2. In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.
  3. In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.
  4. In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.
8. In the **Message Signature Verification Method** section, perform the following steps:
   
   ![Message Signature Verification Method](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")
   
  1. Select **Certificate**.
  2. From the **SSO Certificate** list, select **RSH SHA256**.
  3. Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.  
     >[!TIP]
     >For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Select **Display a link to your SAMLv2 login page**.
9. Click **Update**.
10. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")
    
## <a name="configure-user-provisioning"></a>Configure user provisioning

For AAD users to be able to sign in, they must be provisioned to the Central Desktop application. This section describes how to create AAD user accounts in Central Desktop.

**To provision user accounts to Central Desktop:**
1. Log in to your Central Desktop tenant.
2. Go to **People \> Internal Members**.
3. Click **Add Internal Members**.
   
  ![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")
4. In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.
   
  ![Email Addresses of New Members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")
5. Click **Add Internal member(s)**.
   
  ![Add Internal Member](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")
   
   >[!NOTE]
   >The users you have added will receive an email that includes a confirmation link they need to click to activate the account.
   > 

>[!NOTE]
>You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts
>  

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Central Desktop, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Central Desktop** application integration page, click **Assign users**.
   
   ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).





















