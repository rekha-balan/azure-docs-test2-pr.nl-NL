---
title: 'Tutorial: Azure Active Directory integration with Teamwork | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Teamwork.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 8d24759e1cfb6c12a5c705eb1316e11bf4253a28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550101"
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a>Tutorial: Azure Active Directory integration with Teamwork

In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).

Integrating Teamwork with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Teamwork
- You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure Management portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Teamwork, you need the following items:

- An Azure AD subscription
- A Teamwork single-sign on enabled subscription


> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.


To test the steps in this tutorial, you should follow these recommendations:

- You should not use your production environment, unless this is necessary.
- If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Teamwork from the gallery
2. Configuring and testing Azure AD single sign-on


## <a name="adding-teamwork-from-the-gallery"></a>Adding Teamwork from the gallery
To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.

**To add Teamwork from the gallery, perform the following steps:**

1. In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
3. Click **Add** button on the top of the dialog.

    ![Applications][3]

4. In the search box, type **Teamwork**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. In the results panel, select **Teamwork**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.

To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.

**To configure Azure AD single sign-on with Teamwork, perform the following steps:**

1. In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

2. On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > Please note that this is not the real value. You have to update this value with the actual Sign On URL. Contact [Teamwork support team](mailto:support@teamwork.com) to get this value. 

4. On the **SAML Signing Certificate** section, click **Create new certificate**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)  

5. On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**. Then click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. On the pop-up **Rollover certificate** window, click **OK**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.
  

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure Management portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. Go to **Users and groups** and click **All users** to display the list of users.
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. At the top of the dialog click **Add** to open the **User** dialog.
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**. 



### <a name="creating-a-teamwork-test-user"></a>Creating a Teamwork test user

In this section, you create a user called Britta Simon in Teamwork. Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.


### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.

![Assign User][200] 

**To assign Britta Simon to Teamwork, perform the following steps:**

1. In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Teamwork**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    


### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.


## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png






















