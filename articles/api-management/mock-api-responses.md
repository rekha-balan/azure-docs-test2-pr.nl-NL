---
title: Mock API responses with the Azure portal  | Microsoft Docs
description: This tutorial shows you how to use API Management (APIM) to set a policy on an API so it returns a mocked response. This method endables developers to proceed with implementation and testing of the API Management instance in case the backend is not available to send real responses.
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
ms.openlocfilehash: 916d0cf37ab3588091d4ca2d45f43a5669afe4f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968306"
---
# <a name="mock-api-responses"></a><span data-ttu-id="00bc6-104">Mock API responses</span><span class="sxs-lookup"><span data-stu-id="00bc6-104">Mock API responses</span></span>

<span data-ttu-id="00bc6-105">Backend APIs can be imported into an APIM API or created and managed manually.</span><span class="sxs-lookup"><span data-stu-id="00bc6-105">Backend APIs can be imported into an APIM API or created and managed manually.</span></span> <span data-ttu-id="00bc6-106">The steps in this tutorial show you how to use APIM to create a blank API and manage it manually.</span><span class="sxs-lookup"><span data-stu-id="00bc6-106">The steps in this tutorial show you how to use APIM to create a blank API and manage it manually.</span></span> <span data-ttu-id="00bc6-107">The tutorial shows how to set a policy on an API so it returns a mocked response.</span><span class="sxs-lookup"><span data-stu-id="00bc6-107">The tutorial shows how to set a policy on an API so it returns a mocked response.</span></span> <span data-ttu-id="00bc6-108">This method enables developers to proceed with implementation and testing of the APIM instance even if the backend is not available to send real responses.</span><span class="sxs-lookup"><span data-stu-id="00bc6-108">This method enables developers to proceed with implementation and testing of the APIM instance even if the backend is not available to send real responses.</span></span> <span data-ttu-id="00bc6-109">Ability to mock up responses can be useful in a number of scenarios:</span><span class="sxs-lookup"><span data-stu-id="00bc6-109">Ability to mock up responses can be useful in a number of scenarios:</span></span>

+ <span data-ttu-id="00bc6-110">When the API façade is designed first and the backend implementation comes later.</span><span class="sxs-lookup"><span data-stu-id="00bc6-110">When the API façade is designed first and the backend implementation comes later.</span></span> <span data-ttu-id="00bc6-111">Or, the backend is being developed in parallel.</span><span class="sxs-lookup"><span data-stu-id="00bc6-111">Or, the backend is being developed in parallel.</span></span>
+ <span data-ttu-id="00bc6-112">When the backend is temporarily not operational or not able to scale.</span><span class="sxs-lookup"><span data-stu-id="00bc6-112">When the backend is temporarily not operational or not able to scale.</span></span>

<span data-ttu-id="00bc6-113">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="00bc6-113">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00bc6-114">Create a test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-114">Create a test API</span></span> 
> * <span data-ttu-id="00bc6-115">Add an operation to the test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-115">Add an operation to the test API</span></span>
> * <span data-ttu-id="00bc6-116">Enable response mocking</span><span class="sxs-lookup"><span data-stu-id="00bc6-116">Enable response mocking</span></span>
> * <span data-ttu-id="00bc6-117">Test the mocked API</span><span class="sxs-lookup"><span data-stu-id="00bc6-117">Test the mocked API</span></span>

![Mocked operation response](./media/mock-api-responses/mock-api-responses01.png)

## <a name="prerequisites"></a><span data-ttu-id="00bc6-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00bc6-119">Prerequisites</span></span>

<span data-ttu-id="00bc6-120">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="00bc6-120">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

## <a name="create-a-test-api"></a><span data-ttu-id="00bc6-121">Create a test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-121">Create a test API</span></span> 

<span data-ttu-id="00bc6-122">The steps in this section show how to create a blank API with no backend.</span><span class="sxs-lookup"><span data-stu-id="00bc6-122">The steps in this section show how to create a blank API with no backend.</span></span> <span data-ttu-id="00bc6-123">It also shows how to add an operation to the API.</span><span class="sxs-lookup"><span data-stu-id="00bc6-123">It also shows how to add an operation to the API.</span></span> <span data-ttu-id="00bc6-124">Calling the operation after completing steps in this section produces an error.</span><span class="sxs-lookup"><span data-stu-id="00bc6-124">Calling the operation after completing steps in this section produces an error.</span></span> <span data-ttu-id="00bc6-125">You will get no errors after you complete steps in the "Enable response mocking" section.</span><span class="sxs-lookup"><span data-stu-id="00bc6-125">You will get no errors after you complete steps in the "Enable response mocking" section.</span></span>

