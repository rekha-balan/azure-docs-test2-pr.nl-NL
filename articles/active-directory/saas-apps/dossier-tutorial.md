---
title: 'Tutorial: Azure Active Directory integration with Dossier | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dossier.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7a5fec92-9c01-4ced-99b2-a10e28fc028e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2018
ms.author: jeedes
ms.openlocfilehash: 932a832d4717a788f2d9adfd98ce1ba0c4ca07a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867116"
---
# <a name="tutorial-azure-active-directory-integration-with-dossier"></a>Tutorial: Azure Active Directory integration with Dossier

In this tutorial, you learn how to integrate Dossier with Azure Active Directory (Azure AD).

Integrating Dossier with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Dossier.
- You can enable your users to automatically get signed-on to Dossier (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Dossier, you need the following items:

- An Azure AD subscription
- A Dossier single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description

In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Dossier from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-dossier-from-the-gallery"></a>Adding Dossier from the gallery

To configure the integration of Dossier into Azure AD, you need to add Dossier from the gallery to your list of managed SaaS apps.

**To add Dossier from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.

    ![The Azure Active Directory button][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![The Enterprise applications blade][2]

3. To add new application, click **New application** button on the top of dialog.

    ![The New application button][3]

4. In the search box, type **Dossier**, select **Dossier** from result panel then click **Add** button to add the application.

    ![Dossier in the results list](./media/dossier-tutorial/tutorial_dossier_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Dossier based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Dossier is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Dossier needs to be established.

To configure and test Azure AD single sign-on with Dossier, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Create a Dossier test user](#create-a-dossier-test-user)** - to have a counterpart of Britta Simon in Dossier that is linked to the Azure AD representation of user.
4. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dossier application.

**To configure Azure AD single sign-on with Dossier, perform the following steps:**

1. In the Azure portal, on the **Dossier** application integration page, click **Single sign-on**.

    ![Configure single sign-on link][4]

2. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.

    ![Single sign-on dialog box](./media/dossier-tutorial/tutorial_dossier_samlbase.png)

3. On the **Dossier Domain and URLs** section, perform the following steps:

    ![Dossier Domain and URLs single sign-on information](./media/dossier-tutorial/tutorial_dossier_url1.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern:
    
    | | |
    |-|-|
    | `https://<SUBDOMAIN>.dossiersystems.com/azuresso/account/SignIn`|
    | `https://dossier.<CLIENTDOMAINNAME>/azuresso/account/SignIn`|
    | |

    b. In the **Identifier** textbox, type a URL using the following pattern: `Dossier/<CLIENTNAME>`

    > [!NOTE]
    > For identifier value it should be in the format of `Dossier/<CLIENTNAME>` or any user personalized value.

    c. In the **Reply URL** textbox, type a URL using the following pattern:
    | | |
    |-|-|
    |  `https://<SUBDOMAIN>.dossiersystems.com/azuresso`|
    | `https://dossier.<CLIENTDOMAINNAME>/azuresso`|
    | |

    > [!NOTE]
    > These values are not real. Update these values with the actual Identifier, Reply URL, and Sign-On URL. Contact [Dossier Client support team](mailto:support@intellimedia.ca) to get these values.

4. On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.

    ![The Certificate download link](./media/dossier-tutorial/tutorial_dossier_certificate.png) 

6. Click **Save** button.

    ![Configure Single Sign-On Save button](./media/dossier-tutorial/tutorial_general_400.png)

7. To configure single sign-on on **Dossier** side, you need to send the **App Federation Metadata Url** to [Dossier support team](mailto:support@intellimedia.ca). They set this setting to have the SAML SSO connection set properly on both sides.

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/dossier-tutorial/create_aaduser_01.png)

2. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/dossier-tutorial/create_aaduser_02.png)

3. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/dossier-tutorial/create_aaduser_03.png)

4. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/dossier-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.

### <a name="create-a-dossier-test-user"></a>Create a Dossier test user

In this section, you create a user called Britta Simon in Dossier. Work with [Dossier support team](mailto:support@intellimedia.ca) to add the users in the Dossier platform. Users must be created and activated before you use single sign-on.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dossier.

![Assign the user role][200] 

**To assign Britta Simon to Dossier, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Dossier**.

    ![The Dossier link in the Applications list](./media/dossier-tutorial/tutorial_dossier_app.png)  

3. In the menu on the left, click **Users and groups**.

    ![The "Users and groups" link][202]

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![The Add Assignment pane][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.

### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Dossier tile in the Access Panel, you should get automatically signed-on to your Dossier application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/dossier-tutorial/tutorial_general_01.png
[2]: ./media/dossier-tutorial/tutorial_general_02.png
[3]: ./media/dossier-tutorial/tutorial_general_03.png
[4]: ./media/dossier-tutorial/tutorial_general_04.png

[100]: ./media/dossier-tutorial/tutorial_general_100.png

[200]: ./media/dossier-tutorial/tutorial_general_200.png
[201]: ./media/dossier-tutorial/tutorial_general_201.png
[202]: ./media/dossier-tutorial/tutorial_general_202.png
[203]: ./media/dossier-tutorial/tutorial_general_203.png

