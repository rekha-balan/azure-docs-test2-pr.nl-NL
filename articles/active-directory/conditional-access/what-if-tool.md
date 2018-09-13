---
title: What is the what if tool in Azure Active Directory conditional access?
description: Learn how you can understand the impact of your conditional access policies on your environment.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: d9bdc35e732a84920800424a260610fd6f068c94
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864786"
---
# <a name="what-is-the-what-if-tool-in-azure-active-directory-conditional-access"></a><span data-ttu-id="9af86-104">What is the what if tool in Azure Active Directory conditional access?</span><span class="sxs-lookup"><span data-stu-id="9af86-104">What is the what if tool in Azure Active Directory conditional access?</span></span>

<span data-ttu-id="9af86-105">[Conditional access](../active-directory-conditional-access-azure-portal.md) is a capability of Azure Active Directory (Azure AD) that enables you to control how authorized users access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="9af86-105">[Conditional access](../active-directory-conditional-access-azure-portal.md) is a capability of Azure Active Directory (Azure AD) that enables you to control how authorized users access your cloud apps.</span></span> <span data-ttu-id="9af86-106">How do you know what to expect form the conditional access policies in your environment?</span><span class="sxs-lookup"><span data-stu-id="9af86-106">How do you know what to expect form the conditional access policies in your environment?</span></span> <span data-ttu-id="9af86-107">To answer this question, you can use the **conditional access what if tool**.</span><span class="sxs-lookup"><span data-stu-id="9af86-107">To answer this question, you can use the **conditional access what if tool**.</span></span>

<span data-ttu-id="9af86-108">This article explains how you can use this tool to test your conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="9af86-108">This article explains how you can use this tool to test your conditional access policies.</span></span>

## <a name="what-it-is"></a><span data-ttu-id="9af86-109">What it is</span><span class="sxs-lookup"><span data-stu-id="9af86-109">What it is</span></span>