1. <span data-ttu-id="00bc6-126">Select **APIs** from the **API Management** service.</span><span class="sxs-lookup"><span data-stu-id="00bc6-126">Select **APIs** from the **API Management** service.</span></span>
2. <span data-ttu-id="00bc6-127">From the left menu, select **+ Add API**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-127">From the left menu, select **+ Add API**.</span></span>
3. <span data-ttu-id="00bc6-128">Select **Blank API** from the list.</span><span class="sxs-lookup"><span data-stu-id="00bc6-128">Select **Blank API** from the list.</span></span>
4. <span data-ttu-id="00bc6-129">Enter "*Test API*" for **Display name**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-129">Enter "*Test API*" for **Display name**.</span></span>
5. <span data-ttu-id="00bc6-130">Enter "*Unlimited*" for **Products**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-130">Enter "*Unlimited*" for **Products**.</span></span>
6. <span data-ttu-id="00bc6-131">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-131">Select **Create**.</span></span>

## <a name="add-an-operation-to-the-test-api"></a><span data-ttu-id="00bc6-132">Add an operation to the test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-132">Add an operation to the test API</span></span>

1. <span data-ttu-id="00bc6-133">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="00bc6-133">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="00bc6-134">Click **+ Add Operation**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-134">Click **+ Add Operation**.</span></span>
    <span data-ttu-id="00bc6-135">![Mocked operation response](./media/mock-api-responses/mock-api-responses-add-operation.png)</span><span class="sxs-lookup"><span data-stu-id="00bc6-135">![Mocked operation response](./media/mock-api-responses/mock-api-responses-add-operation.png)</span></span>

    |<span data-ttu-id="00bc6-136">Setting</span><span class="sxs-lookup"><span data-stu-id="00bc6-136">Setting</span></span>|<span data-ttu-id="00bc6-137">Value</span><span class="sxs-lookup"><span data-stu-id="00bc6-137">Value</span></span>|<span data-ttu-id="00bc6-138">Description</span><span class="sxs-lookup"><span data-stu-id="00bc6-138">Description</span></span>|
    |---|---|---|
    |<span data-ttu-id="00bc6-139">**Display name**</span><span class="sxs-lookup"><span data-stu-id="00bc6-139">**Display name**</span></span>|<span data-ttu-id="00bc6-140">*Test call*</span><span class="sxs-lookup"><span data-stu-id="00bc6-140">*Test call*</span></span>|<span data-ttu-id="00bc6-141">The name that is displayed in the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-141">The name that is displayed in the **Developer portal**.</span></span>|
    |<span data-ttu-id="00bc6-142">**URL** (HTTP verb)</span><span class="sxs-lookup"><span data-stu-id="00bc6-142">**URL** (HTTP verb)</span></span>|<span data-ttu-id="00bc6-143">GET</span><span class="sxs-lookup"><span data-stu-id="00bc6-143">GET</span></span>|<span data-ttu-id="00bc6-144">You can choose from one of the predefined HTTP verbs.</span><span class="sxs-lookup"><span data-stu-id="00bc6-144">You can choose from one of the predefined HTTP verbs.</span></span>|
    |<span data-ttu-id="00bc6-145">**URL**</span><span class="sxs-lookup"><span data-stu-id="00bc6-145">**URL**</span></span> |<span data-ttu-id="00bc6-146">*/test*</span><span class="sxs-lookup"><span data-stu-id="00bc6-146">*/test*</span></span>|<span data-ttu-id="00bc6-147">A URL path for the API.</span><span class="sxs-lookup"><span data-stu-id="00bc6-147">A URL path for the API.</span></span> |
    |<span data-ttu-id="00bc6-148">**Description**</span><span class="sxs-lookup"><span data-stu-id="00bc6-148">**Description**</span></span>||<span data-ttu-id="00bc6-149">Provide a description of the operation that is used to provide documentation to the developers using this API in the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-149">Provide a description of the operation that is used to provide documentation to the developers using this API in the **Developer portal**.</span></span>|
    |<span data-ttu-id="00bc6-150">**Query** tab</span><span class="sxs-lookup"><span data-stu-id="00bc6-150">**Query** tab</span></span>||<span data-ttu-id="00bc6-151">You can add query parameters.</span><span class="sxs-lookup"><span data-stu-id="00bc6-151">You can add query parameters.</span></span> <span data-ttu-id="00bc6-152">Besides providing a name and description, you can provide values that can be assigned to this parameter.</span><span class="sxs-lookup"><span data-stu-id="00bc6-152">Besides providing a name and description, you can provide values that can be assigned to this parameter.</span></span> <span data-ttu-id="00bc6-153">One of the values can be marked as default (optional).</span><span class="sxs-lookup"><span data-stu-id="00bc6-153">One of the values can be marked as default (optional).</span></span>|
    |<span data-ttu-id="00bc6-154">**Request** tab</span><span class="sxs-lookup"><span data-stu-id="00bc6-154">**Request** tab</span></span>||<span data-ttu-id="00bc6-155">You can define request content types, examples, and schemas.</span><span class="sxs-lookup"><span data-stu-id="00bc6-155">You can define request content types, examples, and schemas.</span></span> |
    |<span data-ttu-id="00bc6-156">**Response** tab</span><span class="sxs-lookup"><span data-stu-id="00bc6-156">**Response** tab</span></span>|<span data-ttu-id="00bc6-157">See steps that follow this table.</span><span class="sxs-lookup"><span data-stu-id="00bc6-157">See steps that follow this table.</span></span>|<span data-ttu-id="00bc6-158">Define response status codes, content types, examples, and schemas.</span><span class="sxs-lookup"><span data-stu-id="00bc6-158">Define response status codes, content types, examples, and schemas.</span></span>|

