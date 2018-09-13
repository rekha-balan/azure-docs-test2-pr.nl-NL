---
title: 'Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kantega SSO for FishEye/Crucible.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 833c469f70b60eb0a95e65af17956030eed6ee0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870079"
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a>Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible

In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).

Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible
- You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:

- An Azure AD subscription
- A Kantega SSO for FishEye/Crucible single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Kantega SSO for FishEye/Crucible from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a>Adding Kantega SSO for FishEye/Crucible from the gallery
To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.

**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

1. In the search box, type **Kantega SSO for FishEye/Crucible**.

    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

1. In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.

In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.

**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**

1. In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

1. In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    a. In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

1. In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > These values are not real. Update these values with the actual Identifier, Reply URL, and Sign-On URL. These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.

1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
1. In a different web browser window, log in to your FishEye/Crucible on-premises server as an administrator.

1. Hover on cog and click the **Add-ons**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon1.png)

1. Under System Settings section, click **Find new add-ons**. 

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/add-on2.png)

1. Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon2.png)

1. The plugin installation starts. 

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon33.png)

1. Once the installation is complete. Click **Close**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon34.png)

1.  Click **Manage**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon35.png)

1. Click **Configure** to configure the new plugin. 

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon3.png)

1. In the **SAML** section. Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon4.png)

1. Select subscription level as **Basic**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon5.png)

1. On the **App properties** section, perform following steps:

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon6.png)

    a. Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.

    b. Click **Next**.

1. On the **Metadata import** section, perform following steps:

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon7.png)

    a. Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.

    b. Click **Next**.

1. On the **Name and SSO location** section, perform following steps:

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon8.png)

    a. Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).

    b. Click **Next**.

1. Verify the Signing certificate and click **Next**.   

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon9.png)

1. On the **FishEye user accounts** section, perform following steps:

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon10.png)

    a. Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no. of groups separated by comma).

    b. Click **Next**.

1. Click **Finish**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon11.png)

1. On the **Known domains for Azure AD** section, perform following steps:  

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/addon12.png)

    a. Select **Known domains** from the left panel of the page.

    b. Enter domain name in the **Known domains** textbox.

    c. Click **Save**.  

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a>Creating a Kantega SSO for FishEye/Crucible test user

To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible. In Kantega SSO for FishEye/Crucible, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your Crucible on-premises server as an administrator.

1. Hover on cog and click the **Users**.

    ![Add Employee](./media/kantegassoforfisheyecrucible-tutorial/user1.png) 

1. Under **Users** tab section, click **Add user**.

    ![Add Employee](./media/kantegassoforfisheyecrucible-tutorial/user2.png)

1. On the **Add New User** dialog page, perform the following steps:

    ![Add Employee](./media/kantegassoforfisheyecrucible-tutorial/user3.png) 

    a. In the **Username** textbox, type the email of user like Brittasimon@contoso.com.
    
    b. In the **Display Name** textbox, type display name of the user like Britta Simon.
    
    c. In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.

    d. In the **Password** textbox, type the password of user.  

    e. In the **Confirm Password** textbox, reenter the password of user.

    f. Click **Add**.   

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.

![Assign User][200] 

**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Kantega SSO for FishEye/Crucible**.

    ![Configure Single Sign-On](./media/kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png
