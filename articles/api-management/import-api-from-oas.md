---
title: Import an OpenAPI specification using the Azure portal | Microsoft Docs
description: Learn how to import an OpenAPI specification with API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/22/2017
ms.author: apimpm
ms.openlocfilehash: f5132215b1fda93c62c1fbea46c3266fcc44ec46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857332"
---
# <a name="import-an-openapi-specification"></a><span data-ttu-id="69285-103">Import an OpenAPI specification</span><span class="sxs-lookup"><span data-stu-id="69285-103">Import an OpenAPI specification</span></span>

<span data-ttu-id="69285-104">This article shows how to import an "OpenAPI specification" back-end API residing at http://conferenceapi.azurewebsites.net?format=json.</span><span class="sxs-lookup"><span data-stu-id="69285-104">This article shows how to import an "OpenAPI specification" back-end API residing at http://conferenceapi.azurewebsites.net?format=json.</span></span> <span data-ttu-id="69285-105">This back-end API is provided by Microsoft and hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="69285-105">This back-end API is provided by Microsoft and hosted on Azure.</span></span> <span data-ttu-id="69285-106">The article also shows how to test the APIM API.</span><span class="sxs-lookup"><span data-stu-id="69285-106">The article also shows how to test the APIM API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69285-107">See this [document](https://blogs.msdn.microsoft.com/apimanagement/2018/04/11/important-changes-to-openapi-import-and-export/) for important information and tips related to OpenAPI import.</span><span class="sxs-lookup"><span data-stu-id="69285-107">See this [document](https://blogs.msdn.microsoft.com/apimanagement/2018/04/11/important-changes-to-openapi-import-and-export/) for important information and tips related to OpenAPI import.</span></span>

<span data-ttu-id="69285-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="69285-108">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="69285-109">Import an "OpenAPI specification" back-end API</span><span class="sxs-lookup"><span data-stu-id="69285-109">Import an "OpenAPI specification" back-end API</span></span>
> * <span data-ttu-id="69285-110">Test the API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="69285-110">Test the API in the Azure portal</span></span>
> * <span data-ttu-id="69285-111">Test the API in the Developer portal</span><span class="sxs-lookup"><span data-stu-id="69285-111">Test the API in the Developer portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69285-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="69285-112">Prerequisites</span></span>

<span data-ttu-id="69285-113">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span><span class="sxs-lookup"><span data-stu-id="69285-113">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md)</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <span data-ttu-id="69285-114"><a name="create-api"> </a>Import and publish a back-end API</span><span class="sxs-lookup"><span data-stu-id="69285-114"><a name="create-api"> </a>Import and publish a back-end API</span></span>

1. <span data-ttu-id="69285-115">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="69285-115">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="69285-116">Select **OpenAPI specification** from the **Add a new API** list.</span><span class="sxs-lookup"><span data-stu-id="69285-116">Select **OpenAPI specification** from the **Add a new API** list.</span></span>
    <span data-ttu-id="69285-117">![OpenAPI specification](./media/import-api-from-oas/oas-api.png)</span><span class="sxs-lookup"><span data-stu-id="69285-117">![OpenAPI specification](./media/import-api-from-oas/oas-api.png)</span></span>
