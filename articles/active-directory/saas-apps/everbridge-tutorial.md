---
title: 'Tutorial: Azure Active Directory integration with EverBridge | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EverBridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 283379131b02f4ea115052f051ef0114efab1997
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865194"
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>Tutorial: Azure Active Directory integration with EverBridge

In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).

Integrating EverBridge with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to EverBridge
- You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with EverBridge, you need the following items:

- An Azure AD subscription
- An EverBridge single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding EverBridge from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-everbridge-from-the-gallery"></a>Adding EverBridge from the gallery
To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.

**To add EverBridge from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

1. In the search box, type **EverBridge**.

    ![Creating an Azure AD test user](./media/everbridge-tutorial/tutorial_everbridge_search.png)

1. In the results panel, select **EverBridge**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.

In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.

**To configure Azure AD single sign-on with EverBridge, perform the following steps:**

1. In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_samlbase.png)

1. On the **EverBridge Domain and URLs** section, perform the following steps:

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_url.png)

    a. In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`

    > [!NOTE] 
    > These values are not real. Update these values with the actual Identifier and Reply URL. Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.
 
1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_general_400.png)

1. On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window. Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_configure.png) 

1. To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.

1. In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.
   
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_002.png)
   
    a. In the **Name** textbox, type the name of Identifier Provider (for example: your company name).
   
    b. In the **API Name** textbox, type the name of API.
   
    c. Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.
   
    d. In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.
   
    e. In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.
   
    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_003.png)
   
    f. In the Service Provider Initiated Request Binding, select **HTTP Redirect**.

    g. Click **Save**

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/everbridge-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-an-everbridge-test-user"></a>Creating an EverBridge test user

In this section, you create a user called Britta Simon in Everbridge. Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.

![Assign User][200] 

**To assign Britta Simon to EverBridge, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **EverBridge**.

    ![Configure Single Sign-On](./media/everbridge-tutorial/tutorial_everbridge_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.

When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/everbridge-tutorial/tutorial_general_01.png
[2]: ./media/everbridge-tutorial/tutorial_general_02.png
[3]: ./media/everbridge-tutorial/tutorial_general_03.png
[4]: ./media/everbridge-tutorial/tutorial_general_04.png

[100]: ./media/everbridge-tutorial/tutorial_general_100.png

[200]: ./media/everbridge-tutorial/tutorial_general_200.png
[201]: ./media/everbridge-tutorial/tutorial_general_201.png
[202]: ./media/everbridge-tutorial/tutorial_general_202.png
[203]: ./media/everbridge-tutorial/tutorial_general_203.png
