---
title: 'Tutorial: Azure Active Directory integration with Anaplan | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Anaplan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 4936e8d3c48486247677cf072513b7e450f1bf17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867955"
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a>Tutorial: Azure Active Directory integration with Anaplan

In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).

Integrating Anaplan with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Anaplan
- You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Anaplan, you need the following items:

- An Azure AD subscription
- An Anaplan single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Anaplan from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-anaplan-from-the-gallery"></a>Adding Anaplan from the gallery
To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.

**To add Anaplan from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
3. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

4. In the search box, type **Anaplan**.

    ![Creating an Azure AD test user](./media/anaplan-tutorial/tutorial_anaplan_search.png)

5. In the results panel, select **Anaplan**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."

For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.

In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.

**To configure Azure AD single sign-on with Anaplan, perform the following steps:**

1. In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

2. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. On the **Anaplan Domain and URLs** section, perform the following steps:

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`

    b. In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`

    > [!NOTE] 
    > These values are not real. Update these values with the actual Sign-On URL and Identifier. Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values. 
 
4. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. Click **Save** button.

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_general_400.png)

6. On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_configure.png) 

7. To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com). They set this setting to have the SAML SSO connection set properly on both sides.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_01.png) 

2. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_02.png) 

3. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_03.png) 

4. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-an-anaplan-test-user"></a>Creating an Anaplan test user

In this section, you create a user called Britta Simon in Anaplan. Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.

![Assign User][200] 

**To assign Britta Simon to Anaplan, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Anaplan**.

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_app.png) 

3. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.

For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/anaplan-tutorial/tutorial_general_01.png
[2]: ./media/anaplan-tutorial/tutorial_general_02.png
[3]: ./media/anaplan-tutorial/tutorial_general_03.png
[4]: ./media/anaplan-tutorial/tutorial_general_04.png

[100]: ./media/anaplan-tutorial/tutorial_general_100.png

[200]: ./media/anaplan-tutorial/tutorial_general_200.png
[201]: ./media/anaplan-tutorial/tutorial_general_201.png
[202]: ./media/anaplan-tutorial/tutorial_general_202.png
[203]: ./media/anaplan-tutorial/tutorial_general_203.png
