---
title: 'Tutorial: Azure Active Directory integration with Amazon Web Services (AWS) | Microsoft Docs'
description: Learn how to use Amazon Web Services (AWS) with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 2aafe870e60a091f4f4687bd8e12edabda4d869e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556698"
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)
The objective of this tutorial is to show you how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).  

Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits: 

* You can control in Azure AD who has access to Amazon Web Services (AWS) 
* You can enable your users to automatically get signed-on to Amazon Web Services (AWS) single sign-on (SSO) with their Azure AD accounts
* You can manage your accounts in one central location - the Azure classic portal

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisites
To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:

* An Azure AD subscription
* An Amazon Web Services (AWS) SSO enabled subscription

>[!NOTE]
>To test the steps in this tutorial, we do not recommend using a production environment. 
> 

To test the steps in this tutorial, you should follow these recommendations:

* You should not use your production environment, unless this is necessary.
* If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenario Description
The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.  

The scenario outlined in this tutorial consists of two main building blocks:

1. Adding Amazon Web Services (AWS) from the gallery 
2. Configuring and testing Azure AD SSO

## <a name="add-amazon-web-services-aws-from-the-gallery"></a>Add Amazon Web Services (AWS) from the gallery
To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.

**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**. 
   
    ![Active Directory][1] 

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To open the applications view, in the directory view, click **Applications** in the top menu. 
   
    ![Applications][2]

4. Click **Add** at the bottom of the page. 
   
    ![Applications][3]

5. On the **What do you want to do** dialog, click **Add an application from the gallery**. 
   
    ![Applications][4]

6. In the search box, type **Amazon Web Services (AWS)**.
   
    ![Applications][5]

7. In the results pane, select **Amazon Web Services (AWS)**, and then click **Complete** to add the application.
   
    ![Applications][6]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configure and test Azure AD single sign-on
The objective of this section is to show you how to configure and test Azure AD SSO with Amazon Web Services (AWS) based on a test user called "Britta Simon".

For SSO to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) to an user in Azure AD is. In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.  

This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).

To configure and test Azure AD SSO with Amazon Web Services (AWS), you need to complete the following building blocks:

1. **[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.
2. **[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
3. **[Creating a Amazon Web Services (AWS) test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.
4. **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.

### <a name="configure-azure-ad-single-sign-on"></a>Configure Azure AD single sign-on
The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your Amazon Web Services (AWS) application.  

Your Amazon Web Services (AWS) application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration. 

The following screenshot shows an example for this.

![Configure Single Sign-On][27]

**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**

1. In the Azure classic portal, on the **Amazon Web Services (AWS)** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.
   
    ![Configure Single Sign-On][7]

2. On the **How would you like users to sign on to Amazon Web Services (AWS)** page, select **Azure AD Single Sign-On**, and then click **Next**.
   
    ![Configure Single Sign-On][8]

3. On the **Configure App Settings** dialog page, click **Next**. 
   
    ![Configure App Settings][9]

4. On the **Configure single sign-on at Amazon Web Services (AWS)** page, click **Download metadata**, and then save the metadata file locally on your computer.
   
    ![Configure Single Sign-On][10]

5. In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.

6. Click **Console Home**.
   
    ![Configure Single Sign-On][11]

7. Click **Identity and Access Management**. 
   
    ![Configure Single Sign-On][12]

8. Click **Identity Providers**, and then click **Create Provider**. 
   
    ![Configure Single Sign-On][13]

9. On the **Configure Provider** dialog page, perform the following steps: 
   
    ![Configure Single Sign-On][14]   
  1. As **Provider Type**, select **SAML**.
  2. In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).
  3. To upload your downloaded metadata file, click **Choose File**.
  4. Click **Next Step**.

10. On the **Verify Provider Information** dialog page, click **Create**. 
    
    ![Configure Single Sign-On][15]

11. Click **Roles**, and then click **Create New Role**. 
    
    ![Configure Single Sign-On][16]

12. On the **Set Role Name** dialog, perform the following steps: 
    
    ![Configure Single Sign-On][17] 
  1. In the **Role Name** textbox, type a role name (e.g.: *TestUser*). 
  2. Click **Next Step**.

13. On the **Select Role Type** dialog, perform the following steps: 
    
    ![Configure Single Sign-On][18] 
  1. Select **Role For Identity Provider Access**. 
  2. In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.

14. On the **Establish Trust** dialog, perform the following steps:  
    
    ![Configure Single Sign-On][19] 
  1. As SAML provider, select the SAML provider you have created previousley (e.g.: *WAAD*)   
  2. Click **Next Step**.

15. On the **Verify Role Trust** dialog, click **Next Step**. 
    
    ![Configure Single Sign-On][32]

16. On the **Attach Policy** dialog, click **Next Step**.  
    
    ![Configure Single Sign-On][33]

17. On the **Review** dialog, perform the following steps:   
    
    ![Configure Single Sign-On][34] 
  1. Copy the **Role ARN** value.  
  2. Copy the **Trusted Entities** ARN value. 
  3. Click **Create Role**. 

18. On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.
    
    ![What is Azure AD Connect][20]

19. On the **Single sign-on confirmation** page, click **Complete** to close the **Configure single sign-on** dialog.
    
    ![What is Azure AD Connect][22]

20. In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog. 
    
    ![Configure Single Sign-On][21]

21. Click **add user attribute**. 
    
    ![Configure Single Sign-On][23]

22. On the Add User Attribute dialog, perform the following steps. 
    
    ![Configure Single Sign-On][24]  
  1. In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/Role**.  
  2. In the **Attribute Value** textbox, type **[the Role ARN value],[the Trusted Entity ARN value]**.
    
     >[!TIP]
     >These are the values you have copied from the Review dialog when you have created your role. 
     > 
     
  3. Click **Complete** to close the **Add User Attribute** dialog.

23. Click **add user attribute**. 
    
    ![Configure Single Sign-On][23]

24. On the Add User Attribute dialog, perform the following steps, and then click **Apply Changes**. 
    
    ![Configure Single Sign-On][25]
 1. In the **Attribute Name** textbox, type **https://aws.amazon.com/SAML/Attributes/RoleSessionName**.
 2. In the **Attribute Value** textbox, type or select **user.userprincipalname** from the drop down list.

     ![Configure Single Sign-On][35]
 3. Click **Complete** to close the **Add User Attribute** dialog.

### <a name="create-an-azure-ad-test-user"></a>Create an Azure AD test user
The objective of this section is to create a test user in the Azure classic portal called Britta Simon.

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png)

**To create a test user in Azure AD, perform the following steps:**

1. In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

2. From the **Directory** list, select the directory for which you want to enable directory integration.

3. To display the list of users, in the menu on the top, click **Users**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**. 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

5. On the **Tell us about this user** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_05.png) 
 1. As Type Of User, select New user in your organization.
 2. In the User Name **textbox**, type **BrittaSimon**.
 3. Click Next.

