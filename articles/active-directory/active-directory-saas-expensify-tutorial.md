---
title: 'Tutorial: Azure Active Directory integration with Expensify | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Expensify.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 5e73c5d52e47ca37f9851ae1c82cd8ab82d0e2ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661534"
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a>Tutorial: Azure Active Directory integration with Expensify
In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).

Integrating Expensify with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Expensify
* You can enable your users to automatically get signed-on to Expensify single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Expensify, you need the following items:

* An Azure AD subscription
* An Expensify SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment.
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario Description
In this tutorial, you test Azure AD SSO in a test environment. 

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Expensify from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-expensify-from-the-gallery"></a>Adding Expensify from the gallery
To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.

**To add Expensify from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **Expensify**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_01.png)
7. In the results pane, select **Expensify**, and then click **Complete** to add the application.

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.  

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Expensify.

To configure and test Azure AD SSO with Expensify, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-sso"></a>Configure Azure AD SSO
In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Expensify application.

**To configure Azure AD SSO with Expensify, perform the following steps:**

1. In the classic portal, on the **Expensify** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to Expensify** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_04.png) 
  1. In the Sign On URL textbox, type the URL used by your users to sign-on to your Expensify application using the following pattern: **“https://www.expensify.com/authentication/saml/login”**.
4. On the **Configure single sign-on at Expensify** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_05.png)   
  1. Click **Download metadata**, and then save the file on your computer.
  2. Click **Next**.
5. To enable SSO in Expensify you first need to enable **Domain Control** in the application. You can enable Domain Control in the application. The steps are listed [here](http://help.expensify.com/domain-control). For additional support, you can contact the Expensify support via [help@expensify.com](mailto:help@expensify.com). Once you have Domain Control enabled, follow these steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png) 
  1. Sign on to your Expensify application.
  2. In the toolbar on the top, click **Admin**.
  3. In the left panel, click **Domain Control**.
  4. Click your verified domain name.
  5. In the left panel, click **SAML**, and then select **Enabled**.
  6. Open the downloaded Federation Metadata from Azure AD, copy the content, and then paste it into the **Identity Provider Metadata** textbox.
6. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
7. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
In this section, you create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_09.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_05.png) 
  1. As Type Of User, select New user in your organization.
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_06.png) 
  1. In the **First Name** textbox, type **Britta**.  
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_08.png) 
  1. Write down the value of the **New Password**.
  2. Click **Complete**.   

### <a name="create-an-expensify-test-user"></a>Create an Expensify test user
In this section, you create a user called Britta Simon in Expensify. Please work with Expensify support team to add the users in the Expensify platform.

>[!NOTE]
>If you need to create a user manually, you need to contact the Expensify support team. 
> 

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Expensify.

![Assign User][200] 

**To assign Britta Simon to Expensify, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **Expensify**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
In this section, you test your Azure AD single sign-on configuration using the Access Panel.  

When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_205.png

























