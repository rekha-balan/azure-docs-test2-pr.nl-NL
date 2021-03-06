---
title: 'Tutorial: Azure Active Directory integration with Zscaler Beta | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler Beta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 29637f8a733e9f92f37144491bef4ab4ba5aae07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856286"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a>Tutorial: Azure Active Directory integration with Zscaler Beta

In this tutorial, you learn how to integrate Zscaler Beta with Azure Active Directory (Azure AD).

Integrating Zscaler Beta with Azure AD provides you with the following benefits:

- You can control in Azure AD who has access to Zscaler Beta
- You can enable your users to automatically get signed-on to Zscaler Beta (Single Sign-On) with their Azure AD accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisites

To configure Azure AD integration with Zscaler Beta, you need the following items:

- An Azure AD subscription
- A Zscaler Beta single sign-on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

To test the steps in this tutorial, you should follow these recommendations:

- Do not use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario description
In this tutorial, you test Azure AD single sign-on in a test environment. The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Zscaler Beta from the gallery
1. Configuring and testing Azure AD single sign-on

## <a name="adding-zscaler-beta-from-the-gallery"></a>Adding Zscaler Beta from the gallery
To configure the integration of Zscaler Beta into Azure AD, you need to add Zscaler Beta from the gallery to your list of managed SaaS apps.

**To add Zscaler Beta from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon. 

    ![Active Directory][1]

1. Navigate to **Enterprise applications**. Then go to **All applications**.

    ![Applications][2]
    
1. To add new application, click **New application** button on the top of dialog.

    ![Applications][3]

1. In the search box, type **Zscaler Beta**.

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

1. In the results panel, select **Zscaler Beta**, and then click **Add** button to add the application.

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Beta is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in Zscaler Beta needs to be established.

In Zscaler Beta, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.

To configure and test Azure AD single sign-on with Zscaler Beta, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
1. **[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer
1. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
1. **[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - to have a counterpart of Britta Simon in Zscaler Beta that is linked to the Azure AD representation of user.
1. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
1. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Beta application.

**To configure Azure AD single sign-on with Zscaler Beta, perform the following steps:**

1. In the Azure portal, on the **Zscaler Beta** application integration page, click **Single sign-on**.

    ![Configure Single Sign-On][4]

1. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
 
    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

1. On the **Zscaler Beta Domain and URLs** section, perform the following steps:

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler Beta application.

    > [!NOTE] 
    > You have to update this value with the actual Sign-On URL. Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) to get this value. 

1. On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

1. Click **Save** button.

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_general_400.png)

1. On the **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** to open **Configure sign-on** window. Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

1. In a different web browser window, log in to your Zscaler Beta company site as an administrator.

1. In the menu on the top, click **Administration**.
   
    ![Administration](./media/zscaler-beta-tutorial/ic800206.png "Administration")

1. Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.   
            
    ![Manage Users & Authentication](./media/zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")

1. In the **Choose Authentication Options for your Organization** section, perform the following steps:   
                
    ![Authentication](./media/zscaler-beta-tutorial/ic800208.png "Authentication")
   
    a. Select **Authenticate using SAML Single Sign-On**.

    b. Click **Configure SAML Single Sign-On Parameters**.

1. On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**

    ![Single Sign-On](./media/zscaler-beta-tutorial/ic800209.png "Single Sign-On")
    
    a. Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.
    
    b. In the **Attribute containing Login Name** textbox, type **NameID**.
    
    c. To upload your downloaded certificate, click **Zscaler pem**.
    
    d. Select **Enable SAML Auto-Provisioning**.

1. On the **Configure User Authentication** dialog page, perform the following steps:

    ![Administration](./media/zscaler-beta-tutorial/ic800210.png "Administration")
    
    a. Click **Save**.

    b. Click **Activate Now**.

## <a name="configuring-proxy-settings"></a>Configuring proxy settings
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a>To configure the proxy settings in Internet Explorer

1. Start **Internet Explorer**.

1. Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.   
    
     ![Internet Options](./media/zscaler-beta-tutorial/ic769492.png "Internet Options")

1. Click the **Connections** tab.   
  
     ![Connections](./media/zscaler-beta-tutorial/ic769493.png "Connections")

1. Click **LAN settings** to open the **LAN Settings** dialog.

1. In the Proxy server section, perform the following steps:   
   
    ![Proxy server](./media/zscaler-beta-tutorial/ic769494.png "Proxy server")

    a. Select **Use a proxy server for your LAN**.

    b. In the Address textbox, type **gateway.zscalerbeta.net**.

    c. In the Port textbox, type **80**.

    d. Select **Bypass proxy server for local addresses**.

    e. Click **OK** to close the **Local Area Network (LAN) Settings** dialog.

1. Click **OK** to close the **Internet Options** dialog.

> [!TIP]
> You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!  After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure portal called Britta Simon.

![Create Azure AD User][100]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_01.png) 

1. To display the list of users, go to **Users and groups** and click **All users**.
    
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_02.png) 

1. To open the **User** dialog, click **Add** on the top of the dialog.
 
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_03.png) 

1. On the **User** dialog page, perform the following steps:
 
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_04.png) 

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Click **Create**.
 
### <a name="creating-a-zscaler-beta-test-user"></a>Creating a Zscaler Beta test user

To enable Azure AD users to log in to Zscaler Beta, they must be provisioned to Zscaler Beta. In the case of Zscaler Beta, provisioning is a manual task.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>To configure user provisioning, perform the following steps:

1. Log in to your **Zscaler Beta** tenant.

1. Click **Administration**.   
   
    ![Administration](./media/zscaler-beta-tutorial/ic781035.png "Administration")

1. Click **User Management**.   
        
     ![Add](./media/zscaler-beta-tutorial/ic781036.png "Add")

1. In the **Users** tab, click **Add**.
      
    ![Add](./media/zscaler-beta-tutorial/ic781037.png "Add")

1. In the Add User section, perform the following steps:
        
    ![Add User](./media/zscaler-beta-tutorial/ic781038.png "Add User")
   
    a. Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.

    b. Click **Save**.

> [!NOTE]
> You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta to provision Azure AD user accounts.

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Beta.

![Assign User][200] 

**To assign Britta Simon to Zscaler Beta, perform the following steps:**

1. In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.

    ![Assign User][201] 

1. In the applications list, select **Zscaler Beta**.

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

1. In the menu on the left, click **Users and groups**.

    ![Assign User][202] 

1. Click **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Assign User][203]

1. On **Users and groups** dialog, select **Britta Simon** in the Users list.

1. Click **Select** button on **Users and groups** dialog.

1. Click **Assign** button on **Add Assignment** dialog.
    
### <a name="testing-single-sign-on"></a>Testing single sign-on

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Zscaler Beta tile in the Access Panel, you should get automatically signed-on to your Zscaler Beta application.
For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Additional resources

* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-beta-tutorial/tutorial_general_203.png

