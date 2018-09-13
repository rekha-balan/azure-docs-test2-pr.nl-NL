---
title: 'Tutorial: Azure Active Directory integration with NetDocuments | Microsoft Docs'
description: Learn how to use NetDocuments with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 7162dc3daea0f454423868ac2e23f055e7d48683
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552707"
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a>Tutorial: Azure Active Directory integration with NetDocuments
The objective of this tutorial is to show the integration of Azure and NetDocuments. The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* A NetDocuments tenant

After completing this tutorial, the Azure AD users you have assigned to NetDocuments will be able to single sign into the application at your NetDocuments company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

1. Enabling the application integration for NetDocuments
2. Configuring single sign-on (SSO)
3. Configuring user provisioning
4. Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795040.png "Scenario")

## <a name="enabling-the-application-integration-for-netdocuments"></a>Enabling the application integration for NetDocuments
The objective of this section is to outline how to enable the application integration for NetDocuments.

**To enable the application integration for NetDocuments, perform the following steps:**

1. In the Azure classic portal, on the left navigation pane, click **Active Directory**.
   
   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.
   
   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
   ![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC749322.png "Add an application from gallerry")
6. In the **search box**, type **NetDocuments**.
   
   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795041.png "Application Gallery")
7. In the results pane, select **NetDocuments**, and then click **Complete** to add the application.
   
   ![NetDocuments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795042.png "NetDocuments")
   
## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to NetDocuments with their account in Azure AD using federation based on the SAML protocol.  

Configuring SSO for NetDocuments requires you to retrieve a thumbprint value from a certificate. If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).

**To configure SSO, perform the following steps:**

1. In the Azure classic portal, on the **NetDocuments** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795043.png "Configure Single Sign-On")
2. On the **How would you like users to sign on to NetDocuments** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795044.png "Configure Single Sign-On")
3. On the **Configure App URL** page, perform the following steps:
   
   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795045.png "Configure App URL")
   
   1. In the **Sign On URL** textbox, type your URL used by your users to sign on to your NetDocuments application (e.g.: "*https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=CA-JI1BG3H1*").
   2. In the **NetDocuments Reply URL** textbox, type the same value you have typed into the the **Sign On URL** textbox.  
      
      >[!NOTE]
      >You can find the correct value at the end of the **Federated Identity** dialog (See the screenshot for step 9).
      >
      >
     
   3. Click **Next**.
4. On the **Configure single sign-on at NetDocuments** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795046.png "Configure Single Sign-On")
5. In a different web browser window, log into your NetDocuments company site as an administrator.
6. Go to **Admin**.
7. Click **Add and remove users and groups**.
   
   ![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")
8. Click **Configure advanced authentication options**.
   
   ![Configure advanced authentication options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795048.png "Configure advanced authentication options")
9. On **the Federated Identity** dialog, perform the following steps:
   
   ![Federated Identitty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795049.png "Federated Identitty")
   
   1. As **Federated identity server type**, select **Active Directory Federation Services**.
   2. Click **Choose file**, to upload the downloaded metadata file.
   3. Click **OK**.
10. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795050.png "Configure Single Sign-On")
    
## <a name="configure-user-provisioning"></a>Configure user provisioning

In order to enable Azure AD users to log into NetDocuments, they must be provisioned into NetDocuments. In the case of NetDocuments, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Sing on to your **NetDocuments** company site as administrator.
2. In the menu on the top, click **Admin**.
   
   ![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795051.png "Admin")
3. Click **Add and remove users and groups**.
   
   ![Repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795047.png "Repository")
4. In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.
   
   ![Email Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795053.png "Email Address")
   
   >[!NOTE]
   >The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.
   > 
   > 

>[!NOTE]
>You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision AAD user accounts.
>
>

## <a name="assign-users"></a>Assign users
To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.

**To assign users to NetDocuments, perform the following steps;**

1. In the Azure classic portal, create a test account.
2. On the **NetDocuments **application integration page, click **Assign users**.
   
   ![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC795054.png "Assign Users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.
   
   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netdocuments-tutorial/IC767830.png "Yes")

If you want to test your SSO settings, open the Access Panel. For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



















