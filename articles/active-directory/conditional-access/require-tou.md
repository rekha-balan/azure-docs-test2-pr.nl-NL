---
title: Quickstart - Require terms of use to be accepted before accessing cloud apps that are protected by Azure Active Directory conditional access | Microsoft Docs
description: In this quickstart, you learn how you can require that your terms of use are accepted before access to selected cloud apps is granted by by Azure Active Directory conditional access.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies, terms of use
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: conditional-access
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/13/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: a7aeecc84a3629b43f2c1eb40030866a941d0d3b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868451"
---
# <a name="quickstart-require-terms-of-use-to-be-accepted-before-accessing-cloud-apps"></a><span data-ttu-id="812f6-104">Quickstart: Require terms of use to be accepted before accessing cloud apps</span><span class="sxs-lookup"><span data-stu-id="812f6-104">Quickstart: Require terms of use to be accepted before accessing cloud apps</span></span> 

<span data-ttu-id="812f6-105">Before accessing certain cloud apps in your environment, you might want to get consent from users in form of accepting your terms of use (ToU).</span><span class="sxs-lookup"><span data-stu-id="812f6-105">Before accessing certain cloud apps in your environment, you might want to get consent from users in form of accepting your terms of use (ToU).</span></span> <span data-ttu-id="812f6-106">Azure Active Directory (Azure AD) conditional access provides you with:</span><span class="sxs-lookup"><span data-stu-id="812f6-106">Azure Active Directory (Azure AD) conditional access provides you with:</span></span> 

- <span data-ttu-id="812f6-107">A simple method to configure ToU</span><span class="sxs-lookup"><span data-stu-id="812f6-107">A simple method to configure ToU</span></span>
- <span data-ttu-id="812f6-108">The option to require accepting your terms of use through a conditional access policy</span><span class="sxs-lookup"><span data-stu-id="812f6-108">The option to require accepting your terms of use through a conditional access policy</span></span>  

<span data-ttu-id="812f6-109">This quickstart shows how to configure an [Azure AD conditional access policy](../active-directory-conditional-access-azure-portal.md) that requires a ToU to be accepted for a selected cloud app in your environment.</span><span class="sxs-lookup"><span data-stu-id="812f6-109">This quickstart shows how to configure an [Azure AD conditional access policy](../active-directory-conditional-access-azure-portal.md) that requires a ToU to be accepted for a selected cloud app in your environment.</span></span>

![Create policy](./media/require-tou/5555.png)


<span data-ttu-id="812f6-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="812f6-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="812f6-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="812f6-112">Prerequisites</span></span> 

<span data-ttu-id="812f6-113">To complete the scenario in this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="812f6-113">To complete the scenario in this quickstart, you need:</span></span>

- <span data-ttu-id="812f6-114">**Access to an Azure AD Premium edition** - Azure AD conditional access is an Azure AD Premium capability.</span><span class="sxs-lookup"><span data-stu-id="812f6-114">**Access to an Azure AD Premium edition** - Azure AD conditional access is an Azure AD Premium capability.</span></span> 

- <span data-ttu-id="812f6-115">**A test account called Isabella Simonsen** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span><span class="sxs-lookup"><span data-stu-id="812f6-115">**A test account called Isabella Simonsen** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span></span>


## <a name="test-your-sign-in"></a><span data-ttu-id="812f6-116">Test your sign-in</span><span class="sxs-lookup"><span data-stu-id="812f6-116">Test your sign-in</span></span>

<span data-ttu-id="812f6-117">The goal of this step is to get an impression of the sign-in experience without a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="812f6-117">The goal of this step is to get an impression of the sign-in experience without a conditional access policy.</span></span>

<span data-ttu-id="812f6-118">**To test your sign-in:**</span><span class="sxs-lookup"><span data-stu-id="812f6-118">**To test your sign-in:**</span></span>

