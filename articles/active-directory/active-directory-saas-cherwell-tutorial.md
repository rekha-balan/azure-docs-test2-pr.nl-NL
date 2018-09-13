---
title: 'Tutorial: Azure Active Directory integration with Cherwell | Microsoft Docs'
description: Learn how to use Cherwell with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d5b72801c20f23ffb105bccb9d5f4caee2875d65
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550091"
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a>Tutorial: Azure Active Directory integration with Cherwell
The objective of this tutorial is to show the integration of Azure and Cherwell. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Cherwell single sign-on (SSO) enabled subscription

After completing this tutorial, the Azure AD users you have assigned to Cherwell will be able to single sign into the application at your Cherwell company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Cherwell
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798988.png "Scenario")

## <a name="enable-the-application-integration-for-cherwell"></a>Enable the application integration for Cherwell
The objective of this section is to outline how to enable the application integration for Cherwell.

**To enable the application integration for Cherwell, perform the following** steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **Cherwell**.
   
   ![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798989.png "Cherwell")
7. In the results pane, select **Cherwell**, and then click **Complete** to add the application.
   
## <a name="configure-single-sign-on"></a>Configure single sign-on
   ![Cherwell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798996.png "Cherwell")

The objective of this section is to outline how to enable users to authenticate to Cherwell with their account in Azure AD using federation based on the SAML protocol.

**To configure SSO, perform the following steps:**

1. In the Azure classic portal, on the **Cherwell** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798990.png "Configure Single Sign-On")
2. On the **How would you like users to sign on to Cherwell** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798991.png "Configure Single Sign-On")
3. On the **Configure App URL** page, perform the following steps:
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798992.png "Configure App URL")
  1. In the **Sign On URL** textbox, type the URL used by your users to sign into your **Cherwell** (e.g.: *https://\<company name\>.cherwellondemand.com/cherwellclient*). 
  2.  Click **Next**.
4. On the **Configure single sign-on at Cherwell** page, perform the following steps:
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798993.png "Configure Single Sign-On")
  1.  Click **Download certificate**, and then save the certificate locally on your computer.
  2.  Copy the **Identity Provider URL**.
  3.  Copy the **Single Sign-On Service URL**.
  4.  Click **Next**.
5. Submit the downloaded certificate, the **Identity Provider URL** and the **Single Sign-On Service URL** to your Cherwell support team.
   
   >[!NOTE]
   >Your Cherwell support team has to do the actual SSO configuration. You will get a notification when SSO has been enabled for your subscription.
   > 
6. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798994.png "Configure Single Sign-On")

## <a name="configure-user-provisioning"></a>Configure user provisioning
In order to enable Azure AD users to log into Cherwell, they must be provisioned into Cherwell.

In the case of Cherwell, the user accounts need to be created by your Cherwell support team.

>[!NOTE]
>You can use any other Cherwell user account creation tools or APIs provided by Cherwell to provision Azure Active Directory user accounts.
>  

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Cherwell, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Cherwell** application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC798995.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cherwell-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).