3. <span data-ttu-id="00bc6-159">Select the **Response** tab, located under the URL, Display name, and Description fields.</span><span class="sxs-lookup"><span data-stu-id="00bc6-159">Select the **Response** tab, located under the URL, Display name, and Description fields.</span></span>
4. <span data-ttu-id="00bc6-160">Click **+ Add response**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-160">Click **+ Add response**.</span></span>
5. <span data-ttu-id="00bc6-161">Select **200 OK** from the list.</span><span class="sxs-lookup"><span data-stu-id="00bc6-161">Select **200 OK** from the list.</span></span>
6. <span data-ttu-id="00bc6-162">Under the **Representations** heading on the right, select **+ Add representation**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-162">Under the **Representations** heading on the right, select **+ Add representation**.</span></span>
7. <span data-ttu-id="00bc6-163">Enter "*application/json*" into the search box and select the **application/json** content type.</span><span class="sxs-lookup"><span data-stu-id="00bc6-163">Enter "*application/json*" into the search box and select the **application/json** content type.</span></span>
8. <span data-ttu-id="00bc6-164">In the **Sample** text box, enter  `{ 'sampleField' : 'test' }`.</span><span class="sxs-lookup"><span data-stu-id="00bc6-164">In the **Sample** text box, enter  `{ 'sampleField' : 'test' }`.</span></span>
9. <span data-ttu-id="00bc6-165">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-165">Select **Create**.</span></span>

## <a name="enable-response-mocking"></a><span data-ttu-id="00bc6-166">Enable response mocking</span><span class="sxs-lookup"><span data-stu-id="00bc6-166">Enable response mocking</span></span>

