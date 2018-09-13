---
title: 'Tutorial: Azure Active Directory integration with PerformanceCentre | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PerformanceCentre.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: db83d30cf5cef08832d0947f7adb6371e2a2267c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549801"
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a>Tutorial: Azure Active Directory integration with PerformanceCentre
The objective of this tutorial is to show you how to integrate PerformanceCentre with Azure Active Directory (Azure AD).  

Integrating PerformanceCentre with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to PerformanceCentre 
* You can enable your users to automatically get signed-on to PerformanceCentre single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure Active Directory classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with PerformanceCentre, you need the following items:

* An Azure AD subscription
* A PerformanceCentre single-sign (SSO) on enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment.
> 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.  

The scenario outlined in this tutorial consists of these main building blocks:

*  Adding PerformanceCentre from the gallery 
*  Configuring and testing Azure AD SSO

## <a name="add-performancecentre-from-the-gallery"></a>Add PerformanceCentre from the gallery
To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.

**To add PerformanceCentre from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **PerformanceCentre**.
   
    ![Applications][5]
7. In the results pane, select **PerformanceCentre**, and then click **Complete** to add the application.
   
    ![Applications][500]

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
The objective of this section is to show you how to configure and test Azure AD SSO with PerformanceCentre based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in PerformanceCentre to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.  

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PerformanceCentre.

**To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:**

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a PerformanceCentre test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on
The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your PerformanceCentre application.

**To configure Azure AD SSO with PerformanceCentre, perform the following steps:**

1. In the Azure AD classic portal, on the **PerformanceCentre** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6] 
2. On the **How would you like users to sign on to PerformanceCentre** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Azure AD Single Sign-On][7] 
3. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Azure AD Single Sign-On][8] 
   
   1. In the **Sign On URL** textbox, type the URL used by your users to sign-on to your PerformanceCentre site (e.g.: *http://companyname.performancecentre.com/saml/SSO*).
   2. Click **Next**.
4. On the **Configure single sign-on at PerformanceCentre** page, perform the following steps:
   
    ![Azure AD Single Sign-On][9] 
   
  * Click **Download metadata**, and then save the file on your computer.
5. Sign-on to your **PerformanceCentre** company site as administrator.
6. In the tab on the left side, click **Configure**.
   
    ![Azure AD Single Sign-On][10]
7. In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.
   
    ![Azure AD Single Sign-On][11]
8. As **Protocol**, select **SAML**.
   
    ![Azure AD Single Sign-On][12]
9. Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.
   
    ![Azure AD Single Sign-On][13]
10. Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.
    
     ![Azure AD Single Sign-On][14]
11. On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**. 
    
     ![Azure AD Single Sign-On][15]
12. On the **Single sign-on confirmation** page, click **Complete**.  
    
     ![Azure AD Single Sign-On][16]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.  

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_09.png)  
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_05.png)  
   
   1. As Type Of User, select New user in your organization.
   2. In the User Name **textbox**, type **BrittaSimon**.
   3. Click **Next**.
   
6. On the **User Profile** dialog page, perform the following steps: 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_06.png) 
   
   1. In the **First Name** textbox, type **Britta**.  
   2. In the **Last Name** textbox, type, **Simon**.
   3. In the **Display Name** textbox, type **Britta Simon**.
   4. In the **Role** list, select **User**.
   5. Click **Next**.
   
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/create_aaduser_08.png) 
   
   1. Write down the value of the **New Password**.
   2. Click **Complete**.   

### <a name="create-a-performancecentre-test-user"></a>Create a PerformanceCentre test user
The objective of this section is to create a user called Britta Simon in PerformanceCentre.

**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**

1. Sign on to your PerformanceCentre company site as administrator.
2. In the menu on the left, click **Interrelate**, and then click **Create Participant**.
   
    ![Create User][400]
3. On the **Interrelate - Create Participant** dialog, perform the following steps:
   
    ![Create User][401]
   
   1. Type the required attributes for Britta Simon into related textboxes.

    >[!IMPORTANT]
    >Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.
    > 
    > 
 
   2. Select **Client Administrator** as **Choose Role**.
   3. Click **Save**.   


### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to PerformanceCentre.

![Assign User][200] 

**To assign Britta Simon to PerformanceCentre, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201]
2. In the applications list, select **PerformanceCentre**.
   
    ![Assign User][202]
3. In the menu on the top, click **Users**.
   
    ![Assign User][203]
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSO configuration using the Access Panel.  

When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_01.png
[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_06.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_07.png


[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_50.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_general_205.png


[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png
[402]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_402.png


































