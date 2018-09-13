---
title: 'Tutorial: Azure Active Directory integration with Greenhouse | Microsoft Docs'
description: Learn how to use Greenhouse with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 3f3c1d757d3f1f18c48123905a5261f63da17fdc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550158"
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a>Tutorial: Azure Active Directory integration with Greenhouse
The objective of this tutorial is to show the integration of Azure and Greenhouse.  

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Greenhouse single sign-on (SSO) subscription

After completing this tutorial, the Azure AD users you have assigned to Greenhouse will be able to single sign into the application at your Greenhouse company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Greenhouse
* Configuring single sign-on (SSO)
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790783.png "Scenario")

## <a name="enable-the-application-integration-for-greenhouse"></a>Enable the application integration for Greenhouse
The objective of this section is to outline how to enable the application integration for Greenhouse.

**To enable the application integration for Greenhouse, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **greenhouse**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790784.png "Application Gallery")
7. In the results pane, select **Greenhouse**, and then click **Complete** to add the application.
   
   ![Greenhouse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790785.png "Greenhouse")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Greenhouse with their account in Azure AD using federation based on the SAML protocol.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Greenhouse** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790786.png "Configure single sign-on")
2. On the **How would you like users to sign on to Greenhouse** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790787.png "Configure single sign-on")
3. On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern "*https://company.greenhouse.io*", and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790788.png "Configure App URL")
4. On the **Configure single sign-on at Greenhouse** page, click **Download metadata**, and then save metadata file locally on your computer.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790789.png "Configure single sign-on")
5. Forward that Metadata file to Greenhouse Support team.

>[!NOTE]
>Single sign-on has to be enabled by the Greenhouse support team.
>

6. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790790.png "Configure single sign-on")
   
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse. In the case of Greenhouse, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Log in to your **Greenhouse** company site as an administrator.
2. In the menu on the top, click **Configure**, and then click **Users**.
   
   ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790791.png "Users")
3. Click **New Users**.
   
   ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790792.png "New User")
4. In the **Add New User** section, perform the following steps:
   
   ![Add New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790793.png "Add New User")
   1. In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.
   2. Click **Save**.    
   
      >[!NOTE]
      >The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.
      >  

>[!NOTE]
>You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts. 
> 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Greenhouse, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Greenhouse** application integration page, click **Assign users**.
   
   ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC790794.png "Assign users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-greenhouse-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).


















