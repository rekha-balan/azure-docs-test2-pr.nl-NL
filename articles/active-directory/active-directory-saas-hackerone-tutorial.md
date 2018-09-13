---
title: 'Tutorial: Azure Active Directory integration with HackerOne | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HackerOne.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: 4f6c7b09a7fcdf450163ac7ecd3113d4c4aac806
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660523"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>Tutorial: Azure Active Directory integration with HackerOne
In this tutorial, you integrate HackerOne with Azure Active Directory (Azure AD).

Integrating HackerOne with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to HackerOne
* You can enable your users to automatically get signed-on to HackerOne single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with HackerOne, you need the following items:

* An Azure subscription
* A HackerOne SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario Description
In this tutorial, you configure and test Azure AD single sign-on in a test environment.  

The scenario outlined in this tutorial consists of two main building blocks:

*  Adding HackerOne from the gallery
*  Configuring and testing Azure AD SSO

## <a name="add-hackerone-from-the-gallery"></a>Add HackerOne from the gallery
To integrate HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.

**To add HackerOne from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.

  ![Applications][4]
6. In the search box, type **HackerOne**.

  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_01.png)

7. In the results pane, select **HackerOne**, and then click **Complete** to add the application.

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on
Next, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.  
This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HackerOne.

To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD Single Sign-On
Next, you enable Azure AD single sign-on in the classic portal and to configure single sign-on in your HackerOne application.

As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure Azure AD single sign-on with HackerOne, perform the following steps:**

1. In the Azure classic portal, on the **HackerOne** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to HackerOne** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps and then click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_04.png) 
    1. In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HackerOne application using the following pattern: **“https://hackerone.com/\<company name\>/authentication”**. 
    2. Contact the HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to get your tenant URL if you don't know it.
    3. In the **Identifier** textbox, type the tenant URL. 
    4. Click **Next**.

4. On the **Configure single sign-on at HackerOne** page, perform the following steps and then click **Next**:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_05.png) 
    1. Click **Download certificate**, and then save the file on your computer.
    2. Click **Next**.
5. Sign-on to your HackerOne tenant as an administrator.
6. In the menu on the top, click the **Settings**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 
7. Navigate to "**Authentication**" and click "**Add SAML settings**".
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 
8. On the **SAML Settings** dialog, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 
    1. In the **Email Domain** textbox, type a registered domain.
    2. On the Azure classic portal, copy the **Single Sign-On Service URL**, and then paste it into the Single Sign On URL textbox.
    3. Create a **base-64 encoded** file from your downloaded certificate.  
    
       >[!TIP] 
       >For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).
       >
    4. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X509 Certificate** textbox.
    5. Click **Save**.
9. On the Authentication Settings dialog, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 
    1. Click **Run test**.
    2. If the value of the **Status** field equals **Last test status: created**, contact your HackerOne support team via [support@hackerone.com](mailto:support@hackerone.com) to request a review of your configuration.
10. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
11. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
Next, you create a test user in the classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a SECURE DELIVER test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_09.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_05.png) 
    1. As Type Of User, select New user in your organization.
    2. In the User Name **textbox**, type **BrittaSimon**.
    3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_06.png) 
   1. In the **First Name** textbox, type **Britta**.  
   2. In the **Last Name** textbox, type, **Simon**.
   3. In the **Display Name** textbox, type **Britta Simon**.
   4. In the **Role** list, select **User**.
   5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/create_aaduser_08.png) 
    1. Write down the value of the **New Password**.
    2. Click **Complete**.   

### <a name="create-a-hackerone-test-user"></a>Create a HackerOne test user
Next, you create a user called Britta Simon in HackerOne. HackerOne supports just-in-time provisioning, which is enabled by default.

There is no action item for you in this section. When you access HackerOne, a new user is created if it doesn't exist yet. [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>If you need to create a user manually, you need to contact the Certify support team. 
> 

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
Next, you enable Britta Simon to use Azure single sign-on by granting her access to HackerOne.

![Assign User][200] 

**To assign Britta Simon to HackerOne, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **HackerOne**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
Finally, you test your Azure AD single sign-on configuration using the Access Panel.  

When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hackerone-tutorial/tutorial_general_205.png




























