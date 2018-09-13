---
title: 'Tutorial: Azure Active Directory integration with TargetProcess | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TargetProcess.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d3ae285bf6399f14ca938268dec3672db8633ed8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550160"
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a>Tutorial: Azure Active Directory integration with TargetProcess
The objective of this tutorial is to show you how to integrate TargetProcess with Azure Active Directory (Azure AD).

Integrating TargetProcess with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to TargetProcess 
* You can enable your users to automatically get signed-on to TargetProcess single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure Active Directory classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with TargetProcess, you need the following items:

* An Azure AD subscription
* A TargetProcess SSO on enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD SSO in a test environment. 

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding TargetProcess from the gallery 
2. Configuring and testing Azure AD SSO

## <a name="adding-targetprocess-from-the-gallery"></a>Adding TargetProcess from the gallery
To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.

**To add TargetProcess from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1]
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Applications][2]
4. Click **Add** at the bottom of the page.
   
    ![Applications][3]
5. On the **What do you want to do** dialog, click **Add an application from the gallery**.
   
    ![Applications][4]
6. In the search box, type **TargetProcess**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_01.png)
7. In the results pane, select **TargetProcess**, and then click **Complete** to add the application.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_10.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configure and test Azure AD SSO
The objective of this section is to show you how to configure and test Azure AD SSO with TargetProcess based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in TargetProcess to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TargetProcess.

To configure and test Azure AD SSO with TargetProcess, you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a TargetProcess test user](#creating-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-sso"></a>Configure Azure AD SSO
The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your TargetProcess application. 

As part of this procedure, you are required to create a base-64 encoded certificate file. If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).

To configure SSO for TargetProcess, you need a registered domain. If you don't have a registered domain yet, contact your TargetProcess support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).  

**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**

1. In the Azure AD classic portal, on the **TargetProcess** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][6]
2. On the **How would you like users to sign on to TargetProcess** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_02.png) 
3. On the **Configure App Settings** dialog page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_03.png) 
  1. In the **Sign On URL** textbox, type the URL used by your users to sign-on to your TargetProcess application (e.g.: *https://fabrikam.TargetProcess.com/*).
  2. Click **Next**.
4. On the **Configure single sign-on at TargetProcess** page, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_04.png)   
  1. Click **Download certificate**, and then save the file on your computer.
  2. Click **Next**.
5. Sign-on to your TargetProcess application as an administrator.
6. In the menu on the top, click **Setup**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)
7. Click **Settings**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 
8. Click **Single Sign-on**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 
9. On the Single Sign-on settings dialog, perform the following steps:
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)   
  1. Click **Enable Single Sign-on**.
  2. In the Azure classic portal, on the **Configure single sign-on at TargetProcess** page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-on URL** textbox.
  3. Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.
  4. click **Enable JIT Provisioning**.
10. In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**. 
   
    ![Azure AD Single Sign-On][10]
11. On the **Single sign-on confirmation** page, click **Complete**.  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.

* In the Users list, select **Britta Simon**.

![Create Azure AD User][20]

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_09.png)  
2. From the **Directory** list, select the directory for which you want to enable directory integration.
3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 
4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 
5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_05.png)   
  1. As Type Of User, select New user in your organization. 
  2. In the User Name **textbox**, type **BrittaSimon**.
  3. Click **Next**.
6. On the **User Profile** dialog page, perform the following steps: 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_06.png) 
  1. In the **First Name** textbox, type **Britta**.  
  2. In the **Last Name** textbox, type, **Simon**.
  3. In the **Display Name** textbox, type **Britta Simon**.
  4. In the **Role** list, select **User**.
  5. Click **Next**.
7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_07.png) 
8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_08.png) 
  1. Write down the value of the **New Password**.
  2. Click **Complete**.   

### <a name="create-a-targetprocess-test-user"></a>Create a TargetProcess test user
The objective of this section is to create a user called Britta Simon in TargetProcess.

TargetProcess supports just-in-time provisioning. You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).

There is no action item for you in this section.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure AD SSO by granting her access to TargetProcess.

![Assign User][200] 

**To assign Britta Simon to TargetProcess, perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][201] 
2. In the applications list, select **TargetProcess**.
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_09.png) 
3. In the menu on the top, click **Users**.
   
    ![Assign User][203] 
4. In the Users list, select **Britta Simon**.
5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.

When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_205.png



































