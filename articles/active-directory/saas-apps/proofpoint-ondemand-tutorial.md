---
title: 'Tutorial: Azure Active Directory integration with Proofpoint on Demand | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Proofpoint on Demand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/13/2017
ms.author: jeedes
ms.openlocfilehash: 3127eb4173661e943f108a890bd66a3de11dde85
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871702"
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a>Tutorial: Azure Active Directory integration with Proofpoint on Demand

In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).

Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Proofpoint on Demand.
- You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts.
- You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Proofpoint on Demand, you need the following items:

- An Azure AD subscription
- A Proofpoint on Demand single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Proofpoint on Demand from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a>Adding Proofpoint on Demand from the gallery
To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.

**To add Proofpoint on Demand from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![The Azure Active Directory button][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![The Enterprise applications blade][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![The New application button][3]

1. In the search box, type **Proofpoint on Demand**, select **Proofpoint on Demand** from result panel then click **Add** button to add the application.

    ![Proofpoint on Demand in the results list](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.

In Proofpoint on Demand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Create a Proofpoint on Demand test user](#create-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.
1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.

**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**

1. In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.

    ![Configure single sign-on link][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Single sign-on dialog box](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

1. On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:

    ![Proofpoint on Demand Domain and URLs single sign-on information](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`

    b. In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`

    c. In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`
    
    > [!NOTE] 
    > These values are not real. Update these values with the actual Identifier, Reply URL, and Sign-On URL. Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.

1. On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.

    ![The Certificate download link](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On Save button](./media/proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
1. On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Proofpoint on Demand Configuration](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

1. To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Proofpoint on Demand support team](https://www.proofpoint.com/us/support-services). They set this setting to have the SAML SSO connection set properly on both sides.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user

The objective of this section is to create a test user in the Azure portal called Britta Simon.

   ![Create an Azure AD test user][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the Azure portal, in the left pane, click the **Azure Active Directory** button.

    ![The Azure Active Directory button](./media/proofpoint-ondemand-tutorial/create_aaduser_01.png)

1. To display the list of users, go to **Users and groups**, and then click **All users**.

    ![The "Users and groups" and "All users" links](./media/proofpoint-ondemand-tutorial/create_aaduser_02.png)

1. To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.

    ![The Add button](./media/proofpoint-ondemand-tutorial/create_aaduser_03.png)

1. In the **User** dialog box, perform the following steps:

    ![The User dialog box](./media/proofpoint-ondemand-tutorial/create_aaduser_04.png)

    a. In the **Name** box, type **BrittaSimon**.

    b. In the **User name** box, type the email address of user Britta Simon.

    c. Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.

    d. Click **Create**.
 
### <a name="create-a-proofpoint-on-demand-test-user"></a>Create a Proofpoint on Demand test user

In this section, you create a user called Britta Simon in Proofpoint on Demand. Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.

![Assign the user role][200] 

**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Proofpoint on Demand**.

    ![The Proofpoint on Demand link in the Applications list](./media/proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png)  

1. In the menu on the left, click **Users and groups**.

    ![The "Users and groups" link][202]

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![The Add Assignment pane][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Proofpoint on Demand tile in the Access Panel, you should get automatically signed-on to your Proofpoint on Demand application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/proofpoint-ondemand-tutorial/tutorial_general_203.png

