---
title: 'Tutorial: Azure Active Directory integration with Amplitude | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Amplitude.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 496c9ffa-c833-41fa-8d17-2dc3044954d1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: jeedes
ms.openlocfilehash: a2815b60799f98071915a0f06908fd92ff3fb2f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869998"
---
# <a name="tutorial-azure-active-directory-integration-with-amplitude"></a>Tutorial: Azure Active Directory integration with Amplitude

In this tutorial, you learn how to integrate Amplitude with Azure Active Directory (Azure AD).

Integrating Amplitude with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Amplitude.
- You can enable your users to automatically get signed-on to Amplitude (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Amplitude, you need the following items:

- An Azure AD subscription
- An Amplitude single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Amplitude from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-amplitude-from-the-gallery"></a>Adding Amplitude from the gallery
To configure the integration of Amplitude into Azure AD, you need to add Amplitude from the gallery to your list of managed SaaS apps.

**To add Amplitude from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![The Azure Active Directory button][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![The Enterprise applications blade][2]
    
3. To add new application, click **New application** button on the top of dialog.

    ![The New application button][3]

4. In the search box, type **Amplitude**, select **Amplitude** from result panel then click **Add** button to add the application.

    ![Amplitude in the results list](./media/amplitude-tutorial/tutorial_amplitude_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Amplitude based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Amplitude is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Amplitude needs to be established.

To configure and test Azure AD single sign-on with Amplitude, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Create an Amplitude test user](#create-an-amplitude-test-user)** - to have a counterpart of Britta Simon in Amplitude that is linked to the Azure AD representation of user.
4. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amplitude application.

**To configure Azure AD single sign-on with Amplitude, perform the following steps:**

1. In the Azure portal, on the **Amplitude** application integration page, click **Single sign-on**.

    ![Configure single sign-on link][4]

2. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Single sign-on dialog box](./media/amplitude-tutorial/tutorial_amplitude_samlbase.png)

3. On the **Amplitude Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:

    ![Amplitude Domain and URLs single sign-on information](./media/amplitude-tutorial/tutorial_amplitude_url.png)

    a. In the **Identifier** textbox, type the URL: `https://amplitude.com/saml/sso/metadata`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://analytics.amplitude.com/saml/sso/<uniqueid>`

    > [!NOTE]
    > The Reply URL value is not real. You will get the Reply URL value later in this tutorial.

4. Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:

    ![Amplitude Domain and URLs single sign-on information](./media/amplitude-tutorial/tutorial_amplitude_url1.png)

    In the **Sign-on URL** textbox, type the URL: `https://analytics.amplitude.com/sso`

5. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![The Certificate download link](./media/amplitude-tutorial/tutorial_amplitude_certificate.png) 

6. Click **Save** button.

    ![Configure Single Sign-On Save button](./media/amplitude-tutorial/tutorial_general_400.png)
    
7. Sign-on to your Amplitude company site as administrator.

8. Click on the **Plan Admin** from the left navigation bar.

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure1.png)

9. Select **Microsoft Azure Active Directory Metadata** from the **SSO Integration**.

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure2.png)

10. On the **Set Up Single Sign-On** section, perform the following steps:

    ![Configure Single Sign-On](./media/amplitude-tutorial/configure3.png)

    a. Open the downloaded **Metadata Xml** from Azure portal in notepad, paste the content into the **Microsoft Azure Active Directory Metadata** textbox.

    b. Copy the **Reply URL (ACS)** value and paste it into the **Reply URL** textbox of Amplitude Domain and URLs section in the Azure portal.

    c. Click **Save**

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/amplitude-tutorial/create_aaduser_01.png)

2. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/amplitude-tutorial/create_aaduser_02.png)

3. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/amplitude-tutorial/create_aaduser_03.png)

4. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/amplitude-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### <a name="create-an-amplitude-test-user"></a>Create an Amplitude test user

The objective of this section is to create a user called Britta Simon in Amplitude. Amplitude supports just-in-time provisioning, which is by default enabled. There is no action item for you in this section. A new user is created during an attempt to access Amplitude if it doesn't exist yet.
>[!Note]
>If you need to create a user manually, contact [Amplitude support team](https://amplitude.zendesk.com).

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Amplitude.

![Assign the user role][200] 

**To assign Britta Simon to Amplitude, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Amplitude**.

    ![The Amplitude link in the Applications list](./media/amplitude-tutorial/tutorial_amplitude_app.png)  

3. In the menu on the left, click **Users and groups**.

    ![The "Users and groups" link][202]

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![The Add Assignment pane][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Amplitude tile in the Access Panel, you should get automatically signed-on to your Amplitude application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/amplitude-tutorial/tutorial_general_01.png
[2]: ./media/amplitude-tutorial/tutorial_general_02.png
[3]: ./media/amplitude-tutorial/tutorial_general_03.png
[4]: ./media/amplitude-tutorial/tutorial_general_04.png

[100]: ./media/amplitude-tutorial/tutorial_general_100.png

[200]: ./media/amplitude-tutorial/tutorial_general_200.png
[201]: ./media/amplitude-tutorial/tutorial_general_201.png
[202]: ./media/amplitude-tutorial/tutorial_general_202.png
[203]: ./media/amplitude-tutorial/tutorial_general_203.png
