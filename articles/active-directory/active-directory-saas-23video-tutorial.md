---
title: 'Tutorial: Azure Active Directory integration with 23 Video | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 23 Video.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: bdc6c41e31d27f6c13a94f3998e20f8682f3a947
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662264"
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="af6d9-103">Tutorial: Azure Active Directory integration with 23 Video</span><span class="sxs-lookup"><span data-stu-id="af6d9-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>
<span data-ttu-id="af6d9-104">The objective of this tutorial is to show you how to integrate 23 Video with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af6d9-104">The objective of this tutorial is to show you how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af6d9-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="af6d9-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="af6d9-106">You can control in Azure AD who has access to 23 Video</span><span class="sxs-lookup"><span data-stu-id="af6d9-106">You can control in Azure AD who has access to 23 Video</span></span> 
* <span data-ttu-id="af6d9-107">You can enable your users to automatically get signed-on to 23 Video single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="af6d9-107">You can enable your users to automatically get signed-on to 23 Video single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="af6d9-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af6d9-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af6d9-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af6d9-109">Prerequisites</span></span>
<span data-ttu-id="af6d9-110">To configure Azure AD integration with 23 Video, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="af6d9-110">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

* <span data-ttu-id="af6d9-111">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="af6d9-111">An Azure AD subscription</span></span>
* <span data-ttu-id="af6d9-112">A 23 Video single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="af6d9-112">A 23 Video single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="af6d9-113">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="af6d9-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="af6d9-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="af6d9-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="af6d9-115">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="af6d9-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="af6d9-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af6d9-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="af6d9-117">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="af6d9-117">Scenario Description</span></span>
<span data-ttu-id="af6d9-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="af6d9-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="af6d9-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="af6d9-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af6d9-120">Adding 23 Video from the gallery</span><span class="sxs-lookup"><span data-stu-id="af6d9-120">Adding 23 Video from the gallery</span></span> 
2. <span data-ttu-id="af6d9-121">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="af6d9-121">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="af6d9-122">Adding 23 Video from the gallery</span><span class="sxs-lookup"><span data-stu-id="af6d9-122">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="af6d9-123">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="af6d9-123">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af6d9-124">**To add 23 Video from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af6d9-124">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af6d9-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="af6d9-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="af6d9-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="af6d9-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="af6d9-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="af6d9-130">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="af6d9-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="af6d9-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="af6d9-134">In the search box, type **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-134">In the search box, type **23 Video**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="af6d9-136">In the results pane, select **23 Video**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="af6d9-136">In the results pane, select **23 Video**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][25]

## <a name="configuring-and-testing-azure-ad-sso"></a><span data-ttu-id="af6d9-138">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="af6d9-138">Configuring and testing Azure AD SSO</span></span>
<span data-ttu-id="af6d9-139">The objective of this section is to show you how to configure and test Azure AD SSO with 23 Video based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af6d9-139">The objective of this section is to show you how to configure and test Azure AD SSO with 23 Video based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af6d9-140">For SSO to work, Azure AD needs to know what the counterpart user in 23 Video to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="af6d9-140">For SSO to work, Azure AD needs to know what the counterpart user in 23 Video to an user in Azure AD is.</span></span> <span data-ttu-id="af6d9-141">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span><span class="sxs-lookup"><span data-stu-id="af6d9-141">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>  

<span data-ttu-id="af6d9-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="af6d9-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 23 Video.</span></span>

<span data-ttu-id="af6d9-143">To configure and test Azure AD SSO with 23 Video, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="af6d9-143">To configure and test Azure AD SSO with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af6d9-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="af6d9-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af6d9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af6d9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af6d9-146">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="af6d9-146">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="af6d9-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af6d9-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af6d9-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="af6d9-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="af6d9-149">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="af6d9-149">Configure Azure AD SSO</span></span>
<span data-ttu-id="af6d9-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your 23 Video application.</span><span class="sxs-lookup"><span data-stu-id="af6d9-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure SSO in your 23 Video application.</span></span>

