---
title: 'Tutorial: Azure Active Directory integration with @Task| Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and @Task.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: fc037fa0b7f30018294499840f0dc597202674a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548740"
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="849a8-103">Tutorial: Azure Active Directory integration with @Task</span><span class="sxs-lookup"><span data-stu-id="849a8-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="849a8-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="849a8-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="849a8-105">Integrating @Task with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="849a8-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="849a8-106">You can control in Azure AD who has access to @Task</span><span class="sxs-lookup"><span data-stu-id="849a8-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="849a8-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="849a8-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="849a8-108">You can manage your accounts in one central location - the Azure classic Portal</span><span class="sxs-lookup"><span data-stu-id="849a8-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="849a8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="849a8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="849a8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="849a8-110">Prerequisites</span></span>
<span data-ttu-id="849a8-111">To configure Azure AD integration with @Task, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="849a8-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="849a8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="849a8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="849a8-113">An @Task single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="849a8-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="849a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="849a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="849a8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="849a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="849a8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="849a8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="849a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="849a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="849a8-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="849a8-118">Scenario Description</span></span>
<span data-ttu-id="849a8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="849a8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="849a8-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="849a8-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="849a8-121">Adding @Task from the gallery</span><span class="sxs-lookup"><span data-stu-id="849a8-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="849a8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="849a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="849a8-123">Adding @Task from the gallery</span><span class="sxs-lookup"><span data-stu-id="849a8-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="849a8-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="849a8-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="849a8-125">**To add @Task from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="849a8-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="849a8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="849a8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="849a8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="849a8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="849a8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="849a8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2] 
4. <span data-ttu-id="849a8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="849a8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3] 
5. <span data-ttu-id="849a8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="849a8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4] 
6. <span data-ttu-id="849a8-135">In the search box, type **@Task**.</span><span class="sxs-lookup"><span data-stu-id="849a8-135">In the search box, type **@Task**.</span></span>
   
    ![Applications][5] 
7. <span data-ttu-id="849a8-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="849a8-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="849a8-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="849a8-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="849a8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="849a8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="849a8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="849a8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="849a8-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span><span class="sxs-lookup"><span data-stu-id="849a8-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="849a8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span><span class="sxs-lookup"><span data-stu-id="849a8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="849a8-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="849a8-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="849a8-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="849a8-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="849a8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="849a8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="849a8-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="849a8-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="849a8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="849a8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="849a8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="849a8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="849a8-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="849a8-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="849a8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span><span class="sxs-lookup"><span data-stu-id="849a8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="849a8-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="849a8-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="849a8-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="849a8-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="849a8-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="849a8-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="849a8-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure App Settings][8] 
   
     <span data-ttu-id="849a8-159">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-159">a.</span></span> <span data-ttu-id="849a8-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="849a8-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="849a8-161">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-161">b.</span></span> <span data-ttu-id="849a8-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-162">Click **Next**.</span></span>
4. <span data-ttu-id="849a8-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![What is Azure AD Connect][9] 
5. <span data-ttu-id="849a8-165">Sign-on to your @Task company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="849a8-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="849a8-166">Go to **Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="849a8-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="849a8-167">On the **Single Sign-On** dialog, perform the following steps</span><span class="sxs-lookup"><span data-stu-id="849a8-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Configure Single Sign-On][23]
   
    <span data-ttu-id="849a8-169">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-169">a.</span></span> <span data-ttu-id="849a8-170">As **Type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="849a8-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="849a8-171">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-171">b.</span></span> <span data-ttu-id="849a8-172">Select **Service Provider ID**.</span><span class="sxs-lookup"><span data-stu-id="849a8-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="849a8-173">c.</span><span class="sxs-lookup"><span data-stu-id="849a8-173">c.</span></span> <span data-ttu-id="849a8-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="849a8-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="849a8-175">d.</span><span class="sxs-lookup"><span data-stu-id="849a8-175">d.</span></span> <span data-ttu-id="849a8-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="849a8-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="849a8-177">e.</span><span class="sxs-lookup"><span data-stu-id="849a8-177">e.</span></span> <span data-ttu-id="849a8-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="849a8-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="849a8-179">f.</span><span class="sxs-lookup"><span data-stu-id="849a8-179">f.</span></span> <span data-ttu-id="849a8-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="849a8-180">Click **Save**.</span></span>
