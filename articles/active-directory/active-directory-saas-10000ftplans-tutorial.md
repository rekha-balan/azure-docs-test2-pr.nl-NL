---
title: 'Tutorial: Azure Active Directory integration with 10,000ft Plans | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 10,000ft Plans.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 6820b3f00412e0ee87701d1b7e5547c1cb84da5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550156"
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a>Tutorial: Azure Active Directory integration with 10,000ft Plans
The objective of this tutorial is to show you how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).  
Integrating 10,000ft Plans with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to 10,000ft Plans
* You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with 10,000ft Plans, you need the following items:

* An Azure AD subscription
* A 10,000ft Plans single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.
> 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.  
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding 10,000ft Plans from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-10000ft-plans-from-the-gallery"></a>Adding 10,000ft Plans from the gallery
To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.

**To add 10,000ft Plans from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **10,000ft Plans**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_01.png)
7. In the results pane, select **10,000ft Plans**, and then click **Complete** to add the application.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
The objective of this section is to show you how to configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.  
This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 10,000ft Plans.

To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your 10,000ft Plans application.

**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**

1. In the Azure classic portal, on the **10,000ft Plans** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to 10,000ft Plans** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_04.png) 

    a. In the **Sign On URL** textbox, type `https://app.10000ft.com`.

    b. In the **Identifier** textbox, type `https://app.10000ft.com/saml/metadata`.

    > [!NOTE] 
    > The value for **Identifier** is different if you have a custom domain. If you need assistance, contact your [10,000ft Plans support team](mailto:support@10000ft.com).  

    c. Click **Next**


1. On the **Configure single sign-on at 10,000ft Plans** page, perform the following steps and then click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_05.png) 
   
    a. Click **Download certificate**, and then save the file on your computer.
   
    b. Click **Next**.
2. To get SSO configured for your application, contact your [10,000ft Plans support team](mailto:support@10000ft.com), attach the downloaded certificate and provide them with the Issuer URL, the SAML SSO URL and the Sign Out URL.
3. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
4. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_09.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_05.png) 
   
    a. As Type Of User, select New user in your organization.
   
    b. In the User Name **textbox**, type **BrittaSimon**.
   
    c. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_06.png) 
   
    a. In the **First Name** textbox, type **Britta**.  
   
    b. In the **Last Name** textbox, type, **Simon**.
   
    c. In the **Display Name** textbox, type **Britta Simon**.
   
    d. In the **Role** list, select **User**.
   
    e. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/create_aaduser_08.png) 
   
    a. Write down the value of the **New Password**.
   
    b. Click **Complete**.   

### <a name="creating-a-10000ft-plans-test-user"></a>Creating a 10,000ft Plans test user
The objective of this section is to create a user called Britta Simon in 10,000ft Plans. 10,000ft Plans supports just-in-time provisioning, which is by default enabled.

There is no action item for you in this section. A new user will be created during an attempt to access 10,000ft Plans if it doesn't exist yet. 

> [!NOTE]
> If you need to create an user manually, you need to contact the Certify support team.
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to 10,000ft Plans.

![Assign User][200] 

**To assign Britta Simon to 10,000ft Plans, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **10,000ft Plans**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_10000ftplans_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a>Testing single sign-on
The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.  
When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.

## <a name="additional-resources"></a>Additional resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-10000ftplans-tutorial/tutorial_general_205.png

























