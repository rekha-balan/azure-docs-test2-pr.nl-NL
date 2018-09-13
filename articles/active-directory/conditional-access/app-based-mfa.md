---
title: Quickstart - Require multi-factor authentication (MFA) for specific apps with Azure Active Directory conditional access | Microsoft Docs
description: In this quickstart, you learn how you can tie your authentication requirements to the type of accessed cloud app using Azure Active Directory (Azure AD) conditional access.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
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
ms.openlocfilehash: eee4d73042232aabd995a749b7848306be0ef655
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868725"
---
# <a name="quickstart-require-mfa-for-specific-apps-with-azure-active-directory-conditional-access"></a><span data-ttu-id="b0760-104">Quickstart: Require MFA for specific apps with Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="b0760-104">Quickstart: Require MFA for specific apps with Azure Active Directory conditional access</span></span> 

<span data-ttu-id="b0760-105">To simplify the sign-in experience of your users, you might want to allow them to sign in to your cloud apps using a user name and a password.</span><span class="sxs-lookup"><span data-stu-id="b0760-105">To simplify the sign-in experience of your users, you might want to allow them to sign in to your cloud apps using a user name and a password.</span></span> <span data-ttu-id="b0760-106">However, many environments have at least a few apps for which it is advisable to require a stronger form of account verification, such as multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="b0760-106">However, many environments have at least a few apps for which it is advisable to require a stronger form of account verification, such as multi-factor authentication (MFA).</span></span> <span data-ttu-id="b0760-107">This might be, for example true, for access to your organization's email system or your HR apps.</span><span class="sxs-lookup"><span data-stu-id="b0760-107">This might be, for example true, for access to your organization's email system or your HR apps.</span></span> <span data-ttu-id="b0760-108">In Azure Active Directory (Azure AD), you can accomplish this goal with a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="b0760-108">In Azure Active Directory (Azure AD), you can accomplish this goal with a conditional access policy.</span></span>    

<span data-ttu-id="b0760-109">This quickstart shows how to configure an [Azure AD conditional access policy](../active-directory-conditional-access-azure-portal.md) that requires multi-factor authentication for a selected cloud app in your environment.</span><span class="sxs-lookup"><span data-stu-id="b0760-109">This quickstart shows how to configure an [Azure AD conditional access policy](../active-directory-conditional-access-azure-portal.md) that requires multi-factor authentication for a selected cloud app in your environment.</span></span>

![Create policy](./media/app-based-mfa/32.png)


<span data-ttu-id="b0760-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b0760-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="b0760-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0760-112">Prerequisites</span></span> 

<span data-ttu-id="b0760-113">To complete the scenario in this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="b0760-113">To complete the scenario in this quickstart, you need:</span></span>

- <span data-ttu-id="b0760-114">**Access to an Azure AD Premium edition** - Azure AD conditional access is an Azure AD Premium capability.</span><span class="sxs-lookup"><span data-stu-id="b0760-114">**Access to an Azure AD Premium edition** - Azure AD conditional access is an Azure AD Premium capability.</span></span> 

- <span data-ttu-id="b0760-115">**A test account called Isabella Simonsen** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span><span class="sxs-lookup"><span data-stu-id="b0760-115">**A test account called Isabella Simonsen** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span></span>


## <a name="test-your-sign-in"></a><span data-ttu-id="b0760-116">Test your sign-in</span><span class="sxs-lookup"><span data-stu-id="b0760-116">Test your sign-in</span></span>

<span data-ttu-id="b0760-117">The goal of this step is to get an impression of the sign-in experience without a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="b0760-117">The goal of this step is to get an impression of the sign-in experience without a conditional access policy.</span></span>

<span data-ttu-id="b0760-118">**To initialize your environment:**</span><span class="sxs-lookup"><span data-stu-id="b0760-118">**To initialize your environment:**</span></span>

1. <span data-ttu-id="b0760-119">Sign in to your Azure portal as Isabella Simonsen.</span><span class="sxs-lookup"><span data-stu-id="b0760-119">Sign in to your Azure portal as Isabella Simonsen.</span></span>

2. <span data-ttu-id="b0760-120">Sign out.</span><span class="sxs-lookup"><span data-stu-id="b0760-120">Sign out.</span></span>


## <a name="create-your-conditional-access-policy"></a><span data-ttu-id="b0760-121">Create your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="b0760-121">Create your conditional access policy</span></span> 

<span data-ttu-id="b0760-122">This section shows how to create the required conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="b0760-122">This section shows how to create the required conditional access policy.</span></span> <span data-ttu-id="b0760-123">The scenario in this quickstart uses:</span><span class="sxs-lookup"><span data-stu-id="b0760-123">The scenario in this quickstart uses:</span></span>