1. <span data-ttu-id="812f6-119">Sign in to your [Azure portal](https://portal.azure.com/) as Isabella Simonsen.</span><span class="sxs-lookup"><span data-stu-id="812f6-119">Sign in to your [Azure portal](https://portal.azure.com/) as Isabella Simonsen.</span></span>

2. <span data-ttu-id="812f6-120">Sign out.</span><span class="sxs-lookup"><span data-stu-id="812f6-120">Sign out.</span></span>




## <a name="create-your-terms-of-use"></a><span data-ttu-id="812f6-121">Create your terms of use</span><span class="sxs-lookup"><span data-stu-id="812f6-121">Create your terms of use</span></span>

<span data-ttu-id="812f6-122">This section provides you with the steps to create a sample ToU.</span><span class="sxs-lookup"><span data-stu-id="812f6-122">This section provides you with the steps to create a sample ToU.</span></span> <span data-ttu-id="812f6-123">When you create a ToU, you select a value for **Enforce with conditional access policy templates**.</span><span class="sxs-lookup"><span data-stu-id="812f6-123">When you create a ToU, you select a value for **Enforce with conditional access policy templates**.</span></span> <span data-ttu-id="812f6-124">Selecting **Custom policy** opens the dialog to create a new conditional access policy as soon as your ToU has been created.</span><span class="sxs-lookup"><span data-stu-id="812f6-124">Selecting **Custom policy** opens the dialog to create a new conditional access policy as soon as your ToU has been created.</span></span>


<span data-ttu-id="812f6-125">**To create your terms of use:**</span><span class="sxs-lookup"><span data-stu-id="812f6-125">**To create your terms of use:**</span></span>

1. <span data-ttu-id="812f6-126">In Microsoft Word, create a new document.</span><span class="sxs-lookup"><span data-stu-id="812f6-126">In Microsoft Word, create a new document.</span></span>

2. <span data-ttu-id="812f6-127">Type **My terms of use**, and then save the document on your computer as **mytou.pdf**.</span><span class="sxs-lookup"><span data-stu-id="812f6-127">Type **My terms of use**, and then save the document on your computer as **mytou.pdf**.</span></span>

3. <span data-ttu-id="812f6-128">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span><span class="sxs-lookup"><span data-stu-id="812f6-128">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span></span>

4. <span data-ttu-id="812f6-129">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="812f6-129">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Azure Active Directory](./media/require-tou/02.png)

5. <span data-ttu-id="812f6-131">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="812f6-131">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/require-tou/03.png) 

6. <span data-ttu-id="812f6-133">In the **Manage** section, click **Terms of use**.</span><span class="sxs-lookup"><span data-stu-id="812f6-133">In the **Manage** section, click **Terms of use**.</span></span>

    ![Terms of use](./media/require-tou/04.png) 

7. <span data-ttu-id="812f6-135">In the menu on the top, click **New terms**.</span><span class="sxs-lookup"><span data-stu-id="812f6-135">In the menu on the top, click **New terms**.</span></span>

    ![Terms of use](./media/require-tou/05.png) 

