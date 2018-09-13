---
title: 'Tutorial: Azure Active Directory integration with Concur | Microsoft Docs'
description: Learn how to use Concur with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 8bf48b7454e1574612def957924b857eb8477bc5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551491"
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a>Tutorial: Azure Active Directory integration with Concur
The objective of this tutorial is to show the integration of Azure and Concur.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A tenant in Concur

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Concur
* Configuring single sign-on (SSO)
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769766.png "Scenario")

>[!NOTE]
>The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform. 
> 

## <a name="enable-the-application-integration-for-concur"></a>Enable the application integration for Concur
The objective of this section is to outline how to enable the application integration for Concur.

**To enable the application integration for Concur, perform the following steps:**
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
  ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
  ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700994.png "Applications")
4. To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.
   
  ![What do you want to do?](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC700995.png "What do you want to do?")
5. In the **search box**, type **Concur**.
   
  ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721727.png "Application Gallery")
6. In the results pane, select **Concur**, and then click **Complete** to add the application.
   
  ![Concur](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721728.png "Concur")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Concur with their account in Azure AD using federation based on the SAML protocol.

>[!NOTE]
>The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform.
> 

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Concur **application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769767.png "Configure single sign-on")
2. On the **How would you like users to sign on to Concur** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769768.png "Configure single sign-on")
3. On the **Configure App URL** page, in the **Concur Sign In URL** textbox, type your concur tenant sign-in URL, and then click **Next**: 
   
   ![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769769.png "Configure sign in URL")
4. On the **Configure single sign-on at Concur** page, perform the following steps.
   
   ![Configure sign in URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769770.png "Configure sign in URL")
   1. Click Download the metadata, and then safe the data file to your computer.
   2. Contact the Concur support team to configure SSO for your tenant.
   3. Select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.  
   
   >[!NOTE]
   >The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur to perform. 
   > 

## <a name="configure-user-provisioning"></a>Configure user provisioning
The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.

To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile. Don't simply add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.

Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (e.g. enabling apps). These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).

When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields. This will assign ownership to the profile.Once the profile(s) is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.

For the following reasons, this action should not be done with the profile they use for normal T&E administration.

1. The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled. This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.
2. If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile will not function until the app is enabled with another active WS Admin profile. This is why you are supposed to create distinct WS Admin profiles.
3. If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated

**To configure user provisioning, perform the following steps:**

1. Logon to your **Concur** tenant.
2. From the **Administration** menu, select **Web Services**.
   
   ![Concur tenant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721729.png "Concur tenant")
3. On the left side, from the **Web Services** pane, select **Enable Partner Application**.
   
   ![Enable Partner Application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721730.png "Enable Partner Application")
4. From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.
   
   ![Microsoft Azure Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721731.png "Microsoft Azure Active Directory")
5. Click **Yes** to close the **Confirm Action** dialog.
   
   ![Confirm Action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC721732.png "Confirm Action")
6. In the Azure classic portal, select **Concur** from the applications list to open the **Concur** dialog page.
7. To open the **Configure User Provisioning** dialog page, click **Configure user provisioning**.
8. Enter the user name and the password of your Concur administrator, and then click **Next**.
9. To finish the configuration, on the **Confirmation** page, click the **Complete** button.

You can now create a test account, wait for 10 minutes and verify that the account has been synchronized to Concur.

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Concur, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Concur **application integration page, click **Assign users**.
   
   ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC769771.png "Assign users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-concur-tutorial/IC767830.png "Yes")

You should now wait for 10 minutes and verify that the account has been synchronized to Concur.

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

















