---
title: 'Tutorial: Azure Active Directory integration with Hackerone | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Hackerone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 4e33ad66fe0ced9a426a608f4193ff52dec4f7ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866619"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>Tutorial: Azure Active Directory integration with HackerOne

In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).

Integrating HackerOne with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to HackerOne
- You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with HackerOne, you need the following items:

- An Azure AD subscription
- A HackerOne single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding HackerOne from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-hackerone-from-the-gallery"></a>Adding HackerOne from the gallery
To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.

**To add HackerOne from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

1. In the search box, type **HackerOne**.

    ![Creating an Azure AD test user](./media/hackerone-tutorial/tutorial_hackerone_search.png)

1. In the results panel, select **HackerOne**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."

For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.

In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.

**To configure Azure AD single sign-on with HackerOne, perform the following steps:**

1. In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_samlbase.png)

1. On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`

    b. In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`
    
    > [!NOTE] 
    > This value is not real. Update this value with the actual Sign-On URL. Contact [HackerOne support team](mailto:support@hackerone.com) to get this value. 
 
1. On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_general_400.png)

1. On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window. Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_configure.png) 

1. Sign On to your HackerOne tenant as an administrator.

1. In the menu on the top, click the "**Settings**."
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_001.png) 

1. Navigate to "**Authentication**" and click "**Add SAML settings**."
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_003.png) 

1. On the **SAML Settings** dialog, perform the following steps:
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_004.png) 

    a. In the **Email Domain** textbox, type a registered domain.

    b. In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.

    c. Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.
    
    d. Click **Save**.

1. On the Authentication Settings dialog, perform the following steps:
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_005.png) 

    a. Click **Run test**.

    b. If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/hackerone-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-a-hackerone-test-user"></a>Creating a HackerOne test user

Next, you create a user called Britta Simon in HackerOne. HackerOne supports just-in-time provisioning, which is enabled by default.

There is no action item for you in this section. When you access HackerOne, a new user is created if it doesn't exist yet.

>[!NOTE]
>If you need to create a user manually, you need to contact the Certify support team. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.

![Assign User][200] 

**To assign Britta Simon to HackerOne, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **HackerOne**.

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

Finally, you test your Azure AD single sign-on configuration using the Access Panel.  

When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hackerone-tutorial/tutorial_general_01.png
[2]: ./media/hackerone-tutorial/tutorial_general_02.png
[3]: ./media/hackerone-tutorial/tutorial_general_03.png
[4]: ./media/hackerone-tutorial/tutorial_general_04.png

[100]: ./media/hackerone-tutorial/tutorial_general_100.png

[200]: ./media/hackerone-tutorial/tutorial_general_200.png
[201]: ./media/hackerone-tutorial/tutorial_general_201.png
[202]: ./media/hackerone-tutorial/tutorial_general_202.png
[203]: ./media/hackerone-tutorial/tutorial_general_203.png
