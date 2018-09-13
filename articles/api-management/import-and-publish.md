---
title: Import and publish your first API in Azure API Management | Microsoft Docs
description: Learn how to import and publish your first API with API Management.
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
ms.openlocfilehash: 538977b9057a5699d61d6c2cc44209367e3550e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871068"
---
# <a name="import-and-publish-your-first-api"></a><span data-ttu-id="c04ae-103">Import and publish your first API</span><span class="sxs-lookup"><span data-stu-id="c04ae-103">Import and publish your first API</span></span> 

<span data-ttu-id="c04ae-104">This tutorial shows how to import an "OpenAPI specification" backend API residing at http://conferenceapi.azurewebsites.net?format=json.</span><span class="sxs-lookup"><span data-stu-id="c04ae-104">This tutorial shows how to import an "OpenAPI specification" backend API residing at http://conferenceapi.azurewebsites.net?format=json.</span></span> <span data-ttu-id="c04ae-105">This backend API is provided by Microsoft and hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="c04ae-105">This backend API is provided by Microsoft and hosted on Azure.</span></span> 

<span data-ttu-id="c04ae-106">Once the backend API is imported into API Management (APIM), the APIM API becomes a facade for the backend API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-106">Once the backend API is imported into API Management (APIM), the APIM API becomes a facade for the backend API.</span></span> <span data-ttu-id="c04ae-107">At the time you import the backend API, both the source API and the APIM API are identical.</span><span class="sxs-lookup"><span data-stu-id="c04ae-107">At the time you import the backend API, both the source API and the APIM API are identical.</span></span> <span data-ttu-id="c04ae-108">APIM enables you to customize the facade according to your needs without touching the backend API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-108">APIM enables you to customize the facade according to your needs without touching the backend API.</span></span> <span data-ttu-id="c04ae-109">For more information, see [Transform and protect your API](transform-api.md).</span><span class="sxs-lookup"><span data-stu-id="c04ae-109">For more information, see [Transform and protect your API](transform-api.md).</span></span> 

<span data-ttu-id="c04ae-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="c04ae-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c04ae-111">Import your first API</span><span class="sxs-lookup"><span data-stu-id="c04ae-111">Import your first API</span></span>
> * <span data-ttu-id="c04ae-112">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-112">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="c04ae-113">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-113">Test the API in the Developer portal</span></span>

![New API](./media/api-management-get-started/created-api.png)

## <a name="prerequisites"></a><span data-ttu-id="c04ae-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c04ae-115">Prerequisites</span></span>

<span data-ttu-id="c04ae-116">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="c04ae-116">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="c04ae-117"><a name="create-api"> </a>Import and publish a backend API</span><span class="sxs-lookup"><span data-stu-id="c04ae-117"><a name="create-api"> </a>Import and publish a backend API</span></span>

<span data-ttu-id="c04ae-118">This section shows how to import and publish an OpenAPI specification backend API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-118">This section shows how to import and publish an OpenAPI specification backend API.</span></span>
 