- <span data-ttu-id="b0760-124">The Azure portal as placeholder for a cloud app that requires MFA.</span><span class="sxs-lookup"><span data-stu-id="b0760-124">The Azure portal as placeholder for a cloud app that requires MFA.</span></span> 
- <span data-ttu-id="b0760-125">Your sample user to test the conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="b0760-125">Your sample user to test the conditional access policy.</span></span>  

<span data-ttu-id="b0760-126">In your policy, set:</span><span class="sxs-lookup"><span data-stu-id="b0760-126">In your policy, set:</span></span>

|<span data-ttu-id="b0760-127">Setting</span><span class="sxs-lookup"><span data-stu-id="b0760-127">Setting</span></span> |<span data-ttu-id="b0760-128">Value</span><span class="sxs-lookup"><span data-stu-id="b0760-128">Value</span></span>|
|---     | --- |
|<span data-ttu-id="b0760-129">Users and groups</span><span class="sxs-lookup"><span data-stu-id="b0760-129">Users and groups</span></span> | <span data-ttu-id="b0760-130">Isabella Simonsen</span><span class="sxs-lookup"><span data-stu-id="b0760-130">Isabella Simonsen</span></span> |
|<span data-ttu-id="b0760-131">Cloud apps</span><span class="sxs-lookup"><span data-stu-id="b0760-131">Cloud apps</span></span> | <span data-ttu-id="b0760-132">Microsoft Azure Management</span><span class="sxs-lookup"><span data-stu-id="b0760-132">Microsoft Azure Management</span></span> |
|<span data-ttu-id="b0760-133">Grant access</span><span class="sxs-lookup"><span data-stu-id="b0760-133">Grant access</span></span> | <span data-ttu-id="b0760-134">Require multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="b0760-134">Require multi-factor authentication</span></span> |
 

![Create policy](./media/app-based-mfa/31.png)

 


<span data-ttu-id="b0760-136">**To configure your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="b0760-136">**To configure your conditional access policy:**</span></span>

1. <span data-ttu-id="b0760-137">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span><span class="sxs-lookup"><span data-stu-id="b0760-137">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span></span>

2. <span data-ttu-id="b0760-138">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0760-138">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Azure Active Directory](./media/app-based-mfa/02.png)

3. <span data-ttu-id="b0760-140">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="b0760-140">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/app-based-mfa/03.png)
 
4. <span data-ttu-id="b0760-142">On the **Conditional Access** page, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b0760-142">On the **Conditional Access** page, in the toolbar on the top, click **Add**.</span></span>

    ![Add](./media/app-based-mfa/04.png)

5. <span data-ttu-id="b0760-144">On the **New** page, in the **Name** textbox, type **Require MFA for Azure portal access**.</span><span class="sxs-lookup"><span data-stu-id="b0760-144">On the **New** page, in the **Name** textbox, type **Require MFA for Azure portal access**.</span></span>

    ![Name](./media/app-based-mfa/05.png)

6. <span data-ttu-id="b0760-146">In the **Assignment** section, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b0760-146">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Users and groups](./media/app-based-mfa/06.png)

7. <span data-ttu-id="b0760-148">On the **Users and groups** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0760-148">On the **Users and groups** page, perform the following steps:</span></span>

    ![Users and groups](./media/app-based-mfa/24.png)

    <span data-ttu-id="b0760-150">a.</span><span class="sxs-lookup"><span data-stu-id="b0760-150">a.</span></span> <span data-ttu-id="b0760-151">Click **Select users and groups**, and then select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b0760-151">Click **Select users and groups**, and then select **Users and groups**.</span></span>

    <span data-ttu-id="b0760-152">b.</span><span class="sxs-lookup"><span data-stu-id="b0760-152">b.</span></span> <span data-ttu-id="b0760-153">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-153">Click **Select**.</span></span>

    <span data-ttu-id="b0760-154">c.</span><span class="sxs-lookup"><span data-stu-id="b0760-154">c.</span></span> <span data-ttu-id="b0760-155">On the **Select** page, select **Isabella Simonsen**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-155">On the **Select** page, select **Isabella Simonsen**, and then click **Select**.</span></span>

    <span data-ttu-id="b0760-156">d.</span><span class="sxs-lookup"><span data-stu-id="b0760-156">d.</span></span> <span data-ttu-id="b0760-157">On the **Users and groups** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b0760-157">On the **Users and groups** page, click **Done**.</span></span>

8. <span data-ttu-id="b0760-158">Click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="b0760-158">Click **Cloud apps**.</span></span>

    ![Cloud apps](./media/app-based-mfa/08.png)