1. <span data-ttu-id="00bc6-167">Select the API you created in the "Create a test API" step.</span><span class="sxs-lookup"><span data-stu-id="00bc6-167">Select the API you created in the "Create a test API" step.</span></span>
2. <span data-ttu-id="00bc6-168">Select the test operation that you added.</span><span class="sxs-lookup"><span data-stu-id="00bc6-168">Select the test operation that you added.</span></span>
3. <span data-ttu-id="00bc6-169">In the window on the right, click the **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="00bc6-169">In the window on the right, click the **Design** tab.</span></span>
4. <span data-ttu-id="00bc6-170">In the **Inbound processing** window, click the pencil icon.</span><span class="sxs-lookup"><span data-stu-id="00bc6-170">In the **Inbound processing** window, click the pencil icon.</span></span>
5. <span data-ttu-id="00bc6-171">In the **Mocking** tab, select **Static responses** for **Mocking behavior**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-171">In the **Mocking** tab, select **Static responses** for **Mocking behavior**.</span></span>
6. <span data-ttu-id="00bc6-172">In the **API Management returns the following response:** text box, type **200 OK, application/json**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-172">In the **API Management returns the following response:** text box, type **200 OK, application/json**.</span></span> <span data-ttu-id="00bc6-173">This selection indicates that your API should return the response sample you defined in the previous section.</span><span class="sxs-lookup"><span data-stu-id="00bc6-173">This selection indicates that your API should return the response sample you defined in the previous section.</span></span>
    <span data-ttu-id="00bc6-174">![Enable response mocking](./media/mock-api-responses/mock-api-responses-set-mocking.png)</span><span class="sxs-lookup"><span data-stu-id="00bc6-174">![Enable response mocking](./media/mock-api-responses/mock-api-responses-set-mocking.png)</span></span>
7. <span data-ttu-id="00bc6-175">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="00bc6-175">Click **Save**.</span></span>

## <a name="test-the-mocked-api"></a><span data-ttu-id="00bc6-176">Test the mocked API</span><span class="sxs-lookup"><span data-stu-id="00bc6-176">Test the mocked API</span></span>

1. <span data-ttu-id="00bc6-177">Select the API you created in the "Create a test API" step.</span><span class="sxs-lookup"><span data-stu-id="00bc6-177">Select the API you created in the "Create a test API" step.</span></span>
2. <span data-ttu-id="00bc6-178">Open the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="00bc6-178">Open the **Test** tab.</span></span>
3. <span data-ttu-id="00bc6-179">Ensure the **Test call** API is selected.</span><span class="sxs-lookup"><span data-stu-id="00bc6-179">Ensure the **Test call** API is selected.</span></span>

    > [!TIP]
    > <span data-ttu-id="00bc6-180">A yellow bar with the text **Mocking is enabled** indicates that responses returned from the API Management, sends a mocking policy and not an actual backend response.</span><span class="sxs-lookup"><span data-stu-id="00bc6-180">A yellow bar with the text **Mocking is enabled** indicates that responses returned from the API Management, sends a mocking policy and not an actual backend response.</span></span>

4. <span data-ttu-id="00bc6-181">Select **Send** to make a test call.</span><span class="sxs-lookup"><span data-stu-id="00bc6-181">Select **Send** to make a test call.</span></span>
5. <span data-ttu-id="00bc6-182">The **HTTP response** displays the JSON provided as a sample in the first section of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="00bc6-182">The **HTTP response** displays the JSON provided as a sample in the first section of the tutorial.</span></span>
    <span data-ttu-id="00bc6-183">![Enable response mocking](./media/mock-api-responses/mock-api-responses-test-response.png)</span><span class="sxs-lookup"><span data-stu-id="00bc6-183">![Enable response mocking](./media/mock-api-responses/mock-api-responses-test-response.png)</span></span>

## <a name="video"></a><span data-ttu-id="00bc6-184">Video</span><span class="sxs-lookup"><span data-stu-id="00bc6-184">Video</span></span>

> [!VIDEO https://www.youtube.com/embed/i9PjUAvw7DQ]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="00bc6-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="00bc6-185">Next steps</span></span>
<span data-ttu-id="00bc6-186">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="00bc6-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="00bc6-187">Create a test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-187">Create a test API</span></span>
> * <span data-ttu-id="00bc6-188">Add an operation to the test API</span><span class="sxs-lookup"><span data-stu-id="00bc6-188">Add an operation to the test API</span></span>
> * <span data-ttu-id="00bc6-189">Enable response mocking</span><span class="sxs-lookup"><span data-stu-id="00bc6-189">Enable response mocking</span></span>
> * <span data-ttu-id="00bc6-190">Test the mocked API</span><span class="sxs-lookup"><span data-stu-id="00bc6-190">Test the mocked API</span></span>

<span data-ttu-id="00bc6-191">Advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="00bc6-191">Advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00bc6-192">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="00bc6-192">Transform and protect a published API</span></span>](transform-api.md)
