---
title: 'Tutorial: Azure Active Directory integration with Moxtra | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Moxtra.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: jeedes
ms.openlocfilehash: a5ff803dc1e88b0012e3ceb448f55aa4fb7f2b36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555463"
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Tutorial: Azure Active Directory integration with Moxtra
The objective of this tutorial is to show you how to integrate Moxtra with Azure Active Directory (Azure AD).

Integrating Moxtra with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to Moxtra 
* You can enable your users to automatically get signed-on to Moxtra single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Moxtra, you need the following items:

* An Azure AD subscription
* A Moxtra single-sign (SSO) on enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment. 

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Moxtra from the gallery 
2. Configuring and testing Azure AD SSO

## <a name="adding-moxtra-from-the-gallery"></a>Adding Moxtra from the gallery
To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.

**To add Moxtra from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **Moxtra**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_01.png)
7. In the results pane, select **Moxtra**, and then click **Complete** to add the application.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_02.png)

## <a name="configuring-and-testing-azure-ad-sso"></a>Configuring and testing Azure AD SSO
The objective of this section is to show you how to configure and test Azure AD sSSO with Moxtra based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Moxtra to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Moxtra.

To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-sso"></a>Configure Azure AD SSO
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your Moxtra application. 

Your Moxtra application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your saml token attributes configuration. The following screenshot shows an example for this.

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_09.png) 

**To configure Azure AD single sign-on with Moxtra, perform the following steps:**

1. In the Azure classic portal, on the **Moxtra** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to Moxtra** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps:.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_04.png) 
  1. In the **Sign On URL** textbox, type the following URL: **https://www.moxtra.com/service/#login**. 
  2. Click **Next**.
4. On the **Configure single sign-on at Moxtra** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_05.png) 
  1. Click **Download certificate**, and then save the file on your computer.
  2. Click **Next**.
5. In another browser window, sign on to your Moxtra company site as an administrator.
6. In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then **New**.
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 
7. On the **SAML** page, perform the following steps:
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
  1. In the **Name** textbox, type a name for your configuration (e.g.: *SAML*). 
  2. In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Entity ID** value, and then paste it into the **IdP Entity ID** textbox. 
  3. In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox. 
  4. In the **AuthnContextClassRef** textbox, tyoe **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**. 
  5. In the Azure classic portal, on the **Configure single sign-on at Moxtra** dialog page, copy the **Name Identifier Format** value, and then paste it into the **NameID Format** textbox. 
  6. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.    
  7. In the SAML email domain textbox, type your SAML email domain.    
   
   >[!NOTE]
   >To see the steps to verify the domain, click the "**i**" below.
   >  
  8. Click **Update**.
8. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**. 
   
  ![Azure AD Single Sign-On][10]
9. On the **Single sign-on confirmation** page, click **Complete**.  
  
  ![Azure AD Single Sign-On][11]
19. To add custom attribute mappings to your saml token attributes configuration, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog. 
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_80.png) 
11. For each data row in the table below, perform the following steps:
   
     | Attribute Name | Attribute Value |
     | --- | --- |
     | firstname |givenname |
     | lastname |surname |
     | idpid |*\<the **Entity ID** value from the **Configure single sign-on at Moxtra** dialog in the Azure classic portal \>* |
  1. Click add user attribute 

     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_81.png) 
  2. On the **Add User Attribute** dialog, type the attribute name and attribute value shown for that row in the table. 

     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_82.png) 
  3. Click **Complete**.
12. Click **Apply Changes**. 
   
  ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_84.png) 

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_09.png)  
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_05.png)  
  1. As Type Of User, select New user in your organization.
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps: 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_06.png) 
  1. In the **First Name** textbox, type **Britta**.  
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/create_aaduser_08.png) 
  1. Write down the value of the **New Password**.
  2. Click **Complete**.   

### <a name="create-a-moxtra-test-user"></a>Create a Moxtra test user
The objective of this section is to create a user called Britta Simon in Moxtra.

**To create a user called Britta Simon in Moxtra, perform the following steps:**

1. Sign-on to your Moxtra company site as an administrator.
2. In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 
3. On the **Add User** dialog, perform the following steps:
  1. In the **First Name** textbox, type **Britta**.
  2. In the **Last Name** textbox, type **Simon**.
  3. In the **Email** textbox, type Britta's email address in the Azure classic portal.
  4. In the **Division** textbox, type **Dev**.
  5. In the **Department** textbox, type **IT**.
  6. Select **Adminitrator**.
  7. Click **Add**.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Moxtra.

![Assign User][200] 

**To assign Britta Simon to Moxtra, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **Moxtra**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSO configuration using the Access Panel.  

When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-moxtra-tutorial/tutorial_general_205.png







