8. <span data-ttu-id="812f6-137">On the **New terms of use** page:</span><span class="sxs-lookup"><span data-stu-id="812f6-137">On the **New terms of use** page:</span></span>

    ![Terms of use](./media/require-tou/112.png) 

    <span data-ttu-id="812f6-139">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-139">a.</span></span> <span data-ttu-id="812f6-140">In the **Name** textbox, type **My TOU**.</span><span class="sxs-lookup"><span data-stu-id="812f6-140">In the **Name** textbox, type **My TOU**.</span></span>

    <span data-ttu-id="812f6-141">b.</span><span class="sxs-lookup"><span data-stu-id="812f6-141">b.</span></span> <span data-ttu-id="812f6-142">In the **Display name** textbox, type **My TOU**.</span><span class="sxs-lookup"><span data-stu-id="812f6-142">In the **Display name** textbox, type **My TOU**.</span></span>

    <span data-ttu-id="812f6-143">c.</span><span class="sxs-lookup"><span data-stu-id="812f6-143">c.</span></span> <span data-ttu-id="812f6-144">Upload your terms of use PDF file.</span><span class="sxs-lookup"><span data-stu-id="812f6-144">Upload your terms of use PDF file.</span></span>

    <span data-ttu-id="812f6-145">d.</span><span class="sxs-lookup"><span data-stu-id="812f6-145">d.</span></span> <span data-ttu-id="812f6-146">As **Language**, select **English**.</span><span class="sxs-lookup"><span data-stu-id="812f6-146">As **Language**, select **English**.</span></span>

    <span data-ttu-id="812f6-147">e.</span><span class="sxs-lookup"><span data-stu-id="812f6-147">e.</span></span> <span data-ttu-id="812f6-148">As **Require users to expand the terms of use**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="812f6-148">As **Require users to expand the terms of use**, select **On**.</span></span>

    <span data-ttu-id="812f6-149">f.</span><span class="sxs-lookup"><span data-stu-id="812f6-149">f.</span></span> <span data-ttu-id="812f6-150">As **Enforce with conditional access policy templates**, select **Custom policy**.</span><span class="sxs-lookup"><span data-stu-id="812f6-150">As **Enforce with conditional access policy templates**, select **Custom policy**.</span></span>

    <span data-ttu-id="812f6-151">g.</span><span class="sxs-lookup"><span data-stu-id="812f6-151">g.</span></span> <span data-ttu-id="812f6-152">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="812f6-152">Click **Create**.</span></span>
 


## <a name="create-your-conditional-access-policy"></a><span data-ttu-id="812f6-153">Create your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="812f6-153">Create your conditional access policy</span></span> 

<span data-ttu-id="812f6-154">This section shows how to create the required conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="812f6-154">This section shows how to create the required conditional access policy.</span></span> <span data-ttu-id="812f6-155">The scenario in this quickstart uses:</span><span class="sxs-lookup"><span data-stu-id="812f6-155">The scenario in this quickstart uses:</span></span>

- <span data-ttu-id="812f6-156">The Azure portal as placeholder for a cloud app that requires your ToU to be accepted.</span><span class="sxs-lookup"><span data-stu-id="812f6-156">The Azure portal as placeholder for a cloud app that requires your ToU to be accepted.</span></span> 
- <span data-ttu-id="812f6-157">Your sample user to test the conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="812f6-157">Your sample user to test the conditional access policy.</span></span>  

<span data-ttu-id="812f6-158">In your policy, set:</span><span class="sxs-lookup"><span data-stu-id="812f6-158">In your policy, set:</span></span>

|<span data-ttu-id="812f6-159">Setting</span><span class="sxs-lookup"><span data-stu-id="812f6-159">Setting</span></span> |<span data-ttu-id="812f6-160">Value</span><span class="sxs-lookup"><span data-stu-id="812f6-160">Value</span></span>|
|---     | --- |
|<span data-ttu-id="812f6-161">Users and groups</span><span class="sxs-lookup"><span data-stu-id="812f6-161">Users and groups</span></span> | <span data-ttu-id="812f6-162">Isabella Simonsen</span><span class="sxs-lookup"><span data-stu-id="812f6-162">Isabella Simonsen</span></span> |
|<span data-ttu-id="812f6-163">Cloud apps</span><span class="sxs-lookup"><span data-stu-id="812f6-163">Cloud apps</span></span> | <span data-ttu-id="812f6-164">Microsoft Azure Management</span><span class="sxs-lookup"><span data-stu-id="812f6-164">Microsoft Azure Management</span></span> |
|<span data-ttu-id="812f6-165">Grant access</span><span class="sxs-lookup"><span data-stu-id="812f6-165">Grant access</span></span> | <span data-ttu-id="812f6-166">My TOU</span><span class="sxs-lookup"><span data-stu-id="812f6-166">My TOU</span></span> |
 

