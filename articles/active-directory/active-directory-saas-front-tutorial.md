---
title: 'Tutorial: Azure Active Directory integration with Front | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Front.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: jeedes
ms.openlocfilehash: f95cc2ea892ede1ed8894a3479218fb13729fa79
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550869"
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a>Tutorial: Azure Active Directory integration with Front
The objective of this tutorial is to show you how to integrate Front with Azure Active Directory (Azure AD).

Integrating Front with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Front
* You can enable your users to automatically get signed-on to Front single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Front, you need the following items:

* An Azure AD subscription
* A Front single-sign on (SSO) enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Front from the gallery
2. Configuring and testing Azure AD SSO

## <a name="adding-front-from-the-gallery"></a>Adding Front from the gallery
To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.

**To add Front from the gallery, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **Front**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_01.png)
7. In the results panel, select **Front**, and then click **Complete** to add the application.
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
The objective of this section is to show you how to configure and test Azure AD SSO with Front based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Front to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Front.

To configure and test Azure AD SSO with Front, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Front test user](#creating-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-sso"></a>Configuring Azure AD SSO
In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Front application.

**To configure Azure AD SSO with Front, perform the following steps:**

1. In the classic portal, on the **Front** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to Front** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_03.png)
3. On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_04.png)
  1. In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`.
  2. In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com/sso/saml/callback`
  3. Click **Next**.
4. If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_05.png)
   
  1. In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.frontapp.com`
  2. Click **Next**.
   
   >[!NOTE]
   >Please note that these are not the real values. You have to update these values with the actual Sign On URL, Identifier and Reply URL. To get these values, you can refer **step 12** for details or contact Front via [support@frontapp.com](emailTo:support@frontapp.com).
   >  
5. On the **Configure single sign-on at Front** page, perform the following steps and click **Next**:
   
 ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_06.png) 
 1. Click **Download certificate**, and then save the file on your computer.
 2. Click **Next**.
6. Sign-on to your Front tenant as an administrator.
7. Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_000.png)
8. Click **Single Sign On** link.
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_001.png)
9. Select **SAML** in the drop down list of **Single Sign On**.
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_002.png)
10. In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_003.png)
11. Copy the content of the downloaded certificate file, and then paste it into the **Signing certificate** textbox.
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_004.png)
12. Confirm these URls match your configuration in step 3.
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_005.png)
13. Click **Save** button.
14. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
    
    ![Azure AD Single Sign-On][10]
15. On the **Single sign-on confirmation** page, click **Complete**.  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_09.png)
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_03.png)
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_04.png)
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_05.png)
 1. As Type Of User, select New user in your organization.
 2. In the User Name **textbox**, type **BrittaSimon**. 
 3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_06.png) 
 1. In the **First Name** textbox, type **Britta**.   
 2. In the **Last Name** textbox, type, **Simon**. 
 3. In the **Display Name** textbox, type **Britta Simon**. 
 4. In the **Role** list, select **User**. 
 5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_07.png)
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/create_aaduser_08.png) 
 1. Write down the value of the **New Password**. 
 2. Click **Complete**.   

### <a name="create-a-front-test-user"></a>Create a Front test user
The objective of this section is to create a user called Britta Simon in Front.Please work with your Front support team to add the users in the Front account.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Front.

![Assign User][200]

**To assign Britta Simon to Front, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201]
2. In the applications list, select **Front**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_front_50.png)
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.

When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.

## <a name="additional-resources"></a>Additional resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-front-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-front-tutorial/tutorial_general_205.png
































