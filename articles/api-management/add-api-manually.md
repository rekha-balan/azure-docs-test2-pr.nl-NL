---
title: Add an API manually using the Azure portal  | Microsoft Docs
description: This tutorial shows you how to use API Management (APIM) to add an API manually.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/27/2018
ms.author: apimpm
ms.openlocfilehash: 35b4777c7de4db1f8514b24e7b1e4d11775d0ca0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857906"
---
# <a name="add-an-api-manually"></a><span data-ttu-id="9cb3a-103">Add an API manually</span><span class="sxs-lookup"><span data-stu-id="9cb3a-103">Add an API manually</span></span>

<span data-ttu-id="9cb3a-104">The steps in this article show how to use the Azure portal to add an API manually to the API Management (APIM) instance.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-104">The steps in this article show how to use the Azure portal to add an API manually to the API Management (APIM) instance.</span></span> <span data-ttu-id="9cb3a-105">A common scenario when you would want to create a blank API and define it manually is when you want to mock the API.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-105">A common scenario when you would want to create a blank API and define it manually is when you want to mock the API.</span></span> <span data-ttu-id="9cb3a-106">For details about mocking an API, see [Mock API responses](mock-api-responses.md).</span><span class="sxs-lookup"><span data-stu-id="9cb3a-106">For details about mocking an API, see [Mock API responses](mock-api-responses.md).</span></span>