3. <span data-ttu-id="69285-118">Enter appropriate settings.</span><span class="sxs-lookup"><span data-stu-id="69285-118">Enter appropriate settings.</span></span> <span data-ttu-id="69285-119">You can set all the API values during creation.</span><span class="sxs-lookup"><span data-stu-id="69285-119">You can set all the API values during creation.</span></span> <span data-ttu-id="69285-120">Alternately, you can set some of them later by going to the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="69285-120">Alternately, you can set some of them later by going to the **Settings** tab.</span></span> <br/> <span data-ttu-id="69285-121">If you press **tab** some (or all) of the fields get filled up with the info from the specified back-end service.</span><span class="sxs-lookup"><span data-stu-id="69285-121">If you press **tab** some (or all) of the fields get filled up with the info from the specified back-end service.</span></span>

    ![Create an API](./media/api-management-get-started/create-api.png)

    |<span data-ttu-id="69285-123">Setting</span><span class="sxs-lookup"><span data-stu-id="69285-123">Setting</span></span>|<span data-ttu-id="69285-124">Value</span><span class="sxs-lookup"><span data-stu-id="69285-124">Value</span></span>|<span data-ttu-id="69285-125">Description</span><span class="sxs-lookup"><span data-stu-id="69285-125">Description</span></span>|
    |---|---|---|
    |<span data-ttu-id="69285-126">**OpenAPI Specification**</span><span class="sxs-lookup"><span data-stu-id="69285-126">**OpenAPI Specification**</span></span>|http://conferenceapi.azurewebsites.net?format=json|<span data-ttu-id="69285-127">References the service implementing the API.</span><span class="sxs-lookup"><span data-stu-id="69285-127">References the service implementing the API.</span></span> <span data-ttu-id="69285-128">API management forwards requests to this address.</span><span class="sxs-lookup"><span data-stu-id="69285-128">API management forwards requests to this address.</span></span>|
    |<span data-ttu-id="69285-129">**Display name**</span><span class="sxs-lookup"><span data-stu-id="69285-129">**Display name**</span></span>|<span data-ttu-id="69285-130">*Demo Conference API*</span><span class="sxs-lookup"><span data-stu-id="69285-130">*Demo Conference API*</span></span>|<span data-ttu-id="69285-131">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="69285-131">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span> <br/><span data-ttu-id="69285-132">This name is displayed in the Developer portal.</span><span class="sxs-lookup"><span data-stu-id="69285-132">This name is displayed in the Developer portal.</span></span>|
    |<span data-ttu-id="69285-133">**Name**</span><span class="sxs-lookup"><span data-stu-id="69285-133">**Name**</span></span>|<span data-ttu-id="69285-134">*demo-conference-api*</span><span class="sxs-lookup"><span data-stu-id="69285-134">*demo-conference-api*</span></span>|<span data-ttu-id="69285-135">Provides a unique name for the API.</span><span class="sxs-lookup"><span data-stu-id="69285-135">Provides a unique name for the API.</span></span> <br/><span data-ttu-id="69285-136">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="69285-136">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span>|
    |<span data-ttu-id="69285-137">**Description**</span><span class="sxs-lookup"><span data-stu-id="69285-137">**Description**</span></span>|<span data-ttu-id="69285-138">Provide an optional description of the API.</span><span class="sxs-lookup"><span data-stu-id="69285-138">Provide an optional description of the API.</span></span>|<span data-ttu-id="69285-139">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span><span class="sxs-lookup"><span data-stu-id="69285-139">If you press tab after entering the service URL, APIM will fill out this field based on what is in the json.</span></span>|
    |<span data-ttu-id="69285-140">**API URL suffix**</span><span class="sxs-lookup"><span data-stu-id="69285-140">**API URL suffix**</span></span>|<span data-ttu-id="69285-141">*conference*</span><span class="sxs-lookup"><span data-stu-id="69285-141">*conference*</span></span>|<span data-ttu-id="69285-142">The suffix is appended to the base URL for the API management service.</span><span class="sxs-lookup"><span data-stu-id="69285-142">The suffix is appended to the base URL for the API management service.</span></span> <span data-ttu-id="69285-143">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span><span class="sxs-lookup"><span data-stu-id="69285-143">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>|
    |<span data-ttu-id="69285-144">**URL scheme**</span><span class="sxs-lookup"><span data-stu-id="69285-144">**URL scheme**</span></span>|<span data-ttu-id="69285-145">*HTTPS*</span><span class="sxs-lookup"><span data-stu-id="69285-145">*HTTPS*</span></span>|<span data-ttu-id="69285-146">Determines which protocols can be used to access the API.</span><span class="sxs-lookup"><span data-stu-id="69285-146">Determines which protocols can be used to access the API.</span></span> |
    |<span data-ttu-id="69285-147">**Products**</span><span class="sxs-lookup"><span data-stu-id="69285-147">**Products**</span></span>|<span data-ttu-id="69285-148">*Unlimited*</span><span class="sxs-lookup"><span data-stu-id="69285-148">*Unlimited*</span></span>| <span data-ttu-id="69285-149">Publish the API by associating the API with a product.</span><span class="sxs-lookup"><span data-stu-id="69285-149">Publish the API by associating the API with a product.</span></span> <span data-ttu-id="69285-150">To optionally add this new API to a product, type the product name.</span><span class="sxs-lookup"><span data-stu-id="69285-150">To optionally add this new API to a product, type the product name.</span></span> <span data-ttu-id="69285-151">This step can be repeated multiple times to add the API to multiple products.</span><span class="sxs-lookup"><span data-stu-id="69285-151">This step can be repeated multiple times to add the API to multiple products.</span></span><br/><span data-ttu-id="69285-152">Products are associations of one or more APIs.</span><span class="sxs-lookup"><span data-stu-id="69285-152">Products are associations of one or more APIs.</span></span> <span data-ttu-id="69285-153">You can include a number of APIs and offer them to developers through the developer portal.</span><span class="sxs-lookup"><span data-stu-id="69285-153">You can include a number of APIs and offer them to developers through the developer portal.</span></span> <span data-ttu-id="69285-154">Developers must first subscribe to a product to get access to the API.</span><span class="sxs-lookup"><span data-stu-id="69285-154">Developers must first subscribe to a product to get access to the API.</span></span> <span data-ttu-id="69285-155">When they subscribe, they get a subscription key that is good for any API in that product.</span><span class="sxs-lookup"><span data-stu-id="69285-155">When they subscribe, they get a subscription key that is good for any API in that product.</span></span> <span data-ttu-id="69285-156">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="69285-156">If you created the APIM instance, you are an administrator already, so you are subscribed to every product by default.</span></span><br/> <span data-ttu-id="69285-157">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="69285-157">By default, each API Management instance comes with two sample products: **Starter** and **Unlimited**.</span></span> |

