---
title: 'Tutorial: Azure Active Directory integration with BenSelect | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BenSelect.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: jeedes
ms.openlocfilehash: 141cd3fe539fdedada7949d1202ee20a44754108
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554788"
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a>Tutorial: Azure Active Directory integration with BenSelect
In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).

Integrating BenSelect with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to BenSelect
* You can enable your users to automatically get signed-on to BenSelect single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with BenSelect, you need the following items:

* An Azure AD subscription
* A BenSelect single-sign on (SSO) enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment.
>  

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario Description
In this tutorial, you test Azure AD SSO in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

* Adding BenSelect from the gallery
* Configuring and testing Azure AD SSO

## <a name="adding-benselect-from-the-gallery"></a>Adding BenSelect from the gallery
To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.

**To add BenSelect from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **BenSelect**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_01.png)
7. In the results pane, select **BenSelect**, and then click **Complete** to add the application.
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD. In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in BenSelect.

To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD Single Sign-On
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your BenSelect application.

BenSelect application expects the SAML assertions in a specific format. Please configure the following claims for this application. You can manage the values of these attributes from the "**Atrribute**" tab of the application. The following screenshot shows an example for this. 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

**To configure Azure AD single sign-on with BenSelect, perform the following steps:**

1. In the Azure classic portal, on the **BenSelect** application integration page, in the menu on the top, click **Attributes**.
   
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_07.png)
2. On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:
   
   | Attribute Name | Attribute Value |
   | --- | --- |
   | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier |extractmailprefix([userprincipalname]) |
  1. Click **add user attribute** to open the **Add User Attribure** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_08.png)
  2. In the **Attribute Name** textbox, type the attribute name shown for that row 
  3. From the **Attribute Value** list, type ExtractMailPrefix().
  4. From the **Mail** list, type User.userprincipalname.
  5. Click **Complete**.
3. In the menu on the top, click **Quick Start**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_09.png)
4. On the **How would you like users to sign on to BenSelect** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_03.png) 
5. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_04.png) 
   1. In the **Reply URL** textbox, type the URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path={<tenant name>}`
   2. click **Next**.
6. On the **Configure single sign-on at BenSelect** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_05.png)
  1. Click **Download certificate**, and then save the file on your computer.
  2. Click **Next**.
7. To get SSO configured for your application, contact your BenSelect support team via [support@selerix.com](mailto:support@selerix.com) and provide them with the following:
   * The downloaded certificate
   * The SAML SSO URL
   * The Sign Out URL 
   * The Issuer 
     
   >[!NOTE]
   >You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc. 
   > 
8. In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
9. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
In this section, you create a test user in the classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_09.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps:

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_05.png)    
  1. As Type Of User, select New user in your organization.
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_06.png)   
  1. In the **First Name** textbox, type **Britta**. 
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/create_aaduser_08.png) 
   1. Write down the value of the **New Password**.
   2. Click **Complete**.   

### <a name="create-an-benselect-test-user"></a>Create an BenSelect test user
The objective of this section is to create a user called Britta Simon in BenSelect. Please work with BenSelect support team to add the users in the BenSelect account.

>[!NOTE]
>If you need to create an user manually, you need to contact the BenSelect support team via <mailto:support@selerix.com>.
>  

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
In this section, you enable Britta Simon to use Azure single sign-on by granting her access to BenSelect.

![Assign User][200] 

**To assign Britta Simon to BenSelect, perform the following steps:**

1. On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **BenSelect**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_benselect_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
In this section, you test your Azure AD SSO configuration using the Access Panel.

When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benselect-tutorial/tutorial_general_205.png





























