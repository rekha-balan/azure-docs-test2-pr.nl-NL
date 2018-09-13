---
title: 'Tutorial: Azure Active Directory integration with Bonusly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 42875d53-0769-4520-a6af-7308b5240d6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: jeedes
ms.openlocfilehash: 24f9a1ca1a88cd4491c1b0062b8d754d4a694a41
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563901"
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Tutorial: Azure Active Directory integration with Bonusly

In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).

Integrating Bonusly with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Bonusly
- You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure Management portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Bonusly, you need the following items:

- An Azure AD subscription
- A Bonusly single-sign on enabled subscription


> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.


To test the steps in this tutorial, you should follow these recommendations:

- You should not use your production environment, unless this is necessary.
- If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Bonusly from the gallery
2. Configuring and testing Azure AD single sign-on


## <a name="adding-bonusly-from-the-gallery"></a>Adding Bonusly from the gallery
To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.

**To add Bonusly from the gallery, perform the following steps:**

1. In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
3. Click **Add** button on the top of the dialog.

    ![Applications][3]

4. In the search box, type **Bonusly**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_001.png)

5. In the results panel, select **Bonusly**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bonusly.

To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Bonusly test user](#creating-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Bonusly application.

**To configure Azure AD single sign-on with Bonusly, perform the following steps:**

1. In the Azure Management portal, on the **Bonusly** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

2. On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_01.png)

3. On the **Bonusly Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_02.png)

    a. In the **Identifier** textbox, type the value as: `bonusly`
    
    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<APP-ID>/consume`
    
4. If you wish to configure the application in **SP initiated mode**, on the **Bonusly Domain and URLs** section perform the following steps:
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_03.png)

    a. Click on the **Show advanced URL settings** option

    b. In the **Sign On URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<your_subdomain>/consume`

    > [!NOTE] 
    > Please note that these are not the real values. You have to update these values with the actual Sign On URL, Identifier and Reply URL. Here we suggest you to use the unique value of string in the Identifier. Contact [Bonusly support team](mailto:sales@easyterritory.com) to get these values.

5. On the **SAML Signing Certificate** section, click **Create new certificate**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_04.png)    

6. On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**. Then click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_300.png)

7. On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_05.png)

8. On the pop-up **Rollover certificate** window, click **OK**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_400.png)

9. On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_06.png) 

10. On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_07.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_08.png)

11. In a different web browser window, log into your Bonusly company site as an administrator.

12. In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_002.png)

13. Under **Single Sign-On**, select **SAML**.

14. On the **SAML** dialog page, perform the following steps:

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_003.png)

    a. In the **IdP SSO target URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.

    b. In the **IdP Login URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.

    c. In the **IdP Issuer** textbox put the value of **SAML Entity ID** from Azure AD application configuration window.

    d. Copy the thumbprint value from the downloaded certificate, and then paste it into the **Cert Fingerprint** textbox.

    e. Click **Save**.

    > [!NOTE] 
    > For more details, see [How to retrieve a certificate's thumbprint value](https://www.youtube.com/watch?v=YKQF266SAxI&feature=youtu.be).



### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure Management portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_01.png) 

2. Go to **Users and groups** and click **All users** to display the list of users.
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_02.png) 

3. At the top of the dialog click **Add** to open the **User** dialog.
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_03.png) 

4. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**. 



### <a name="creating-a-bonusly-test-user"></a>Creating a Bonusly test user

In order to enable Azure AD users to log into Bonusly, they must be provisioned into Bonusly.
In the case of Bonusly, provisioning is a manual task.

####<a name="to-provision-a-user-account-perform-the-following-steps"></a>To provision a user account, perform the following steps:

1. Log into your Bonusly company site as an administrator.

2. Click **Settings**.

    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_010.png "New User")

3. Click the **Users and bonuses** tab.

    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_011.png "New User")

4. Click **Manage Users**.

    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_012.png "New User")

5. Click **Add User**.

    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_013.png "New User")

6. In the **Add User** section, perform the following steps:

    ![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_014.png "New User")

    a. In the **First Name** textbox, type **Britta**.  

    b. In the **Last Name** textbox, type **Simon**.

    c. In the **Email** textbox, type the email address of Britta Simon account.

    d. Click **Save**.

    > [!NOTE] 
    > The AAD account holder will receive an email that includes a link to confirm the account before it becomes active. You can use any other Bonus.ly user account creation tools or APIs provided by Bonus.ly to provision AAD user accounts.



### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bonusly.

![Assign User][200] 

**To assign Britta Simon to Bonusly, perform the following steps:**

1. In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Bonusly**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_50.png) 

3. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    


### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.


## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_203.png
































