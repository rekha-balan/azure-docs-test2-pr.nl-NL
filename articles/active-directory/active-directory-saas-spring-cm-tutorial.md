---
title: 'Tutorial: Azure Active Directory integration with SpringCM | Microsoft Docs'
description: Learn how to use Spring CM with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/10/2017
ms.author: jeedes
ms.openlocfilehash: ccb6ae4291aa0813775d6adfe342b47673a67f1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553154"
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a>Tutorial: Azure Active Directory integration with SpringCM
The objective of this tutorial is to show how to set up single sign-on (SSO) between Azure Active Directory and SpringCM.

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A SpringCM single sign-on (SSO) enabled subscription

After completing this tutorial, the Azure Active Directory users you have assigned to SpringCM will be able to SSO using the AAD Access Panel.

1. Enabling the application integration for SpringCM
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797044.png "Scenario")

## <a name="enabling-the-application-integration-for-springcm"></a>Enabling the application integration for SpringCM
The objective of this section is to outline how to enable the application integration for SpringCM.

**To enable the application integration for SpringCM, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **SpringCM**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797045.png "Application Gallery")

7. In the results pane, select **SpringCM**, and then click **Complete** to add the application.
   
    ![SpringCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797046.png "SpringCM")

## <a name="configure-single-sign-on"></a>Configure single sign-on
This section outlines how to enable users to authenticate to SpringCM with their account in Azure Active Directory, using federation based on the SAML protocol.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **SpringCM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
    ![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797047.png "Configure single Sign-On")

2. On the **How would you like users to sign on to SpringCM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797048.png "Configure single Sign-On")

3. On the **Configure App URL** page, in the **SpringCM Sign On URL** textbox, type the URL used by your users to sign on to your SpringCM application, and then click **Next**. 
   
    The app URL is your SpringCM tenant URL (e.g.: *https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=16826*):
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797049.png "Configure App URL")

4. On the **Configure single sign-on at SpringCM** page, to download your certificate, click **Download certificate**, and then save the certificate file locally to your computer.
   
    ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797050.png "Configure Single SignOn")

5. In a different web browser window, sign on to your **SpringCM** company site as administrator.

6. In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.
   
    ![SAML SSO](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797051.png "SAML SSO")

7. In the Identity Provider Configuration section, perform the following steps:
   
    ![Identity Provider Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797052.png "Identity Provider Configuration")   
  1. To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.
  2. In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.
  3. In the Azure classic portal, on the **Configure single sign-on at SpringCM** page, copy the **Singel Sign-On Service URL** value, and then paste it into the **Service Provider (SP) Initiated Endpoint** textbox.
  4. As **SAML Enabled**, select **Enable**.
  5. Click **Save**.

8. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure Single SignOn](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797053.png "Configure Single SignOn")

## <a name="configure-user-provisioning"></a>Configure user provisioning
In order to enable Azure Active Directory users to log into SpringCM, they must be provisioned into SpringCM.  

In the case of SpringCM, provisioning is a manual task.

>[!NOTE]
>For more details, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user). 
> 

**To provision a user account to SpringCM, perform the following steps:**

1. Log in to your **SpringCM** company site as administrator.

2. Click **GOTO**, and then click **Address Book**.
   
    ![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797054.png "Create User")

3. Click **Create User**.

4. Select a **User Role**.

5. Select **Send Activation Email**.

6. Type the first name, last name and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.

7. Add the user to a **Security group**.

8. Click **Save**.

  >[!NOTE]
  >You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.  
  > 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to SpringCM, perform the following steps:**

1. In the Azure classic portal, create a test account.

2. On the **SpringCM** application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC797055.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-spring-cm-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).


