8. <span data-ttu-id="849a8-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![What is Azure AD Connect][10]
9. <span data-ttu-id="849a8-183">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="849a8-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="849a8-185">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="849a8-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="849a8-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="849a8-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="849a8-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="849a8-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="849a8-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="849a8-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="849a8-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="849a8-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="849a8-192">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="849a8-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="849a8-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="849a8-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="849a8-196">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="849a8-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="849a8-198">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-198">a.</span></span> <span data-ttu-id="849a8-199">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="849a8-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="849a8-200">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-200">b.</span></span> <span data-ttu-id="849a8-201">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="849a8-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="849a8-202">c.</span><span class="sxs-lookup"><span data-stu-id="849a8-202">c.</span></span> <span data-ttu-id="849a8-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-203">Click **Next**.</span></span>
6. <span data-ttu-id="849a8-204">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="849a8-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="849a8-206">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-206">a.</span></span> <span data-ttu-id="849a8-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="849a8-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="849a8-208">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-208">b.</span></span> <span data-ttu-id="849a8-209">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="849a8-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="849a8-210">c.</span><span class="sxs-lookup"><span data-stu-id="849a8-210">c.</span></span> <span data-ttu-id="849a8-211">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="849a8-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="849a8-212">d.</span><span class="sxs-lookup"><span data-stu-id="849a8-212">d.</span></span> <span data-ttu-id="849a8-213">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="849a8-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="849a8-214">e.</span><span class="sxs-lookup"><span data-stu-id="849a8-214">e.</span></span> <span data-ttu-id="849a8-215">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="849a8-215">Click **Next**.</span></span>

7. <span data-ttu-id="849a8-216">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="849a8-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="849a8-218">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="849a8-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="849a8-220">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-220">a.</span></span> <span data-ttu-id="849a8-221">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="849a8-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="849a8-222">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-222">b.</span></span> <span data-ttu-id="849a8-223">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="849a8-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="849a8-224">Creating an @Task test user</span><span class="sxs-lookup"><span data-stu-id="849a8-224">Creating an @Task test user</span></span>
<span data-ttu-id="849a8-225">The objective of this section is to create a user called Britta Simon in @Task.</span><span class="sxs-lookup"><span data-stu-id="849a8-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="849a8-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="849a8-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="849a8-227">Sign on to your @Task company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="849a8-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="849a8-228">In the menu on the top, click **People**.</span><span class="sxs-lookup"><span data-stu-id="849a8-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="849a8-229">Click **New Person**.</span><span class="sxs-lookup"><span data-stu-id="849a8-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="849a8-230">On the New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="849a8-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Create an @Task test user][21] 
   
    <span data-ttu-id="849a8-232">a.</span><span class="sxs-lookup"><span data-stu-id="849a8-232">a.</span></span> <span data-ttu-id="849a8-233">In the **First Name** textbox, type "Britta".</span><span class="sxs-lookup"><span data-stu-id="849a8-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="849a8-234">b.</span><span class="sxs-lookup"><span data-stu-id="849a8-234">b.</span></span> <span data-ttu-id="849a8-235">In the **Last Name** textbox, type "Simon".</span><span class="sxs-lookup"><span data-stu-id="849a8-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="849a8-236">c.</span><span class="sxs-lookup"><span data-stu-id="849a8-236">c.</span></span> <span data-ttu-id="849a8-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="849a8-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="849a8-238">d.</span><span class="sxs-lookup"><span data-stu-id="849a8-238">d.</span></span> <span data-ttu-id="849a8-239">Click **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="849a8-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="849a8-240">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="849a8-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="849a8-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span><span class="sxs-lookup"><span data-stu-id="849a8-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Assign User][200] 

<span data-ttu-id="849a8-243">**To assign Britta Simon to @Task, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="849a8-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="849a8-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="849a8-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="849a8-246">In the applications list, select **@Task**.</span><span class="sxs-lookup"><span data-stu-id="849a8-246">In the applications list, select **@Task**.</span></span>
   
    ![Assign User][202] 
3. <span data-ttu-id="849a8-248">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="849a8-248">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="849a8-250">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="849a8-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="849a8-251">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="849a8-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="849a8-253">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="849a8-253">Testing Single Sign-On</span></span>
<span data-ttu-id="849a8-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="849a8-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="849a8-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span><span class="sxs-lookup"><span data-stu-id="849a8-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="849a8-256">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="849a8-256">Additional Resources</span></span>
* [<span data-ttu-id="849a8-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="849a8-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="849a8-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="849a8-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-attask-tutorial/tutorial_general_205.png

































