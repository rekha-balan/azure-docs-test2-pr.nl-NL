---
title: 'Tutorial: Azure Active Directory integration with QuickHelp | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and QuickHelp.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: d8858def16502643ac835eaaf21f0916f3878edd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662244"
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="56a41-103">Tutorial: Azure Active Directory integration with QuickHelp</span><span class="sxs-lookup"><span data-stu-id="56a41-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>
<span data-ttu-id="56a41-104">The objective of this tutorial is to show you how to integrate QuickHelp with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56a41-104">The objective of this tutorial is to show you how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="56a41-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="56a41-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="56a41-106">You can control in Azure AD who has access to QuickHelp</span><span class="sxs-lookup"><span data-stu-id="56a41-106">You can control in Azure AD who has access to QuickHelp</span></span> 
* <span data-ttu-id="56a41-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="56a41-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="56a41-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="56a41-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="56a41-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56a41-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56a41-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="56a41-110">Prerequisites</span></span>
<span data-ttu-id="56a41-111">To configure Azure AD integration with QuickHelp, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="56a41-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

* <span data-ttu-id="56a41-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="56a41-112">An Azure AD subscription</span></span>
* <span data-ttu-id="56a41-113">A QuickHelp single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="56a41-113">A QuickHelp single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56a41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="56a41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="56a41-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="56a41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="56a41-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="56a41-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="56a41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56a41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="56a41-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="56a41-118">Scenario Description</span></span>
<span data-ttu-id="56a41-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="56a41-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="56a41-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="56a41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56a41-121">Adding QuickHelp from the gallery</span><span class="sxs-lookup"><span data-stu-id="56a41-121">Adding QuickHelp from the gallery</span></span> 
2. <span data-ttu-id="56a41-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56a41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="56a41-123">Adding QuickHelp from the gallery</span><span class="sxs-lookup"><span data-stu-id="56a41-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="56a41-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="56a41-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56a41-125">**To add QuickHelp from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56a41-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56a41-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56a41-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="56a41-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="56a41-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="56a41-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="56a41-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="56a41-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="56a41-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="56a41-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="56a41-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="56a41-135">In the search box, type **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="56a41-135">In the search box, type **QuickHelp**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="56a41-137">In the results pane, select **QuickHelp**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="56a41-137">In the results pane, select **QuickHelp**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][500]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56a41-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="56a41-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56a41-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56a41-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56a41-141">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="56a41-141">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56a41-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="56a41-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56a41-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56a41-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56a41-144">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="56a41-144">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="56a41-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="56a41-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56a41-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="56a41-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56a41-147">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56a41-147">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="56a41-148">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your QuickHelp application.</span><span class="sxs-lookup"><span data-stu-id="56a41-148">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="56a41-149">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56a41-149">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="56a41-150">In the Azure classic portal, on the **QuickHelp** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="56a41-150">In the Azure classic portal, on the **QuickHelp** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="56a41-152">On the **How would you like users to sign on to QuickHelp** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56a41-152">On the **How would you like users to sign on to QuickHelp** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="56a41-154">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56a41-154">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure App Settings][8] 
   
    <span data-ttu-id="56a41-156">a.</span><span class="sxs-lookup"><span data-stu-id="56a41-156">a.</span></span> <span data-ttu-id="56a41-157">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your QuickHelp site (e.g.:\* https://quickhelp.com/bsiazure/\*).</span><span class="sxs-lookup"><span data-stu-id="56a41-157">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your QuickHelp site (e.g.:\* https://quickhelp.com/bsiazure/\*).</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="56a41-158">Please contact your QuickHelp support team if you don't know the value of the Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="56a41-158">Please contact your QuickHelp support team if you don't know the value of the Sign On URL.</span></span>
    > 
    > 
   
    <span data-ttu-id="56a41-159">b.</span><span class="sxs-lookup"><span data-stu-id="56a41-159">b.</span></span> <span data-ttu-id="56a41-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56a41-160">Click **Next**.</span></span>
4. <span data-ttu-id="56a41-161">On the **Configure single sign-on at QuickHelp** page, perform the following steps:click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="56a41-161">On the **Configure single sign-on at QuickHelp** page, perform the following steps:click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![What is Azure AD Connect][9] 
5. <span data-ttu-id="56a41-163">Sign-on to your QuickHelp company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="56a41-163">Sign-on to your QuickHelp company site as administrator.</span></span>
6. <span data-ttu-id="56a41-164">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="56a41-164">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On][21]
7. <span data-ttu-id="56a41-166">In the **QuickHelp Admin** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="56a41-166">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configure Single Sign-On][22]
8. <span data-ttu-id="56a41-168">Click **Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="56a41-168">Click **Authentication Settings**.</span></span>
9. <span data-ttu-id="56a41-169">On the **Authentication Settings** page, perform the following steps</span><span class="sxs-lookup"><span data-stu-id="56a41-169">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configure Single Sign-On][23]
   
    <span data-ttu-id="56a41-171">a.</span><span class="sxs-lookup"><span data-stu-id="56a41-171">a.</span></span> <span data-ttu-id="56a41-172">As **SSO Type**, select **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="56a41-172">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="56a41-173">b.</span><span class="sxs-lookup"><span data-stu-id="56a41-173">b.</span></span> <span data-ttu-id="56a41-174">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="56a41-174">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="56a41-175">c.</span><span class="sxs-lookup"><span data-stu-id="56a41-175">c.</span></span> <span data-ttu-id="56a41-176">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="56a41-176">In the **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
   
    <span data-ttu-id="56a41-177">d.</span><span class="sxs-lookup"><span data-stu-id="56a41-177">d.</span></span> <span data-ttu-id="56a41-178">In the **First Name** textbox, **type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="56a41-178">In the **First Name** textbox, **type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
   
    <span data-ttu-id="56a41-179">e.</span><span class="sxs-lookup"><span data-stu-id="56a41-179">e.</span></span> <span data-ttu-id="56a41-180">In the **Last Name** textbox, **type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="56a41-180">In the **Last Name** textbox, **type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
   
    <span data-ttu-id="56a41-181">f.</span><span class="sxs-lookup"><span data-stu-id="56a41-181">f.</span></span> <span data-ttu-id="56a41-182">In the **Action Bar**, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="56a41-182">In the **Action Bar**, click **Save**.</span></span>
