---
title: Override HTTP behavior using the Azure CDN rules engine | Microsoft Docs
description: The rules engine allows you to customize how HTTP requests are handled by Azure CDN, such as blocking the delivery of certain types of content, define a caching policy, and modify HTTP headers.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: c246be51526e582b8d9d7092213689dbe1cfe407
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562976"
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="3bf8c-103">Override HTTP behavior using the Azure CDN rules engine</span><span class="sxs-lookup"><span data-stu-id="3bf8c-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="3bf8c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3bf8c-104">Overview</span></span>
<span data-ttu-id="3bf8c-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="3bf8c-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="3bf8c-107">There's also video content available in the "[See also](#see-also)" section.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="3bf8c-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="3bf8c-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="3bf8c-109">Tutorial</span></span>
1. <span data-ttu-id="3bf8c-110">From the CDN profile blade, click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profile blade manage button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="3bf8c-112">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="3bf8c-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="3bf8c-114">Options for a new rule are displayed.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-114">Options for a new rule are displayed.</span></span>
   
    ![CDN new rule options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="3bf8c-116">The order in which multiple rules are listed affects how they are handled.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="3bf8c-117">A subsequent rule may override the actions specified by a previous rule.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="3bf8c-118">Enter a name in the **Name / Description** textbox.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="3bf8c-119">Identify the type of requests the rule will apply to.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="3bf8c-120">By default, the **Always** match condition is selected.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="3bf8c-121">You'll use **Always** for this tutorial, so leave that selected.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN match condition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="3bf8c-123">There are many types of match conditions available in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="3bf8c-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="3bf8c-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="3bf8c-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="3bf8c-127">Click the **+** button next to **Features** to add a new feature.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="3bf8c-128">In the dropdown on the left, select **Force Internal Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="3bf8c-129">In the textbox that appears, enter **300**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="3bf8c-130">Leave the remaining default values.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-130">Leave the remaining default values.</span></span>
   
   ![CDN feature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="3bf8c-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="3bf8c-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="3bf8c-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="3bf8c-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="3bf8c-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="3bf8c-136">Click the **Add** button to save the new rule.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="3bf8c-137">The new rule is now awaiting approval.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="3bf8c-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3bf8c-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span><span class="sxs-lookup"><span data-stu-id="3bf8c-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="3bf8c-140">See also</span><span class="sxs-lookup"><span data-stu-id="3bf8c-140">See also</span></span>
* [<span data-ttu-id="3bf8c-141">Azure CDN Overview</span><span class="sxs-lookup"><span data-stu-id="3bf8c-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="3bf8c-142">Rules Engine Reference</span><span class="sxs-lookup"><span data-stu-id="3bf8c-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="3bf8c-143">Rules Engine Match Conditions</span><span class="sxs-lookup"><span data-stu-id="3bf8c-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="3bf8c-144">Rules Engine Conditional Expressions</span><span class="sxs-lookup"><span data-stu-id="3bf8c-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="3bf8c-145">Rules Engine Features</span><span class="sxs-lookup"><span data-stu-id="3bf8c-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="3bf8c-146">Overriding default HTTP behavior using the rules engine</span><span class="sxs-lookup"><span data-stu-id="3bf8c-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="3bf8c-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="3bf8c-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>