6. On the **User Profile** dialog page, perform the following steps: 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_06.png)  
 1. In the **First Name** textbox, type **Britta**.   
 2. In the **Last Name** txtbox, type, **Simon**. 
 3. In the **Display Name** textbox, type **Britta Simon**. 
 4. In the **Role** list, select **User**. 
 5. Click **Next**.

7. On the **Get temporary password** dialog page, click **create**.
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_07.png) 

8. On the **Get temporary password** dialog page, perform the following steps:
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_08.png)  
 1. Write down the value of the **New Password**.  
 2. Click **Complete**.   

### <a name="create-a-amazon-web-services-aws-test-user"></a>Create a Amazon Web Services (AWS) test user
The objective of this section is to create a user called Britta Simon in Amazon Web Services (AWS).

**To create a user called Britta Simon in Amazon Web Services (AWS), perform the following steps:**

1. Log in to your **Amazon Web Services (AWS)** company site as administrator.

2. Click the **Console Home** icon. 
   
    ![Configure Single Sign-On][11]

3. Click Identity and Access Management. 
   
    ![Configure Single Sign-On][28]

4. In the Dashboard, click Users, and then click Create New Users. 
   
    ![Configure Single Sign-On][29]

5. On the Create User dialog, perform the following steps: 
   
    ![Configure Single Sign-On][30]   
 1. In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD. 
 2. Click **Create**.

### <a name="assign-the-azure-ad-test-user"></a>Assign the Azure AD test user
The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Amazon Web Services (AWS).

![Assign User][31]

**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**

1. On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.
   
    ![Assign User][26]

2. In the applications list, select **Amazon Web Services (AWS)**.
   
    ![Assign User][27]

3. In the menu on the top, click **Users**.
   
    ![Assign User][25]

4. In the Users list, select **Britta Simon**.

5. In the toolbar on the bottom, click **Assign**.
   
    ![Assign User][29]

### <a name="test-single-sign-on"></a>Test single sign-on
The objective of this section is to test your Azure AD SSO configuration using the Access Panel.  

When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.

## <a name="additional-resources"></a>Additional Resources
* [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795019.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795020.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795027.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795028.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/capture23.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/capture24.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_18.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950357.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_16.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_17.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-amazon-web-service-tutorial/user_attributes_01.png

































































