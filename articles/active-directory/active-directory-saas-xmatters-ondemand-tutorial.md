---
title: 'Tutorial: Azure Active Directory Integration with xMatters OnDemand | Microsoft Docs'
description: Learn how to use xMatters OnDemand with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 3536d48b117520824f0741366037c97902c833d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555468"
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Tutorial: Azure Active Directory Integration with xMatters OnDemand
The objective of this tutorial is to show the integration of Azure and xMatters OnDemand. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A xMatters OnDemand tenant

After completing this tutorial, the Azure AD users you have assigned to xMatters OnDemand will be able to single sign into the application at your xMatters OnDemand company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for xMatters OnDemand
2. Configuring single sign-on
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776788.png "Scenario")

## <a name="enabling-the-application-integration-for-xmatters-ondemand"></a>Enabling the application integration for xMatters OnDemand
The objective of this section is to outline how to enable the application integration for xMatters OnDemand.

### <a name="to-enable-the-application-integration-for-xmatters-ondemand-perform-the-following-steps"></a>To enable the application integration for xMatters OnDemand, perform the following steps:
1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700993.png "Active Directory")

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC700994.png "Applications")

4. Click **Add** at the bottom of the page.
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749321.png "Add application")

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC749322.png "Add an application from gallerry")

6. In the **search box**, type **xMatters OnDemand**.
   
    ![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776789.png "Application gallery")

7. In the results pane, select **XMatters OnDemand**, and then click **Complete** to add the application.
   
    ![xMatters OnDemand](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776790.png "xMatters OnDemand")

## <a name="configuring-single-sign-on"></a>Configuring single sign-on
The objective of this section is to outline how to enable users to authenticate to XMatters OnDemand with their account in Azure AD using federation based on the SAML protocol.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>To configure single sign-on, perform the following steps:
1. In the Azure classic portal, on the **XMatters OnDemand** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776791.png "Configure single sign-on")

2. On the **How would you like users to sign on to XMatters OnDemand** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776792.png "Configure single sign-on")

3. On the **Configure App URL** page, perform the following steps:
   
    ![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776793.png "Configure app URL")
   
    a. In the **XMatters OnDemand Sign In URL** textbox, type your URL using the following pattern: `https://<tenant-name>.XMattersOnDemandapp.com`
   
    b. Click **Next**.

4. On the **Configure single sign-on at XMatters OnDemand** page, to download your certificate, click **Download certificate**, and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.
   
    > [!IMPORTANT]
    > You need to forward the certificate to the xMatters support team. The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.
    > 
    > 
   
    ![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776794.png "Configure single sign on")

5. In a different web browser window, log into your XMatters OnDemand company site as an administrator.

6. In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.
   
    ![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")

7. On the **SAML Configuration** page, perform the following steps:
   
    ![SAML configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")
   
    a. Select **Enable SAML**.
   
    b. In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider ID** textbox.
   
    c. In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign On URL** textbox.
   
    d. In the Azure classic portal, on the **Configure single sign-on at XMatters OnDemand** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Single Logout URL** textbox.
   
    e. On the Company Details page, at the top, click **Save Changes**.
    
    ![Company details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")

8. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
   
    ![Configure single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776798.png "Configure single sign on")

## <a name="configuring-user-provisioning"></a>Configuring user provisioning
In order to enable Azure AD users to log into XMatters OnDemand, they must be provisioned into XMatters OnDemand.  
In the case of XMatters OnDemand, provisioning is a manual task.

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a>To provision a user accounts, perform the following steps:
1. Log in to your **XMatters OnDemand** tenant.

2. Click the **Users** tab.

3. Click **Add User**.
  
    ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")

4. Select **Active**.

5. In the **Add a User** section, perform the following steps:
   
    ![Add a User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")
   
    a. Enter the **UserID**, **First name**, **Last name**, **Site** of a valid AAD account you want to provision.
    
    b. Click **Save**.


## <a name="assigning-users"></a>Assigning users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

### <a name="to-assign-users-to-xmatters-ondemand-perform-the-following-steps"></a>To assign users to XMatters OnDemand, perform the following steps:
1. In the Azure classic portal, create a test account.

2. On the **XMatters OnDemand **application integration page, click **Assign users**.
   
    ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC776799.png "Assign users")

3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
    ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-xmatters-ondemand-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).




















