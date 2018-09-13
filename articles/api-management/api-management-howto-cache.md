---
title: Add caching to improve performance in Azure API Management | Microsoft Docs
description: Learn how to improve the latency, bandwidth consumption, and web service load for API Management service calls.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8d97da329175eea95058a5e948992b4560cc5a29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551106"
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="da06b-103">Add caching to improve performance in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="da06b-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="da06b-104">Operations in API Management can be configured for response caching.</span><span class="sxs-lookup"><span data-stu-id="da06b-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="da06b-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span><span class="sxs-lookup"><span data-stu-id="da06b-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="da06b-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span><span class="sxs-lookup"><span data-stu-id="da06b-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="da06b-107">You can then call the operation from the developer portal to verify caching in action.</span><span class="sxs-lookup"><span data-stu-id="da06b-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="da06b-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="da06b-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="da06b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="da06b-109">Prerequisites</span></span>
<span data-ttu-id="da06b-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span><span class="sxs-lookup"><span data-stu-id="da06b-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="da06b-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="da06b-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="da06b-112"><a name="configure-caching"> </a>Configure an operation for caching</span><span class="sxs-lookup"><span data-stu-id="da06b-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="da06b-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span><span class="sxs-lookup"><span data-stu-id="da06b-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="da06b-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span><span class="sxs-lookup"><span data-stu-id="da06b-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="da06b-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="da06b-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="da06b-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="da06b-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="da06b-117">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="da06b-117">This takes you to the API Management publisher portal.</span></span>

![Publisher portal][api-management-management-console]

<span data-ttu-id="da06b-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="da06b-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![Echo API][api-management-echo-api]

<span data-ttu-id="da06b-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span><span class="sxs-lookup"><span data-stu-id="da06b-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Echo API operations][api-management-echo-api-operations]

<span data-ttu-id="da06b-123">Click the **Caching** tab to view the caching settings for this operation.</span><span class="sxs-lookup"><span data-stu-id="da06b-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Caching tab][api-management-caching-tab]

<span data-ttu-id="da06b-125">To enable caching for an operation, select the **Enable** check box.</span><span class="sxs-lookup"><span data-stu-id="da06b-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="da06b-126">In this example, caching is enabled.</span><span class="sxs-lookup"><span data-stu-id="da06b-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="da06b-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span><span class="sxs-lookup"><span data-stu-id="da06b-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="da06b-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span><span class="sxs-lookup"><span data-stu-id="da06b-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="da06b-129">**Duration** specifies the expiration interval of the cached responses.</span><span class="sxs-lookup"><span data-stu-id="da06b-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="da06b-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span><span class="sxs-lookup"><span data-stu-id="da06b-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="da06b-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span><span class="sxs-lookup"><span data-stu-id="da06b-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="da06b-132">This response will be cached, keyed by the specified headers and query string parameters.</span><span class="sxs-lookup"><span data-stu-id="da06b-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="da06b-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span><span class="sxs-lookup"><span data-stu-id="da06b-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="da06b-134"><a name="caching-policies"> </a>Review the caching policies</span><span class="sxs-lookup"><span data-stu-id="da06b-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="da06b-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span><span class="sxs-lookup"><span data-stu-id="da06b-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="da06b-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span><span class="sxs-lookup"><span data-stu-id="da06b-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="da06b-137">These policies can be viewed and edited in the policy editor.</span><span class="sxs-lookup"><span data-stu-id="da06b-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="da06b-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="da06b-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Policy scope operation][api-management-operation-dropdown]

<span data-ttu-id="da06b-140">This displays the policies for this operation in the policy editor.</span><span class="sxs-lookup"><span data-stu-id="da06b-140">This displays the policies for this operation in the policy editor.</span></span>

![API Management policy editor][api-management-policy-editor]

<span data-ttu-id="da06b-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span><span class="sxs-lookup"><span data-stu-id="da06b-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="da06b-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span><span class="sxs-lookup"><span data-stu-id="da06b-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="da06b-144"><a name="test-operation"> </a>Call an operation and test the caching</span><span class="sxs-lookup"><span data-stu-id="da06b-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="da06b-145">To see the caching in action, we can call the operation from the developer portal.</span><span class="sxs-lookup"><span data-stu-id="da06b-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="da06b-146">Click **Developer portal** in the top right menu.</span><span class="sxs-lookup"><span data-stu-id="da06b-146">Click **Developer portal** in the top right menu.</span></span>

![Developer portal][api-management-developer-portal-menu]

<span data-ttu-id="da06b-148">Click **APIs** in the top menu, and then select **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="da06b-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> <span data-ttu-id="da06b-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span><span class="sxs-lookup"><span data-stu-id="da06b-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="da06b-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span><span class="sxs-lookup"><span data-stu-id="da06b-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="da06b-153">The console allows you to invoke operations directly from the developer portal.</span><span class="sxs-lookup"><span data-stu-id="da06b-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="da06b-155">Keep the default values for **param1** and **param2**.</span><span class="sxs-lookup"><span data-stu-id="da06b-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="da06b-156">Select the desired key from the **subscription-key** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="da06b-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="da06b-157">If your account has only one subscription, it will already be selected.</span><span class="sxs-lookup"><span data-stu-id="da06b-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="da06b-158">Enter **sampleheader:value1** in the **Request headers** text box.</span><span class="sxs-lookup"><span data-stu-id="da06b-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="da06b-159">Click **HTTP Get** and make a note of the response headers.</span><span class="sxs-lookup"><span data-stu-id="da06b-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="da06b-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="da06b-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="da06b-161">Note that the value of **sampleheader** is still **value1** in the response.</span><span class="sxs-lookup"><span data-stu-id="da06b-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="da06b-162">Try some different values and note that the cached response from the first call is returned.</span><span class="sxs-lookup"><span data-stu-id="da06b-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="da06b-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="da06b-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="da06b-164">Note that the value of **sampleheader** in the response is now **value2**.</span><span class="sxs-lookup"><span data-stu-id="da06b-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="da06b-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span><span class="sxs-lookup"><span data-stu-id="da06b-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="da06b-166"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="da06b-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="da06b-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="da06b-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="da06b-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="da06b-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-cache/api-management-console.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps










