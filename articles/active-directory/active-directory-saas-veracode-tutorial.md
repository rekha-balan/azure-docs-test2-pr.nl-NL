---
title: 'Tutorial: Azure Active Directory integration with Veracode | Microsoft Docs'
description: Learn how to use Veracode with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: b6e29876b1a0a091b009d557903a998766084e75
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552705"
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Tutorial: Azure Active Directory integration with Veracode
The objective of this tutorial is to show the integration of Azure and Veracode. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A Veracode single sign-on enabled subscription

After completing this tutorial, the Azure AD users you have assigned to Veracode will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for Veracode
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802903.png "Scenario")

## <a name="enabling-the-application-integration-for-veracode"></a>Enabling the application integration for Veracode
The objective of this section is to outline how to enable the application integration for Veracode.

### <a name="to-enable-the-application-integration-for-veracode-perform-the-following-steps"></a>To enable the application integration for Veracode, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **Veracode**.
   
    ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802904.png "Application Gallery")

7. In the results pane, select **Veracode**, and then click **Complete** to add the application.
   
    ![Veracode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802905.png "Veracode")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.  
Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.  
The following screenshot shows an example for this.

![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. In the Azure classic portal, on the **Veracode** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802907.png "Configure Single Sign-On")

2. On the **How would you like users to sign on to Veracode** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802908.png "Configure Single Sign-On")

3. On the **Configure App Settings** page, click **Next**.
   
    ![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802909.png "Configure App Settings")

4. On the **Configure single sign-on at Veracode** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802910.png "Configure Single Sign-On")

5. In a different web browser window, log into your Veracode company site as an administrator.

6. In the menu on the top, click **Settings**, and then click **Admin**.
   
    ![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802911.png "Administration")

7. Click the **SAML** tab.

8. In the **Organization SAML Settings** section, perform the following steps:
   
    ![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802912.png "Administration")
   
    a. In the Azure classic portal, on the **Configure single sign-on at Veracode** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox
   
    b. To upload your downloaded certificate, click **Choose File**.
   
    c. Select **Enable Self Registration**.

9. In the **Self Registration Settings** section, perform the following steps, and then click **Save**:
   
    ![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802913.png "Administration")
   
    a. As **New User Activation**, select **No Activation Required**.
   
    b. As **User Data Updates**, select **Preference Veracode User Data**.
   
    c. For **SAML Attribute Details**, select the following:
      * **User Roles**
      * **Policy Administrator**
      * **Reviewer**
      * **Security Lead**
      * **Executive**
      * **Submitter**
      * **Creator**
      * **All Scan Types**
      * **Team Memberships**
      * **Default Team**

10. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802914.png "Configure Single Sign-On")

11. In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.
    
    ![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC795920.png "Attributes")

12. To add the required attribute mappings, perform the following steps:
    
    ![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802906.png "Attributes")
    
    | Attribute Name | Attribute Value |
    |:--- |:--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | email |User.mail |
    
    a. For each data row in the table above, click **add user attribute**.

    b. In the **Attribute Name** textbox, type the attribute name shown for that row.

    c. In the **Attribute Value** textbox, select the attribute value shown for that row.

    d. Click **Complete**.

13. Click **Apply Changes**.

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.  
In the case of Veracode, provisioning is an automated task.  
There is no action item for you..

Users are automatically created if necessary during the first single sign-on attempt.

> [!NOTE]
> You can use any other Veracode user account creation tools or APIs provided by Veracode to provision AAD user accounts.
> 
> 

## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-veracode-perform-the-following-steps"></a>To assign users to Veracode, perform the following steps:
1. In the Azure classic portal, create a test account.

2. On the **Veracode **application integration page, click **Assign users**.
   
    ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC802915.png "Assign Users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-veracode-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).





















