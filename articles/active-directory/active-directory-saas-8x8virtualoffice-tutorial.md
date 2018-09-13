---
title: 'Tutorial: Azure Active Directory integration with 8x8 Virtual Office | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 8x8 Virtual Office.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 28f90473458138c57e1290174011649c38c55045
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550284"
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a>Tutorial: Azure Active Directory integration with 8x8 Virtual Office
The objective of this tutorial is to show you how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).

Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to 8x8 Virtual Office
* You can enable your users to automatically get signed-on to 8x8 Virtual Office single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with 8x8 Virtual Office, you need the following items:

* An Azure AD subscription
* A 8x8 Virtual Office single-sign on (SSO) enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

    To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding 8x8 Virtual Office from the gallery
2. Configuring and testing Microsoft Azure AD SSO

## <a name="adding-8x8-virtual-office-from-the-gallery"></a>Adding 8x8 Virtual Office from the gallery
To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.

**To add 8x8 Virtual Office from the gallery, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **8x8 Virtual Office**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_01.png)
7. In the results pane, select **8x8 Virtual Office**, and then click **Complete** to add the application.
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_0001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configure and test Microsoft Azure AD SSO
The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with 8x8 Virtual Office based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 8x8 Virtual Office.

To configure and test Microsoft Azure AD SSO with 8x8 Virtual Office, you need to complete the following building blocks:

1. **[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.
3. **[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuring Microsoft Azure AD SSO
In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your 8x8 Virtual Office application.

**To configure Microsoft Azure AD Single Sign-On with 8x8 Virtual Office, perform the following steps:**

1. In the classic portal, on the **8x8 Virtual Office** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to 8x8 Virtual Office** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps and click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_04.png)
  1. In the **Reply URL** textbox, type: `https://sso.8x8.com/saml2`
  2. Click **Next**.
4. On the **Configure single sign-on at 8x8 Virtual Office** page, perform the following steps and click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_05.png)
  1. Click **Download certificate**, and then save the file on your computer.
  2. Click **Next**.
5. Sign-on to your 8x8 Virtual Office tenant as an administrator.
6. Select **Virtual Office Account Mgr** on Application Panel.
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)
7. Select **Business** account to manage and click **Sign In** button.
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)
8. Click **Accounts** tab in the menu list.
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)
9. Click **Single Sign On** in the list of Accounts.
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)
10. Select **Signle Sign On** under Authentication method and click **SAML**.
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)
11. Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office. 
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_007.png)
12. Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.
13. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
    
    ![Azure AD Single Sign-On][10]
14. On the **Single sign-on confirmation** page, click **Complete**.  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_09.png)
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png)
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png)
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_05.png)
  1. As Type Of User, select New user in your organization.
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_06.png)
  1. In the **First Name** textbox, type **Britta**.  
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_07.png)
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_08.png)
  1. Write down the value of the **New Password**.
  2. Click **Complete**.   

### <a name="create-a-8x8-virtual-office-test-user"></a>Create a 8x8 Virtual Office test user
The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office. 8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.

There is no action item for you in this section. A new user will be created during an attempt to access 8x8 Virtual Office if it doesn't exist yet. 

>[!NOTE]
>If you need to create an user manually, you need to contact the 8x8 Virtual Office support team. 
> 

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to 8x8 Virtual Office.

![Assign User][200]

**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201]
2. In the applications list, select **8x8 Virtual Office**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_50.png)
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.

When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.

## <a name="additional-resources"></a>Additional resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_205.png
































