---
title: 'Tutorial: Azure Active Directory integration with Tidemark | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tidemark.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: jeedes
ms.openlocfilehash: 66026beed28e865165384ba5ba57199755e55271
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552613"
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="d55d2-103">Tutorial: Azure Active Directory integration with Tidemark</span><span class="sxs-lookup"><span data-stu-id="d55d2-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>
<span data-ttu-id="d55d2-104">The objective of this tutorial is to show you how to integrate Tidemark with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d55d2-104">The objective of this tutorial is to show you how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d55d2-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d55d2-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d55d2-106">You can control in Azure AD who has access to Tidemark</span><span class="sxs-lookup"><span data-stu-id="d55d2-106">You can control in Azure AD who has access to Tidemark</span></span>
* <span data-ttu-id="d55d2-107">You can enable your users to automatically get signed-on to Tidemark single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d55d2-107">You can enable your users to automatically get signed-on to Tidemark single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d55d2-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d55d2-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d55d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d55d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d55d2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d55d2-110">Prerequisites</span></span>
<span data-ttu-id="d55d2-111">To configure Azure AD integration with Tidemark, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d55d2-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

* <span data-ttu-id="d55d2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d55d2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d55d2-113">A Tidemark single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d55d2-113">A Tidemark single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d55d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d55d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d55d2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d55d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d55d2-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d55d2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d55d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d55d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d55d2-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="d55d2-118">Scenario Description</span></span>
<span data-ttu-id="d55d2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d55d2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="d55d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d55d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="d55d2-121">Adding Tidemark from the gallery</span><span class="sxs-lookup"><span data-stu-id="d55d2-121">Adding Tidemark from the gallery</span></span>
* <span data-ttu-id="d55d2-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d55d2-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-tidemark-from-the-gallery"></a><span data-ttu-id="d55d2-123">Add Tidemark from the gallery</span><span class="sxs-lookup"><span data-stu-id="d55d2-123">Add Tidemark from the gallery</span></span>
<span data-ttu-id="d55d2-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d55d2-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d55d2-125">**To add Tidemark from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d55d2-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d55d2-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d55d2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d55d2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d55d2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d55d2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d55d2-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d55d2-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d55d2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d55d2-135">In the search box, type **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-135">In the search box, type **Tidemark**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_01.png)
7. <span data-ttu-id="d55d2-137">In the results pane, select **Tidemark**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d55d2-137">In the results pane, select **Tidemark**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d55d2-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d55d2-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d55d2-140">The objective of this section is to show you how to configure and test Azure AD SSO with Tidemark based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d55d2-140">The objective of this section is to show you how to configure and test Azure AD SSO with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d55d2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="d55d2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark to an user in Azure AD is.</span></span> <span data-ttu-id="d55d2-142">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d55d2-142">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="d55d2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d55d2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tidemark.</span></span>

<span data-ttu-id="d55d2-144">To configure and test Azure AD SSO with Tidemark, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d55d2-144">To configure and test Azure AD SSO with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d55d2-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d55d2-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d55d2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d55d2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d55d2-147">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d55d2-147">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d55d2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d55d2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d55d2-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d55d2-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d55d2-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d55d2-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="d55d2-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Tidemark application.</span><span class="sxs-lookup"><span data-stu-id="d55d2-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="d55d2-152">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d55d2-152">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="d55d2-153">In the Azure classic portal, on the **Tidemark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d55d2-153">In the Azure classic portal, on the **Tidemark** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="d55d2-155">On the **How would you like users to sign on to Tidemark** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-155">On the **How would you like users to sign on to Tidemark** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_03.png) 
3. <span data-ttu-id="d55d2-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d55d2-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_04.png)
  * <span data-ttu-id="d55d2-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Tidemark application using the following pattern: **“https://contoso.tidemark.com/login”** or **"https://contoso.tidemark.net/login"**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Tidemark application using the following pattern: **“https://contoso.tidemark.com/login”** or **"https://contoso.tidemark.net/login"**.</span></span>