10. <span data-ttu-id="56a41-183">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56a41-183">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
    
     ![What is Azure AD Connect][10]
11. <span data-ttu-id="56a41-185">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="56a41-185">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56a41-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56a41-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="56a41-188">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56a41-188">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  
<span data-ttu-id="56a41-189">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56a41-189">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="56a41-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56a41-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56a41-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56a41-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="56a41-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="56a41-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="56a41-195">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="56a41-195">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="56a41-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="56a41-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="56a41-199">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56a41-199">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="56a41-201">a.</span><span class="sxs-lookup"><span data-stu-id="56a41-201">a.</span></span> <span data-ttu-id="56a41-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="56a41-202">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="56a41-203">b.</span><span class="sxs-lookup"><span data-stu-id="56a41-203">b.</span></span> <span data-ttu-id="56a41-204">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56a41-204">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="56a41-205">c.</span><span class="sxs-lookup"><span data-stu-id="56a41-205">c.</span></span> <span data-ttu-id="56a41-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56a41-206">Click **Next**.</span></span>
6. <span data-ttu-id="56a41-207">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56a41-207">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="56a41-209">a.</span><span class="sxs-lookup"><span data-stu-id="56a41-209">a.</span></span> <span data-ttu-id="56a41-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="56a41-210">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="56a41-211">b.</span><span class="sxs-lookup"><span data-stu-id="56a41-211">b.</span></span> <span data-ttu-id="56a41-212">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="56a41-212">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="56a41-213">c.</span><span class="sxs-lookup"><span data-stu-id="56a41-213">c.</span></span> <span data-ttu-id="56a41-214">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56a41-214">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="56a41-215">d.</span><span class="sxs-lookup"><span data-stu-id="56a41-215">d.</span></span> <span data-ttu-id="56a41-216">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="56a41-216">In the **Role** list, select **User**.</span></span>
    <span data-ttu-id="56a41-217">e.</span><span class="sxs-lookup"><span data-stu-id="56a41-217">e.</span></span> <span data-ttu-id="56a41-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="56a41-218">Click **Next**.</span></span>
7. <span data-ttu-id="56a41-219">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="56a41-219">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_07.png) 

1. <span data-ttu-id="56a41-221">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="56a41-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="56a41-223">a.</span><span class="sxs-lookup"><span data-stu-id="56a41-223">a.</span></span> <span data-ttu-id="56a41-224">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="56a41-224">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="56a41-225">b.</span><span class="sxs-lookup"><span data-stu-id="56a41-225">b.</span></span> <span data-ttu-id="56a41-226">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="56a41-226">Click **Complete**.</span></span>   

### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="56a41-227">Creating a QuickHelp test user</span><span class="sxs-lookup"><span data-stu-id="56a41-227">Creating a QuickHelp test user</span></span>
<span data-ttu-id="56a41-228">The objective of this section is to create a user called Britta Simon in QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="56a41-228">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="56a41-229">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="56a41-229">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to an user in Azure AD is.</span></span> <span data-ttu-id="56a41-230">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span><span class="sxs-lookup"><span data-stu-id="56a41-230">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="56a41-231">QuickHelp supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="56a41-231">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="56a41-232">This means, if required, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="56a41-232">This means, if required, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="56a41-233">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="56a41-233">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56a41-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="56a41-234">Assigning the Azure AD test user</span></span>
<span data-ttu-id="56a41-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="56a41-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to QuickHelp.</span></span>

![Assign User][200] 

<span data-ttu-id="56a41-237">**To assign Britta Simon to QuickHelp, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="56a41-237">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="56a41-238">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="56a41-238">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="56a41-240">In the applications list, select **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="56a41-240">In the applications list, select **QuickHelp**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="56a41-242">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="56a41-242">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="56a41-244">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56a41-244">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="56a41-245">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="56a41-245">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="56a41-247">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="56a41-247">Testing Single Sign-On</span></span>
<span data-ttu-id="56a41-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="56a41-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="56a41-249">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span><span class="sxs-lookup"><span data-stu-id="56a41-249">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56a41-250">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="56a41-250">Additional Resources</span></span>
* [<span data-ttu-id="56a41-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56a41-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56a41-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56a41-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_01.png
[500]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_14.png


[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_02.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_03.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_04.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_08.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_09.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_10.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_11.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_12.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_13.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-quickhelp-tutorial/tutorial_general_205.png


[400]: ./media/active-directory-saas-QuickHelp-tutorial/tutorial_QuickHelp_400.png
[401]: ./media/active-directory-saas-QuickHelp-tutorial/tutorial_QuickHelp_401.png
[402]: ./media/active-directory-saas-QuickHelp-tutorial/tutorial_QuickHelp_402.png





