<span data-ttu-id="af6d9-151">**To configure Azure AD SSO with 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af6d9-151">**To configure Azure AD SSO with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="af6d9-152">In the Azure classic portal, on the **23 Video** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="af6d9-152">In the Azure classic portal, on the **23 Video** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="af6d9-154">On the **How would you like users to sign on to 23 Video** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-154">On the **How would you like users to sign on to 23 Video** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="af6d9-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8] 
  1. <span data-ttu-id="af6d9-158">In the **Reply URL** textbox, type the URL used by your users to sign-on to your 23 Video site (e.g.: *https://britta-simon.23Video.com/saml/login*).</span><span class="sxs-lookup"><span data-stu-id="af6d9-158">In the **Reply URL** textbox, type the URL used by your users to sign-on to your 23 Video site (e.g.: *https://britta-simon.23Video.com/saml/login*).</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="af6d9-159">Active Directory integration using SAML 2.0 is available for all 23 Video users.</span><span class="sxs-lookup"><span data-stu-id="af6d9-159">Active Directory integration using SAML 2.0 is available for all 23 Video users.</span></span> <span data-ttu-id="af6d9-160">Please contact the Support at [support@23company.com](mailto:support@23company.com) if you need the related metadata.</span><span class="sxs-lookup"><span data-stu-id="af6d9-160">Please contact the Support at [support@23company.com](mailto:support@23company.com) if you need the related metadata.</span></span> 
    > 
 
  2. <span data-ttu-id="af6d9-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-161">Click **Next**.</span></span>
4. <span data-ttu-id="af6d9-162">On the **Configure single sign-on at 23 Video** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-162">On the **Configure single sign-on at 23 Video** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9] 
 1. <span data-ttu-id="af6d9-164">Click Download certificate, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="af6d9-164">Click Download certificate, and then save the file on your computer.</span></span>
 2. <span data-ttu-id="af6d9-165">Contact your 23 Video support team via [support@23company.com](mailto:support@23company.com), provide them with the downloaded certificate, the **Issuer URL**, the **Single Sign-On Service URL**, the **Single Sign-Out URL**, and then ask them to setup SSO for your 23 Video app.</span><span class="sxs-lookup"><span data-stu-id="af6d9-165">Contact your 23 Video support team via [support@23company.com](mailto:support@23company.com), provide them with the downloaded certificate, the **Issuer URL**, the **Single Sign-On Service URL**, the **Single Sign-Out URL**, and then ask them to setup SSO for your 23 Video app.</span></span>    
 3. <span data-ttu-id="af6d9-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-166">Click **Next**.</span></span>
5. <span data-ttu-id="af6d9-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
6. <span data-ttu-id="af6d9-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="af6d9-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="af6d9-171">Create an Azure AD test user</span></span>
<span data-ttu-id="af6d9-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af6d9-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="af6d9-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af6d9-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af6d9-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="af6d9-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="af6d9-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="af6d9-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="af6d9-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="af6d9-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="af6d9-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="af6d9-184">As Type Of User, select New user in your organization.</span></span> 
 2. <span data-ttu-id="af6d9-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-185">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="af6d9-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-186">Click **Next**.</span></span>
6. <span data-ttu-id="af6d9-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-187">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="af6d9-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-189">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="af6d9-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-190">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="af6d9-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-191">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="af6d9-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-192">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="af6d9-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-193">Click **Next**.</span></span>
7. <span data-ttu-id="af6d9-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-194">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="af6d9-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="af6d9-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-198">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="af6d9-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-199">Click **Complete**.</span></span>   

### <a name="create-a-23-video-test-user"></a><span data-ttu-id="af6d9-200">Create a 23 Video test user</span><span class="sxs-lookup"><span data-stu-id="af6d9-200">Create a 23 Video test user</span></span>
<span data-ttu-id="af6d9-201">The objective of this section is to create a user called Britta Simon in 23 Video.</span><span class="sxs-lookup"><span data-stu-id="af6d9-201">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="af6d9-202">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af6d9-202">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="af6d9-203">Sign on to your 23 Video company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="af6d9-203">Sign on to your 23 Video company site as administrator.</span></span>
2. <span data-ttu-id="af6d9-204">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-204">Go to **Settings**.</span></span>
3. <span data-ttu-id="af6d9-205">In **Users** section, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-205">In **Users** section, click **Configure**.</span></span>
   
    ![Assign User][400]
4. <span data-ttu-id="af6d9-207">Click **Add a new user**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-207">Click **Add a new user**.</span></span> 
   
    ![Assign User][401]
5. <span data-ttu-id="af6d9-209">In the **Invite someone to join this site** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af6d9-209">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Assign User][402]
 1. <span data-ttu-id="af6d9-211">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af6d9-211">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 2. <span data-ttu-id="af6d9-212">Click **Add the user**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-212">Click **Add the user**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="af6d9-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="af6d9-213">Assign the Azure AD test user</span></span>
<span data-ttu-id="af6d9-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to 23 Video.</span><span class="sxs-lookup"><span data-stu-id="af6d9-214">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to 23 Video.</span></span>

![Assign User][200] 

<span data-ttu-id="af6d9-216">**To assign Britta Simon to 23 Video, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af6d9-216">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="af6d9-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="af6d9-217">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="af6d9-219">In the applications list, select **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-219">In the applications list, select **23 Video**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="af6d9-221">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-221">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="af6d9-223">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-223">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="af6d9-224">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="af6d9-224">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="af6d9-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="af6d9-226">Test single sign-on</span></span>
<span data-ttu-id="af6d9-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="af6d9-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="af6d9-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span><span class="sxs-lookup"><span data-stu-id="af6d9-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af6d9-229">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="af6d9-229">Additional Resources</span></span>
* [<span data-ttu-id="af6d9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af6d9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af6d9-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af6d9-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_01.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_02.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_07.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-23video-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_general_205.png

[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
































