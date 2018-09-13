---
title: 'Tutorial: Azure Active Directory integration with Trello | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trello.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: 0d6b955c035e028c1ab1bedaf9312900458cecc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563918"
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a>Tutorial: Azure Active Directory integration with Trello
In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).

Integrating Trello with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Trello
* You can enable your users to automatically get signed-on to Trello single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Trello, you need the following items:

* An Azure AD subscription
* A **Trello** single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.
> 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Trello from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="add-trello-from-the-gallery"></a>Add Trello from the gallery
To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.

**To add Trello from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]

4. Click **Add** at the bottom of the page.
   
    ![Applications][3]

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]

6. In the search box, type **Trello**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_01.png)

7. In the results pane, select **Trello**, and then click **Complete** to add the application.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_02.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trello. To configure and test Azure AD SSO with Trello, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Trello test user](#creating-a-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trello application.

Trello application expects the SAML assertions to contain specific attributes. Please configure the following attributes  for this application. You can manage the values of these attributes from the **"Atrributes"** tab of the application. The following screenshot shows an example for this.

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_03.png) 

**To configure Azure AD single sign-on with Trello, perform the following steps:**

1. In the Azure classic portal, on the **Trello** application integration page, in the menu on the top, click **Attributes**.
   
    ![Configure Single Sign-On][5]

2. On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:

    | Attribute Name | Attribute Value |
    | --- | --- |    
    | User.Email | user.mail |
    | User.FirstName | user.givenname |
    | User.LastName | user.surname |

   1. Click **add user attribute** to open the **Add User Attribure** dialog.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_05.png)
   2. In the **Attribute Name** textbox, type the attribute name shown for that row.
   3. From the **Attribute Value** list, select the value shown for that row.
   4. Click **Complete**. Then, **Apply Changes** at the bottom of the page.

1. In the menu on the top, click **Quick Start**.
   
    ![Configure Single Sign-On][6]

2. In the classic portal, on the **Trello** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][7] 

3. On the **How would you like users to sign on to Trello** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_06.png)

4. On the **Configure App Settings** dialog page, if you wish to configure the application in **IDP initiated mode**, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_07.png)

   1. In the Reply URL text box, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`
   2. Click **Next**.

    >[!NOTE]
    >You should get the **\<enterprise\>** slug from Trello. If you don't have the slug value, please contact Trello support team at <mailto:support@trello.com> to get the slug for you enterprise.
    > 
    > 

5. If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_08.png)
   
   1. In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`
   2. Click **Next**.

6. On the **Configure single sign-on at Trello** page, Click **Download certificate**, and then save the file on your computer.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_09.png)

7. To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send Trello team the Sign On URL and attach downloaded certificate.
8. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]

9. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
In this section, you create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_09.png) 

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_05.png) 
   
   1. As Type Of User, select New user in your organization.
   2. In the User Name **textbox**, type **BrittaSimon**.
   3. Click **Next**.

6. On the **User Profile** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_06.png) 
   
   1. In the **First Name** textbox, type **Britta**.  
   2. In the **Last Name** textbox, type, **Simon**.
   3. In the **Display Name** textbox, type **Britta Simon**.
   4. In the **Role** list, select **User**.
   5. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_07.png) 

8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/create_aaduser_08.png) 
   
   1. Write down the value of the **New Password**.
   2. Click **Complete**.   

### <a name="create-a-trello-test-user"></a>Create a Trello test user
In this section, you create a user called Britta Simon in Trello. In this section, you create a user called Britta Simon in Trello. Trello supports just-in-time provisioning and a new account will be created the first time you sign in from Azure AD.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Trello.

![Assign User][200] 

**To assign Britta Simon to Trello, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 

2. In the applications list, select **Trello**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_trello_10.png) 

3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 

4. In the All Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSO configuration using the Access Panel.

When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.

## <a name="additional-resources"></a>Additional resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-trello-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trello-tutorial/tutorial_general_205.png






