9. <span data-ttu-id="b0760-160">On the **Cloud apps** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0760-160">On the **Cloud apps** page, perform the following steps:</span></span>

    ![Select cloud apps](./media/app-based-mfa/26.png)

    <span data-ttu-id="b0760-162">a.</span><span class="sxs-lookup"><span data-stu-id="b0760-162">a.</span></span> <span data-ttu-id="b0760-163">Click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="b0760-163">Click **Select apps**.</span></span>

    <span data-ttu-id="b0760-164">b.</span><span class="sxs-lookup"><span data-stu-id="b0760-164">b.</span></span> <span data-ttu-id="b0760-165">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-165">Click **Select**.</span></span>

    <span data-ttu-id="b0760-166">c.</span><span class="sxs-lookup"><span data-stu-id="b0760-166">c.</span></span> <span data-ttu-id="b0760-167">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-167">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span></span>

    <span data-ttu-id="b0760-168">d.</span><span class="sxs-lookup"><span data-stu-id="b0760-168">d.</span></span> <span data-ttu-id="b0760-169">On the **Cloud apps** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b0760-169">On the **Cloud apps** page, click **Done**.</span></span>


10. <span data-ttu-id="b0760-170">In the **Access controls** section, click **Grant**.</span><span class="sxs-lookup"><span data-stu-id="b0760-170">In the **Access controls** section, click **Grant**.</span></span>

    ![Access controls](./media/app-based-mfa/10.png)

11. <span data-ttu-id="b0760-172">On the **Grant** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0760-172">On the **Grant** page, perform the following steps:</span></span>

    ![Grant](./media/app-based-mfa/11.png)

    <span data-ttu-id="b0760-174">a.</span><span class="sxs-lookup"><span data-stu-id="b0760-174">a.</span></span> <span data-ttu-id="b0760-175">Select **Grant access**.</span><span class="sxs-lookup"><span data-stu-id="b0760-175">Select **Grant access**.</span></span>

    <span data-ttu-id="b0760-176">a.</span><span class="sxs-lookup"><span data-stu-id="b0760-176">a.</span></span> <span data-ttu-id="b0760-177">Select **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="b0760-177">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="b0760-178">b.</span><span class="sxs-lookup"><span data-stu-id="b0760-178">b.</span></span> <span data-ttu-id="b0760-179">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-179">Click **Select**.</span></span>

12. <span data-ttu-id="b0760-180">In the **Enable policy** section, click **On**.</span><span class="sxs-lookup"><span data-stu-id="b0760-180">In the **Enable policy** section, click **On**.</span></span>

    ![Enable policy](./media/app-based-mfa/18.png)

13. <span data-ttu-id="b0760-182">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0760-182">Click **Create**.</span></span>


## <a name="evaluate-a-simulated-sign-in"></a><span data-ttu-id="b0760-183">Evaluate a simulated sign-in</span><span class="sxs-lookup"><span data-stu-id="b0760-183">Evaluate a simulated sign-in</span></span>

<span data-ttu-id="b0760-184">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span><span class="sxs-lookup"><span data-stu-id="b0760-184">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span></span> <span data-ttu-id="b0760-185">As a first step, use the conditional access what if policy tool to simulate a sign-in of your test user.</span><span class="sxs-lookup"><span data-stu-id="b0760-185">As a first step, use the conditional access what if policy tool to simulate a sign-in of your test user.</span></span> <span data-ttu-id="b0760-186">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span><span class="sxs-lookup"><span data-stu-id="b0760-186">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span></span>  

<span data-ttu-id="b0760-187">To initialize the what if policy evaluation tool, set:</span><span class="sxs-lookup"><span data-stu-id="b0760-187">To initialize the what if policy evaluation tool, set:</span></span>

- <span data-ttu-id="b0760-188">**Isabella Simonsen** as user</span><span class="sxs-lookup"><span data-stu-id="b0760-188">**Isabella Simonsen** as user</span></span> 
- <span data-ttu-id="b0760-189">**Microsoft Azure Management** as cloud app</span><span class="sxs-lookup"><span data-stu-id="b0760-189">**Microsoft Azure Management** as cloud app</span></span>

 <span data-ttu-id="b0760-190">Clicking **What If** creates a simulation report that shows:</span><span class="sxs-lookup"><span data-stu-id="b0760-190">Clicking **What If** creates a simulation report that shows:</span></span>

- <span data-ttu-id="b0760-191">**Require MFA for Azure portal access** under **Policies that will apply**</span><span class="sxs-lookup"><span data-stu-id="b0760-191">**Require MFA for Azure portal access** under **Policies that will apply**</span></span> 
- <span data-ttu-id="b0760-192">**Require multi-factor authentication** as **Grant Controls**.</span><span class="sxs-lookup"><span data-stu-id="b0760-192">**Require multi-factor authentication** as **Grant Controls**.</span></span>

