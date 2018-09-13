---
title: 'Tutorial: Azure Active Directory integration with Namely | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Namely.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: prasannas
editor: ''
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 46a8b3bd71fa145e823484c601b40bf53a8e6b8c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563147"
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="91ee0-103">Tutorial: Azure Active Directory integration with Namely</span><span class="sxs-lookup"><span data-stu-id="91ee0-103">Tutorial: Azure Active Directory integration with Namely</span></span>
<span data-ttu-id="91ee0-104">The objective of this tutorial is to show you how to integrate Namely with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91ee0-104">The objective of this tutorial is to show you how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91ee0-105">Integrating Namely with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="91ee0-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="91ee0-106">You can control in Azure AD who has access to Namely</span><span class="sxs-lookup"><span data-stu-id="91ee0-106">You can control in Azure AD who has access to Namely</span></span> 
* <span data-ttu-id="91ee0-107">You can enable your users to automatically get signed-on to Namely single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="91ee0-107">You can enable your users to automatically get signed-on to Namely single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="91ee0-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="91ee0-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="91ee0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91ee0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91ee0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91ee0-110">Prerequisites</span></span>
<span data-ttu-id="91ee0-111">To configure Azure AD integration with Namely, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="91ee0-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

* <span data-ttu-id="91ee0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="91ee0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="91ee0-113">A Namely SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="91ee0-113">A Namely SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="91ee0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="91ee0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="91ee0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="91ee0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="91ee0-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="91ee0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="91ee0-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91ee0-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="91ee0-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="91ee0-118">Scenario Description</span></span>
<span data-ttu-id="91ee0-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="91ee0-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="91ee0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="91ee0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91ee0-121">Adding Namely from the gallery</span><span class="sxs-lookup"><span data-stu-id="91ee0-121">Adding Namely from the gallery</span></span> 
2. <span data-ttu-id="91ee0-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="91ee0-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-namely-from-the-gallery"></a><span data-ttu-id="91ee0-123">Add Namely from the gallery</span><span class="sxs-lookup"><span data-stu-id="91ee0-123">Add Namely from the gallery</span></span>
<span data-ttu-id="91ee0-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="91ee0-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91ee0-125">**To add Namely from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91ee0-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91ee0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="91ee0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="91ee0-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="91ee0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="91ee0-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="91ee0-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="91ee0-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="91ee0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="91ee0-135">In the search box, type **Namely**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-135">In the search box, type **Namely**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_01.png)
7. <span data-ttu-id="91ee0-137">In the results pane, select **Namely**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="91ee0-137">In the results pane, select **Namely**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="91ee0-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="91ee0-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="91ee0-140">The objective of this section is to show you how to configure and test Azure AD SSO with Namely based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91ee0-140">The objective of this section is to show you how to configure and test Azure AD SSO with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91ee0-141">For SSO to work, Azure AD needs to know what the counterpart user in Namely to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="91ee0-141">For SSO to work, Azure AD needs to know what the counterpart user in Namely to an user in Azure AD is.</span></span> <span data-ttu-id="91ee0-142">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span><span class="sxs-lookup"><span data-stu-id="91ee0-142">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="91ee0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Namely.</span><span class="sxs-lookup"><span data-stu-id="91ee0-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Namely.</span></span>

<span data-ttu-id="91ee0-144">To configure and test Azure AD SSO with Namely, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="91ee0-144">To configure and test Azure AD SSO with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91ee0-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="91ee0-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91ee0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91ee0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91ee0-147">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="91ee0-147">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="91ee0-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91ee0-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91ee0-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="91ee0-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="91ee0-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="91ee0-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="91ee0-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Namely application.</span><span class="sxs-lookup"><span data-stu-id="91ee0-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Namely application.</span></span> 

