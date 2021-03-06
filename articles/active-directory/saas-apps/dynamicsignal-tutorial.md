---
title: 'Tutorial: Azure Active Directory integration with Dynamic Signal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dynamic Signal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 863f7340-b065-4f59-b092-daa67da6f703
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2018
ms.author: jeedes
ms.openlocfilehash: 2ca787be6d3697c84b8eeef637af8a14b190b428
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965544"
---
# <a name="tutorial-azure-active-directory-integration-with-dynamic-signal"></a>Tutorial: Azure Active Directory integration with Dynamic Signal

In this tutorial, you learn how to integrate Dynamic Signal with Azure Active Directory (Azure AD).

Integrating Dynamic Signal with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Dynamic Signal.
- You can enable your users to automatically get signed-on to Dynamic Signal (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Dynamic Signal, you need the following items:

- An Azure AD subscription
- A Dynamic Signal single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Dynamic Signal from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-dynamic-signal-from-the-gallery"></a>Adding Dynamic Signal from the gallery
To configure the integration of Dynamic Signal into Azure AD, you need to add Dynamic Signal from the gallery to your list of managed SaaS apps.

**To add Dynamic Signal from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![The Azure Active Directory button][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![The Enterprise applications blade][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![The New application button][3]

1. In the search box, type **Dynamic Signal**, select **Dynamic Signal** from result panel then click **Add** button to add the application.

    ![Dynamic Signal in the results list](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Dynamic Signal based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Dynamic Signal is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Dynamic Signal needs to be established.

To configure and test Azure AD single sign-on with Dynamic Signal, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Create a Dynamic Signal test user](#create-a-dynamic-signal-test-user)** - to have a counterpart of Britta Simon in Dynamic Signal that is linked to the Azure AD representation of user.
1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dynamic Signal application.

**To configure Azure AD single sign-on with Dynamic Signal, perform the following steps:**

1. In the Azure portal, on the **Dynamic Signal** application integration page, click **Single sign-on**.

    ![Configure single sign-on link][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Single sign-on dialog box](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_samlbase.png)

1. On the **Dynamic Signal Domain and URLs** section, perform the following steps:
 
    ![Dynamic Signal Domain and URLs single sign-on information](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`

    b. In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com`

    c. In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.voicestorm.com/User/SsoResponse`

    > [!NOTE] 
    > These values are not real. Update these values with the actual Identifier, Reply URL, and Sign-On URL. Contact [Dynamic Signal Client support team](mailto:support@dynamicsignal.com) to get these values. 

1. On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.

    ![The Certificate download link](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On Save button](./media/dynamicsignal-tutorial/tutorial_general_400.png)
    
1. On the **Dynamic Signal Configuration** section, click **Configure Dynamic Signal** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Dynamic Signal Configuration](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_configure.png) 

1. To configure single sign-on on **Dynamic Signal** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Dynamic Signal support team](mailto:support@dynamicsignal.com). They set this setting to have the SAML SSO connection set properly on both sides.

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/dynamicsignal-tutorial/create_aaduser_01.png)

1. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/dynamicsignal-tutorial/create_aaduser_02.png)

1. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/dynamicsignal-tutorial/create_aaduser_03.png)

1. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/dynamicsignal-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### <a name="create-a-dynamic-signal-test-user"></a>Create a Dynamic Signal test user

The objective of this section is to create a user called Britta Simon in Dynamic Signal. Dynamic Signal supports just-in-time provisioning, which is by default enabled. There is no action item for you in this section. A new user is created during an attempt to access Dynamic Signal if it doesn't exist yet.

>[!Note]
>If you need to create a user manually, contact [Dynamic Signal support team](mailto:support@dynamicsignal.com).

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dynamic Signal.

![Assign the user role][200] 

**To assign Britta Simon to Dynamic Signal, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Dynamic Signal**.

    ![The Dynamic Signal link in the Applications list](./media/dynamicsignal-tutorial/tutorial_dynamicsignal_app.png)  

1. In the menu on the left, click **Users and groups**.

    ![The "Users and groups" link][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![The Add Assignment pane][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Dynamic Signal tile in the Access Panel, you should get automatically signed-on to your Dynamic Signal application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dynamicsignal-tutorial/tutorial_general_01.png
[2]: ./media/dynamicsignal-tutorial/tutorial_general_02.png
[3]: ./media/dynamicsignal-tutorial/tutorial_general_03.png
[4]: ./media/dynamicsignal-tutorial/tutorial_general_04.png

[100]: ./media/dynamicsignal-tutorial/tutorial_general_100.png

[200]: ./media/dynamicsignal-tutorial/tutorial_general_200.png
[201]: ./media/dynamicsignal-tutorial/tutorial_general_201.png
[202]: ./media/dynamicsignal-tutorial/tutorial_general_202.png
[203]: ./media/dynamicsignal-tutorial/tutorial_general_203.png

