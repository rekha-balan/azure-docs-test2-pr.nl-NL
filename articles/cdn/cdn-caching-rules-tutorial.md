---
title: Tutorial - Set Azure CDN caching rules | Microsoft Docs
description: In this tutorial, you set an Azure CDN global caching rule and a custom caching rule.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 04/20/2018
ms.author: v-deasim
ms.custom: mvc
ms.openlocfilehash: a4b5a6a44fe9271f6ff9627c1c5623f0031f23ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867262"
---
# <a name="tutorial-set-azure-cdn-caching-rules"></a><span data-ttu-id="1956a-103">Tutorial: Set Azure CDN caching rules</span><span class="sxs-lookup"><span data-stu-id="1956a-103">Tutorial: Set Azure CDN caching rules</span></span>

> [!NOTE] 
> <span data-ttu-id="1956a-104">Azure CDN caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai**.</span><span class="sxs-lookup"><span data-stu-id="1956a-104">Azure CDN caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai**.</span></span> <span data-ttu-id="1956a-105">For **Azure CDN Premium from Verizon**, use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.</span><span class="sxs-lookup"><span data-stu-id="1956a-105">For **Azure CDN Premium from Verizon**, use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.</span></span>
 

<span data-ttu-id="1956a-106">This tutorial describes how you can use Azure Content Delivery Network (CDN) caching rules to set or modify default cache expiration behavior both globally and with custom conditions, such as a URL path and file extension.</span><span class="sxs-lookup"><span data-stu-id="1956a-106">This tutorial describes how you can use Azure Content Delivery Network (CDN) caching rules to set or modify default cache expiration behavior both globally and with custom conditions, such as a URL path and file extension.</span></span> <span data-ttu-id="1956a-107">Azure CDN provides two types of caching rules:</span><span class="sxs-lookup"><span data-stu-id="1956a-107">Azure CDN provides two types of caching rules:</span></span>
- <span data-ttu-id="1956a-108">Global caching rules: You can set one global caching rule for each endpoint in your profile, which affects all requests to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="1956a-108">Global caching rules: You can set one global caching rule for each endpoint in your profile, which affects all requests to the endpoint.</span></span> <span data-ttu-id="1956a-109">The global caching rule overrides any HTTP cache-directive headers, if set.</span><span class="sxs-lookup"><span data-stu-id="1956a-109">The global caching rule overrides any HTTP cache-directive headers, if set.</span></span>

- <span data-ttu-id="1956a-110">Custom caching rules: You can set one or more custom caching rules for each endpoint in your profile.</span><span class="sxs-lookup"><span data-stu-id="1956a-110">Custom caching rules: You can set one or more custom caching rules for each endpoint in your profile.</span></span> <span data-ttu-id="1956a-111">Custom caching rules match specific paths and file extensions, are processed in order, and override the global caching rule, if set.</span><span class="sxs-lookup"><span data-stu-id="1956a-111">Custom caching rules match specific paths and file extensions, are processed in order, and override the global caching rule, if set.</span></span> 

<span data-ttu-id="1956a-112">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1956a-112">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> - <span data-ttu-id="1956a-113">Open the caching rules page.</span><span class="sxs-lookup"><span data-stu-id="1956a-113">Open the caching rules page.</span></span>
> - <span data-ttu-id="1956a-114">Create a global caching rule.</span><span class="sxs-lookup"><span data-stu-id="1956a-114">Create a global caching rule.</span></span>
> - <span data-ttu-id="1956a-115">Create a custom caching rule.</span><span class="sxs-lookup"><span data-stu-id="1956a-115">Create a custom caching rule.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="1956a-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1956a-116">Prerequisites</span></span>

<span data-ttu-id="1956a-117">Before you can complete the steps in this tutorial, you must first create a CDN profile and at least one CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="1956a-117">Before you can complete the steps in this tutorial, you must first create a CDN profile and at least one CDN endpoint.</span></span> <span data-ttu-id="1956a-118">For more information, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="1956a-118">For more information, see [Quickstart: Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md).</span></span>

## <a name="open-the-azure-cdn-caching-rules-page"></a><span data-ttu-id="1956a-119">Open the Azure CDN caching rules page</span><span class="sxs-lookup"><span data-stu-id="1956a-119">Open the Azure CDN caching rules page</span></span>