1. <span data-ttu-id="c04ae-119">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-119">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="c04ae-120">Select **OpenAPI specification** from the list.</span><span class="sxs-lookup"><span data-stu-id="c04ae-120">Select **OpenAPI specification** from the list.</span></span>

    ![Create an API](./media/api-management-get-started/create-api.png)

    <span data-ttu-id="c04ae-122">You can set the API values during creation or later by going to the **Settings** tab. The red star next to a field indicates that the field is required.</span><span class="sxs-lookup"><span data-stu-id="c04ae-122">You can set the API values during creation or later by going to the **Settings** tab. The red star next to a field indicates that the field is required.</span></span>

    <span data-ttu-id="c04ae-123">Use the values from the table below to create your first API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-123">Use the values from the table below to create your first API.</span></span>

    |<span data-ttu-id="c04ae-124">Setting</span><span class="sxs-lookup"><span data-stu-id="c04ae-124">Setting</span></span>|<span data-ttu-id="c04ae-125">Value</span><span class="sxs-lookup"><span data-stu-id="c04ae-125">Value</span></span>|<span data-ttu-id="c04ae-126">Description</span><span class="sxs-lookup"><span data-stu-id="c04ae-126">Description</span></span>|
    |---|---|---|
    |<span data-ttu-id="c04ae-127">**OpenAPI Specification**</span><span class="sxs-lookup"><span data-stu-id="c04ae-127">**OpenAPI Specification**</span></span>|http://conferenceapi.azurewebsites.net?format=json|<span data-ttu-id="c04ae-128">References the service implementing the API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-128">References the service implementing the API.</span></span> <span data-ttu-id="c04ae-129">API management forwards requests to this address.</span><span class="sxs-lookup"><span data-stu-id="c04ae-129">API management forwards requests to this address.</span></span>|
    |<span data-ttu-id="c04ae-130">**Display name**</span><span class="sxs-lookup"><span data-stu-id="c04ae-130">**Display name**</span></span>|<span data-ttu-id="c04ae-131">*Demo Conference API*</span><span class="sxs-lookup"><span data-stu-id="c04ae-131">*Demo Conference API*</span></span>|<span data-ttu-id="c04ae-132">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="c04ae-132">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span> <br/><span data-ttu-id="c04ae-133">This name is displayed in the Developer portal.</span><span class="sxs-lookup"><span data-stu-id="c04ae-133">This name is displayed in the Developer portal.</span></span>|
    |<span data-ttu-id="c04ae-134">**Name**</span><span class="sxs-lookup"><span data-stu-id="c04ae-134">**Name**</span></span>|<span data-ttu-id="c04ae-135">*demo-conference-api*</span><span class="sxs-lookup"><span data-stu-id="c04ae-135">*demo-conference-api*</span></span>|<span data-ttu-id="c04ae-136">Provides a unique name for the API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-136">Provides a unique name for the API.</span></span> <br/><span data-ttu-id="c04ae-137">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="c04ae-137">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span>|
    |<span data-ttu-id="c04ae-138">**Description**</span><span class="sxs-lookup"><span data-stu-id="c04ae-138">**Description**</span></span>|<span data-ttu-id="c04ae-139">Provide an optional description of the API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-139">Provide an optional description of the API.</span></span>|<span data-ttu-id="c04ae-140">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="c04ae-140">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span>|
    |<span data-ttu-id="c04ae-141">**URL scheme**</span><span class="sxs-lookup"><span data-stu-id="c04ae-141">**URL scheme**</span></span>|<span data-ttu-id="c04ae-142">*HTTPS*</span><span class="sxs-lookup"><span data-stu-id="c04ae-142">*HTTPS*</span></span>|<span data-ttu-id="c04ae-143">Determines which protocols can be used to access the API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-143">Determines which protocols can be used to access the API.</span></span> |
    |<span data-ttu-id="c04ae-144">**API URL suffix**</span><span class="sxs-lookup"><span data-stu-id="c04ae-144">**API URL suffix**</span></span>|<span data-ttu-id="c04ae-145">*conference*</span><span class="sxs-lookup"><span data-stu-id="c04ae-145">*conference*</span></span>|<span data-ttu-id="c04ae-146">The suffix is appended to the base URL for the API management service.</span><span class="sxs-lookup"><span data-stu-id="c04ae-146">The suffix is appended to the base URL for the API management service.</span></span> <span data-ttu-id="c04ae-147">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span><span class="sxs-lookup"><span data-stu-id="c04ae-147">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>|
    |<span data-ttu-id="c04ae-148">**Products**</span><span class="sxs-lookup"><span data-stu-id="c04ae-148">**Products**</span></span>|<span data-ttu-id="c04ae-149">*Unlimited*</span><span class="sxs-lookup"><span data-stu-id="c04ae-149">*Unlimited*</span></span>|<span data-ttu-id="c04ae-150">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="c04ae-150">Products are associations of one or more APIs.</span></span> <span data-ttu-id="c04ae-151">You can include a number of APIs into a Product and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c04ae-151">You can include a number of APIs into a Product and offer them to developers through the developer portal.</span></span> <br/><span data-ttu-id="c04ae-152">You publish the API by associating the API with a product (in this example, *Unlimited*).</span><span class="sxs-lookup"><span data-stu-id="c04ae-152">You publish the API by associating the API with a product (in this example, *Unlimited*).</span></span> <span data-ttu-id="c04ae-153">To add this new API to a product, type the product name (you can also do it later from the **Settings** page).</span><span class="sxs-lookup"><span data-stu-id="c04ae-153">To add this new API to a product, type the product name (you can also do it later from the **Settings** page).</span></span> <span data-ttu-id="c04ae-154">This step can be repeated multiple times to add the API to multiple products.</span><span class="sxs-lookup"><span data-stu-id="c04ae-154">This step can be repeated multiple times to add the API to multiple products.</span></span><br/><span data-ttu-id="c04ae-155">To get access to the API, developers must first subscribe to a product.</span><span class="sxs-lookup"><span data-stu-id="c04ae-155">To get access to the API, developers must first subscribe to a product.</span></span> <span data-ttu-id="c04ae-156">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="c04ae-156">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <br/> <span data-ttu-id="c04ae-157">If you created the APIM instance, you are an administrator already, so you are subscribed to every product.</span><span class="sxs-lookup"><span data-stu-id="c04ae-157">If you created the APIM instance, you are an administrator already, so you are subscribed to every product.</span></span><br/> <span data-ttu-id="c04ae-158">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-158">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span></span> |
    |<span data-ttu-id="c04ae-159">Version this API?</span><span class="sxs-lookup"><span data-stu-id="c04ae-159">Version this API?</span></span>||<span data-ttu-id="c04ae-160">For more information about versioning, see [Publish multiple versions of your API](api-management-get-started-publish-versions.md)</span><span class="sxs-lookup"><span data-stu-id="c04ae-160">For more information about versioning, see [Publish multiple versions of your API](api-management-get-started-publish-versions.md)</span></span>|
    
    >[!NOTE]
    > <span data-ttu-id="c04ae-161">To publish the API, you must associate it with a product.</span><span class="sxs-lookup"><span data-stu-id="c04ae-161">To publish the API, you must associate it with a product.</span></span> <span data-ttu-id="c04ae-162">You can do it from the **Settings page**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-162">You can do it from the **Settings page**.</span></span>
    