<span data-ttu-id="9cb3a-107">If you want to import an existing API, see [related topics](#related-topics) section.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-107">If you want to import an existing API, see [related topics](#related-topics) section.</span></span>

<span data-ttu-id="9cb3a-108">In this article, we create a blank API and specify [httpbin.org](http://httpbin.org) (a public testing service) as a back-end API.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-108">In this article, we create a blank API and specify [httpbin.org](http://httpbin.org) (a public testing service) as a back-end API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cb3a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9cb3a-109">Prerequisites</span></span>

<span data-ttu-id="9cb3a-110">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span><span class="sxs-lookup"><span data-stu-id="9cb3a-110">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="create-an-api"></a><span data-ttu-id="9cb3a-111">Create an API</span><span class="sxs-lookup"><span data-stu-id="9cb3a-111">Create an API</span></span>

1. <span data-ttu-id="9cb3a-112">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-112">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="9cb3a-113">From the left menu, select **+ Add API**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-113">From the left menu, select **+ Add API**.</span></span>
3. <span data-ttu-id="9cb3a-114">Select **Blank API** from the list.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-114">Select **Blank API** from the list.</span></span>

    ![Blank API](media/add-api-manually/blank-api.png)
4. <span data-ttu-id="9cb3a-116">Enter settings for the API.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-116">Enter settings for the API.</span></span>

    ![Settings](media/add-api-manually/settings.png)

    |<span data-ttu-id="9cb3a-118">**Name**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-118">**Name**</span></span>|<span data-ttu-id="9cb3a-119">**Value**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-119">**Value**</span></span>|<span data-ttu-id="9cb3a-120">**Description**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-120">**Description**</span></span>|
    |---|---|---|
    |<span data-ttu-id="9cb3a-121">**Display name**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-121">**Display name**</span></span>|<span data-ttu-id="9cb3a-122">"*Blank API*"</span><span class="sxs-lookup"><span data-stu-id="9cb3a-122">"*Blank API*"</span></span> |<span data-ttu-id="9cb3a-123">This name is displayed in the Developer portal.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-123">This name is displayed in the Developer portal.</span></span>|
    |<span data-ttu-id="9cb3a-124">**Web Service URL** (optional)</span><span class="sxs-lookup"><span data-stu-id="9cb3a-124">**Web Service URL** (optional)</span></span>| <span data-ttu-id="9cb3a-125">"*http://httpbin.org*"</span><span class="sxs-lookup"><span data-stu-id="9cb3a-125">"*http://httpbin.org*"</span></span>| <span data-ttu-id="9cb3a-126">If you want to mock an API, you might not enter anything.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-126">If you want to mock an API, you might not enter anything.</span></span> <br/><span data-ttu-id="9cb3a-127">In this case, we enter [http://httpbin.org](http://httpbin.org). This is a public testing service.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-127">In this case, we enter [http://httpbin.org](http://httpbin.org). This is a public testing service.</span></span> <br/><span data-ttu-id="9cb3a-128">If you want to import an API that is mapped to a back end automatically, see one of the topics in the [related topics](#related-topics) section.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-128">If you want to import an API that is mapped to a back end automatically, see one of the topics in the [related topics](#related-topics) section.</span></span>|
    |<span data-ttu-id="9cb3a-129">**URL scheme**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-129">**URL scheme**</span></span>|<span data-ttu-id="9cb3a-130">"*HTTPS*"</span><span class="sxs-lookup"><span data-stu-id="9cb3a-130">"*HTTPS*"</span></span>|<span data-ttu-id="9cb3a-131">In this case, even though the back end has non-secure HTTP access, we specify a secure HTTPS APIM access to the back end.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-131">In this case, even though the back end has non-secure HTTP access, we specify a secure HTTPS APIM access to the back end.</span></span> <br/><span data-ttu-id="9cb3a-132">This kind of scenario (HTTPS to HTTP) is called HTTPS termination.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-132">This kind of scenario (HTTPS to HTTP) is called HTTPS termination.</span></span> <span data-ttu-id="9cb3a-133">You might do it if your API exists within a virtual network (where you know the access is secure even if HTTPS is not used).</span><span class="sxs-lookup"><span data-stu-id="9cb3a-133">You might do it if your API exists within a virtual network (where you know the access is secure even if HTTPS is not used).</span></span> <br/><span data-ttu-id="9cb3a-134">You might want to use "HTTPS termination" to save on some CPU cycles.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-134">You might want to use "HTTPS termination" to save on some CPU cycles.</span></span>|
    |<span data-ttu-id="9cb3a-135">**URL suffix**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-135">**URL suffix**</span></span>|<span data-ttu-id="9cb3a-136">"*hbin*"</span><span class="sxs-lookup"><span data-stu-id="9cb3a-136">"*hbin*"</span></span>| <span data-ttu-id="9cb3a-137">The suffix is a name that identifies this specific API in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-137">The suffix is a name that identifies this specific API in this APIM instance.</span></span> <span data-ttu-id="9cb3a-138">It has to be unique in this APIM instance.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-138">It has to be unique in this APIM instance.</span></span>|
    |<span data-ttu-id="9cb3a-139">**Products**</span><span class="sxs-lookup"><span data-stu-id="9cb3a-139">**Products**</span></span>|<span data-ttu-id="9cb3a-140">"*Unlimited*"</span><span class="sxs-lookup"><span data-stu-id="9cb3a-140">"*Unlimited*"</span></span> |<span data-ttu-id="9cb3a-141">Publish the API by associating the API with a product.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-141">Publish the API by associating the API with a product.</span></span> <span data-ttu-id="9cb3a-142">If you want for the API to be published and be available to developers, add it to a product.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-142">If you want for the API to be published and be available to developers, add it to a product.</span></span> <span data-ttu-id="9cb3a-143">You can do it during API creation or set it later.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-143">You can do it during API creation or set it later.</span></span><br/><br/><span data-ttu-id="9cb3a-144">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-144">Products are associations of one or more APIs.</span></span> <span data-ttu-id="9cb3a-145">You can include a number of APIs and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-145">You can include a number of APIs and offer them to developers through the developer portal.</span></span> <br/><span data-ttu-id="9cb3a-146">Developers must first subscribe to a product to get access to the API.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-146">Developers must first subscribe to a product to get access to the API.</span></span> <span data-ttu-id="9cb3a-147">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-147">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <span data-ttu-id="9cb3a-148">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-148">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span></span><br/><br/> <span data-ttu-id="9cb3a-149">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-149">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span></span>| 
5. <span data-ttu-id="9cb3a-150">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-150">Select **Create**.</span></span>

<span data-ttu-id="9cb3a-151">At this point, you have no operations in APIM that map to the operations in your back-end API.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-151">At this point, you have no operations in APIM that map to the operations in your back-end API.</span></span> <span data-ttu-id="9cb3a-152">If you call an operation that is exposed through the back end but not through the APIM, you get a **404**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-152">If you call an operation that is exposed through the back end but not through the APIM, you get a **404**.</span></span>

>[!NOTE] 
> <span data-ttu-id="9cb3a-153">By default, when you add an API, even if it is connected to some back-end service, APIM will not expose any operations until you whitelist them.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-153">By default, when you add an API, even if it is connected to some back-end service, APIM will not expose any operations until you whitelist them.</span></span> <span data-ttu-id="9cb3a-154">To whitelist an operation of your back-end service, create an APIM operation that maps to the back-end operation.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-154">To whitelist an operation of your back-end service, create an APIM operation that maps to the back-end operation.</span></span>

## <a name="add-and-test-an-operation"></a><span data-ttu-id="9cb3a-155">Add and test an operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-155">Add and test an operation</span></span>

<span data-ttu-id="9cb3a-156">This section shows how to add a "/get" operation in order to map it to the back end "http://httpbin.org/get" operation.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-156">This section shows how to add a "/get" operation in order to map it to the back end "http://httpbin.org/get" operation.</span></span>

### <a name="add-an-operation"></a><span data-ttu-id="9cb3a-157">Add an operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-157">Add an operation</span></span>

1. <span data-ttu-id="9cb3a-158">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-158">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="9cb3a-159">Click **+ Add Operation**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-159">Click **+ Add Operation**.</span></span>
3. <span data-ttu-id="9cb3a-160">In the **URL**, select **GET** and enter "*/get*" in the resource.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-160">In the **URL**, select **GET** and enter "*/get*" in the resource.</span></span>
4. <span data-ttu-id="9cb3a-161">Enter "*FetchData*" for **Display name**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-161">Enter "*FetchData*" for **Display name**.</span></span>
5. <span data-ttu-id="9cb3a-162">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-162">Select **Save**.</span></span>

### <a name="test-an-operation"></a><span data-ttu-id="9cb3a-163">Test an operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-163">Test an operation</span></span>

<span data-ttu-id="9cb3a-164">Test the operation in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-164">Test the operation in the Azure portal.</span></span> <span data-ttu-id="9cb3a-165">Alternatively, you can test it in the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-165">Alternatively, you can test it in the **Developer portal**.</span></span>

1. <span data-ttu-id="9cb3a-166">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-166">Select the **Test** tab.</span></span>
2. <span data-ttu-id="9cb3a-167">Select **FetchData**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-167">Select **FetchData**.</span></span>
3. <span data-ttu-id="9cb3a-168">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-168">Press **Send**.</span></span>

<span data-ttu-id="9cb3a-169">The response that the "http://httpbin.org/get" operation generates appears.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-169">The response that the "http://httpbin.org/get" operation generates appears.</span></span> <span data-ttu-id="9cb3a-170">If you want to transform your operations, see [Transform and protect your API](transform-api.md).</span><span class="sxs-lookup"><span data-stu-id="9cb3a-170">If you want to transform your operations, see [Transform and protect your API](transform-api.md).</span></span>

## <a name="add-and-test-a-parameterized-operation"></a><span data-ttu-id="9cb3a-171">Add and test a parameterized operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-171">Add and test a parameterized operation</span></span>

<span data-ttu-id="9cb3a-172">This section shows how to add an operation that takes a parameter.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-172">This section shows how to add an operation that takes a parameter.</span></span> <span data-ttu-id="9cb3a-173">In this case, we map the operation to "http://httpbin.org/status/200".</span><span class="sxs-lookup"><span data-stu-id="9cb3a-173">In this case, we map the operation to "http://httpbin.org/status/200".</span></span>

### <a name="add-the-operation"></a><span data-ttu-id="9cb3a-174">Add the operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-174">Add the operation</span></span>

1. <span data-ttu-id="9cb3a-175">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-175">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="9cb3a-176">Click **+ Add Operation**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-176">Click **+ Add Operation**.</span></span>
3. <span data-ttu-id="9cb3a-177">In the **URL**, select **GET** and enter "*/status/{code}*" in the resource.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-177">In the **URL**, select **GET** and enter "*/status/{code}*" in the resource.</span></span> <span data-ttu-id="9cb3a-178">Optionally, you can provide some information associated with this parameter.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-178">Optionally, you can provide some information associated with this parameter.</span></span> <span data-ttu-id="9cb3a-179">For example, enter "*Number*" for **TYPE**, "*200*" (default) for **VALUES**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-179">For example, enter "*Number*" for **TYPE**, "*200*" (default) for **VALUES**.</span></span>
4. <span data-ttu-id="9cb3a-180">Enter "GetStatus" for **Display name**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-180">Enter "GetStatus" for **Display name**.</span></span>
5. <span data-ttu-id="9cb3a-181">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-181">Select **Save**.</span></span>

### <a name="test-the-operation"></a><span data-ttu-id="9cb3a-182">Test the operation</span><span class="sxs-lookup"><span data-stu-id="9cb3a-182">Test the operation</span></span> 

<span data-ttu-id="9cb3a-183">Test the operation in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-183">Test the operation in the Azure portal.</span></span>  <span data-ttu-id="9cb3a-184">Alternatively, you can test it in the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-184">Alternatively, you can test it in the **Developer portal**.</span></span>

1. <span data-ttu-id="9cb3a-185">Select the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-185">Select the **Test** tab.</span></span>
2. <span data-ttu-id="9cb3a-186">Select **GetStatus**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-186">Select **GetStatus**.</span></span> <span data-ttu-id="9cb3a-187">By default the code value is set to "*200*".</span><span class="sxs-lookup"><span data-stu-id="9cb3a-187">By default the code value is set to "*200*".</span></span> <span data-ttu-id="9cb3a-188">You can change it to test other values.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-188">You can change it to test other values.</span></span> <span data-ttu-id="9cb3a-189">For example, type "*418*".</span><span class="sxs-lookup"><span data-stu-id="9cb3a-189">For example, type "*418*".</span></span>
3. <span data-ttu-id="9cb3a-190">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-190">Press **Send**.</span></span>

    <span data-ttu-id="9cb3a-191">The response that the "http://httpbin.org/status/200" operation generates appears.</span><span class="sxs-lookup"><span data-stu-id="9cb3a-191">The response that the "http://httpbin.org/status/200" operation generates appears.</span></span> <span data-ttu-id="9cb3a-192">If you want to transform your operations, see [Transform and protect your API](transform-api.md).</span><span class="sxs-lookup"><span data-stu-id="9cb3a-192">If you want to transform your operations, see [Transform and protect your API](transform-api.md).</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="9cb3a-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="9cb3a-193">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9cb3a-194">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="9cb3a-194">Transform and protect a published API</span></span>](transform-api.md)