1. <span data-ttu-id="1956a-120">In the [Azure portal](https://portal.azure.com), select a CDN profile, then select an endpoint.</span><span class="sxs-lookup"><span data-stu-id="1956a-120">In the [Azure portal](https://portal.azure.com), select a CDN profile, then select an endpoint.</span></span>

2. <span data-ttu-id="1956a-121">In the left pane under Settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="1956a-121">In the left pane under Settings, select **Caching rules**.</span></span>

   ![CDN Caching rules button](./media/cdn-caching-rules/cdn-caching-rules-btn.png)

   <span data-ttu-id="1956a-123">The **Caching rules** page appears.</span><span class="sxs-lookup"><span data-stu-id="1956a-123">The **Caching rules** page appears.</span></span>

   ![CDN Caching rules page](./media/cdn-caching-rules/cdn-caching-rules-page.png)


## <a name="set-global-caching-rules"></a><span data-ttu-id="1956a-125">Set global caching rules</span><span class="sxs-lookup"><span data-stu-id="1956a-125">Set global caching rules</span></span>

<span data-ttu-id="1956a-126">Create a global caching rule as follows:</span><span class="sxs-lookup"><span data-stu-id="1956a-126">Create a global caching rule as follows:</span></span>

1. <span data-ttu-id="1956a-127">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings**.</span><span class="sxs-lookup"><span data-stu-id="1956a-127">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings**.</span></span>

2. <span data-ttu-id="1956a-128">Set **Caching behavior** to **Set if missing**.</span><span class="sxs-lookup"><span data-stu-id="1956a-128">Set **Caching behavior** to **Set if missing**.</span></span>
       
3. <span data-ttu-id="1956a-129">For **Cache expiration duration**, enter 10 in the **Days** field.</span><span class="sxs-lookup"><span data-stu-id="1956a-129">For **Cache expiration duration**, enter 10 in the **Days** field.</span></span>

    <span data-ttu-id="1956a-130">The global caching rule affects all requests to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="1956a-130">The global caching rule affects all requests to the endpoint.</span></span> <span data-ttu-id="1956a-131">This rule honors the origin cache-directive headers, if they exist (`Cache-Control` or `Expires`); otherwise, if they are not specified, it sets the cache to 10 days.</span><span class="sxs-lookup"><span data-stu-id="1956a-131">This rule honors the origin cache-directive headers, if they exist (`Cache-Control` or `Expires`); otherwise, if they are not specified, it sets the cache to 10 days.</span></span> 

    ![Global caching rules](./media/cdn-caching-rules/cdn-global-caching-rules.png)

## <a name="set-custom-caching-rules"></a><span data-ttu-id="1956a-133">Set custom caching rules</span><span class="sxs-lookup"><span data-stu-id="1956a-133">Set custom caching rules</span></span>

<span data-ttu-id="1956a-134">Create a custom caching rule as follows:</span><span class="sxs-lookup"><span data-stu-id="1956a-134">Create a custom caching rule as follows:</span></span>

1. <span data-ttu-id="1956a-135">Under **Custom caching rules**, set **Match condition** to **Path** and **Match value** to `/images/*.jpg`.</span><span class="sxs-lookup"><span data-stu-id="1956a-135">Under **Custom caching rules**, set **Match condition** to **Path** and **Match value** to `/images/*.jpg`.</span></span>
    
2. <span data-ttu-id="1956a-136">Set **Caching behavior** to **Override** and enter 30 in the **Days** field.</span><span class="sxs-lookup"><span data-stu-id="1956a-136">Set **Caching behavior** to **Override** and enter 30 in the **Days** field.</span></span>
       
    <span data-ttu-id="1956a-137">This custom caching rule sets a cache duration of 30 days on any `.jpg` image files in the `/images` folder of your endpoint.</span><span class="sxs-lookup"><span data-stu-id="1956a-137">This custom caching rule sets a cache duration of 30 days on any `.jpg` image files in the `/images` folder of your endpoint.</span></span> <span data-ttu-id="1956a-138">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server.</span><span class="sxs-lookup"><span data-stu-id="1956a-138">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server.</span></span>

    ![Custom caching rules](./media/cdn-caching-rules/cdn-custom-caching-rules.png)

    
## <a name="clean-up-resources"></a><span data-ttu-id="1956a-140">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1956a-140">Clean up resources</span></span>

<span data-ttu-id="1956a-141">In the preceding steps, you created caching rules.</span><span class="sxs-lookup"><span data-stu-id="1956a-141">In the preceding steps, you created caching rules.</span></span> <span data-ttu-id="1956a-142">If you no longer want to use these caching rules, you can remove them by performing these steps:</span><span class="sxs-lookup"><span data-stu-id="1956a-142">If you no longer want to use these caching rules, you can remove them by performing these steps:</span></span>
 
1. <span data-ttu-id="1956a-143">Select a CDN profile, then select the endpoint with the caching rules you want to remove.</span><span class="sxs-lookup"><span data-stu-id="1956a-143">Select a CDN profile, then select the endpoint with the caching rules you want to remove.</span></span>

2. <span data-ttu-id="1956a-144">In the left pane under Settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="1956a-144">In the left pane under Settings, select **Caching rules**.</span></span>

3. <span data-ttu-id="1956a-145">Under **Global caching rules**, set **Caching behavior** to **Not set**.</span><span class="sxs-lookup"><span data-stu-id="1956a-145">Under **Global caching rules**, set **Caching behavior** to **Not set**.</span></span>
 
4. <span data-ttu-id="1956a-146">Under **Custom caching rules**, select the check box next to the rule you want to delete.</span><span class="sxs-lookup"><span data-stu-id="1956a-146">Under **Custom caching rules**, select the check box next to the rule you want to delete.</span></span>

5. <span data-ttu-id="1956a-147">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1956a-147">Select **Delete**.</span></span>

6. <span data-ttu-id="1956a-148">From the top of the page, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1956a-148">From the top of the page, select **Save**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1956a-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="1956a-149">Next steps</span></span>

<span data-ttu-id="1956a-150">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="1956a-150">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="1956a-151">Open the caching rules page.</span><span class="sxs-lookup"><span data-stu-id="1956a-151">Open the caching rules page.</span></span>
> - <span data-ttu-id="1956a-152">Create a global caching rule.</span><span class="sxs-lookup"><span data-stu-id="1956a-152">Create a global caching rule.</span></span>
> - <span data-ttu-id="1956a-153">Create a custom caching rule.</span><span class="sxs-lookup"><span data-stu-id="1956a-153">Create a custom caching rule.</span></span>

<span data-ttu-id="1956a-154">Advance to the next article to learn how to configure additional caching rule settings.</span><span class="sxs-lookup"><span data-stu-id="1956a-154">Advance to the next article to learn how to configure additional caching rule settings.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1956a-155">Control Azure CDN caching behavior with caching rules</span><span class="sxs-lookup"><span data-stu-id="1956a-155">Control Azure CDN caching behavior with caching rules</span></span>](cdn-caching-rules.md)