<span data-ttu-id="9af86-110">The **conditional access what if policy tool** allows you to understand the impact of your conditional access policies on your environment.</span><span class="sxs-lookup"><span data-stu-id="9af86-110">The **conditional access what if policy tool** allows you to understand the impact of your conditional access policies on your environment.</span></span> <span data-ttu-id="9af86-111">Instead of test driving your policies by performing multiple sign-ins manually, this tool enables you to evaluate a simulated sign-in of a user.</span><span class="sxs-lookup"><span data-stu-id="9af86-111">Instead of test driving your policies by performing multiple sign-ins manually, this tool enables you to evaluate a simulated sign-in of a user.</span></span> <span data-ttu-id="9af86-112">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span><span class="sxs-lookup"><span data-stu-id="9af86-112">The simulation estimates the impact this sign-in has on your policies and generates a simulation report.</span></span> <span data-ttu-id="9af86-113">The report does not only list the applied conditional access policies but also [classic policies](policy-migration.md#classic-policies) if they exist.</span><span class="sxs-lookup"><span data-stu-id="9af86-113">The report does not only list the applied conditional access policies but also [classic policies](policy-migration.md#classic-policies) if they exist.</span></span>    

<span data-ttu-id="9af86-114">The what if tools also provides a way to quickly determine the policies that apply to a specific user.</span><span class="sxs-lookup"><span data-stu-id="9af86-114">The what if tools also provides a way to quickly determine the policies that apply to a specific user.</span></span> <span data-ttu-id="9af86-115">You can use the information, for example, if you need to troubleshoot an issue.</span><span class="sxs-lookup"><span data-stu-id="9af86-115">You can use the information, for example, if you need to troubleshoot an issue.</span></span>  

## <a name="how-it-works"></a><span data-ttu-id="9af86-116">How it works</span><span class="sxs-lookup"><span data-stu-id="9af86-116">How it works</span></span>

<span data-ttu-id="9af86-117">In the **conditional access what if tool**, you first need to configure the settings of the sign-in scenario you want to simulate.</span><span class="sxs-lookup"><span data-stu-id="9af86-117">In the **conditional access what if tool**, you first need to configure the settings of the sign-in scenario you want to simulate.</span></span> <span data-ttu-id="9af86-118">These settings include:</span><span class="sxs-lookup"><span data-stu-id="9af86-118">These settings include:</span></span>

- <span data-ttu-id="9af86-119">The user you want to test</span><span class="sxs-lookup"><span data-stu-id="9af86-119">The user you want to test</span></span> 

- <span data-ttu-id="9af86-120">The cloud apps the user would attempt to access</span><span class="sxs-lookup"><span data-stu-id="9af86-120">The cloud apps the user would attempt to access</span></span>

- <span data-ttu-id="9af86-121">The conditions under which access to the configures cloud apps is performed</span><span class="sxs-lookup"><span data-stu-id="9af86-121">The conditions under which access to the configures cloud apps is performed</span></span>
     
<span data-ttu-id="9af86-122">As a next step, you can initiate a simulation run that evaluates your settings.</span><span class="sxs-lookup"><span data-stu-id="9af86-122">As a next step, you can initiate a simulation run that evaluates your settings.</span></span> <span data-ttu-id="9af86-123">Only policies that are enabled are part of an evaluation run.</span><span class="sxs-lookup"><span data-stu-id="9af86-123">Only policies that are enabled are part of an evaluation run.</span></span>


<span data-ttu-id="9af86-124">When the evaluation has finished, the tool generates a report of the affected policies.</span><span class="sxs-lookup"><span data-stu-id="9af86-124">When the evaluation has finished, the tool generates a report of the affected policies.</span></span>


> [!NOTE]
> <span data-ttu-id="9af86-125">Currently, the What If tool does not support nested groups.</span><span class="sxs-lookup"><span data-stu-id="9af86-125">Currently, the What If tool does not support nested groups.</span></span> <span data-ttu-id="9af86-126">If a user is in a group and that group is member of another group that is used in a conditional access policy, then the what if tool does not correctly display the effect of that policy to the user.</span><span class="sxs-lookup"><span data-stu-id="9af86-126">If a user is in a group and that group is member of another group that is used in a conditional access policy, then the what if tool does not correctly display the effect of that policy to the user.</span></span> 


## <a name="running-the-tool"></a><span data-ttu-id="9af86-127">Running the tool</span><span class="sxs-lookup"><span data-stu-id="9af86-127">Running the tool</span></span>

<span data-ttu-id="9af86-128">You can find the **what if** tool on the **[Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)** page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9af86-128">You can find the **what if** tool on the **[Conditional access - Policies](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)** page in the Azure portal.</span></span>

<span data-ttu-id="9af86-129">To start the tool, in the toolbar on top of the list of policies, click **What if**.</span><span class="sxs-lookup"><span data-stu-id="9af86-129">To start the tool, in the toolbar on top of the list of policies, click **What if**.</span></span>

![What if](./media/what-if-tool/01.png)

<span data-ttu-id="9af86-131">Before you can run an evaluation, you must configure the settings.</span><span class="sxs-lookup"><span data-stu-id="9af86-131">Before you can run an evaluation, you must configure the settings.</span></span>

## <a name="settings"></a><span data-ttu-id="9af86-132">Settings</span><span class="sxs-lookup"><span data-stu-id="9af86-132">Settings</span></span>

<span data-ttu-id="9af86-133">This section provides you with information about the settings of simulation run.</span><span class="sxs-lookup"><span data-stu-id="9af86-133">This section provides you with information about the settings of simulation run.</span></span>

![What if](./media/what-if-tool/02.png)


### <a name="user"></a><span data-ttu-id="9af86-135">User</span><span class="sxs-lookup"><span data-stu-id="9af86-135">User</span></span>

<span data-ttu-id="9af86-136">You can only select one user.</span><span class="sxs-lookup"><span data-stu-id="9af86-136">You can only select one user.</span></span> <span data-ttu-id="9af86-137">This is the only required field.</span><span class="sxs-lookup"><span data-stu-id="9af86-137">This is the only required field.</span></span>

### <a name="cloud-apps"></a><span data-ttu-id="9af86-138">Cloud apps</span><span class="sxs-lookup"><span data-stu-id="9af86-138">Cloud apps</span></span>

<span data-ttu-id="9af86-139">The default for this setting is **All cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="9af86-139">The default for this setting is **All cloud apps**.</span></span> <span data-ttu-id="9af86-140">The default setting performs an evaluation of all available policies in your environment.</span><span class="sxs-lookup"><span data-stu-id="9af86-140">The default setting performs an evaluation of all available policies in your environment.</span></span> <span data-ttu-id="9af86-141">You can narrow down the scope to policies affecting specific cloud apps.</span><span class="sxs-lookup"><span data-stu-id="9af86-141">You can narrow down the scope to policies affecting specific cloud apps.</span></span>


### <a name="ip-address"></a><span data-ttu-id="9af86-142">IP address</span><span class="sxs-lookup"><span data-stu-id="9af86-142">IP address</span></span>

<span data-ttu-id="9af86-143">The IP address is a single IPv4 address to mimic the [location condition](location-condition.md).</span><span class="sxs-lookup"><span data-stu-id="9af86-143">The IP address is a single IPv4 address to mimic the [location condition](location-condition.md).</span></span> <span data-ttu-id="9af86-144">The address represents Internet facing address of the device used by your user to sign in.</span><span class="sxs-lookup"><span data-stu-id="9af86-144">The address represents Internet facing address of the device used by your user to sign in.</span></span> <span data-ttu-id="9af86-145">You can verify the IP address of a device by, for example, navigating to [What is my IP address](https://whatismyipaddress.com).</span><span class="sxs-lookup"><span data-stu-id="9af86-145">You can verify the IP address of a device by, for example, navigating to [What is my IP address](https://whatismyipaddress.com).</span></span>    

### <a name="device-platforms"></a><span data-ttu-id="9af86-146">Device platforms</span><span class="sxs-lookup"><span data-stu-id="9af86-146">Device platforms</span></span>

<span data-ttu-id="9af86-147">This setting mimics the [device platforms condition](conditions.md#device-platforms) and represents the equivalent of **All platforms (including unsupported)**.</span><span class="sxs-lookup"><span data-stu-id="9af86-147">This setting mimics the [device platforms condition](conditions.md#device-platforms) and represents the equivalent of **All platforms (including unsupported)**.</span></span> 
### <a name="client-apps"></a><span data-ttu-id="9af86-148">Client apps</span><span class="sxs-lookup"><span data-stu-id="9af86-148">Client apps</span></span>

<span data-ttu-id="9af86-149">This setting mimics the [client apps condition](conditions.md#client-apps).</span><span class="sxs-lookup"><span data-stu-id="9af86-149">This setting mimics the [client apps condition](conditions.md#client-apps).</span></span>
<span data-ttu-id="9af86-150">By default, this setting causes an evaluation of all policies having **Browser** or **Mobile apps and desktop clients** either individually or both selected.</span><span class="sxs-lookup"><span data-stu-id="9af86-150">By default, this setting causes an evaluation of all policies having **Browser** or **Mobile apps and desktop clients** either individually or both selected.</span></span> <span data-ttu-id="9af86-151">It also detects policies that enforce **Exchange ActiveSync (EAS)**.</span><span class="sxs-lookup"><span data-stu-id="9af86-151">It also detects policies that enforce **Exchange ActiveSync (EAS)**.</span></span> <span data-ttu-id="9af86-152">You can narrow this setting down by selecting:</span><span class="sxs-lookup"><span data-stu-id="9af86-152">You can narrow this setting down by selecting:</span></span>

- <span data-ttu-id="9af86-153">**Browser** to evaluate all policies having at least **Browser** selected.</span><span class="sxs-lookup"><span data-stu-id="9af86-153">**Browser** to evaluate all policies having at least **Browser** selected.</span></span> 

- <span data-ttu-id="9af86-154">**Mobile apps and desktop clients** to evaluate all policies having at least **Mobile apps and desktop clients** selected.</span><span class="sxs-lookup"><span data-stu-id="9af86-154">**Mobile apps and desktop clients** to evaluate all policies having at least **Mobile apps and desktop clients** selected.</span></span> 


### <a name="sign-in-risk"></a><span data-ttu-id="9af86-155">Sign-in risk</span><span class="sxs-lookup"><span data-stu-id="9af86-155">Sign-in risk</span></span>

<span data-ttu-id="9af86-156">This setting mimics the [sign-in risk condition](conditions.md#sign-in-risk).</span><span class="sxs-lookup"><span data-stu-id="9af86-156">This setting mimics the [sign-in risk condition](conditions.md#sign-in-risk).</span></span>   


## <a name="evaluation"></a><span data-ttu-id="9af86-157">Evaluation</span><span class="sxs-lookup"><span data-stu-id="9af86-157">Evaluation</span></span> 

<span data-ttu-id="9af86-158">You start an evaluation by clicking **What if**.</span><span class="sxs-lookup"><span data-stu-id="9af86-158">You start an evaluation by clicking **What if**.</span></span> <span data-ttu-id="9af86-159">The evaluation result provides you with a report that consists of:</span><span class="sxs-lookup"><span data-stu-id="9af86-159">The evaluation result provides you with a report that consists of:</span></span> 

![What if](./media/what-if-tool/03.png)

- <span data-ttu-id="9af86-161">An indicator whether classic policies exist in your environment</span><span class="sxs-lookup"><span data-stu-id="9af86-161">An indicator whether classic policies exist in your environment</span></span>
- <span data-ttu-id="9af86-162">Policies that apply to your user</span><span class="sxs-lookup"><span data-stu-id="9af86-162">Policies that apply to your user</span></span>
- <span data-ttu-id="9af86-163">Policies that don't apply to your user</span><span class="sxs-lookup"><span data-stu-id="9af86-163">Policies that don't apply to your user</span></span>


<span data-ttu-id="9af86-164">If [classic policies](policy-migration.md#classic-policies) exist for the selected cloud apps, an indicator is presented to you.</span><span class="sxs-lookup"><span data-stu-id="9af86-164">If [classic policies](policy-migration.md#classic-policies) exist for the selected cloud apps, an indicator is presented to you.</span></span> <span data-ttu-id="9af86-165">By clicking the indicator, you are redirected to the classic policies page.</span><span class="sxs-lookup"><span data-stu-id="9af86-165">By clicking the indicator, you are redirected to the classic policies page.</span></span> <span data-ttu-id="9af86-166">On the classic policies page, you can migrate a classic policy or just disable it.</span><span class="sxs-lookup"><span data-stu-id="9af86-166">On the classic policies page, you can migrate a classic policy or just disable it.</span></span> <span data-ttu-id="9af86-167">You can return to your evaluation result by closing this page.</span><span class="sxs-lookup"><span data-stu-id="9af86-167">You can return to your evaluation result by closing this page.</span></span>

<span data-ttu-id="9af86-168">On the list of policies that apply to your selected user, you can also find a list of [grant controls](controls.md#grant-controls) and [session](controls.md#session-controls) controls your user must satisfy.</span><span class="sxs-lookup"><span data-stu-id="9af86-168">On the list of policies that apply to your selected user, you can also find a list of [grant controls](controls.md#grant-controls) and [session](controls.md#session-controls) controls your user must satisfy.</span></span>

<span data-ttu-id="9af86-169">On the list of policies that don't apply to your user, you can and also find the reasons why these policies don't apply.</span><span class="sxs-lookup"><span data-stu-id="9af86-169">On the list of policies that don't apply to your user, you can and also find the reasons why these policies don't apply.</span></span> <span data-ttu-id="9af86-170">For each listed policy, the reason represents the first condition that was not satisfied.</span><span class="sxs-lookup"><span data-stu-id="9af86-170">For each listed policy, the reason represents the first condition that was not satisfied.</span></span> <span data-ttu-id="9af86-171">A possible reason for a policy that is not applied is a disabled policy because they are not further evaluated.</span><span class="sxs-lookup"><span data-stu-id="9af86-171">A possible reason for a policy that is not applied is a disabled policy because they are not further evaluated.</span></span>   



## <a name="next-steps"></a><span data-ttu-id="9af86-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="9af86-172">Next steps</span></span>

- <span data-ttu-id="9af86-173">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="9af86-173">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="9af86-174">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="9af86-174">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 

- <span data-ttu-id="9af86-175">if you want to migrate classic policies, see [Migrate classic policies in the Azure portal](policy-migration.md)</span><span class="sxs-lookup"><span data-stu-id="9af86-175">if you want to migrate classic policies, see [Migrate classic policies in the Azure portal](policy-migration.md)</span></span>  
