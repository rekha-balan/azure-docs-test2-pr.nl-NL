---
title: Quickstart - Block access when a session risk is detected with Azure Active Directory conditional access | Microsoft Docs
description: In this quickstart, you learn how you can configure an Azure Active Directory (Azure AD) conditional access policy to block sign-ins based on session risks.
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
ms.date: 07/17/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 2bd52486a78ca103e0070d94ea423c069f845587
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856838"
---
# <a name="quickstart-block-access-when-a-session-risk-is-detected-with-azure-active-directory-conditional-access"></a><span data-ttu-id="33d58-104">Quickstart: Block access when a session risk is detected with Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="33d58-104">Quickstart: Block access when a session risk is detected with Azure Active Directory conditional access</span></span>  

<span data-ttu-id="33d58-105">To keep your environment protected, you might want to block suspicious users from signing insign-in activity.</span><span class="sxs-lookup"><span data-stu-id="33d58-105">To keep your environment protected, you might want to block suspicious users from signing insign-in activity.</span></span> <span data-ttu-id="33d58-106">[Azure Active Directory (Azure AD) Identity Protection](../active-directory-identityprotection.md) analyzes each sign-in and calculates the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="33d58-106">[Azure Active Directory (Azure AD) Identity Protection](../active-directory-identityprotection.md) analyzes each sign-in and calculates the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span> <span data-ttu-id="33d58-107">The likelihood (low, medium, high) is indicated in form of a calculated value called [sign-in risk levels](conditions.md#sign-in-risk).</span><span class="sxs-lookup"><span data-stu-id="33d58-107">The likelihood (low, medium, high) is indicated in form of a calculated value called [sign-in risk levels](conditions.md#sign-in-risk).</span></span> <span data-ttu-id="33d58-108">By setting the sign-in risk condition, you can configure a conditional access policy to respond to specific sign-in risk levels.</span><span class="sxs-lookup"><span data-stu-id="33d58-108">By setting the sign-in risk condition, you can configure a conditional access policy to respond to specific sign-in risk levels.</span></span> 

<span data-ttu-id="33d58-109">This quickstart shows how to configure a [conditional access policy](../active-directory-conditional-access-azure-portal.md) that blocks a sign-in when a configured sign-in risk level has been detected.</span><span class="sxs-lookup"><span data-stu-id="33d58-109">This quickstart shows how to configure a [conditional access policy](../active-directory-conditional-access-azure-portal.md) that blocks a sign-in when a configured sign-in risk level has been detected.</span></span> 

![Create policy](./media/app-sign-in-risk/1000.png)


<span data-ttu-id="33d58-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="33d58-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="33d58-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33d58-112">Prerequisites</span></span> 

<span data-ttu-id="33d58-113">To complete the scenario in this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="33d58-113">To complete the scenario in this tutorial, you need:</span></span>

- <span data-ttu-id="33d58-114">**Access to an Azure AD Premium P2 edition** - While conditional access is an Azure AD Premium P1 capability, you need a P2 edition because the scenario in this quickstart requires Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="33d58-114">**Access to an Azure AD Premium P2 edition** - While conditional access is an Azure AD Premium P1 capability, you need a P2 edition because the scenario in this quickstart requires Identity Protection.</span></span> 

- <span data-ttu-id="33d58-115">**Identity Protection** - The scenario in this quickstart requires Identity Protection to be enabled.</span><span class="sxs-lookup"><span data-stu-id="33d58-115">**Identity Protection** - The scenario in this quickstart requires Identity Protection to be enabled.</span></span> <span data-ttu-id="33d58-116">If you don't know how to enable Identity Protection, see [Enabling Azure Active Directory Identity Protection](../identity-protection/enable.md).</span><span class="sxs-lookup"><span data-stu-id="33d58-116">If you don't know how to enable Identity Protection, see [Enabling Azure Active Directory Identity Protection](../identity-protection/enable.md).</span></span>

- <span data-ttu-id="33d58-117">**Tor Browser** - The [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en) is designed to help you preserve your privacy online.</span><span class="sxs-lookup"><span data-stu-id="33d58-117">**Tor Browser** - The [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en) is designed to help you preserve your privacy online.</span></span> <span data-ttu-id="33d58-118">Identity Protection detects a sign-in from a Tor Browser as **sign-ins from anonymous IP addresses**, which has a medium risk level.</span><span class="sxs-lookup"><span data-stu-id="33d58-118">Identity Protection detects a sign-in from a Tor Browser as **sign-ins from anonymous IP addresses**, which has a medium risk level.</span></span> <span data-ttu-id="33d58-119">For more information, see [Azure Active Directory risk events](../reports-monitoring/concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="33d58-119">For more information, see [Azure Active Directory risk events](../reports-monitoring/concept-risk-events.md).</span></span>  

- <span data-ttu-id="33d58-120">**A test account called Alain Charon** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span><span class="sxs-lookup"><span data-stu-id="33d58-120">**A test account called Alain Charon** - If you don't know how to create a test account, see [Add cloud-based users](../fundamentals/add-users-azure-active-directory.md#add-cloud-based-users).</span></span>


## <a name="test-your-sign-in"></a><span data-ttu-id="33d58-121">Test your sign-in</span><span class="sxs-lookup"><span data-stu-id="33d58-121">Test your sign-in</span></span> 

<span data-ttu-id="33d58-122">The goal of this step is to make sure that your test account can access your tenant using the Tor Browser.</span><span class="sxs-lookup"><span data-stu-id="33d58-122">The goal of this step is to make sure that your test account can access your tenant using the Tor Browser.</span></span>

<span data-ttu-id="33d58-123">**To test your sign-in:**</span><span class="sxs-lookup"><span data-stu-id="33d58-123">**To test your sign-in:**</span></span>

1. <span data-ttu-id="33d58-124">Sign in to your [Azure portal](https://portal.azure.com) as **Alain Charon**.</span><span class="sxs-lookup"><span data-stu-id="33d58-124">Sign in to your [Azure portal](https://portal.azure.com) as **Alain Charon**.</span></span>

2. <span data-ttu-id="33d58-125">Sign out.</span><span class="sxs-lookup"><span data-stu-id="33d58-125">Sign out.</span></span> 


## <a name="create-your-conditional-access-policy"></a><span data-ttu-id="33d58-126">Create your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="33d58-126">Create your conditional access policy</span></span> 

<span data-ttu-id="33d58-127">The scenario in this quickstart uses a sign-in from a Tor Browser to generate a detected **Sign-ins from anonymous IP addresses** risk event.</span><span class="sxs-lookup"><span data-stu-id="33d58-127">The scenario in this quickstart uses a sign-in from a Tor Browser to generate a detected **Sign-ins from anonymous IP addresses** risk event.</span></span> <span data-ttu-id="33d58-128">The risk level of this risk event is medium.</span><span class="sxs-lookup"><span data-stu-id="33d58-128">The risk level of this risk event is medium.</span></span> <span data-ttu-id="33d58-129">To respond to this risk event, you set the sign-in risk condition to medium.</span><span class="sxs-lookup"><span data-stu-id="33d58-129">To respond to this risk event, you set the sign-in risk condition to medium.</span></span> <span data-ttu-id="33d58-130">In a production environment, you should set the sign-in risk condition either to high or to medium and high.</span><span class="sxs-lookup"><span data-stu-id="33d58-130">In a production environment, you should set the sign-in risk condition either to high or to medium and high.</span></span>     

<span data-ttu-id="33d58-131">This section shows how to create the required conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="33d58-131">This section shows how to create the required conditional access policy.</span></span> <span data-ttu-id="33d58-132">In your policy, set:</span><span class="sxs-lookup"><span data-stu-id="33d58-132">In your policy, set:</span></span>

|<span data-ttu-id="33d58-133">Setting</span><span class="sxs-lookup"><span data-stu-id="33d58-133">Setting</span></span> |<span data-ttu-id="33d58-134">Value</span><span class="sxs-lookup"><span data-stu-id="33d58-134">Value</span></span>|
|---     | --- |
| <span data-ttu-id="33d58-135">Users and groups</span><span class="sxs-lookup"><span data-stu-id="33d58-135">Users and groups</span></span> | <span data-ttu-id="33d58-136">Alain Charon</span><span class="sxs-lookup"><span data-stu-id="33d58-136">Alain Charon</span></span>  |
| <span data-ttu-id="33d58-137">Cloud apps</span><span class="sxs-lookup"><span data-stu-id="33d58-137">Cloud apps</span></span> | <span data-ttu-id="33d58-138">All cloud apps</span><span class="sxs-lookup"><span data-stu-id="33d58-138">All cloud apps</span></span> |
| <span data-ttu-id="33d58-139">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="33d58-139">Sign-in risk</span></span> | <span data-ttu-id="33d58-140">Medium</span><span class="sxs-lookup"><span data-stu-id="33d58-140">Medium</span></span> |
| <span data-ttu-id="33d58-141">Grant</span><span class="sxs-lookup"><span data-stu-id="33d58-141">Grant</span></span> | <span data-ttu-id="33d58-142">Block access</span><span class="sxs-lookup"><span data-stu-id="33d58-142">Block access</span></span> |
 

![Create policy](./media/app-sign-in-risk/130.png)

 


<span data-ttu-id="33d58-144">**To configure your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="33d58-144">**To configure your conditional access policy:**</span></span>

1. <span data-ttu-id="33d58-145">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span><span class="sxs-lookup"><span data-stu-id="33d58-145">Sign in to your [Azure portal](https://portal.azure.com) as global administrator, security administrator, or a conditional access administrator.</span></span>

2. <span data-ttu-id="33d58-146">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="33d58-146">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Azure Active Directory](./media/app-sign-in-risk/02.png)

3. <span data-ttu-id="33d58-148">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="33d58-148">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/app-sign-in-risk/03.png)
 
4. <span data-ttu-id="33d58-150">On the **Conditional Access** page, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="33d58-150">On the **Conditional Access** page, in the toolbar on the top, click **Add**.</span></span>

    ![Name](./media/app-sign-in-risk/108.png)

5. <span data-ttu-id="33d58-152">On the **New** page, in the **Name** textbox, type **Block access for medium risk level**.</span><span class="sxs-lookup"><span data-stu-id="33d58-152">On the **New** page, in the **Name** textbox, type **Block access for medium risk level**.</span></span>

    ![Name](./media/app-sign-in-risk/104.png)

6. <span data-ttu-id="33d58-154">In the **Assignment** section, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="33d58-154">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Users and groups](./media/app-sign-in-risk/06.png)

7. <span data-ttu-id="33d58-156">On the **Users and groups** page:</span><span class="sxs-lookup"><span data-stu-id="33d58-156">On the **Users and groups** page:</span></span>

    ![Conditional access](./media/app-sign-in-risk/107.png)

    <span data-ttu-id="33d58-158">a.</span><span class="sxs-lookup"><span data-stu-id="33d58-158">a.</span></span> <span data-ttu-id="33d58-159">Click **Select users and groups**, and then select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="33d58-159">Click **Select users and groups**, and then select **Users and groups**.</span></span>

    <span data-ttu-id="33d58-160">b.</span><span class="sxs-lookup"><span data-stu-id="33d58-160">b.</span></span> <span data-ttu-id="33d58-161">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="33d58-161">Click **Select**.</span></span>

    <span data-ttu-id="33d58-162">c.</span><span class="sxs-lookup"><span data-stu-id="33d58-162">c.</span></span> <span data-ttu-id="33d58-163">On the **Select** page, select **Alain Charon**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="33d58-163">On the **Select** page, select **Alain Charon**, and then click **Select**.</span></span>

    <span data-ttu-id="33d58-164">d.</span><span class="sxs-lookup"><span data-stu-id="33d58-164">d.</span></span> <span data-ttu-id="33d58-165">On the **Users and groups** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="33d58-165">On the **Users and groups** page, click **Done**.</span></span>

8. <span data-ttu-id="33d58-166">Click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="33d58-166">Click **Cloud apps**.</span></span>

    ![Cloud apps](./media/app-sign-in-risk/08.png)

9. <span data-ttu-id="33d58-168">On the **Cloud apps** page:</span><span class="sxs-lookup"><span data-stu-id="33d58-168">On the **Cloud apps** page:</span></span>

    ![Conditional access](./media/app-sign-in-risk/109.png)

    <span data-ttu-id="33d58-170">a.</span><span class="sxs-lookup"><span data-stu-id="33d58-170">a.</span></span> <span data-ttu-id="33d58-171">Click **All cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="33d58-171">Click **All cloud apps**.</span></span>

    <span data-ttu-id="33d58-172">b.</span><span class="sxs-lookup"><span data-stu-id="33d58-172">b.</span></span> <span data-ttu-id="33d58-173">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="33d58-173">Click **Done**.</span></span>

10. <span data-ttu-id="33d58-174">Click **Conditions**.</span><span class="sxs-lookup"><span data-stu-id="33d58-174">Click **Conditions**.</span></span> 

    ![Access controls](./media/app-sign-in-risk/19.png)

11. <span data-ttu-id="33d58-176">On the **Conditions** page:</span><span class="sxs-lookup"><span data-stu-id="33d58-176">On the **Conditions** page:</span></span>

    ![Sign-in risk level](./media/app-sign-in-risk/21.png)

    <span data-ttu-id="33d58-178">a.</span><span class="sxs-lookup"><span data-stu-id="33d58-178">a.</span></span> <span data-ttu-id="33d58-179">Click **Sign-in risk**.</span><span class="sxs-lookup"><span data-stu-id="33d58-179">Click **Sign-in risk**.</span></span>
 
    <span data-ttu-id="33d58-180">b.</span><span class="sxs-lookup"><span data-stu-id="33d58-180">b.</span></span> <span data-ttu-id="33d58-181">As **Configure**, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="33d58-181">As **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="33d58-182">c.</span><span class="sxs-lookup"><span data-stu-id="33d58-182">c.</span></span> <span data-ttu-id="33d58-183">As sign-in risk level, select **Medium**.</span><span class="sxs-lookup"><span data-stu-id="33d58-183">As sign-in risk level, select **Medium**.</span></span>

    <span data-ttu-id="33d58-184">d.</span><span class="sxs-lookup"><span data-stu-id="33d58-184">d.</span></span> <span data-ttu-id="33d58-185">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="33d58-185">Click **Select**.</span></span>

    <span data-ttu-id="33d58-186">e.</span><span class="sxs-lookup"><span data-stu-id="33d58-186">e.</span></span> <span data-ttu-id="33d58-187">On the **Conditions** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="33d58-187">On the **Conditions** page, click **Done**.</span></span>



10. <span data-ttu-id="33d58-188">In the **Access controls** section, click **Grant**.</span><span class="sxs-lookup"><span data-stu-id="33d58-188">In the **Access controls** section, click **Grant**.</span></span>

    ![Access controls](./media/app-sign-in-risk/10.png)

11. <span data-ttu-id="33d58-190">On the **Grant** page:</span><span class="sxs-lookup"><span data-stu-id="33d58-190">On the **Grant** page:</span></span>

    ![Conditional access](./media/app-sign-in-risk/105.png)

    <span data-ttu-id="33d58-192">a.</span><span class="sxs-lookup"><span data-stu-id="33d58-192">a.</span></span> <span data-ttu-id="33d58-193">Select **Block access**.</span><span class="sxs-lookup"><span data-stu-id="33d58-193">Select **Block access**.</span></span>

    <span data-ttu-id="33d58-194">b.</span><span class="sxs-lookup"><span data-stu-id="33d58-194">b.</span></span> <span data-ttu-id="33d58-195">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="33d58-195">Click **Select**.</span></span>

12. <span data-ttu-id="33d58-196">In the **Enable policy** section, click **On**.</span><span class="sxs-lookup"><span data-stu-id="33d58-196">In the **Enable policy** section, click **On**.</span></span>

    ![Enable policy](./media/app-sign-in-risk/18.png)

13. <span data-ttu-id="33d58-198">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="33d58-198">Click **Create**.</span></span>


## <a name="evaluate-a-simulated-sign-in"></a><span data-ttu-id="33d58-199">Evaluate a simulated sign-in</span><span class="sxs-lookup"><span data-stu-id="33d58-199">Evaluate a simulated sign-in</span></span>

<span data-ttu-id="33d58-200">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span><span class="sxs-lookup"><span data-stu-id="33d58-200">Now that you have configured your conditional access policy, you probably want to know whether it works as expected.</span></span> <span data-ttu-id="33d58-201">As a first step, use the conditional access **what if policy tool** to simulate a sign-in of your test user.</span><span class="sxs-lookup"><span data-stu-id="33d58-201">As a first step, use the conditional access **what if policy tool** to simulate a sign-in of your test user.</span></span> <span data-ttu-id="33d58-202">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span><span class="sxs-lookup"><span data-stu-id="33d58-202">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span></span>  

<span data-ttu-id="33d58-203">When you run the **what if policy tool** for this scenario, the **Block access for medium risk level** should be listed under **Policies that will apply**.</span><span class="sxs-lookup"><span data-stu-id="33d58-203">When you run the **what if policy tool** for this scenario, the **Block access for medium risk level** should be listed under **Policies that will apply**.</span></span> 

![User](./media/app-sign-in-risk/117.png)


<span data-ttu-id="33d58-205">**To evaluate your conditional access policy:**</span><span class="sxs-lookup"><span data-stu-id="33d58-205">**To evaluate your conditional access policy:**</span></span>

1. <span data-ttu-id="33d58-206">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span><span class="sxs-lookup"><span data-stu-id="33d58-206">On the [Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) page, in the menu on the top, click **What If**.</span></span>  
 
    ![What If](./media/app-sign-in-risk/14.png)

2. <span data-ttu-id="33d58-208">Click **User**, select **Alan Charon** on the **Users** page, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="33d58-208">Click **User**, select **Alan Charon** on the **Users** page, and then click **Select**.</span></span>

    ![User](./media/app-sign-in-risk/116.png)

3. <span data-ttu-id="33d58-210">As **Sign-in risk**, select **Medium**.</span><span class="sxs-lookup"><span data-stu-id="33d58-210">As **Sign-in risk**, select **Medium**.</span></span>

    ![User](./media/app-sign-in-risk/119.png)


3. <span data-ttu-id="33d58-212">Click **What If**.</span><span class="sxs-lookup"><span data-stu-id="33d58-212">Click **What If**.</span></span>


## <a name="test-your-conditional-access-policy"></a><span data-ttu-id="33d58-213">Test your conditional access policy</span><span class="sxs-lookup"><span data-stu-id="33d58-213">Test your conditional access policy</span></span>

<span data-ttu-id="33d58-214">In the previous section, you have learned how to evaluate a simulated sign-in.</span><span class="sxs-lookup"><span data-stu-id="33d58-214">In the previous section, you have learned how to evaluate a simulated sign-in.</span></span> <span data-ttu-id="33d58-215">In addition to a simulation, you should also test your conditional access policy to make sure that it works as expected.</span><span class="sxs-lookup"><span data-stu-id="33d58-215">In addition to a simulation, you should also test your conditional access policy to make sure that it works as expected.</span></span> 

<span data-ttu-id="33d58-216">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) as **Alan Charon** using the Tor Browser.</span><span class="sxs-lookup"><span data-stu-id="33d58-216">To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) as **Alan Charon** using the Tor Browser.</span></span> <span data-ttu-id="33d58-217">Your sign-in attempt should be blocked by your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="33d58-217">Your sign-in attempt should be blocked by your conditional access policy.</span></span>