![Create policy](./media/require-tou/1234.png)

 


<span data-ttu-id="812f6-168">**To configure your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="812f6-168">**To configure your conditional access policy:**</span></span>

1. <span data-ttu-id="812f6-169">On the **New** page, in the **Name** textbox, type **Require TOU for Isabella**.</span><span class="sxs-lookup"><span data-stu-id="812f6-169">On the **New** page, in the **Name** textbox, type **Require TOU for Isabella**.</span></span>

    ![Name](./media/require-tou/71.png)

2. <span data-ttu-id="812f6-171">In the **Assignment** section, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="812f6-171">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Users and groups](./media/require-tou/06.png)

3. <span data-ttu-id="812f6-173">On the **Users and groups** page:</span><span class="sxs-lookup"><span data-stu-id="812f6-173">On the **Users and groups** page:</span></span>

    ![Users and groups](./media/require-tou/24.png)

    <span data-ttu-id="812f6-175">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-175">a.</span></span> <span data-ttu-id="812f6-176">Click **Select users and groups**, and then select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="812f6-176">Click **Select users and groups**, and then select **Users and groups**.</span></span>

    <span data-ttu-id="812f6-177">b.</span><span class="sxs-lookup"><span data-stu-id="812f6-177">b.</span></span> <span data-ttu-id="812f6-178">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-178">Click **Select**.</span></span>

    <span data-ttu-id="812f6-179">c.</span><span class="sxs-lookup"><span data-stu-id="812f6-179">c.</span></span> <span data-ttu-id="812f6-180">On the **Select** page, select **Isabella Simonsen**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-180">On the **Select** page, select **Isabella Simonsen**, and then click **Select**.</span></span>

    <span data-ttu-id="812f6-181">d.</span><span class="sxs-lookup"><span data-stu-id="812f6-181">d.</span></span> <span data-ttu-id="812f6-182">On the **Users and groups** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="812f6-182">On the **Users and groups** page, click **Done**.</span></span>

4. <span data-ttu-id="812f6-183">Click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="812f6-183">Click **Cloud apps**.</span></span>

    ![Cloud apps](./media/require-tou/08.png)

5. <span data-ttu-id="812f6-185">On the **Cloud apps** page:</span><span class="sxs-lookup"><span data-stu-id="812f6-185">On the **Cloud apps** page:</span></span>

    ![Select cloud apps](./media/require-tou/26.png)

    <span data-ttu-id="812f6-187">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-187">a.</span></span> <span data-ttu-id="812f6-188">Click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="812f6-188">Click **Select apps**.</span></span>

    <span data-ttu-id="812f6-189">b.</span><span class="sxs-lookup"><span data-stu-id="812f6-189">b.</span></span> <span data-ttu-id="812f6-190">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-190">Click **Select**.</span></span>

    <span data-ttu-id="812f6-191">c.</span><span class="sxs-lookup"><span data-stu-id="812f6-191">c.</span></span> <span data-ttu-id="812f6-192">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-192">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span></span>

    <span data-ttu-id="812f6-193">d.</span><span class="sxs-lookup"><span data-stu-id="812f6-193">d.</span></span> <span data-ttu-id="812f6-194">On the **Cloud apps** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="812f6-194">On the **Cloud apps** page, click **Done**.</span></span>


6. <span data-ttu-id="812f6-195">In the **Access controls** section, click **Grant**.</span><span class="sxs-lookup"><span data-stu-id="812f6-195">In the **Access controls** section, click **Grant**.</span></span>

    ![Access controls](./media/require-tou/10.png)

