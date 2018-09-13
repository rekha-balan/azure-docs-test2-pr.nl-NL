---
title: Override HTTP behavior using the Azure CDN rules engine | Microsoft Docs
description: The rules engine allows you to customize how HTTP requests are handled by Azure CDN, such as blocking the delivery of certain types of content, define a caching policy, and modify HTTP headers.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: v-deasim
ms.openlocfilehash: df8114aaf5b4672ea51482978abde6f0ce724528
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44785010"
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="68b20-103">Override HTTP behavior using the Azure CDN rules engine</span><span class="sxs-lookup"><span data-stu-id="68b20-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="68b20-104">Overview</span><span class="sxs-lookup"><span data-stu-id="68b20-104">Overview</span></span>
<span data-ttu-id="68b20-105">The Azure CDN rules engine allows you to customize how HTTP requests are handled.</span><span class="sxs-lookup"><span data-stu-id="68b20-105">The Azure CDN rules engine allows you to customize how HTTP requests are handled.</span></span> <span data-ttu-id="68b20-106">For example, blocking the delivery of certain content types, defining a caching policy, or modifying an HTTP header.</span><span class="sxs-lookup"><span data-stu-id="68b20-106">For example, blocking the delivery of certain content types, defining a caching policy, or modifying an HTTP header.</span></span> <span data-ttu-id="68b20-107">This tutorial demonstrates how to create a rule that changes the caching behavior of CDN assets.</span><span class="sxs-lookup"><span data-stu-id="68b20-107">This tutorial demonstrates how to create a rule that changes the caching behavior of CDN assets.</span></span> <span data-ttu-id="68b20-108">For more information about the rules engine syntax, see [Azure CDN rules engine reference](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="68b20-108">For more information about the rules engine syntax, see [Azure CDN rules engine reference](cdn-rules-engine-reference.md).</span></span>

## <a name="access"></a><span data-ttu-id="68b20-109">Access</span><span class="sxs-lookup"><span data-stu-id="68b20-109">Access</span></span>
<span data-ttu-id="68b20-110">To access the rules engine, you must first select **Manage** from the top of the **CDN profile** page to access the Azure CDN management page.</span><span class="sxs-lookup"><span data-stu-id="68b20-110">To access the rules engine, you must first select **Manage** from the top of the **CDN profile** page to access the Azure CDN management page.</span></span> <span data-ttu-id="68b20-111">Depending on whether your endpoint is optimized for dynamic site acceleration (DSA), you then access the rules engine with the set of rules appropriate for your type of endpoint:</span><span class="sxs-lookup"><span data-stu-id="68b20-111">Depending on whether your endpoint is optimized for dynamic site acceleration (DSA), you then access the rules engine with the set of rules appropriate for your type of endpoint:</span></span>

- <span data-ttu-id="68b20-112">Endpoints optimized for general web delivery or other non-DSA optimization:</span><span class="sxs-lookup"><span data-stu-id="68b20-112">Endpoints optimized for general web delivery or other non-DSA optimization:</span></span> 
    
    <span data-ttu-id="68b20-113">Select the **HTTP Large** tab, then select **Rules Engine**.</span><span class="sxs-lookup"><span data-stu-id="68b20-113">Select the **HTTP Large** tab, then select **Rules Engine**.</span></span>

    ![Rules engine for HTTP](./media/cdn-rules-engine/cdn-http-rules-engine.png)

- <span data-ttu-id="68b20-115">Endpoints optimized for DSA:</span><span class="sxs-lookup"><span data-stu-id="68b20-115">Endpoints optimized for DSA:</span></span> 
    
    <span data-ttu-id="68b20-116">Select the **ADN** tab, then select **Rules Engine**.</span><span class="sxs-lookup"><span data-stu-id="68b20-116">Select the **ADN** tab, then select **Rules Engine**.</span></span> 
    
    <span data-ttu-id="68b20-117">ADN is a term used by Verizon to specify DSA content.</span><span class="sxs-lookup"><span data-stu-id="68b20-117">ADN is a term used by Verizon to specify DSA content.</span></span> <span data-ttu-id="68b20-118">Any rules you create here are ignored by any endpoints in your profile that are not optimized for DSA.</span><span class="sxs-lookup"><span data-stu-id="68b20-118">Any rules you create here are ignored by any endpoints in your profile that are not optimized for DSA.</span></span> 

    ![Rules engine for DSA](./media/cdn-rules-engine/cdn-dsa-rules-engine.png)

## <a name="tutorial"></a><span data-ttu-id="68b20-120">Tutorial</span><span class="sxs-lookup"><span data-stu-id="68b20-120">Tutorial</span></span>
1. <span data-ttu-id="68b20-121">From the **CDN profile** page, select **Manage**.</span><span class="sxs-lookup"><span data-stu-id="68b20-121">From the **CDN profile** page, select **Manage**.</span></span>
   
    ![CDN profile Manage button](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="68b20-123">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="68b20-123">The CDN management portal opens.</span></span>

2. <span data-ttu-id="68b20-124">Select the **HTTP Large** tab, then select **Rules Engine**.</span><span class="sxs-lookup"><span data-stu-id="68b20-124">Select the **HTTP Large** tab, then select **Rules Engine**.</span></span>
   
    <span data-ttu-id="68b20-125">The options for a new rule are displayed.</span><span class="sxs-lookup"><span data-stu-id="68b20-125">The options for a new rule are displayed.</span></span>
   
    ![CDN new rule options](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="68b20-127">The order in which multiple rules are listed affects how they are handled.</span><span class="sxs-lookup"><span data-stu-id="68b20-127">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="68b20-128">A subsequent rule may override the actions specified by a previous rule.</span><span class="sxs-lookup"><span data-stu-id="68b20-128">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 

3. <span data-ttu-id="68b20-129">Enter a name in the **Name / Description** textbox.</span><span class="sxs-lookup"><span data-stu-id="68b20-129">Enter a name in the **Name / Description** textbox.</span></span>

4. <span data-ttu-id="68b20-130">Identify the type of requests the rule applies to.</span><span class="sxs-lookup"><span data-stu-id="68b20-130">Identify the type of requests the rule applies to.</span></span> <span data-ttu-id="68b20-131">Use the default match condition, **Always**.</span><span class="sxs-lookup"><span data-stu-id="68b20-131">Use the default match condition, **Always**.</span></span> 
   
   ![CDN rule match condition](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="68b20-133">Multiple match conditions are available in the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="68b20-133">Multiple match conditions are available in the dropdown list.</span></span> <span data-ttu-id="68b20-134">For information about the currently selected match condition, select the blue informational icon to its left.</span><span class="sxs-lookup"><span data-stu-id="68b20-134">For information about the currently selected match condition, select the blue informational icon to its left.</span></span>
   > 
   >  <span data-ttu-id="68b20-135">For a detailed list of conditional expressions, see [Rules engine conditional expressions](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="68b20-135">For a detailed list of conditional expressions, see [Rules engine conditional expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="68b20-136">For a detailed list of match conditions, see [Rules engine match conditions](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="68b20-136">For a detailed list of match conditions, see [Rules engine match conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 

5. <span data-ttu-id="68b20-137">To add a new feature, select the **+** button next to **Features**.</span><span class="sxs-lookup"><span data-stu-id="68b20-137">To add a new feature, select the **+** button next to **Features**.</span></span>  <span data-ttu-id="68b20-138">In the dropdown on the left, select **Force Internal Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="68b20-138">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="68b20-139">In the textbox that appears, enter **300**.</span><span class="sxs-lookup"><span data-stu-id="68b20-139">In the textbox that appears, enter **300**.</span></span> <span data-ttu-id="68b20-140">Do not change the remaining default values.</span><span class="sxs-lookup"><span data-stu-id="68b20-140">Do not change the remaining default values.</span></span>
   
   ![CDN rule feature](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="68b20-142">Multiple features are available in the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="68b20-142">Multiple features are available in the dropdown list.</span></span> <span data-ttu-id="68b20-143">For information about the currently selected feature, select the blue informational icon to its left.</span><span class="sxs-lookup"><span data-stu-id="68b20-143">For information about the currently selected feature, select the blue informational icon to its left.</span></span> 
   >
   > <span data-ttu-id="68b20-144">For **Force Internal Max-Age**, the asset's `Cache-Control` and `Expires` headers are overridden to control when the CDN edge node refreshes the asset from the origin.</span><span class="sxs-lookup"><span data-stu-id="68b20-144">For **Force Internal Max-Age**, the asset's `Cache-Control` and `Expires` headers are overridden to control when the CDN edge node refreshes the asset from the origin.</span></span> <span data-ttu-id="68b20-145">In this example, the CDN edge node caches the asset for 300 seconds, or 5 minutes, before it refreshes the asset from its origin.</span><span class="sxs-lookup"><span data-stu-id="68b20-145">In this example, the CDN edge node caches the asset for 300 seconds, or 5 minutes, before it refreshes the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="68b20-146">For a detailed list of features, see [Rules engine features](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="68b20-146">For a detailed list of features, see [Rules engine features](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 

6. <span data-ttu-id="68b20-147">Select **Add** to save the new rule.</span><span class="sxs-lookup"><span data-stu-id="68b20-147">Select **Add** to save the new rule.</span></span>  <span data-ttu-id="68b20-148">The new rule is now awaiting approval.</span><span class="sxs-lookup"><span data-stu-id="68b20-148">The new rule is now awaiting approval.</span></span> <span data-ttu-id="68b20-149">After it has been approved, the status changes from **Pending XML** to **Active XML**.</span><span class="sxs-lookup"><span data-stu-id="68b20-149">After it has been approved, the status changes from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="68b20-150">Rules changes can take up to 10 minutes to propagate through Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="68b20-150">Rules changes can take up to 10 minutes to propagate through Azure CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="68b20-151">See also</span><span class="sxs-lookup"><span data-stu-id="68b20-151">See also</span></span>
* [<span data-ttu-id="68b20-152">Azure CDN overview</span><span class="sxs-lookup"><span data-stu-id="68b20-152">Azure CDN overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="68b20-153">Rules engine reference</span><span class="sxs-lookup"><span data-stu-id="68b20-153">Rules engine reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="68b20-154">Rules engine match conditions</span><span class="sxs-lookup"><span data-stu-id="68b20-154">Rules engine match conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="68b20-155">Rules engine conditional expressions</span><span class="sxs-lookup"><span data-stu-id="68b20-155">Rules engine conditional expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="68b20-156">Rules engine features</span><span class="sxs-lookup"><span data-stu-id="68b20-156">Rules engine features</span></span>](cdn-rules-engine-reference-features.md)
* <span data-ttu-id="68b20-157">[Azure Fridays: Azure CDN's powerful new premium features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="68b20-157">[Azure Fridays: Azure CDN's powerful new premium features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>