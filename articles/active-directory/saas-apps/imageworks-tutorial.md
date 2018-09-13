---
title: 'Tutorial: Azure Active Directory integration with IMAGE WORKS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IMAGE WORKS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 635d86a1-b512-442d-8851-3b18ec1a24a5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2017
ms.author: jeedes
ms.openlocfilehash: 5d0ee49bf2a792e855ed020eba74db1d15278fad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867390"
---
# <a name="tutorial-azure-active-directory-integration-with-image-works"></a>Tutorial: Azure Active Directory integration with IMAGE WORKS

In this tutorial, you learn how to integrate IMAGE WORKS with Azure Active Directory (Azure AD).

Integrating IMAGE WORKS with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to IMAGE WORKS.
- You can enable your users to automatically get signed-on to IMAGE WORKS (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with IMAGE WORKS, you need the following items:

- An Azure AD subscription
- A IMAGE WORKS single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding IMAGE WORKS from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-image-works-from-the-gallery"></a>Adding IMAGE WORKS from the gallery
To configure the integration of IMAGE WORKS into Azure AD, you need to add IMAGE WORKS from the gallery to your list of managed SaaS apps.

**To add IMAGE WORKS from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![The Azure Active Directory button][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![The Enterprise applications blade][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![The New application button][3]

1. In the search box, type **IMAGE WORKS**, select **IMAGE WORKS** from result panel then click **Add** button to add the application.

    ![IMAGE WORKS in the results list](./media/imageworks-tutorial/tutorial_imageworks_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with IMAGE WORKS based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in IMAGE WORKS is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in IMAGE WORKS needs to be established.

In IMAGE WORKS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with IMAGE WORKS, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Create a IMAGE WORKS test user](#create-a-image-works-test-user)** - to have a counterpart of Britta Simon in IMAGE WORKS that is linked to the Azure AD representation of user.
1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IMAGE WORKS application.

**To configure Azure AD single sign-on with IMAGE WORKS, perform the following steps:**

1. In the Azure portal, on the **IMAGE WORKS** application integration page, click **Single sign-on**.

    ![Configure single sign-on link][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Single sign-on dialog box](./media/imageworks-tutorial/tutorial_imageworks_samlbase.png)

1. On the **IMAGE WORKS Domain and URLs** section, perform the following steps:

    ![IMAGE WORKS Domain and URLs single sign-on information](./media/imageworks-tutorial/tutorial_imageworks_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://i-imageworks.jp/iw/<tenantName>/sso/Login.do`

    b. In the **Identifier** textbox, type a URL using the following pattern: `https://sp.i-imageworks.jp/iw/<tenantName>/postResponse`

    > [!NOTE] 
    > These values are not real. Update these values with the actual Sign-On URL and Identifier. Contact [IMAGE WORKS Client support team](mailto:iw-sd-support@fujifilm.com) to get these values. 
 
1. On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.

    ![The Certificate download link](./media/imageworks-tutorial/tutorial_imageworks_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On Save button](./media/imageworks-tutorial/tutorial_general_400.png)

1. On the **IMAGE WORKS Configuration** section, click **Configure IMAGE WORKS** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![IMAGE WORKS Configuration](./media/imageworks-tutorial/tutorial_imageworks_configure.png) 

1. To configure single sign-on on **IMAGE WORKS** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID and SAML Single Sign-On Service URL** to [IMAGE WORKS support team](mailto:iw-sd-support@fujifilm.com). They set this setting to have the SAML SSO connection set properly on both sides.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/imageworks-tutorial/create_aaduser_01.png)

1. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/imageworks-tutorial/create_aaduser_02.png)

1. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/imageworks-tutorial/create_aaduser_03.png)

1. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/imageworks-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### <a name="create-a-image-works-test-user"></a>Create a IMAGE WORKS test user

In this section, you create a user called Britta Simon in IMAGE WORKS. Work with [IMAGE WORKS support team](mailto:iw-sd-support@fujifilm.com) to add the users in the IMAGE WORKS platform. Users must be created and activated before you use single sign-on.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to IMAGE WORKS.

![Assign the user role][200] 

**To assign Britta Simon to IMAGE WORKS, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **IMAGE WORKS**.

    ![The IMAGE WORKS link in the Applications list](./media/imageworks-tutorial/tutorial_imageworks_app.png)  

1. In the menu on the left, click **Users and groups**.

    ![The "Users and groups" link][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![The Add Assignment pane][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the IMAGE WORKS tile in the Access Panel, you should get automatically signed-on to your IMAGE WORKS application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/imageworks-tutorial/tutorial_general_01.png
[2]: ./media/imageworks-tutorial/tutorial_general_02.png
[3]: ./media/imageworks-tutorial/tutorial_general_03.png
[4]: ./media/imageworks-tutorial/tutorial_general_04.png

[100]: ./media/imageworks-tutorial/tutorial_general_100.png

[200]: ./media/imageworks-tutorial/tutorial_general_200.png
[201]: ./media/imageworks-tutorial/tutorial_general_201.png
[202]: ./media/imageworks-tutorial/tutorial_general_202.png
[203]: ./media/imageworks-tutorial/tutorial_general_203.png