4. <span data-ttu-id="d55d2-160">On the **Configure single sign-on at Tidemark** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d55d2-160">On the **Configure single sign-on at Tidemark** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_05.png)   
  1. <span data-ttu-id="d55d2-162">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d55d2-162">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d55d2-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-163">Click **Next**.</span></span>
5. <span data-ttu-id="d55d2-164">To get SSO configured for your application, contact your Tidemark support team and attach the downloaded certificate file to your email.</span><span class="sxs-lookup"><span data-stu-id="d55d2-164">To get SSO configured for your application, contact your Tidemark support team and attach the downloaded certificate file to your email.</span></span> <span data-ttu-id="d55d2-165">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="d55d2-165">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span></span>
6. <span data-ttu-id="d55d2-166">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-166">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="d55d2-168">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-168">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d55d2-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d55d2-170">Create an Azure AD test user</span></span>
<span data-ttu-id="d55d2-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d55d2-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d55d2-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d55d2-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d55d2-174">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-174">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="d55d2-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d55d2-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d55d2-177">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d55d2-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="d55d2-181">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d55d2-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="d55d2-183">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d55d2-183">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d55d2-184">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-184">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d55d2-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-185">Click **Next**.</span></span>
6. <span data-ttu-id="d55d2-186">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d55d2-186">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="d55d2-188">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-188">In the **First Name** textbox, type **Britta**.</span></span> 
  2. <span data-ttu-id="d55d2-189">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-189">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d55d2-190">In the **Display Name** textbox, type **Britta Simon**</span><span class="sxs-lookup"><span data-stu-id="d55d2-190">In the **Display Name** textbox, type **Britta Simon**</span></span>   
  4. <span data-ttu-id="d55d2-191">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-191">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d55d2-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-192">Click **Next**.</span></span>
7. <span data-ttu-id="d55d2-193">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-193">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d55d2-195">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d55d2-195">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="d55d2-197">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-197">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="d55d2-198">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-198">Click **Complete**.</span></span>   

### <a name="create-a-tidemark-test-user"></a><span data-ttu-id="d55d2-199">Create a Tidemark test user</span><span class="sxs-lookup"><span data-stu-id="d55d2-199">Create a Tidemark test user</span></span>
<span data-ttu-id="d55d2-200">The objective of this section is to create a user called Britta Simon in Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d55d2-200">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="d55d2-201">Please work with Tidemark support team to add the users in the Tidemark account.</span><span class="sxs-lookup"><span data-stu-id="d55d2-201">Please work with Tidemark support team to add the users in the Tidemark account.</span></span> 

>[!NOTE]
><span data-ttu-id="d55d2-202">If you need to create an user manually, you need to contact the Tidemark support team.</span><span class="sxs-lookup"><span data-stu-id="d55d2-202">If you need to create an user manually, you need to contact the Tidemark support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d55d2-203">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d55d2-203">Assign the Azure AD test user</span></span>
<span data-ttu-id="d55d2-204">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d55d2-204">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Tidemark.</span></span>

![Assign User][200] 

<span data-ttu-id="d55d2-206">**To assign Britta Simon to Tidemark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d55d2-206">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="d55d2-207">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d55d2-207">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="d55d2-209">In the applications list, select **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-209">In the applications list, select **Tidemark**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_50.png) 
3. <span data-ttu-id="d55d2-211">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-211">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="d55d2-213">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-213">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d55d2-214">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d55d2-214">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d55d2-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d55d2-216">Test single sign-on</span></span>
<span data-ttu-id="d55d2-217">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d55d2-217">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d55d2-218">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span><span class="sxs-lookup"><span data-stu-id="d55d2-218">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d55d2-219">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="d55d2-219">Additional Resources</span></span>
* [<span data-ttu-id="d55d2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55d2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d55d2-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d55d2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tidemark-tutorial/tutorial_general_205.png

























