---
title: 'Tutorial: Azure Active Directory integration with Aravo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Aravo.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d86c0602b85dc24399446355f9b070c4b440b586
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563898"
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a>Tutorial: Azure Active Directory integration with Aravo
The objective of this tutorial is to show you how to integrate Aravo with Azure Active Directory (Azure AD).

Integrating Aravo with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Aravo
* You can enable your users to automatically get signed-on to Aravo single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Aravo, you need the following items:

* An Azure AD subscription
* A Aravo SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Aravo from the gallery
2. Configuring and testing Microsoft Azure AD SSO

## <a name="add-aravo-from-the-gallery"></a>Add Aravo from the gallery
To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.

**To add Aravo from the gallery, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **Aravo**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_01.png)
7. In the results pane, select **Aravo**, and then click **Complete** to add the application.
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_0001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configure and test Microsoft Azure AD SSO
The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Aravo based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Aravo to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Aravo.

To configure and test Microsoft Azure AD SSO with Aravo, you need to complete the following building blocks:

1. **[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.
3. **[Creating a Aravo test user](#creating-a-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-microsoft-azure-ad-sso"></a>Configure Microsoft Azure AD SSO
In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your Aravo application.

**To configure Microsoft Azure AD SSO with Aravo, perform the following steps:**

1. In the classic portal, on the **Aravo** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to Aravo** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps and click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_04.png)
  1. In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.aravo.com`
  2. In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.aravo.com/aems/login.do`
  3. Click **Next**.
   
    >[!NOTE]
    >Please note that these are not the real value. You have to update the values with the actual Identifier and Reply URL. To get these values, contact Aravo. 
    > 
4. On the **Configure single sign-on at Aravo** page, perform the following steps and click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_05.png)
  1. Click **Download certificate**, and then save the file on your computer. 
  2. Click **Next**.
5. To get SSO configured for your application, contact your Aravo support team and provide them with the following: 
 
  *  The **Downloaded certificate** file
  *  The **Issuer URL** 
  *  The **SAML SSO URL**
  *  The **single sign-out Service URL**
6. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
7. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_09.png)
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_03.png)
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_04.png)
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_05.png)
  1. As Type Of User, select New user in your organization.
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_06.png)
  1. In the **First Name** textbox, type **Britta**. 
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_07.png)
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/create_aaduser_08.png)
  1. Write down the value of the **New Password**. 
  2. Click **Complete**.   

### <a name="create-a-aravo-test-user"></a>Create a Aravo test user
The objective of this section is to create a user called Britta Simon in Aravo.Please work with Aravo support team to add the users in the Aravo account.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Aravo.

![Assign User][200]

**To assign Britta Simon to Aravo, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201]
2. In the applications list, select **Aravo**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_aravo_50.png)
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.

When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.

## <a name="additional-resources"></a>Additional resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-aravo-tutorial/tutorial_general_205.png

