<span data-ttu-id="91ee0-152">**To configure Azure AD SSO with Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91ee0-152">**To configure Azure AD SSO with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="91ee0-153">In the Azure classic portal, on the **Namely** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="91ee0-153">In the Azure classic portal, on the **Namely** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="91ee0-155">On the **How would you like users to sign on to Namely** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-155">On the **How would you like users to sign on to Namely** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_03.png) 
3. <span data-ttu-id="91ee0-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="91ee0-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_04.png) 
  1. <span data-ttu-id="91ee0-159">In the **Sign On URL** textbox, type the URL used by your users to sign on to your Namely application (e.g.: *https://fabrikam.Namely.com/*).</span><span class="sxs-lookup"><span data-stu-id="91ee0-159">In the **Sign On URL** textbox, type the URL used by your users to sign on to your Namely application (e.g.: *https://fabrikam.Namely.com/*).</span></span>
  2. <span data-ttu-id="91ee0-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-160">Click **Next**.</span></span>
4. <span data-ttu-id="91ee0-161">On the **Configure single sign-on at Namely** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-161">On the **Configure single sign-on at Namely** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_05.png) 
  1. <span data-ttu-id="91ee0-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="91ee0-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="91ee0-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-164">Click **Next**.</span></span>
5. <span data-ttu-id="91ee0-165">In another browser window, sign on to your Namely company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="91ee0-165">In another browser window, sign on to your Namely company site as an administrator.</span></span>
6. <span data-ttu-id="91ee0-166">In the toolbar on the top, click **Company**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-166">In the toolbar on the top, click **Company**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 
7. <span data-ttu-id="91ee0-168">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="91ee0-168">Click the **Settings** tab.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 
8. <span data-ttu-id="91ee0-170">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-170">Click **SAML**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 
9. <span data-ttu-id="91ee0-172">On the **SAML Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-172">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_09.png) 
  1. <span data-ttu-id="91ee0-174">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-174">Click **Enable SAML**.</span></span> 
  2. <span data-ttu-id="91ee0-175">In the Azure classic portal, on the **Configure single sign-on at Namely** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity provider SSO url** textbox.</span><span class="sxs-lookup"><span data-stu-id="91ee0-175">In the Azure classic portal, on the **Configure single sign-on at Namely** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity provider SSO url** textbox.</span></span> 
  3. <span data-ttu-id="91ee0-176">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="91ee0-176">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>     
  4. <span data-ttu-id="91ee0-177">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-177">Click **Save**.</span></span>
10. <span data-ttu-id="91ee0-178">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-178">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
    
     ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="91ee0-180">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-180">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91ee0-182">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91ee0-182">Create an Azure AD test user</span></span>
<span data-ttu-id="91ee0-183">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91ee0-183">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="91ee0-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91ee0-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91ee0-186">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-186">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="91ee0-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="91ee0-188">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="91ee0-189">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-189">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="91ee0-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-191">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="91ee0-193">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-193">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="91ee0-195">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="91ee0-195">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="91ee0-196">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-196">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="91ee0-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-197">Click **Next**.</span></span>
6. <span data-ttu-id="91ee0-198">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-198">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="91ee0-200">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-200">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="91ee0-201">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-201">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="91ee0-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-202">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="91ee0-203">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-203">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="91ee0-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-204">Click **Next**.</span></span>
7. <span data-ttu-id="91ee0-205">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-205">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="91ee0-207">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-207">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="91ee0-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-209">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="91ee0-210">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-210">Click **Complete**.</span></span>   

### <a name="create-a-namely-test-user"></a><span data-ttu-id="91ee0-211">Create a Namely test user</span><span class="sxs-lookup"><span data-stu-id="91ee0-211">Create a Namely test user</span></span>
<span data-ttu-id="91ee0-212">The objective of this section is to create a user called Britta Simon in Namely.</span><span class="sxs-lookup"><span data-stu-id="91ee0-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="91ee0-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91ee0-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="91ee0-214">Sign-on to your Namely company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="91ee0-214">Sign-on to your Namely company site as an administrator.</span></span>
2. <span data-ttu-id="91ee0-215">In the toolbar on the top, click **People**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 
3. <span data-ttu-id="91ee0-217">Click the **Directory** tab.</span><span class="sxs-lookup"><span data-stu-id="91ee0-217">Click the **Directory** tab.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 
4. <span data-ttu-id="91ee0-219">Click **Add New Person**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-219">Click **Add New Person**.</span></span>
5. <span data-ttu-id="91ee0-220">On the **Add New Person** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91ee0-220">On the **Add New Person** dialog, perform the following steps:</span></span>
  1. <span data-ttu-id="91ee0-221">In the **First name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-221">In the **First name** textbox, type **Britta**.</span></span>
  2. <span data-ttu-id="91ee0-222">In the **Last name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-222">In the **Last name** textbox, type **Simon**.</span></span>
  3. <span data-ttu-id="91ee0-223">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="91ee0-223">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span></span>
  4. <span data-ttu-id="91ee0-224">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-224">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="91ee0-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91ee0-225">Assign the Azure AD test user</span></span>
<span data-ttu-id="91ee0-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Namely.</span><span class="sxs-lookup"><span data-stu-id="91ee0-226">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Namely.</span></span>

![Assign User][200] 

<span data-ttu-id="91ee0-228">**To assign Britta Simon to Namely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91ee0-228">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="91ee0-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="91ee0-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="91ee0-231">In the applications list, select **Namely**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-231">In the applications list, select **Namely**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_namely_50.png) 
3. <span data-ttu-id="91ee0-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="91ee0-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="91ee0-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="91ee0-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="91ee0-238">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="91ee0-238">Test single sign-on</span></span>
<span data-ttu-id="91ee0-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="91ee0-239">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="91ee0-240">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application.</span><span class="sxs-lookup"><span data-stu-id="91ee0-240">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91ee0-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="91ee0-241">Additional Resources</span></span>
* [<span data-ttu-id="91ee0-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91ee0-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91ee0-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91ee0-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-namely-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-namely-tutorial/tutorial_general_205.png





































