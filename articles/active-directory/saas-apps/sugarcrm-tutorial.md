---
title: 'Tutorial: Azure Active Directory integration with Sugar CRM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sugar CRM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1acaf5e530f5d5563901d8d498901ecc1bffecdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864640"
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Tutorial: Azure Active Directory integration with Sugar CRM

In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).

Integrating Sugar CRM with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Sugar CRM
- You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Sugar CRM, you need the following items:

- An Azure AD subscription
- A Sugar CRM single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Sugar CRM from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-sugar-crm-from-the-gallery"></a>Adding Sugar CRM from the gallery
To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.

**To add Sugar CRM from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

1. In the search box, type **Sugar CRM**.

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/tutorial_sugarcrm_search.png)

1. In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.

In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.

**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**

1. In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

1. On the **Sugar CRM Domain and URLs** section, perform the following steps:

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    In the **Sign-on URL** textbox, type a URL using the following pattern:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > The value is not real. Update the value with the actual Sign-On URL. Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value. 
 
1. On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_general_400.png)

1. On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window. Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

1. In a different web browser window, log in to your Sugar CRM company site as an administrator.

1. Go to **Admin**.
   
    ![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")

1. In the **Administration** section, click **Password Management**.
   
    ![Administration](./media/sugarcrm-tutorial/ic795889.png "Administration")

1. Select **Enable SAML Authentication**.
   
    ![Administration](./media/sugarcrm-tutorial/ic795890.png "Administration")

1. In the **SAML Authentication** section, perform the following steps:
   
    ![SAML Authentication](./media/sugarcrm-tutorial/ic795891.png "SAML Authentication")  
 
    a. In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.
  
    b. In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.
  
    c. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.
  
    d. Click **Save**.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/sugarcrm-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-a-sugar-crm-test-user"></a>Creating a Sugar CRM test user

In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.

In the case of Sugar CRM, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Log in to your **Sugar CRM** company site as administrator.

1. Go to **Admin**.
   
    ![Admin](./media/sugarcrm-tutorial/ic795888.png "Admin")

1. In the **Administration** section, click **User Management**.
   
    ![Administration](./media/sugarcrm-tutorial/ic795893.png "Administration")

1. Go to **Users \> Create New User**.
   
    ![Create New User](./media/sugarcrm-tutorial/ic795894.png "Create New User")

1. On the **User Profile** tab, perform the following steps:
   
    ![New User](./media/sugarcrm-tutorial/ic795895.png "New User")

    a. Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.
  
1. As **Status**, select **Active**.

1. On the Password tab, perform the following steps:
   
    ![New User](./media/sugarcrm-tutorial/ic795896.png "New User")

    a. Type the password into the related textbox.

    b. Click **Save**.

>[!NOTE]
>You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.

![Assign User][200] 

**To assign Britta Simon to Sugar CRM, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Sugar CRM**.

    ![Configure Single Sign-On](./media/sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.

When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/sugarcrm-tutorial/tutorial_general_203.png
