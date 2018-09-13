---
title: 'Tutorial: Azure Active Directory integration with Egnyte | Microsoft Docs'
description: Learn how to use Egnyte with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 58cefccd92b4f5db27f23fe04a5f7f4e6104fbb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553708"
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Tutorial: Azure Active Directory integration with Egnyte
The objective of this tutorial is to show the integration of Azure and Egnyte.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* An Egnyte single sign-on (SSO) enabled subscription

After completing this tutorial, the Azure AD users you have assigned to Egnyte will be able to single sign into the application at your Egnyte company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Egnyte
* Configuring single sign-on
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787812.png "Scenario")

## <a name="enable-the-application-integration-for-egnyte"></a>Enable the application integration for Egnyte
The objective of this section is to outline how to enable the application integration for Egnyte.

**To enable the application integration for Egnyte, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **egnyte**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787813.png "Application Gallery")
7. In the results pane, select **Egnyte**, and then click **Complete** to add the application.
   
   ![Egnyte](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787814.png "Egnyte")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Egnyte with their account in Azure AD using federation based on the SAML protocol.  

As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Egnyte** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787815.png "Configure Single Sign-On")
2. On the **How would you like users to sign on to Egnyte** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787816.png "Configure Single Sign-On")
3. On the **Configure App URL** page, in the **Egnyte Sign In URL** textbox, type your URL using the following pattern "*https://company.egnyte.com*", and then click **Next**.
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787817.png "Configure App URL")
4. On the **Configure single sign-on at Egnyte** page, click **Download certificate**, and then save the certificate file on your computer.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787818.png "Configure Single Sign-On")
5. In a different web browser window, log into your Egnyte company site as an administrator.
6. Click **Settings**.
   
   ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787819.png "Settings")
7. In the menu, click **Settings**.
   
   ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787820.png "Settings")
8. Click the **Configuration** tab, and then click **Security**.
   
   ![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787821.png "Security")
9. In the **Single Sign-On Authentication** section, perform the following steps:
   
   ![Single Sign On Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787822.png "Single Sign On Authentication")   
   1. As **Single sign-on authentication**, select **SAML 2.0**.
   2. As **Identity provider**, select **AzureAD**.
   3. In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Remote Login URL** value, and then paste it into the **Identity provider login URL ** textbox.
   4. In the Azure classic portal, on the **Configure single sign-on at Egnyte** dialog page, copy the **Entity ID** value, and then paste it into the **Identity provider entity ID** textbox.
   5. Create a **base-64 encoded** file from your downloaded certificate.  
     >[!TIP]
     >For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)
      > 
   6. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.
   7. As **Default user mapping**, select **Email address**.
   8. As **Use domain-specific issuer value**, select **disabled**.
   9. Click **Save**.
10. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787823.png "Configure Single Sign-On")
    
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into Egnyte, they must be provisioned into Egnyte. In the case of Egnyte, provisioning is a manual task.

**To provision a user accounts, perform the following steps:**

1. Log in to your **Egnyte** Egnyte company site as administrator.
2. Go to **Settings \> Users & Groups**.
3. Click **Add New User**, and then select the type of user you want to add.
   
   ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787824.png "Users")
4. In the **New Standard User** section, perform the following steps:
   
   ![New Standard User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787825.png "New Standard User")   
   1. Type the **Email**, **Username** and other details of a valid Azure Active Directory account you want to provision.
   2. Click **Save**.
    >[!NOTE]
    >The Azure Active Directory account holder will receive a notification email.
    >

>[!NOTE]
>You can use any other Egnyte user account creation tools or APIs provided by Egnyte to provision AAD user accounts.
> 

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to Egnyte, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Egnyte **application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC787826.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-egnyte-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).





















