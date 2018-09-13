---
title: 'Tutorial: Azure Active Directory integration with Pantheon | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ede37f636104826b59240dc4660f1d8c4073aa58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662237"
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a>Tutorial: Azure Active Directory integration with Pantheon

In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).

Integrating Pantheon with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Pantheon
- You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Pantheon, you need the following items:

- An Azure AD subscription
- A Pantheon single-sign on enabled subscription


>[!NOTE] 
>To test the steps in this tutorial, we do not recommend using a production environment.


To test the steps in this tutorial, you should follow these recommendations:

- You should not use your production environment, unless this is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Pantheon from the gallery
2. Configuring and testing Azure AD single sign-on


## <a name="adding-pantheon-from-the-gallery"></a>Adding Pantheon from the gallery
To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.

**To add Pantheon from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.

    ![Active Directory][1]

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.

    ![Applications][2]

4. Click **Add** at the bottom of the page.

    ![Applications][3]

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.

    ![Applications][4]

6. In the search box, type **Pantheon**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_01.png)

7. In the results pane, select **Pantheon**, and then click **Complete** to add the application.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pantheon.

To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Pantheon application.


**To configure Azure AD single sign-on with Pantheon, perform the following steps:**

Pantheon application expects the SAML assertion in specific format, which requires you to set the NameIdentifier attribute value with the user’s email address. By default Azure AD uses the UserPrincipalName for NameIdentifier attribute. But for successful integration you need to adjust this value to match with user’s email address.
The integration will only work after doing the correct mapping.

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_06.png)
    
1. In the classic portal, on the **Pantheon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
     
    ![Configure Single Sign-On][6] 

2. On the **How would you like users to sign on to Pantheon** page, select **Azure AD Single Sign-On**, and then click **Next**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_03.png) 

3. On the **Configure App Settings** dialog page, perform the following steps:

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_04.png) 

    a. In the **Identifier** textbox, type the URN using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`
    
    b. In the **Reply URL** textbox, type the URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO` 

    c. click **Next**
 
4. On the **Configure single sign-on at Pantheon** page, perform the following steps:

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_05.png)

    a. Click **Download certificate**, and then save the file on your computer.

    b. Click **Next**.


5. To get SSO configured for your application, contact [Pantheon support](https://pantheon.io/docs/getting-support) team and provide them with the following information:

    • The downloaded **certificate**

    • The **Single Sign-On Service URL**

    >[!NOTE] 
    >You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection. You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)

6. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
    
    ![Azure AD Single Sign-On][10]

7. On the **Single sign-on confirmation** page, click **Complete**.  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
In this section, you create a test user in the classic portal called Britta Simon.


![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_09.png) 

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To display the list of users, in the menu on the top, click **Users**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

5. On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_05.png) 

    a. As Type Of User, select New user in your organization.

    b. In the User Name **textbox**, type **BrittaSimon**.

    c. Click **Next**.

6.  On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_06.png) 

    a. In the **First Name** textbox, type **Britta**.  

    b. In the **Last Name** textbox, type, **Simon**.

    c. In the **Display Name** textbox, type **Britta Simon**.

    d. In the **Role** list, select **User**.

    e. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_07.png) 

8. On the **Get temporary password** dialog page, perform the following steps:

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/create_aaduser_08.png) 

    a. Write down the value of the **New Password**.

    b. Click **Complete**.   



### <a name="creating-an-pantheon-test-user"></a>Creating an Pantheon test user

In this section, you create a user called Britta Simon in Pantheon. Please follow the below steps to add the user in Pantheon. 

>[!NOTE] 
>For SSO to work user need to be created first in Pantheon.

1. Login to Pantheon with admin credentials.

2. Navigate to **Organization** dashboard page.
 
3. Click **People**.

4. Click **Add user**.

5. Enter the user's email address.

6. Choose the user's role.

7. Click **Add user**.


### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pantheon.

![Assign User][200] 

**To assign Britta Simon to Pantheon, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.

    ![Assign User][201] 

2. In the applications list, select **Pantheon**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_50.png) 

3. In the menu on the top, click **Users**.

    ![Assign User][203]

4. In the Users list, select **Britta Simon**.

5. In the toolbar on the bottom, click **Assign**.

    ![Assign User][205]


### <a name="testing-single-sign-on"></a>Testing Single Sign-On

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.


## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-pantheon-tutorial/tutorial_general_205.png


