7. <span data-ttu-id="812f6-197">On the **Grant** page:</span><span class="sxs-lookup"><span data-stu-id="812f6-197">On the **Grant** page:</span></span>

    ![Grant](./media/require-tou/111.png)

    <span data-ttu-id="812f6-199">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-199">a.</span></span> <span data-ttu-id="812f6-200">Select **Grant access**.</span><span class="sxs-lookup"><span data-stu-id="812f6-200">Select **Grant access**.</span></span>

    <span data-ttu-id="812f6-201">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-201">a.</span></span> <span data-ttu-id="812f6-202">Select **My TOU**.</span><span class="sxs-lookup"><span data-stu-id="812f6-202">Select **My TOU**.</span></span>

    <span data-ttu-id="812f6-203">b.</span><span class="sxs-lookup"><span data-stu-id="812f6-203">b.</span></span> <span data-ttu-id="812f6-204">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-204">Click **Select**.</span></span>

8. <span data-ttu-id="812f6-205">In the **Enable policy** section, click **On**.</span><span class="sxs-lookup"><span data-stu-id="812f6-205">In the **Enable policy** section, click **On**.</span></span>

    ![Enable policy](./media/require-tou/18.png)

9. <span data-ttu-id="812f6-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="812f6-207">Click **Create**.</span></span>


## <a name="evaluate-a-simulated-sign-in"></a><span data-ttu-id="812f6-208">Evaluate a simulated sign-in</span><span class="sxs-lookup"><span data-stu-id="812f6-208">Evaluate a simulated sign-in</span></span>

<span data-ttu-id="812f6-209">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span><span class="sxs-lookup"><span data-stu-id="812f6-209">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span></span> <span data-ttu-id="812f6-210">As a first step, use the conditional access what if policy tool to simulate a sign-in of your test user.</span><span class="sxs-lookup"><span data-stu-id="812f6-210">As a first step, use the conditional access what if policy tool to simulate a sign-in of your test user.</span></span> <span data-ttu-id="812f6-211">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span><span class="sxs-lookup"><span data-stu-id="812f6-211">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span></span>  

<span data-ttu-id="812f6-212">To initialize the what if policy evaluation tool, set:</span><span class="sxs-lookup"><span data-stu-id="812f6-212">To initialize the what if policy evaluation tool, set:</span></span>

- <span data-ttu-id="812f6-213">**Isabella Simonsen** as user</span><span class="sxs-lookup"><span data-stu-id="812f6-213">**Isabella Simonsen** as user</span></span> 
- <span data-ttu-id="812f6-214">**Microsoft Azure Management** as cloud app</span><span class="sxs-lookup"><span data-stu-id="812f6-214">**Microsoft Azure Management** as cloud app</span></span>


<span data-ttu-id="812f6-215">Clicking **What If** creates a simulation report that shows:</span><span class="sxs-lookup"><span data-stu-id="812f6-215">Clicking **What If** creates a simulation report that shows:</span></span>

- <span data-ttu-id="812f6-216">**Require TOU for Isabella** under **Policies that will apply**</span><span class="sxs-lookup"><span data-stu-id="812f6-216">**Require TOU for Isabella** under **Policies that will apply**</span></span> 
- <span data-ttu-id="812f6-217">**My TOU** as **Grant Controls**.</span><span class="sxs-lookup"><span data-stu-id="812f6-217">**My TOU** as **Grant Controls**.</span></span>

![What if policy tool](./media/require-tou/79.png)



<span data-ttu-id="812f6-219">**To evaluate your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="812f6-219">**To evaluate your conditional access policy:**</span></span>

1. <span data-ttu-id="812f6-220">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span><span class="sxs-lookup"><span data-stu-id="812f6-220">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span></span>  
 
    ![What If](./media/require-tou/14.png)

2. <span data-ttu-id="812f6-222">Click **Users**, select **Isabella Simonsen**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-222">Click **Users**, select **Isabella Simonsen**, and then click **Select**.</span></span>

    ![User](./media/require-tou/15.png)

