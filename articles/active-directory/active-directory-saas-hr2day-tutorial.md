---
title: 'Tutorial: Azure Active Directory integration with HR2day by Merces | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HR2day by Merces.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 18d5b5981106a17b354ba1bf3a415c1249ff015f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554686"
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Tutorial: Azure Active Directory integration with HR2day by Merces
The objective of this tutorial is to show you how to integrate HR2day by Merces with Azure Active Directory (Azure AD).  
Integrating HR2day by Merces with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to HR2day by Merces
* You can enable your users to automatically get signed-on to HR2day by Merces (Single Sign-On) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with HR2day by Merces, you need the following items:

* An Azure AD subscription
* A HR2day by Merces single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.
> 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.  
The scenario outlined in this tutorial consists of two main building blocks:

1. Adding HR2day by Merces from the gallery
2. Configuring and testing Azure AD single sign-on

## <a name="adding-hr2day-by-merces-from-the-gallery"></a>Adding HR2day by Merces from the gallery
To configure the integration of HR2day by Merces into Azure AD, you need to add HR2day by Merces from the gallery to your list of managed SaaS apps.

**To add HR2day by Merces from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]

4. Click **Add** at the bottom of the page.
   
    ![Applications][3]

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]

6. In the search box, type **HR2day by Merces**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_01.png)

7. In the results pane, select **HR2day by Merces**, and then click **Complete** to add the application.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuring and testing Azure AD single sign-on
The objective of this section is to show you how to configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon".

For single sign-on to work, Azure AD needs to know what the counterpart user in HR2day by Merces to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in HR2day by Merces needs to be established.  
This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HR2day by Merces.

To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a HR2day by Merces test user](#creating-a-hr2day-by-merces-test-user)** - to have a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuring Azure AD Single Sign-On
The objective of this section is to outline how to enable users to authenticate to HR2day by Merces with their account in Azure AD using federation based on the SAML protocol.

Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png) 

Before you can configure the SAML assertion, you need to contact your HR2day support team via [servicedesk@merces.nl](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant. You need this value to complete the steps in the next section.

**To configure Azure AD single sign-on with HR2day by Merces, perform the following steps:**

1. In the Azure classic portal, on the **HR2day by Merces** application integration page, in the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog. 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_06.png) 

2. To add the required attribute mappings, perform the following steps, perform the following steps: 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_07.png) 

    a. Click **add user attribute**.

    b. In the **Attribute Name** textbox, type **“ATTR_LOGINCLAIM”**.

    c. From the **Attribute Value** list, select **Join()**. 

    d. From the **String1** list, select **User.mail**. 

    e. In the **String2** textbox, type the **unique identifier** provided by your HR2day team. 

    f. In the **Separator** textbox, type **@**.

    g. Click **Complete**.


1. Click **Apply Changes**.

2. In the menu on the top, click **Quick Start** to open the **Quick Start** dialog.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_08.png) 

3. Click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 

4. On the **How would you like users to sign on to HR2day by Merces** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_03.png) 

5. On the **Configure App Settings** dialog page, perform the following steps: 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_04.png) 

    a. In the Sign On URL textbox, type the URL used by your users to sign-on to your HR2day by Merces application using the following pattern: **“https://\<tenant name\>.force.com/\<instance name\>”**.

    b. Click **Next**.

1. On the **Configure single sign-on at HR2day by Merces** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_05.png) 
   
    a. Click **Download certificate**, and then save the file on your computer.
   
    b. Click **Next**.

2. To get SSO configured for your application, contact your HR2day by Merces support team via [servicedesk@merces.nl](emailTo:servicedesk@merces.nl) and attach the downloaded certificate file to your email. Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.

    > [!NOTE]
    > Please mention to Merces team that this integration need Entity ID to be set with this pattern **https://hr2day.force.com/INSTANCENAME**
    > 
    > 

1. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.
   
    ![Azure AD Single Sign-On][10]
2. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a>Creating an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_09.png) 

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

5. On the **Tell us about this user** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_05.png) 
   
    a. As Type Of User, select New user in your organization.
   
    b. In the User Name **textbox**, type **BrittaSimon**.
   
    c. Click **Next**.

6. On the **User Profile** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_06.png) 
   
    a. In the **First Name** textbox, type **Britta**.  
   
    b. In the **Last Name** textbox, type, **Simon**.
   
    c. In the **Display Name** textbox, type **Britta Simon**.
   
    d. In the **Role** list, select **User**.
   
    e. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_07.png) 

8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/create_aaduser_08.png) 
   
    a. Write down the value of the **New Password**.
   
    b. Click **Complete**.   

### <a name="creating-a-hr2day-by-merces-test-user"></a>Creating a HR2day by Merces test user
The objective of this section is to create a user called Britta Simon in HR2day by Merces. Please work with HR2day by Merces support team to add the users in the HR2day account. 

> [!NOTE]
> If you need to create an user manually, you need to contact the HR2day by Merces support team.
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Assigning the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.

![Assign User][200] 

**To assign Britta Simon to HR2day by Merces, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 

2. In the applications list, select **HR2day by Merces**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_50.png) 

3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 

4. In the Users list, select **Britta Simon**.

5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a>Testing Single Sign-On
The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.  
When you click the HR2day by Merces tile in the Access Panel, you should get automatically signed-on to your HR2day by Merces application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hr2day-tutorial/tutorial_general_205.png




























