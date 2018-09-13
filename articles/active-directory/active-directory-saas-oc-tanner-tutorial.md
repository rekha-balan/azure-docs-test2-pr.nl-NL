---
title: 'Tutorial: Azure Active Directory integration with O. C. Tanner - AppreciateHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and O. C. Tanner - AppreciateHub.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 002049d2baee1e38375b110a6993fdfc53fd52f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554677"
---
# <a name="tutorial-azure-active-directory-integration-with-o-c-tanner---appreciatehub"></a>Tutorial: Azure Active Directory integration with O. C. Tanner - AppreciateHub
The objective of this tutorial is to show you how to integrate O.C. Tanner - AppreciateHub with Azure Active Directory (Azure AD).  
Integrating O.C. Tanner - AppreciateHub with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to O.C. Tanner - AppreciateHub 
* You can enable your users to automatically get signed-on to O.C. Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with O.C. Tanner - AppreciateHub, you need the following items:

* An Azure AD subscription
* A O.C. Tanner - AppreciateHub single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.
> 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.  
The scenario outlined in this tutorial consists of three main building blocks:

1. Adding O.C. Tanner - AppreciateHub from the gallery 
2. Configuring and testing Azure AD single sign-on

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a>Adding O.C. Tanner - AppreciateHub from the gallery
To configure the integration of O.C. Tanner - AppreciateHub into Azure AD, you need to add O.C. Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.

**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1] 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2] 
4. Click **Add** at the bottom of the page.
   
    ![Applications][3] 
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4] 
6. In the search box, type **O.C. Tanner - AppreciateHub**.
   
    ![Applications][5] 
7. In the results pane, select **O.C. Tanner - AppreciateHub**, and then click **Complete** to add the application.
   
    ![Applications][25] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
The objective of this section is to show you how to configure and test Azure AD single sign-on with O.C. Tanner - AppreciateHub based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in O.C. Tanner - AppreciateHub to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in O.C. Tanner - AppreciateHub needs to be established.  
This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in O.C. Tanner - AppreciateHub.

To configure and test Azure AD single sign-on with O.C. Tanner - AppreciateHub, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in O.C. Tanner - AppreciateHub that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD Single Sign-On
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your O.C. Tanner - AppreciateHub application.

**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**

1. In the Azure classic portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6]
2. On the **How would you like users to sign on to O.C. Tanner - AppreciateHub** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Azure AD Single Sign-On][7]
3. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Configure App Settings][8]
   
     a. Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).
   
     b. Locate the **md:AssertionConsumerService** node. 
   
     c. Copy the value of the **Location** attribute. 
   
     ![Configure App Settings][12]
   
     d. In the **Sign On URL** textbox, past the value you have obtained in the previous step.
   
    > [!NOTE]
    > If you are expiriencing issues getting the Reply URL from the metadata file, contact the O.C. Tanner - AppreciateHub support team via [sso@octanner.com](mailto:sso@octanner.com).
    > 
    > 
   
    e. Click **Next**.

4. On the **Configure single sign-on at O.C. Tanner - AppreciateHub** page, click **Download metadata**, and then save the metadata file locally on your computer.
   
    ![What is Azure AD Connect][9]
5. Contact the O.C. Tanner - AppreciateHub support team via xyz, provide them with the metadata file, and them let them know that they should enable SSO for you.
6. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**. 
   
    ![What is Azure AD Connect][10]
7. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_05.png) 
   
    a. As Type Of User, select New user in your organization.
   
    b. In the User Name **textbox**, type **BrittaSimon**.
   
    c. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_06.png)
   
    a. In the **First Name** textbox, type **Britta**.  
   
    b. In the **Last Name** textbox, type, **Simon**.
   
    c. In the **Display Name** textbox, type **Britta Simon**.
   
    d. In the **Role** list, select **User**.
    e. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/create_aaduser_08.png) 
   
    a. Write down the value of the **New Password**.
   
    b. Click **Complete**.   

### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a>Creating a O.C. Tanner - AppreciateHub test user
The objective of this section is to create a user called Britta Simon in O.C. Tanner - AppreciateHub.

**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**

Ask your OC Tanner support team to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to O.C. Tanner - AppreciateHub.

![Assign User][200]

**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201]
2. In the applications list, select **O.C. Tanner - AppreciateHub**.
   
    ![Assign User][202]
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a>Testing Single Sign-On
The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.  
When you click the O.C. Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C. Tanner - AppreciateHub application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_01.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_25.png


[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_02.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_05.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_06.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_07.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-oc-tanner-tutorial/tutorial_general_205.png
































