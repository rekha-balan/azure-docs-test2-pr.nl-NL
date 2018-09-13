---
title: Transform and protect your API with Azure API Management | Microsoft Docs
description: Learn how to protect your API with quotas and throttling (rate-limiting) policies.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: b94f6ad4c7c6f3b5e93cdb890e053a3d1678e161
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965913"
---
# <a name="transform-and-protect-your-api"></a><span data-ttu-id="448c0-103">Transform and protect your API</span><span class="sxs-lookup"><span data-stu-id="448c0-103">Transform and protect your API</span></span> 

<span data-ttu-id="448c0-104">The tutorial shows how to transform your API so it does not reveal a private backend info.</span><span class="sxs-lookup"><span data-stu-id="448c0-104">The tutorial shows how to transform your API so it does not reveal a private backend info.</span></span> <span data-ttu-id="448c0-105">For example, you might want to hide the info about technology stack that is running on the backend.</span><span class="sxs-lookup"><span data-stu-id="448c0-105">For example, you might want to hide the info about technology stack that is running on the backend.</span></span> <span data-ttu-id="448c0-106">You might also want to hide original URLs that appear in the body of API's HTTP response and instead redirect them to the APIM gateway.</span><span class="sxs-lookup"><span data-stu-id="448c0-106">You might also want to hide original URLs that appear in the body of API's HTTP response and instead redirect them to the APIM gateway.</span></span>

<span data-ttu-id="448c0-107">This tutorial also shows you how easy it is to add protection for your backend API by configuring rate limit with Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="448c0-107">This tutorial also shows you how easy it is to add protection for your backend API by configuring rate limit with Azure API Management.</span></span> <span data-ttu-id="448c0-108">For example, you may want to limit a number of calls the API is called so it is not overused by developers.</span><span class="sxs-lookup"><span data-stu-id="448c0-108">For example, you may want to limit a number of calls the API is called so it is not overused by developers.</span></span> <span data-ttu-id="448c0-109">For more information, see [API Management policies](api-management-policies.md)</span><span class="sxs-lookup"><span data-stu-id="448c0-109">For more information, see [API Management policies](api-management-policies.md)</span></span>

<span data-ttu-id="448c0-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="448c0-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="448c0-111">Transform an API to strip response headers</span><span class="sxs-lookup"><span data-stu-id="448c0-111">Transform an API to strip response headers</span></span>
> * <span data-ttu-id="448c0-112">Replace original URLs in the body of the API response with APIM gateway URLs</span><span class="sxs-lookup"><span data-stu-id="448c0-112">Replace original URLs in the body of the API response with APIM gateway URLs</span></span>
> * <span data-ttu-id="448c0-113">Protect an API by adding rate limit policy (throttling)</span><span class="sxs-lookup"><span data-stu-id="448c0-113">Protect an API by adding rate limit policy (throttling)</span></span>
> * <span data-ttu-id="448c0-114">Test the transformations</span><span class="sxs-lookup"><span data-stu-id="448c0-114">Test the transformations</span></span>

![Policies](./media/transform-api/api-management-management-console.png)

## <a name="prerequisites"></a><span data-ttu-id="448c0-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="448c0-116">Prerequisites</span></span>

+ <span data-ttu-id="448c0-117">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="448c0-117">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
+ <span data-ttu-id="448c0-118">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span><span class="sxs-lookup"><span data-stu-id="448c0-118">Also, complete the following tutorial: [Import and publish your first API](import-and-publish.md).</span></span>
 