![What if policy tool](./media/app-based-mfa/23.png)



<span data-ttu-id="b0760-194">**To evaluate your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="b0760-194">**To evaluate your conditional access policy:**</span></span>

1. <span data-ttu-id="b0760-195">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span><span class="sxs-lookup"><span data-stu-id="b0760-195">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span></span>  
 
    ![What If](./media/app-based-mfa/14.png)

2. <span data-ttu-id="b0760-197">Click **Users**, select **Isabella Simonsen**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-197">Click **Users**, select **Isabella Simonsen**, and then click **Select**.</span></span>

    ![User](./media/app-based-mfa/15.png)

2. <span data-ttu-id="b0760-199">To select a cloud app, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0760-199">To select a cloud app, perform the following steps:</span></span>

    ![Cloud apps](./media/app-based-mfa/16.png)

    <span data-ttu-id="b0760-201">a.</span><span class="sxs-lookup"><span data-stu-id="b0760-201">a.</span></span> <span data-ttu-id="b0760-202">Click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="b0760-202">Click **Cloud apps**.</span></span>

    <span data-ttu-id="b0760-203">b.</span><span class="sxs-lookup"><span data-stu-id="b0760-203">b.</span></span> <span data-ttu-id="b0760-204">On the **Cloud apps page**, click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="b0760-204">On the **Cloud apps page**, click **Select apps**.</span></span>

    <span data-ttu-id="b0760-205">c.</span><span class="sxs-lookup"><span data-stu-id="b0760-205">c.</span></span> <span data-ttu-id="b0760-206">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-206">Click **Select**.</span></span>

    <span data-ttu-id="b0760-207">d.</span><span class="sxs-lookup"><span data-stu-id="b0760-207">d.</span></span> <span data-ttu-id="b0760-208">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b0760-208">On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.</span></span>

    <span data-ttu-id="b0760-209">e.</span><span class="sxs-lookup"><span data-stu-id="b0760-209">e.</span></span> <span data-ttu-id="b0760-210">On the cloud apps page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b0760-210">On the cloud apps page, click **Done**.</span></span>

3. <span data-ttu-id="b0760-211">Click **What If**.</span><span class="sxs-lookup"><span data-stu-id="b0760-211">Click **What If**.</span></span>


## <a name="test-your-conditional-access-policy"></a><span data-ttu-id="b0760-212">Test your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="b0760-212">Test your conditional access policy</span></span>

<span data-ttu-id="b0760-213">In the previous section, you have learned how to evaluate a simulated sign-in.</span><span class="sxs-lookup"><span data-stu-id="b0760-213">In the previous section, you have learned how to evaluate a simulated sign-in.</span></span> <span data-ttu-id="b0760-214">In addition to a simulation, you should also test your conditional access policy to ensure that it works as expected.</span><span class="sxs-lookup"><span data-stu-id="b0760-214">In addition to a simulation, you should also test your conditional access policy to ensure that it works as expected.</span></span> 

<span data-ttu-id="b0760-215">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) using your **Isabella Simonsen** test account.</span><span class="sxs-lookup"><span data-stu-id="b0760-215">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) using your **Isabella Simonsen** test account.</span></span> <span data-ttu-id="b0760-216">You should see a dialog that requires you to set your account up for additional security verification.</span><span class="sxs-lookup"><span data-stu-id="b0760-216">You should see a dialog that requires you to set your account up for additional security verification.</span></span>

![Multi-factor authentication](./media/app-based-mfa/22.png)


## <a name="clean-up-resources"></a><span data-ttu-id="b0760-218">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b0760-218">Clean up resources</span></span>

<span data-ttu-id="b0760-219">When no longer needed, delete the test user and the conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="b0760-219">When no longer needed, delete the test user and the conditional access policy:</span></span>

- <span data-ttu-id="b0760-220">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="b0760-220">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span></span>

- <span data-ttu-id="b0760-221">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span><span class="sxs-lookup"><span data-stu-id="b0760-221">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span></span>

    ![Multi-factor authentication](./media/app-based-mfa/33.png)


## <a name="next-steps"></a><span data-ttu-id="b0760-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0760-223">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="b0760-224">[Require terms of use to be accepted](require-tou.md)
> [Block access when a session risk is detected](app-sign-in-risk.md)</span><span class="sxs-lookup"><span data-stu-id="b0760-224">[Require terms of use to be accepted](require-tou.md)
[Block access when a session risk is detected](app-sign-in-risk.md)</span></span>