3. <span data-ttu-id="c04ae-163">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-163">Select **Create**.</span></span>

## <a name="test-the-new-apim-api-in-the-azure-portal"></a><span data-ttu-id="c04ae-164">Test the new APIM API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-164">Test the new APIM API in the Azure portal</span></span>

<span data-ttu-id="c04ae-165">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-165">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span></span>  
1. <span data-ttu-id="c04ae-166">Select the API you created in the previous step (from the **APIs** tab).</span><span class="sxs-lookup"><span data-stu-id="c04ae-166">Select the API you created in the previous step (from the **APIs** tab).</span></span>
2. <span data-ttu-id="c04ae-167">Press the **Test** tab.  ![Test API](./media/api-management-get-started/test-api.png)</span><span class="sxs-lookup"><span data-stu-id="c04ae-167">Press the **Test** tab.  ![Test API](./media/api-management-get-started/test-api.png)</span></span>
3. <span data-ttu-id="c04ae-168">Click on **GetSpeakers**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-168">Click on **GetSpeakers**.</span></span>
    <span data-ttu-id="c04ae-169">The page displays fields for query parameters, in this case none, and headers.</span><span class="sxs-lookup"><span data-stu-id="c04ae-169">The page displays fields for query parameters, in this case none, and headers.</span></span> <span data-ttu-id="c04ae-170">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-170">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="c04ae-171">The key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="c04ae-171">The key is filled in automatically.</span></span>
4. <span data-ttu-id="c04ae-172">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-172">Press **Send**.</span></span>

    <span data-ttu-id="c04ae-173">Backend responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="c04ae-173">Backend responds with **200 OK** and some data.</span></span>

## <span data-ttu-id="c04ae-174"><a name="call-operation"> </a>Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-174"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>

<span data-ttu-id="c04ae-175">Operations can also be called from the **Developer portal** to test APIs.</span><span class="sxs-lookup"><span data-stu-id="c04ae-175">Operations can also be called from the **Developer portal** to test APIs.</span></span>

1. <span data-ttu-id="c04ae-176">Navigate to the **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-176">Navigate to the **Developer portal**.</span></span>
<span data-ttu-id="c04ae-177">![Developer portal](./media/api-management-get-started/developer-portal.png)</span><span class="sxs-lookup"><span data-stu-id="c04ae-177">![Developer portal](./media/api-management-get-started/developer-portal.png)</span></span>

2. <span data-ttu-id="c04ae-178">Select **APIS**, click on **Demo Conference API** and then **GetSpeakers**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-178">Select **APIS**, click on **Demo Conference API** and then **GetSpeakers**.</span></span>
    
    <span data-ttu-id="c04ae-179">The page displays fields for query parameters, in this case none, and headers.</span><span class="sxs-lookup"><span data-stu-id="c04ae-179">The page displays fields for query parameters, in this case none, and headers.</span></span> <span data-ttu-id="c04ae-180">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="c04ae-180">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="c04ae-181">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="c04ae-181">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span>
3. <span data-ttu-id="c04ae-182">Press **Try it**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-182">Press **Try it**.</span></span>
4. <span data-ttu-id="c04ae-183">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="c04ae-183">Press **Send**.</span></span>
    
    <span data-ttu-id="c04ae-184">After an operation is invoked, the developer portal shows the responses.</span><span class="sxs-lookup"><span data-stu-id="c04ae-184">After an operation is invoked, the developer portal shows the responses.</span></span>  

## <span data-ttu-id="c04ae-185"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="c04ae-185"><a name="next-steps"> </a>Next steps</span></span>

<span data-ttu-id="c04ae-186">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="c04ae-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c04ae-187">Import your first API</span><span class="sxs-lookup"><span data-stu-id="c04ae-187">Import your first API</span></span>
> * <span data-ttu-id="c04ae-188">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-188">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="c04ae-189">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="c04ae-189">Test the API in the Developer portal</span></span>

<span data-ttu-id="c04ae-190">Advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="c04ae-190">Advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c04ae-191">Create and publish a product</span><span class="sxs-lookup"><span data-stu-id="c04ae-191">Create and publish a product</span></span>](api-management-howto-add-products.md)
