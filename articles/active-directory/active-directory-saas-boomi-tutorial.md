---
title: 'Tutorial: Azure Active Directory integration with Boomi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 4f594d921811180fb3b02560d2cb8f50b90ec114
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553464"
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Tutorial: Azure Active Directory integration with Boomi

In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).

Integrating Boomi with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Boomi
- You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure Management portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Boomi, you need the following items:

- An Azure AD subscription
- A Boomi single-sign on enabled subscription


> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.


To test the steps in this tutorial, you should follow these recommendations:

- You should not use your production environment, unless this is necessary.
- If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Boomi from the gallery
2. Configuring and testing Azure AD single sign-on


## <a name="adding-boomi-from-the-gallery"></a>Adding Boomi from the gallery
To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.

**To add Boomi from the gallery, perform the following steps:**

1. In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

2. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
3. Click **Add** button on the top of the dialog.

    ![Applications][3]

4. In the search box, type **Boomi**.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_000.png)

5. In the results panel, select **Boomi**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Boomi.

To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Boomi application.

**To configure Azure AD single sign-on with Boomi, perform the following steps:**

1. In the Azure Management portal, on the **Boomi** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

2. On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_01.png)

3. On the **Boomi Domain and URLs** section, in the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<account name>/saml`

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_02.png)

    > [!NOTE] 
    > Please note that this is not the real value. You have to update this value with the actual Reply URL. Contact Boomi support team to get this value. 

4. Boomi application expects the SAML assertions in a specific format. Please configure the following claims for this application. You can manage the values of these attributes from the "**User Attributes**" section on application integration page. The following screenshot shows an example for this.
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_03.png)

5. In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:
    
    | Attribute Name | Attribute Value |
    | --- | --- |    
    | FEDERATION_ID | user.mail |

    a. Click **Add attribute** to open the **Add Attribute** dialog.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_04.png)

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_05.png)
    
    b. In the **Name** textbox, type the attribute name shown for that row.
    
    c. From the **Value** list, type the attribute value shown for that row.
    
    d. Click **OK**

6. On the **SAML Signing Certificate** section, click **Create new certificate**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_06.png)    

7. On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**. Then click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_300.png)

8. On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_07.png)

9. On the pop-up **Rollover certificate** window, click **OK**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

10. On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_08.png) 

11. On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_09.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_10.png)

12. In a different web browser window, log into your Boomi company site as an administrator. 

13. Navigate to **Company Name** and go to **Set up**.

14. Click the **SSO options** tab and perform below steps.

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Check **Enable SAML Single Sign-On** checkbox.

    b. Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.
    
    c. In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.

    d. As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button. 

    e. Click **Save** button.
  

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure Management portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. Go to **Users and groups** and click **All users** to display the list of users.
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. At the top of the dialog click **Add** to open the **User** dialog.
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**. 



### <a name="creating-a-boomi-test-user"></a>Creating a Boomi test user

In order to enable Azure AD users to log into Boomi, they must be provisioned into Boomi. In the case of Boomi, provisioning is a manual task.

####<a name="to-provision-a-user-account-perform-the-following-steps"></a>To provision a user account, perform the following steps:

1. Log into your Boomi company site as an administrator.

2. After logging in, navigate to **User Management** and go to **Users**.

    ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")

3. Click **+**  icon and the **Add/Maintain User Roles** dialog opens.

    ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")

    ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")

4. Enter the user's **User e-mail address**.

5. Enter the user's **First name** and **Last name**.

6. Enter the user's **Federation ID**. Each user must have a Federation ID that uniquely identifies the user within the account. 

7. Assign the **Standard User** role to the user. Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.

8. Click **OK**.

    > [!NOTE]
    > The user will not receive a welcome notification email containing a password that can be used to log into the AtomSphere account because his password will be managed through the identity provider. You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts. 

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Boomi.

![Assign User][200] 

**To assign Britta Simon to Boomi, perform the following steps:**

1. In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

2. In the applications list, select **Boomi**.

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_boomi_50.png) 

3. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

4. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

5. On **Users and groups** dialog, select **Britta Simon** in the Users list.

6. Click **Select** button on **Users and groups** dialog.

7. Click **Assign** button on **Add Assignment** dialog.
    


### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.


## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-boomi-tutorial/tutorial_general_203.png































