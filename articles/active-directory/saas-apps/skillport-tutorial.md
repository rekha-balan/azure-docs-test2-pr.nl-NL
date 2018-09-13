---
title: 'Tutorial: Azure Active Directory integration with Skillport | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2017
ms.author: jeedes
ms.openlocfilehash: 71a2b7186c77c6c1872870a594b287479c292472
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865590"
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a>Tutorial: Azure Active Directory integration with Skillport

In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).

Integrating Skillport with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Skillport
- You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Skillport, you need the following items:

- An Azure AD subscription
- A Skillport single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Skillport from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-skillport-from-the-gallery"></a>Adding Skillport from the gallery
To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.

**To add Skillport from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. Click **New Application** button on the top of the dialog.

    ![Applications][3]

1. In the search box, type **Skillport**.

    ![Creating an Azure AD test user](./media/skillport-tutorial/tutorial_skillport_search.png)

1. In the results panel, select **Skillport**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.

To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.

**To configure Azure AD single sign-on with Skillport, perform the following steps:**

1. In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_samlbase.png)

1. On the **Skillport Domain and URLs** section, perform the following steps:

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_url.png)

    a. In the **Sign-on URL** textbox, type the URL:
      
      EU Datacenter: `https://adfs.skillport.eu`
   
      US Datacenter: `https://sso.skillport.com`

    b. In the **Identifier** textbox, type the URL:
      
      EU Datacenter: `http://adfs.skillport.eu/adfs/services/trust`
   
      US Datacenter: `https://sso.skillport.com`
   
    c. In the **Reply URL** textbox, type the URL:
    
      EU Datacenter: ` https://adfs.skillport.eu/adfs/ls/`
    
      US Datacenter: `https://sso.skillport.com/sp/ACS.saml2`
 
1. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_general_400.png)

1. To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp). They will set it up to have the SAML SSO connection set properly on both sides.

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/skillport-tutorial/create_aaduser_01.png) 

1. Go to **Users and groups** and click **All users** to display the list of users.
    
    ![Creating an Azure AD test user](./media/skillport-tutorial/create_aaduser_02.png) 

1. At the top of the dialog, click **Add** to open the **User** dialog.
 
    ![Creating an Azure AD test user](./media/skillport-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/skillport-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-a-skillport-test-user"></a>Creating a Skillport test user

In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user. They will configure it after discussion with the users.  

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.

![Assign User][200] 

**To assign Britta Simon to Skillport, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Skillport**.

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skillport-tutorial/tutorial_general_01.png
[2]: ./media/skillport-tutorial/tutorial_general_02.png
[3]: ./media/skillport-tutorial/tutorial_general_03.png
[4]: ./media/skillport-tutorial/tutorial_general_04.png

[100]: ./media/skillport-tutorial/tutorial_general_100.png

[200]: ./media/skillport-tutorial/tutorial_general_200.png
[201]: ./media/skillport-tutorial/tutorial_general_201.png
[202]: ./media/skillport-tutorial/tutorial_general_202.png
[203]: ./media/skillport-tutorial/tutorial_general_203.png
