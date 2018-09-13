---
title: 'Tutorial: Azure Active Directory integration with SmarterU | Microsoft Docs'
description: Learn how to use SmarterU with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: a5036606aacc2f26196658a0423802f5ce50281c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662218"
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a>Tutorial: Azure Active Directory Integration with SmarterU
The objective of this tutorial is to show the integration of Azure and SmarterU.  

The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A SmarterU tenant

After completing this tutorial, the Azure AD users you have assigned to SmarterU will be able to sign into the application using single sign-on (SSO) at your SmarterU company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for SmarterU
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777320.png "Scenario")

## <a name="enable-the-application-integration-for-smarteru"></a>Enable the application integration for SmarterU
The objective of this section is to outline how to enable the application integration for SmarterU.

**To enable the application integration for SmarterU, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **SmarterU**.
   
    ![Application fallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777321.png "Application fallery")

7. In the results pane, select **SmarterU**, and then click **Complete** to add the application.
   
    ![SmarterU](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777322.png "SmarterU")

## <a name="configure-single-sign-on"></a>Configure single sign-on
The objective of this section is to outline how to enable users to authenticate to SmarterU with their account in Azure AD using federation based on the SAML protocol.

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **SmarterU** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777323.png "Configure Single Sign-On")

2. On the **How would you like users to sign on to SmarterU** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777324.png "Configure Single Sign-On")

3. On the **Configure single sign-on at SmarterU** page, to download your metadata, click **Download metadata**, and then the data file locally as **c:\\SmarterUMetaData.cer**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777325.png "Configure Single Sign-On")

4. In a different web browser window, log into your SmarterU company site as an administrator.

5. In the toolbar on the top, click **Account Settings**.
   
    ![Account Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")

6. On the account configuration page, perform the following steps:
   
    ![External Authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization") 
  1. Select **Enable External Authorization**.
  2. In the **Master Login Control** section, select the **SmarterU** tab.
  3. In the **User Default Login** section, select the **SmarterU** tab.
  4. Select **Enable Okta**.
  5. Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.
  6. Click **Save**.

7. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777328.png "Configure Single Sign-On")

## <a name="configure-user-provisioning"></a>Configure user provisioning
In order to enable Azure AD users to log into SmarterU, they must be provisioned into SmarterU.

In the case of SmarterU, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Log in to your **SmarterU** tenant.

2. Go to **Users**.

3. In the user section, perform the following steps:
   
    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")   
  1. Click **+User**.
  2. Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.
  3. Click **Active**. 
  4. Click **Save**.

>[!NOTE]
>You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.
> 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to SmarterU, perform the following steps:**

1. In the Azure classic portal, create a test account.

2. On the **SmarterU** application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC777330.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smarteru-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

















