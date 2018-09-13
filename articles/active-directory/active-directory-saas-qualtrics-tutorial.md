---
title: 'Tutorial: Azure Active Directory integration with Qualtrics | Microsoft Docs'
description: Learn how to use Qualtrics with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 28e82508628afcdcc7d1eb9d67b75534a503b0ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553817"
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Tutorial: Azure Active Directory integration with Qualtrics
The objective of this tutorial is to show the integration of Azure and Qualtrics.  

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Qualtrics single sign-on (SSO) enabled subscription

After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Qualtrics
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")

## <a name="enabling-the-application-integration-for-qualtrics"></a>Enabling the application integration for Qualtrics
The objective of this section is to outline how to enable the application integration for Qualtrics.

**To enable the application integration for Qualtrics, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **Qualtrics**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")
7. In the results pane, select **Qualtrics**, and then click **Complete** to add the application.
   
   ![Qualtrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")
2. On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")
3. On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")
4. On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")
5. Send the metadata file to the Qualtrics support team.
   
   >[!NOTE]
   >The SSO configuration has to be performed by the Qualtrics support team. You will get a notification as soon as the configuration has been completed.
   > 
   > 
6. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")
   
## <a name="configure-user-provisioning"></a>Configure user provisioning

There is no action item for you to configure user provisioning to Qualtrics. When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.  

If there is no user account available yet, it is automatically created by Qualtrics.

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Qualtrics, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Qualtrics** application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")

If you want to test your SSO settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).















