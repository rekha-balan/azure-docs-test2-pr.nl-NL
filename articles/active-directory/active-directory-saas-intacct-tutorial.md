---
title: 'Tutorial: Azure Active Directory integration with Intacct | Microsoft Docs'
description: Learn how to use Intacct with Azure Active Directory to enable single sign-on, automated provisioning, and more.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/02/2017
ms.author: jeedes
ms.openlocfilehash: 6cc07afc1615e42554b991791b33d67652401690
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554783"
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Tutorial: Azure Active Directory integration with Intacct
The objective of this tutorial is to show the integration of Azure and Intacct.  
The scenario outlined in this tutorial assumes that you already have the following items:

* A valid Azure subscription
* An Intacct tenant

After you complete this tutorial, the Azure Active Directory (Azure AD) users you have assigned to Intacct will be able to sign in to the application at your Intacct company site (service provider initiated sign-on), or use the [Access Panel](active-directory-saas-access-panel-introduction.md).

The scenario outlined in this tutorial consists of the following building blocks:

* Enabling the application integration for Intacct
* Configuring single sign-on
* Configuring user provisioning
* Assigning users

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790030.png "Scenario")

## <a name="enable-the-application-integration-for-intacct"></a>Enable the application integration for Intacct
The objective of this section is to outline how to enable the application integration for Intacct.

**To enable the application integration for Intacct, perform the following steps:**

1. In the Azure classic portal, in the left pane, click the Active Directory icon.

   ![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700993.png "Active Directory")
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** on the top menu.

   ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC700994.png "Applications")
4. Click **Add** at the bottom of the page.

   ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749321.png "Add application")
5. On the **What do you want to do** page, click **Add an application from the gallery**.

   ![Add an application from the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC749322.png "Add an application from gallery")
6. In the search box, enter **Intacct**.

   ![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790031.png "Application Gallery")
7. In the results pane, select **Intacct**, and then click **Complete** to add the application.

   ![Intacct](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790032.png "Intacct")

## <a name="configure-single-sign-on"></a>Configure single sign-on

The objective of this section is to outline how to enable users to authenticate to Intacct with their account in Azure AD. Federation that is based on the SAML protocol is used for this authentication.  

As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

**To configure single sign-on, perform the following steps:**

1. In the Azure classic portal, on the **Intacct** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** page.

   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790033.png "Configure single sign-on")
2. On the **How would you like users to sign on to Intacct** page, select **Windows Azure AD Single Sign-On**, and then click **Next**.

   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790034.png "Configure single sign-on")
3. On the **Configure App URL** page, in the **Sign On URL** box, enter your URL that uses the *https://Intacct.com/company* pattern, and then click **Next**.

   ![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790035.png "Configure App URL")
4. On the **Configure single sign-on at Intacct** page, click **Download certificate**, and then save the certificate file on your computer.

   ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790036.png "Configure single sign-on")
5. In a different web browser window, sign in to your Intacct company site as an administrator.
6. Click the **Company** tab, and then click **Company Info**.

   ![Company](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790037.png "Company")
7. Click the **Security** tab, and then click **Edit**.

   ![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790038.png "Security")
8. In the **Single sign on (SSO)** section, perform the following steps:

   ![Single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790039.png "single sign on")

   1. Select **Enable single sign on**.
   2. As **Identity provider type**, select **SAML 2.0**.
   3. In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** box.
   4. In the Azure classic portal, on the **Configure single sign-on at Intacct** page, copy the **Remote Login URL** value, and then paste it into the **Login URL** box.
   5. Create a **base-64 encoded** file from your downloaded certificate. For more information, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).      
   6. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.
   7. Click **Save**.
9. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign-On** page.

   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790040.png "Configure Single Sign-On")

## <a name="configure-user-provisioning"></a>Configure user provisioning

To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct. For Intacct, provisioning is a manual task.

**To provision user accounts, perform the following steps:**

1. Sign in to your **Intacct** tenant.
2. Click the **Company** tab, and then click **Users**.

   ![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790041.png "Users")
3. Click the **Add** tab.

   ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790042.png "Add")
4. In the **User Information** section, perform the following steps:

   ![User Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790043.png "User Information")

   1. Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.
   2. Select the **Admin privileges** of an Azure AD account that you want to provision.
   3. Click **Save**. The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.

>[!NOTE]
>To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.
>

## <a name="assign-users"></a>Assign users
To test your configuration, you need to assign Azure AD users to Intacct. After a user is assigned, they can access your application.

**To assign users to Intacct, perform the following steps:**

1. In the Azure classic portal, create a test account.
2. On the **Intacct** application integration page, click **Assign users**.

   ![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC790044.png "Assign users")
3. Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.

   ![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/IC767830.png "Yes")

If you want to test your single sign-on settings, open the Access Panel. For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).


### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user

In this section, you set up Britta Simon to use Azure single sign-on by granting Britta access to Intacct.

![Assign user][200]

**To assign Britta Simon to Intacct, perform the following steps:**

1. In the Azure portal, open the applications view, go to the directory view, go to **Enterprise applications**, and then click **All applications**.

    ![Assign user][201]

2. In the applications list, select **Intacct**.

    ![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_intacct_50.png)

3. On the **Manage** menu, click **Users and groups**.

    ![Assign user][202]

4. Click the **Add** button, and then in **Add Assignment**, select **Users and groups**.

    ![Assign user][203]

5. In **Users and groups**, select **Britta Simon** from the user's list.

6. In **Users and groups**, click the **Select** button.

7. In **Add Assignment**, click the **Assign** button.



### <a name="test-single-sign-on"></a>Test single sign-on

In this section, you test your Azure AD single sign-on configuration by using the Access Panel.

When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.


## <a name="additional-resources"></a>Additional resources

* [List of tutorials on how to integrate SaaS apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-intacct-tutorial/tutorial_general_203.png






























