---
title: 'Tutorial: Azure Active Directory integration with ADP eTime | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ADP eTime.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 342ba03125545ade050cf844e903faa4a5d84acb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550403"
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a>Tutorial: Azure Active Directory integration with ADP eTime
The objective of this tutorial is to show you how to integrate ADP eTime with Azure Active Directory (Azure AD).

Integrating ADP eTime with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to ADP eTime
* You can enable your users to automatically get signed-on to ADP eTime single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with ADP eTime, you need the following items:

* An Azure AD subscription
* A ADP eTime SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding ADP eTime from the gallery
2. Configuring and testing Azure AD SSO

## <a name="add-adp-etime-from-the-gallery"></a>Add ADP eTime from the gallery
To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.

**To add ADP eTime from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **ADP eTime**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_01.png)
7. In the results pane, select **ADP eTime**, and then click **Complete** to add the application.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_06.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
The objective of this section is to show you how to configure and test Azure AD SSO with ADP eTime based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in ADP eTime to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.  

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.

To configure and test Azure AD SSO with ADP eTime, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a ADP eTime test user](#creating-a-adpetime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-sso"></a>Configuring Azure AD SSO
The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your ADP eTime application.

Your ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user. 

Here the user mapping fron Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings. So please work with ADP eTime team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.  

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_02.png) 

Before you can configure the SAML assertion, you need to contact your ADP eTime support team and request the value of the unique identifier attribute for your tenant. You need this value to configure the custom claim for your application.

**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**

1. In the Azure classic portal, on the **ADP eTime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to ADP eTime** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_03.png) 
3. On the **Configure App Settings** dialog page, perform the following steps:.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_04.png) 
  1. In the **Reply URL** textbox, type the URL used by your users to sign-on to your ADP eTime application using the following pattern: `https://<server name>.adp.com/affwebservices/public/saml2assertionconsumer`.
  2. Click **Next**.
4. On the **Configure single sign-on at ADP eTime** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_05.png)  
  1. Click **Download metadata**, and then save the file on your computer. 
  2. Click **Next**.
2. To get SSO configured for your application, contact your ADP eTime support team and email the attach downloaded metadata file, so that they can be configured for SSO integration.
   
   >[!NOTE]
   >After **ADP eTime** team configure the instance, get the **RelayState** value from them.Follow the below mentioned steps to configure it. After this configuration you can test the integration. So please note that this is important configuration for this application integration to work.
   >  
6. To configure the RelayState value in Azure AD, perform the following steps: 
  1. Logon to the [Azure Management Portal](https://portal.azure.com) as administrator.
  2. In the left navigation pane, click **More Services**.  

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_07.png) 
 3. In the **Search** textbox, type **Azure Active Directory**, and then click the related link. 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_08.png)   
 4. Click **Enterprise Applications**. 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_09.png)  
 5. In the **Manage** section, click **All Applications**.
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_10.png) 
 6. In the **Search** textbox, type **ADP eTime**, and then click the related link. 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_11.png)  
 7. In the **Manage** section, click **Single sign-on**. 
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_12.png) 
 8. Select **Show advanced URL settings**.
 
     ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_13.png) 
 9. In the **Relay State** textbox, type a value using the following patterns, and then save the settings: 
 
    * Production environment: `https://fed.adp.com/saml/fedlanding.html?<id>` 
    * Staging environment: `https://fed-stag.adp.com/saml/fedlanding.html?PORTAL`
     
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_14.png) 

4. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.
 
 ![Azure AD Single Sign-On][10]
5. On the **Single sign-on confirmation** page, click **Complete**.  
   
 ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

* In the Users list, select **Britta Simon**.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_09.png) 
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_05.png)  
 1. As **Type Of User**, select **New user in your organization**.
 2. In the **User Name** textbox, type **BrittaSimon**. 
 3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps:
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_06.png)  
 1. In the **First Name** textbox, type **Britta**.   
 2. In the **Last Name** textbox, type, **Simon**. 
 3. In the **Display Name** textbox, type **Britta Simon**. 
 4. In the **Role** list, select **User**. 
 5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/create_aaduser_08.png)  
 1. Write down the value of the **New Password**.
 2. Click **Complete**.   

### <a name="create-a-adp-etime-test-user"></a>Create a ADP eTime test user
The objective of this section is to create a user called Britta Simon in ADP eTime. Please work with ADP eTime support team to add the users in the ADP eTime account. 

>[!NOTE]
>If you need to create an user manually, you need to contact the ADP eTime support team.
> 

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ADP eTime.

![Assign User][200] 

**To assign Britta Simon to ADP eTime, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **ADP eTime**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_50.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.

When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpetime-tutorial/tutorial_general_205.png


































