---
title: 'Tutorial: Azure Active Directory Integration with Rally Software | Microsoft Docs'
description: Learn how to use Rally Software with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4ab9b9f78a697bead8599d259c4aad78840594a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563246"
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Tutorial: Azure Active Directory Integration with Rally Software
The objective of this tutorial is to show the integration of Azure and Rally Software.  

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Rally Software tenant

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Rally Software
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769525.png "Scenario")

## <a name="enable-the-application-integration-for-rally-software"></a>Enable the application integration for Rally Software
The objective of this section is to outline how to enable the application integration for Rally Software.

**To enable the application integration for Rally Software, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **rally**.
   
    ![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769526.png "Application gallery")

7. In the results pane, select **Rally Software**, and then click **Complete** to add the application.
   
    ![Rally Software](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769527.png "Rally Software")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Rally Software with their account in Azure AD using federation based on the SAML protocol.

As part of this procedure, you are required to upload a certificate to Rally Software.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Rally Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC749323.png "Configure single sign-on")

2. On the **How would you like users to sign on to Rally** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769528.png "Microsoft Azure AD Single Sign-On")

3. On the **Configure App URL** page, in the **Rally Software Tenant URL** textbox, type your URL using the following pattern "*https://\<tenant-name\>.rally.com*", and then click **Next**.
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769529.png "Configure App URL")

4. On the **Configure single sign-on at Rally** page, click Download metadata, and then save it on your computer.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769530.png "Configure single sign-on")

5. Log in to your **Rally Software** tenant.

6. In the toolbar on the top, click **Setup**, and then select **Subscription**.
   
    ![Subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769531.png "Subscription")

7. Click the **Action** button In the tool bar on the top at the right side and then select **Edit Subscription**.

8. On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:
   
    ![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769542.png "Authentication")
   
  1. Select **Rally or SSO authentication** from Authentication dropdown.
  2. In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.
  3. In the Azure classic portal, on the **Configure single sign-on at Rally Software** dialog page, copy the **Remote Logout URL** value.

9. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769547.png "Configure single sign-on")
   
## <a name="configure-user-provisioning"></a>Configure user provisioning

For AAD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.

**To configure user provisioning, perform the following steps:**

1. Log in to your Rally Software tenant.

2. Go to **Setup \> USERS**, and then click **+ Add New**.
   
    ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781039.png "Users")

3. Type the name in the New User textbox, and then click **Add with Details**.

4. In the **Create User** section, perform the following steps:
   
    ![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC781040.png "Create User")
   
   1. In the **User Name** textbox, type the name of the Azure AD user you want to provision.
   2. In the **Email Address** textbox, type the email address of the Azure AD user you want to provision.
   3. Click **Save & Close**.

>[!NOTE]
>You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision AAD user accounts.
> 
> 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Rally Software, perform the following steps:**

1. In the Azure classic portal, create a test account.

2. On the **Rally Software** application integration page, click **Assign users**.
   
    ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC769548.png "Assign users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rally-software-tutorial/IC767830.png "Yes")

If you want to test your SSO settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).



















