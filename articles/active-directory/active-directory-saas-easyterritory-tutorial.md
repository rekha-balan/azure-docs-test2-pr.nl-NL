---
title: 'Tutorial: Azure Active Directory integration with EasyTerritory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EasyTerritory.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 0974ab08e4e63c3f675f8b0ce83cf1a1c504fe5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548956"
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a>Tutorial: Azure Active Directory integration with EasyTerritory

In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).

Integrating EasyTerritory with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to EasyTerritory
- You can enable your users to automatically get signed-on to EasyTerritory single sign-on (SSO) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure Management portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with EasyTerritory, you need the following items:

- An Azure AD subscription
- An EasyTerritory single-sign (SSO) on enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment.
>
>

To test the steps in this tutorial, you should follow these recommendations:

- You should not use your production environment, unless this is necessary.
- If you don't have an Azure AD trial environment, you can get trial [an one-month](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD SSO in a test environment. 

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding EasyTerritory from the gallery
2. Configuring and testing Azure AD SSO

## <a name="adding-easyterritory-from-the-gallery"></a>Adding EasyTerritory from the gallery
To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.

**To add EasyTerritory from the gallery, perform the following steps:**

1. In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
3. Click **Add** button on the top of the dialog.

    ![Applications][3]

4. In the search box, type **EasyTerritory**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_001.png)

5. In the results panel, select **EasyTerritory**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on
In this section, you configure and test Azure AD SSO with EasyTerritory based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in EasyTerritory.

To configure and test Azure AD SSO with EasyTerritory, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating an EasyTerritory test user](#creating-an-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure Management portal and configure SSO in your EasyTerritory application.

**To configure Azure AD SSO with EasyTerritory, perform the following steps:**

1. In the Azure Management portal, on the **EasyTerritory** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

2. On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable SSO.
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_01.png)

3. On the **EasyTerritory Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_02.png)
   1. In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/`
   2. In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/DEV/AuthServices/Acs`
    
4. If you wish to configure the application in **SP initiated mode**, on the **EasyTerritory Domain and URLs** section perform the following steps:
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_03.png)
  1. Click on the **Show advanced URL settings** option.
  2. In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`

    >[!NOTE] 
    >These are not the real values. You have to update these values with the actual Sign On URL, Identifier and Reply URL.Contact [EasyTerritory support team](mailto:sales@easyterritory.com) to get these values.

5. On the **SAML Signing Certificate** section, click **Create new certificate**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_04.png)    

6. On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**. Then click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_300.png)

7. On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_05.png)

8. On the pop-up **Rollover certificate** window, click **OK**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

9. On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_06.png) 

10. To get SSO configured for your application, contact [EasyTerritory support team](mailto:sales@easyterritory.com) and provide them with downloaded **metadata**. 

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure Management portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png) 

2. Go to **Users and groups** and click **All users** to display the list of users.
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png) 

3. At the top of the dialog click **Add** to open the **User** dialog.
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png) 

4. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png) 
 1. In the **Name** textbox, type **BrittaSimon**.
 2. In the **User name** textbox, type the **email address** of BrittaSimon.
 3. Select **Show Password** and write down the value of the **Password**.
 4. Click **Create**. 

### <a name="create-an-easyterritory-test-user"></a>Create an EasyTerritory test user

In this section, you create a user called Britta Simon in EasyTerritory. Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure SSO by granting her access to EasyTerritory.

![Assign User][200] 

**To assign Britta Simon to EasyTerritory, perform the following steps:**

1. In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **EasyTerritory**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_50.png) 

3. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    

### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD SSO configuration using the Access Panel.

When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png























