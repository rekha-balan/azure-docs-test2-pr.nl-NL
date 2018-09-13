---
title: 'Tutorial: Azure Active Directory integration with FM:Systems | Microsoft Docs'
description: Learn how to use FM:Systems with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 15d504bdf7a0ba034aaf73eecefeb848c3f2fbe9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540656"
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a>Tutorial: Azure Active Directory integration with FM:Systems
The objective of this tutorial is to show the integration of Azure and FM:Systems.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A FM:Systems single sign-on enabled subscription

After completing this tutorial, the Azure AD users you have assigned to FM:Systems will be able to single sign into the application at your FM:Systems company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for FM:Systems
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795899.png "Scenario")

## <a name="enabling-the-application-integration-for-fmsystems"></a>Enabling the application integration for FM:Systems
The objective of this section is to outline how to enable the application integration for FM:Systems.

### <a name="to-enable-the-application-integration-for-fmsystems-perform-the-following-steps"></a>To enable the application integration for FM:Systems, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **FM:Systems**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795900.png "Application Gallery")

7. In the results pane, select **FM:Systems**, and then click **Complete** to add the application.
   
    ![FM:Systems](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC800213.png "FM:Systems")
   
## <a name="configuring-single-sign-on"></a>Configuring single sign-on

The objective of this section is to outline how to enable users to authenticate to FM:Systems with their account in Azure AD using federation based on the SAML protocol.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. In the Azure classic portal, on the **FM:Systems** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC790810.png "Configure Single Sign-On")

2. On the **How would you like users to sign on to FM:Systems** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795901.png "Configure Single Sign-On")

3. On the **Configure App URL** page, perform the following steps:
   
    ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795902.png "Configure App URL")
   
    a. In the **FM:Systems Sign On URL** textbox, type your FM:Systems **Reply URL** (e.g.: *https://dpr.fmshosted.com/fminteract/ConsumerService2.aspx*).  
      
    > [!NOTE]
    > You can get this value from your FM:Systems support team.
    > 
    > 
   
    b. Click **Next**

4. On the **Configure single sign-on at FM:Systems** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795903.png "Configure Single Sign-On")

5. Submit the downloaded metadata file to your FM:Systems support team.
   
    > [!NOTE]
    > Your FM:Systems support team has to do the actual SSO configuration.
    > You will get a notification when SSO has been enabled for your subscription.
    > 
    > 
6. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795904.png "Configure Single Sign-On")
   
## <a name="configuring-user-provisioning"></a>Configuring user provisioning

In order to enable Azure AD users to log into FM:Systems, they must be provisioned into FM:Systems.  
In the case of FM:Systems, provisioning is a manual task.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>To configure user provisioning, perform the following steps:
1. In a web browser window, log into your FM:Systems company site as an administrator.

2. Go to **System Administration \> Manage Security \> Users \> User list**.
   
    ![System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795905.png "System Administration")

3. Click **Create new user**.
   
    ![Create New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795906.png "Create New User")

4. In the **Create User** section, perform the following steps:
   
    ![Create User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795907.png "Create User")
   
    a. Type the user name, the password and its confirmation, the email address and the employee ID of a valid Azure Active Directory account you want to provision into the related textboxes.
   
    b. Click **Next**.
 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-fmsystems-perform-the-following-steps"></a>To assign users to FM:Systems, perform the following steps:
1. In the Azure classic portal, create a test account.
2. On the **FM:Systems **application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC795908.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fm-systems-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).


