![Multi-factor authentication](./media/app-sign-in-risk/118.png)


## <a name="clean-up-resources"></a><span data-ttu-id="33d58-219">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="33d58-219">Clean up resources</span></span>

<span data-ttu-id="33d58-220">When no longer needed, delete the test user, the Tor Browser and the conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="33d58-220">When no longer needed, delete the test user, the Tor Browser and the conditional access policy:</span></span>

- <span data-ttu-id="33d58-221">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="33d58-221">If you don't know how to delete an Azure AD user, see [Delete users from Azure AD](../fundamentals/add-users-azure-active-directory.md#delete-users-from-azure-ad).</span></span>

- <span data-ttu-id="33d58-222">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span><span class="sxs-lookup"><span data-stu-id="33d58-222">To delete your policy, select your policy, and then click **Delete** in the quick access toolbar.</span></span>

    ![Multi-factor authentication](./media/app-sign-in-risk/33.png)

- <span data-ttu-id="33d58-224">For instructions to remove the Tor Browser, see [Uninstalling](https://tb-manual.torproject.org/en-US/uninstalling.html).</span><span class="sxs-lookup"><span data-stu-id="33d58-224">For instructions to remove the Tor Browser, see [Uninstalling](https://tb-manual.torproject.org/en-US/uninstalling.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33d58-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="33d58-225">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="33d58-226">[Require terms of use to be accepted](require-tou.md)
> [Require MFA for specific apps](app-based-mfa.md)</span><span class="sxs-lookup"><span data-stu-id="33d58-226">[Require terms of use to be accepted](require-tou.md)
[Require MFA for specific apps](app-based-mfa.md)</span></span>