4. <span data-ttu-id="69285-158">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="69285-158">Select **Create**.</span></span>

## <a name="test-the-new-apim-api-in-the-azure-portal"></a><span data-ttu-id="69285-159">Test the new APIM API in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="69285-159">Test the new APIM API in the Azure portal</span></span>

<span data-ttu-id="69285-160">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="69285-160">Operations can be called directly from the Azure portal, which provides a convenient way to view and test the operations of an API.</span></span>

1. <span data-ttu-id="69285-161">Select the API you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="69285-161">Select the API you created in the previous step.</span></span>
2. <span data-ttu-id="69285-162">Press the **Test** tab.</span><span class="sxs-lookup"><span data-stu-id="69285-162">Press the **Test** tab.</span></span>

    ![Test API](./media/api-management-get-started/test-api.png)
1. <span data-ttu-id="69285-164">Click on **GetSpeakers**.</span><span class="sxs-lookup"><span data-stu-id="69285-164">Click on **GetSpeakers**.</span></span>

    <span data-ttu-id="69285-165">The page displays fields for query parameters but in this case we don't have any.</span><span class="sxs-lookup"><span data-stu-id="69285-165">The page displays fields for query parameters but in this case we don't have any.</span></span> <span data-ttu-id="69285-166">The page also displays fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="69285-166">The page also displays fields for the headers.</span></span> <span data-ttu-id="69285-167">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="69285-167">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="69285-168">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="69285-168">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span>
4. <span data-ttu-id="69285-169">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="69285-169">Press **Send**.</span></span>

    <span data-ttu-id="69285-170">Backend responds with **200 OK** and some data.</span><span class="sxs-lookup"><span data-stu-id="69285-170">Backend responds with **200 OK** and some data.</span></span>

## <span data-ttu-id="69285-171"><a name="call-operation"> </a>Call an operation from the Developer portal</span><span class="sxs-lookup"><span data-stu-id="69285-171"><a name="call-operation"> </a>Call an operation from the Developer portal</span></span>

<span data-ttu-id="69285-172">Operations can also be called **Developer portal** to test APIs.</span><span class="sxs-lookup"><span data-stu-id="69285-172">Operations can also be called **Developer portal** to test APIs.</span></span>

1. <span data-ttu-id="69285-173">Select the API you created in the "Import and publish a back-end API" step.</span><span class="sxs-lookup"><span data-stu-id="69285-173">Select the API you created in the "Import and publish a back-end API" step.</span></span>
2. <span data-ttu-id="69285-174">Press **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="69285-174">Press **Developer portal**.</span></span>

    ![Test in Developer portal](./media/api-management-get-started/developer-portal.png)

    <span data-ttu-id="69285-176">The "Developer portal" site opens up.</span><span class="sxs-lookup"><span data-stu-id="69285-176">The "Developer portal" site opens up.</span></span>
3. <span data-ttu-id="69285-177">Select **API**.</span><span class="sxs-lookup"><span data-stu-id="69285-177">Select **API**.</span></span>
4. <span data-ttu-id="69285-178">Select **Demo Conference API**.</span><span class="sxs-lookup"><span data-stu-id="69285-178">Select **Demo Conference API**.</span></span>
5. <span data-ttu-id="69285-179">Click **GetSpeakers**.</span><span class="sxs-lookup"><span data-stu-id="69285-179">Click **GetSpeakers**.</span></span>

    <span data-ttu-id="69285-180">The page displays fields for query parameters but in this case we don't have any.</span><span class="sxs-lookup"><span data-stu-id="69285-180">The page displays fields for query parameters but in this case we don't have any.</span></span> <span data-ttu-id="69285-181">The page also displays fields for the headers.</span><span class="sxs-lookup"><span data-stu-id="69285-181">The page also displays fields for the headers.</span></span> <span data-ttu-id="69285-182">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span><span class="sxs-lookup"><span data-stu-id="69285-182">One of the headers is "Ocp-Apim-Subscription-Key", for the subscription key of the product that is associated with this API.</span></span> <span data-ttu-id="69285-183">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span><span class="sxs-lookup"><span data-stu-id="69285-183">If you created the APIM instance, you are an administrator already, so the key is filled in automatically.</span></span>
6. <span data-ttu-id="69285-184">Press **Try it**.</span><span class="sxs-lookup"><span data-stu-id="69285-184">Press **Try it**.</span></span>
7. <span data-ttu-id="69285-185">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="69285-185">Press **Send**.</span></span>

    <span data-ttu-id="69285-186">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="69285-186">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="69285-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="69285-187">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69285-188">Transform and protect a published API</span><span class="sxs-lookup"><span data-stu-id="69285-188">Transform and protect a published API</span></span>](transform-api.md)
