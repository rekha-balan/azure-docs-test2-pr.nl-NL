---
title: 'Tutorial: Azure Active Directory integration with SilkRoad Life Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SilkRoad Life Suite.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d0b2675baf8d9d595585d8fc1a0116b416fbb9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564178"
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Tutorial: Azure Active Directory integration with SilkRoad Life Suite
The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD). 

Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to SilkRoad Life Suite 
* You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with SilkRoad Life Suite, you need the following items:

* An Azure AD subscription
* A SilkRoad Life Suite SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding SilkRoad Life Suite from the gallery 
2. Configuring and testing Azure AD SSO

## <a name="add-silkroad-life-suite-from-the-gallery"></a>Add SilkRoad Life Suite from the gallery
To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.

**To add SilkRoad Life Suite from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]

4. Click **Add** at the bottom of the page.
   
    ![Applications][3]

5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]

6. In the search box, type **SilkRoad Life Suite**.
   
    ![Applications][5]

7. In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.
   
    ![Applications][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on
The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.

To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on
The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.

**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**

1. Sign-on to your SilkRoad company site as administrator. 

  >[!NOTE] 
  > To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.
  > 

2. Go to **Service Provider**, and then click **Federation Details**. 
   
    ![Azure AD Single Sign-On][10] 

3. Click **Download Federation Metadata**, and then save the metadata file on your computer.
   
    ![Azure AD Single Sign-On][11] 

4. In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 

5. On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Azure AD Single Sign-On][7] 

6. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Azure AD Single Sign-On][8]   
 1. In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Open the downloaded **Silkroad** metadata file. 
 3. Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.         
   
    ![Azure AD Single Sign-On][21] 
 4. Paste the value into the **Reply URL** textbox.  
 5. Click **Next**.

6. On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:
   
    ![Azure AD Single Sign-On][9]  
 1. Click Download certificate, and then save the file on your computer.  
 2. Click **Next**.

7. In your **SilkRoad** application, click **Authentication Sources**.
   
    ![Azure AD Single Sign-On][12] 

8. Click **Add Authentication Source**. 
   
    ![Azure AD Single Sign-On][13] 

9. In the **Add Authentication Source** section, perform the following steps: 
   
    ![Azure AD Single Sign-On][14]  
 1. Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.  
 2. Click **Create Identity Provider using File Data**.

10. In the **Authentication Sources** section, click **Edit**. 
    
     ![Azure AD Single Sign-On][15] 

11. On the **Edit Authentication Source** dialog, perform the following steps: 
    
     ![Azure AD Single Sign-On][16] 
 1. As **Enabled**, select **Yes**.   
 2. In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).  
 3. In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).  
 4. Click **Save**.

12. Disable all other authentication sources. 
    
     ![Azure AD Single Sign-On][17]

13. In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.  
    
     ![Azure AD Single Sign-On][18]

14. On the **Single sign-on confirmation** page, click **Complete**.
    
     ![Azure AD Single Sign-On][19]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. As Type Of User, select New user in your organization.  
 2. In the User Name **textbox**, type **BrittaSimon**. 
 3. Click **Next**.

6. On the **User Profile** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. In the **First Name** textbox, type **Britta**.    
 2. In the **Last Name** textbox, type, **Simon**. 
 3. In the **Display Name** textbox, type **Britta Simon**. 
 4. In the **Role** list, select **User**.
 5. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Write down the value of the **New Password**. 
 2. Click **Complete**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Create a SilkRoad Life Suite test user
The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite. Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.

**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**

- Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.

![Assign User][200] 

**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 

2. In the applications list, select **SilkRoad Life Suite**.
   
    ![Assign User][202] 

3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 

4. In the Users list, select **Britta Simon**.

5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSO configuration using the Access Panel.  

When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png







