2. <span data-ttu-id="812f6-224">To select a cloud app:</span><span class="sxs-lookup"><span data-stu-id="812f6-224">To select a cloud app:</span></span>

    ![Cloud apps](./media/require-tou/16.png)

    <span data-ttu-id="812f6-226">a.</span><span class="sxs-lookup"><span data-stu-id="812f6-226">a.</span></span> <span data-ttu-id="812f6-227">Click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="812f6-227">Click **Cloud apps**.</span></span>

    <span data-ttu-id="812f6-228">b.</span><span class="sxs-lookup"><span data-stu-id="812f6-228">b.</span></span> <span data-ttu-id="812f6-229">On the **Cloud apps page**, click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="812f6-229">On the **Cloud apps page**, click **Select apps**.</span></span>

    <span data-ttu-id="812f6-230">c.</span><span class="sxs-lookup"><span data-stu-id="812f6-230">c.</span></span> <span data-ttu-id="812f6-231">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-231">Click **Select**.</span></span>

    <span data-ttu-id="812f6-232">d.</span><span class="sxs-lookup"><span data-stu-id="812f6-232">d.</span></span> <span data-ttu-id="812f6-233">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="812f6-233">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span></span>

    <span data-ttu-id="812f6-234">e.</span><span class="sxs-lookup"><span data-stu-id="812f6-234">e.</span></span> <span data-ttu-id="812f6-235">On the cloud apps page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="812f6-235">On the cloud apps page, click **Done**.</span></span>

3. <span data-ttu-id="812f6-236">Click **What If**.</span><span class="sxs-lookup"><span data-stu-id="812f6-236">Click **What If**.</span></span>


## <a name="test-your-conditional-access-policy"></a><span data-ttu-id="812f6-237">Test your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="812f6-237">Test your conditional access policy</span></span>

<span data-ttu-id="812f6-238">In the previous section, you have learned how to evaluate a simulated sign-in.</span><span class="sxs-lookup"><span data-stu-id="812f6-238">In the previous section, you have learned how to evaluate a simulated sign-in.</span></span> <span data-ttu-id="812f6-239">In addition to a simulation, you should also test your conditional access policy to ensure that it works as expected.</span><span class="sxs-lookup"><span data-stu-id="812f6-239">In addition to a simulation, you should also test your conditional access policy to ensure that it works as expected.</span></span> 

<span data-ttu-id="812f6-240">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) using your **Isabella Simonsen** test account.</span><span class="sxs-lookup"><span data-stu-id="812f6-240">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) using your **Isabella Simonsen** test account.</span></span> <span data-ttu-id="812f6-241">You should see a dialog that requires you to accept your terms of use.</span><span class="sxs-lookup"><span data-stu-id="812f6-241">You should see a dialog that requires you to accept your terms of use.</span></span>

![Terms of use](./media/require-tou/57.png)


## <a name="clean-up-resources"></a><span data-ttu-id="812f6-243">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="812f6-243">Clean up resources</span></span>

<span data-ttu-id="812f6-244">When no longer needed, delete the test user and the conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="812f6-244">When no longer needed, delete the test user and the conditional access policy:</span></span>

- <span data-ttu-id="812f6-245">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="812f6-245">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span></span>

- <span data-ttu-id="812f6-246">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span><span class="sxs-lookup"><span data-stu-id="812f6-246">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span></span>

    ![Multi-factor authentication](./media/require-tou/33.png)

- <span data-ttu-id="812f6-248">To delete your terms of use, select it, and then click **Delete terms** in the toolbar on top.</span><span class="sxs-lookup"><span data-stu-id="812f6-248">To delete your terms of use, select it, and then click **Delete terms** in the toolbar on top.</span></span> 

    ![Multi-factor authentication](./media/require-tou/29.png)

## <a name="next-steps"></a><span data-ttu-id="812f6-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="812f6-250">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="812f6-251">[Require MFA for specific apps](app-based-mfa.md)
> [Block access when a session risk is detected](app-sign-in-risk.md)</span><span class="sxs-lookup"><span data-stu-id="812f6-251">[Require MFA for specific apps](app-based-mfa.md)
[Block access when a session risk is detected](app-sign-in-risk.md)</span></span>