[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="transform-an-api-to-strip-response-headers"></a><span data-ttu-id="448c0-119">Transform an API to strip response headers</span><span class="sxs-lookup"><span data-stu-id="448c0-119">Transform an API to strip response headers</span></span>

<span data-ttu-id="448c0-120">This section shows how to hide the HTTP headers that you do not want to show to your users.</span><span class="sxs-lookup"><span data-stu-id="448c0-120">This section shows how to hide the HTTP headers that you do not want to show to your users.</span></span> <span data-ttu-id="448c0-121">In this example, the following headers get deleted in the HTTP response:</span><span class="sxs-lookup"><span data-stu-id="448c0-121">In this example, the following headers get deleted in the HTTP response:</span></span>

* <span data-ttu-id="448c0-122">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="448c0-122">**X-Powered-By**</span></span>
* <span data-ttu-id="448c0-123">**X-AspNet-Version**</span><span class="sxs-lookup"><span data-stu-id="448c0-123">**X-AspNet-Version**</span></span>

### <a name="test-the-original-response"></a><span data-ttu-id="448c0-124">Test the original response</span><span class="sxs-lookup"><span data-stu-id="448c0-124">Test the original response</span></span>

<span data-ttu-id="448c0-125">To see the original response:</span><span class="sxs-lookup"><span data-stu-id="448c0-125">To see the original response:</span></span>

1. <span data-ttu-id="448c0-126">In your APIM service instance, select **APIs** (under **API MANAGEMENT**).</span><span class="sxs-lookup"><span data-stu-id="448c0-126">In your APIM service instance, select **APIs** (under **API MANAGEMENT**).</span></span>
2. <span data-ttu-id="448c0-127">Click **Demo Conference API** from your API list.</span><span class="sxs-lookup"><span data-stu-id="448c0-127">Click **Demo Conference API** from your API list.</span></span>
3. <span data-ttu-id="448c0-128">Select the **GetSpeakers** operation.</span><span class="sxs-lookup"><span data-stu-id="448c0-128">Select the **GetSpeakers** operation.</span></span>
4. <span data-ttu-id="448c0-129">Click the **Test** tab, on the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="448c0-129">Click the **Test** tab, on the top of the screen.</span></span>
5. <span data-ttu-id="448c0-130">Press the **Send** button, at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="448c0-130">Press the **Send** button, at the bottom of the screen.</span></span> 

    <span data-ttu-id="448c0-131">As you can see the original response looks like this:</span><span class="sxs-lookup"><span data-stu-id="448c0-131">As you can see the original response looks like this:</span></span>

    ![Policies](./media/transform-api/original-response.png)

### <a name="set-the-transformation-policy"></a><span data-ttu-id="448c0-133">Set the transformation policy</span><span class="sxs-lookup"><span data-stu-id="448c0-133">Set the transformation policy</span></span>

1. <span data-ttu-id="448c0-134">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-134">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-135">On the top of the screen, select **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-135">On the top of the screen, select **Design** tab.</span></span>
3. <span data-ttu-id="448c0-136">Select **All operations**.</span><span class="sxs-lookup"><span data-stu-id="448c0-136">Select **All operations**.</span></span>
4. <span data-ttu-id="448c0-137">In the **Outbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="448c0-137">In the **Outbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span></span>
     <span data-ttu-id="448c0-138">![Edit policy](./media/set-edit-policies/set-edit-policies01.png)</span><span class="sxs-lookup"><span data-stu-id="448c0-138">![Edit policy](./media/set-edit-policies/set-edit-policies01.png)</span></span>
5. <span data-ttu-id="448c0-139">Position the cursor inside the **&lt;outbound&gt;** element.</span><span class="sxs-lookup"><span data-stu-id="448c0-139">Position the cursor inside the **&lt;outbound&gt;** element.</span></span>
6. <span data-ttu-id="448c0-140">In the right window, under **Transformation policies**, click **+ Set HTTP header** twice (to insert two policy snippets).</span><span class="sxs-lookup"><span data-stu-id="448c0-140">In the right window, under **Transformation policies**, click **+ Set HTTP header** twice (to insert two policy snippets).</span></span>

    ![Policies](./media/transform-api/transform-api.png)
7. <span data-ttu-id="448c0-142">Modify your **<outbound>** code to look like this:</span><span class="sxs-lookup"><span data-stu-id="448c0-142">Modify your **<outbound>** code to look like this:</span></span>

        <set-header name="X-Powered-By" exists-action="delete" />
        <set-header name="X-AspNet-Version" exists-action="delete" />

    ![Policies](./media/transform-api/set-policy.png)
8. <span data-ttu-id="448c0-144">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="448c0-144">Click the **Save** button.</span></span>


## <a name="replace-original-urls-in-the-body-of-the-api-response-with-apim-gateway-urls"></a><span data-ttu-id="448c0-145">Replace original URLs in the body of the API response with APIM gateway URLs</span><span class="sxs-lookup"><span data-stu-id="448c0-145">Replace original URLs in the body of the API response with APIM gateway URLs</span></span>

<span data-ttu-id="448c0-146">This section shows how to hide original URLs that appear in the body of API's HTTP response and instead redirect them to the APIM gateway.</span><span class="sxs-lookup"><span data-stu-id="448c0-146">This section shows how to hide original URLs that appear in the body of API's HTTP response and instead redirect them to the APIM gateway.</span></span>

### <a name="test-the-original-response"></a><span data-ttu-id="448c0-147">Test the original response</span><span class="sxs-lookup"><span data-stu-id="448c0-147">Test the original response</span></span>

<span data-ttu-id="448c0-148">To see the original response:</span><span class="sxs-lookup"><span data-stu-id="448c0-148">To see the original response:</span></span>

1. <span data-ttu-id="448c0-149">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-149">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-150">Select the **GetSpeakers** operation.</span><span class="sxs-lookup"><span data-stu-id="448c0-150">Select the **GetSpeakers** operation.</span></span>
3. <span data-ttu-id="448c0-151">Click the **Test** tab, on the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="448c0-151">Click the **Test** tab, on the top of the screen.</span></span>
4. <span data-ttu-id="448c0-152">Press the **Send** button, at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="448c0-152">Press the **Send** button, at the bottom of the screen.</span></span> 

    <span data-ttu-id="448c0-153">As you can see the original response looks like this:</span><span class="sxs-lookup"><span data-stu-id="448c0-153">As you can see the original response looks like this:</span></span>

    ![Policies](./media/transform-api/original-response2.png)

### <a name="set-the-transformation-policy"></a><span data-ttu-id="448c0-155">Set the transformation policy</span><span class="sxs-lookup"><span data-stu-id="448c0-155">Set the transformation policy</span></span>

1. <span data-ttu-id="448c0-156">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-156">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-157">Select **All operations**.</span><span class="sxs-lookup"><span data-stu-id="448c0-157">Select **All operations**.</span></span>
3. <span data-ttu-id="448c0-158">On the top of the screen, select **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-158">On the top of the screen, select **Design** tab.</span></span>
4. <span data-ttu-id="448c0-159">In the **Outbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="448c0-159">In the **Outbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span></span>
5. <span data-ttu-id="448c0-160">Position the cursor inside the **&lt;outbound&gt;** element.</span><span class="sxs-lookup"><span data-stu-id="448c0-160">Position the cursor inside the **&lt;outbound&gt;** element.</span></span>
6. <span data-ttu-id="448c0-161">In the right window, under **Transformation policies**, click **+ Find and replace string in body**.</span><span class="sxs-lookup"><span data-stu-id="448c0-161">In the right window, under **Transformation policies**, click **+ Find and replace string in body**.</span></span>
7. <span data-ttu-id="448c0-162">Modify your **find-and-replace** code (in the **\<outbound\>** element) to replace the URL to match your APIM gateway.</span><span class="sxs-lookup"><span data-stu-id="448c0-162">Modify your **find-and-replace** code (in the **\<outbound\>** element) to replace the URL to match your APIM gateway.</span></span> <span data-ttu-id="448c0-163">For example:</span><span class="sxs-lookup"><span data-stu-id="448c0-163">For example:</span></span>

        <find-and-replace from="://conferenceapi.azurewebsites.net" to="://apiphany.azure-api.net/conference"/>

## <a name="protect-an-api-by-adding-rate-limit-policy-throttling"></a><span data-ttu-id="448c0-164">Protect an API by adding rate limit policy (throttling)</span><span class="sxs-lookup"><span data-stu-id="448c0-164">Protect an API by adding rate limit policy (throttling)</span></span>

<span data-ttu-id="448c0-165">This section shows how to add protection for your backend API by configuring rate limits.</span><span class="sxs-lookup"><span data-stu-id="448c0-165">This section shows how to add protection for your backend API by configuring rate limits.</span></span> <span data-ttu-id="448c0-166">For example, you may want to limit a number of calls the API is called so it is not overused by developers.</span><span class="sxs-lookup"><span data-stu-id="448c0-166">For example, you may want to limit a number of calls the API is called so it is not overused by developers.</span></span> <span data-ttu-id="448c0-167">In this example, the limit is set to 3 calls per 15 seconds for each subscription Id. After 15 seconds, a developer can retry calling the API.</span><span class="sxs-lookup"><span data-stu-id="448c0-167">In this example, the limit is set to 3 calls per 15 seconds for each subscription Id. After 15 seconds, a developer can retry calling the API.</span></span>

1. <span data-ttu-id="448c0-168">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-168">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-169">Select **All operations**.</span><span class="sxs-lookup"><span data-stu-id="448c0-169">Select **All operations**.</span></span>
3. <span data-ttu-id="448c0-170">On the top of the screen, select **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-170">On the top of the screen, select **Design** tab.</span></span>
4. <span data-ttu-id="448c0-171">In the **Inbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="448c0-171">In the **Inbound processing** window, click the triangle (next to the pencil) and select **Code editor**.</span></span>
5. <span data-ttu-id="448c0-172">Position the cursor inside the **&lt;inbound&gt;** element.</span><span class="sxs-lookup"><span data-stu-id="448c0-172">Position the cursor inside the **&lt;inbound&gt;** element.</span></span>
6. <span data-ttu-id="448c0-173">In the right window, under **Access restriction policies**, click **+ Limit call rate per key**.</span><span class="sxs-lookup"><span data-stu-id="448c0-173">In the right window, under **Access restriction policies**, click **+ Limit call rate per key**.</span></span>
7. <span data-ttu-id="448c0-174">Modify your **rate-limit-by-key** code (in the **\<inbound\>** element) to the following code:</span><span class="sxs-lookup"><span data-stu-id="448c0-174">Modify your **rate-limit-by-key** code (in the **\<inbound\>** element) to the following code:</span></span>

        <rate-limit-by-key calls="3" renewal-period="15" counter-key="@(context.Subscription.Id)" />

## <a name="test-the-transformations"></a><span data-ttu-id="448c0-175">Test the transformations</span><span class="sxs-lookup"><span data-stu-id="448c0-175">Test the transformations</span></span>
        
<span data-ttu-id="448c0-176">At this point if you look at the code in the code editor, your policies look like this:</span><span class="sxs-lookup"><span data-stu-id="448c0-176">At this point if you look at the code in the code editor, your policies look like this:</span></span>

    <policies>
        <inbound>
            <rate-limit-by-key calls="3" renewal-period="15" counter-key="@(context.Subscription.Id)" />
            <base />
        </inbound>
        <backend>
            <base />
        </backend>
        <outbound>
            <set-header name="X-Powered-By" exists-action="delete" />
            <set-header name="X-AspNet-Version" exists-action="delete" />
            <find-and-replace from="://conferenceapi.azurewebsites.net" to="://apiphany.azure-api.net/conference"/>
            <base />
        </outbound>
        <on-error>
            <base />
        </on-error>
    </policies>

<span data-ttu-id="448c0-177">The rest of this section tests policy transformations that you set in this article.</span><span class="sxs-lookup"><span data-stu-id="448c0-177">The rest of this section tests policy transformations that you set in this article.</span></span>

### <a name="test-the-stripped-response-headers"></a><span data-ttu-id="448c0-178">Test the stripped response headers</span><span class="sxs-lookup"><span data-stu-id="448c0-178">Test the stripped response headers</span></span>

1. <span data-ttu-id="448c0-179">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-179">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-180">Click the **GetSpeakers** operation.</span><span class="sxs-lookup"><span data-stu-id="448c0-180">Click the **GetSpeakers** operation.</span></span>
3. <span data-ttu-id="448c0-181">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-181">Select the **Test** tab.</span></span>
4. <span data-ttu-id="448c0-182">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="448c0-182">Press **Send**.</span></span>

    <span data-ttu-id="448c0-183">As you can see the headers have been stripped:</span><span class="sxs-lookup"><span data-stu-id="448c0-183">As you can see the headers have been stripped:</span></span>

    ![Policies](./media/transform-api/final-response1.png)

### <a name="test-the-replaced-url"></a><span data-ttu-id="448c0-185">Test the replaced URL</span><span class="sxs-lookup"><span data-stu-id="448c0-185">Test the replaced URL</span></span>

1. <span data-ttu-id="448c0-186">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-186">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-187">Click the **GetSpeakers** operation.</span><span class="sxs-lookup"><span data-stu-id="448c0-187">Click the **GetSpeakers** operation.</span></span>
3. <span data-ttu-id="448c0-188">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-188">Select the **Test** tab.</span></span>
4. <span data-ttu-id="448c0-189">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="448c0-189">Press **Send**.</span></span>

    <span data-ttu-id="448c0-190">As you can see the URL has been replaced.</span><span class="sxs-lookup"><span data-stu-id="448c0-190">As you can see the URL has been replaced.</span></span>

    ![Policies](./media/transform-api/final-response2.png)

### <a name="test-the-rate-limit-throttling"></a><span data-ttu-id="448c0-192">Test the rate limit (throttling)</span><span class="sxs-lookup"><span data-stu-id="448c0-192">Test the rate limit (throttling)</span></span>

1. <span data-ttu-id="448c0-193">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="448c0-193">Select **Demo Conference API**.</span></span>
2. <span data-ttu-id="448c0-194">Click the **GetSpeakers** operation.</span><span class="sxs-lookup"><span data-stu-id="448c0-194">Click the **GetSpeakers** operation.</span></span>
3. <span data-ttu-id="448c0-195">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="448c0-195">Select the **Test** tab.</span></span>
4. <span data-ttu-id="448c0-196">Press **Send** three times in a row.</span><span class="sxs-lookup"><span data-stu-id="448c0-196">Press **Send** three times in a row.</span></span>

    <span data-ttu-id="448c0-197">After sending the request 3 times, you get **429 Too many requests** response.</span><span class="sxs-lookup"><span data-stu-id="448c0-197">After sending the request 3 times, you get **429 Too many requests** response.</span></span>
5. <span data-ttu-id="448c0-198">Wait 15 seconds or so and press **Send** again.</span><span class="sxs-lookup"><span data-stu-id="448c0-198">Wait 15 seconds or so and press **Send** again.</span></span> <span data-ttu-id="448c0-199">This time you should get a **200 OK** response.</span><span class="sxs-lookup"><span data-stu-id="448c0-199">This time you should get a **200 OK** response.</span></span>

    ![Throttling](./media/transform-api/test-throttling.png)

## <a name="video"></a><span data-ttu-id="448c0-201">Video</span><span class="sxs-lookup"><span data-stu-id="448c0-201">Video</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="448c0-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="448c0-202">Next steps</span></span>

<span data-ttu-id="448c0-203">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="448c0-203">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="448c0-204">Transform an API to strip response headers</span><span class="sxs-lookup"><span data-stu-id="448c0-204">Transform an API to strip response headers</span></span>
> * <span data-ttu-id="448c0-205">Replace original URLs in the body of the API response with APIM gateway URLs</span><span class="sxs-lookup"><span data-stu-id="448c0-205">Replace original URLs in the body of the API response with APIM gateway URLs</span></span>
> * <span data-ttu-id="448c0-206">Protect an API by adding rate limit policy (throttling)</span><span class="sxs-lookup"><span data-stu-id="448c0-206">Protect an API by adding rate limit policy (throttling)</span></span>
> * <span data-ttu-id="448c0-207">Test the transformations</span><span class="sxs-lookup"><span data-stu-id="448c0-207">Test the transformations</span></span>

<span data-ttu-id="448c0-208">Advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="448c0-208">Advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="448c0-209">Monitor your API</span><span class="sxs-lookup"><span data-stu-id="448c0-209">Monitor your API</span></span>](api-management-howto-use-azure-monitor.md)
