---
title: Azure Resource Manager request limits | Microsoft Docs
description: Describes how to use throttling with Azure Resource Manager requests when subscription limits have been reached.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6780b422138fbe18adfe256e9f7aa279dfed1cd9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551437"
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="38305-103">Throttling Resource Manager requests</span><span class="sxs-lookup"><span data-stu-id="38305-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="38305-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span><span class="sxs-lookup"><span data-stu-id="38305-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="38305-105">If your application or script reaches these limits, you need to throttle your requests.</span><span class="sxs-lookup"><span data-stu-id="38305-105">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="38305-106">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span><span class="sxs-lookup"><span data-stu-id="38305-106">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="38305-107">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span><span class="sxs-lookup"><span data-stu-id="38305-107">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="38305-108">The number of requests is scoped to either your subscription or your tenant.</span><span class="sxs-lookup"><span data-stu-id="38305-108">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="38305-109">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span><span class="sxs-lookup"><span data-stu-id="38305-109">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="38305-110">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span><span class="sxs-lookup"><span data-stu-id="38305-110">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="38305-111">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span><span class="sxs-lookup"><span data-stu-id="38305-111">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="38305-112">Remaining requests</span><span class="sxs-lookup"><span data-stu-id="38305-112">Remaining requests</span></span>
<span data-ttu-id="38305-113">You can determine the number of remaining requests by examining response headers.</span><span class="sxs-lookup"><span data-stu-id="38305-113">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="38305-114">Each request includes values for the number of remaining read and write requests.</span><span class="sxs-lookup"><span data-stu-id="38305-114">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="38305-115">The following table describes the response headers you can examine for those values:</span><span class="sxs-lookup"><span data-stu-id="38305-115">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="38305-116">Response header</span><span class="sxs-lookup"><span data-stu-id="38305-116">Response header</span></span> | <span data-ttu-id="38305-117">Description</span><span class="sxs-lookup"><span data-stu-id="38305-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38305-118">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="38305-118">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="38305-119">Subscription scoped reads remaining</span><span class="sxs-lookup"><span data-stu-id="38305-119">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="38305-120">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="38305-120">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="38305-121">Subscription scoped writes remaining</span><span class="sxs-lookup"><span data-stu-id="38305-121">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="38305-122">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="38305-122">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="38305-123">Tenant scoped reads remaining</span><span class="sxs-lookup"><span data-stu-id="38305-123">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="38305-124">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="38305-124">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="38305-125">Tenant scoped writes remaining</span><span class="sxs-lookup"><span data-stu-id="38305-125">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="38305-126">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="38305-126">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="38305-127">Subscription scoped resource type requests remaining.</span><span class="sxs-lookup"><span data-stu-id="38305-127">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="38305-128">This header value is only returned if a service has overridden the default limit.</span><span class="sxs-lookup"><span data-stu-id="38305-128">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="38305-129">Resource Manager adds this value instead of the subscription reads or writes.</span><span class="sxs-lookup"><span data-stu-id="38305-129">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="38305-130">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="38305-130">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="38305-131">Subscription scoped resource type collection requests remaining.</span><span class="sxs-lookup"><span data-stu-id="38305-131">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="38305-132">This header value is only returned if a service has overridden the default limit.</span><span class="sxs-lookup"><span data-stu-id="38305-132">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="38305-133">This value provides the number of remaining collection requests (list resources).</span><span class="sxs-lookup"><span data-stu-id="38305-133">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="38305-134">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="38305-134">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="38305-135">Tenant scoped resource type requests remaining.</span><span class="sxs-lookup"><span data-stu-id="38305-135">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="38305-136">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span><span class="sxs-lookup"><span data-stu-id="38305-136">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="38305-137">Resource Manager adds this value instead of the tenant reads or writes.</span><span class="sxs-lookup"><span data-stu-id="38305-137">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="38305-138">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="38305-138">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="38305-139">Tenant scoped resource type collection requests remaining.</span><span class="sxs-lookup"><span data-stu-id="38305-139">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="38305-140">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span><span class="sxs-lookup"><span data-stu-id="38305-140">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="38305-141">Retrieving the header values</span><span class="sxs-lookup"><span data-stu-id="38305-141">Retrieving the header values</span></span>
<span data-ttu-id="38305-142">Retrieving these header values in your code or script is no different than retrieving any header value.</span><span class="sxs-lookup"><span data-stu-id="38305-142">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="38305-143">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span><span class="sxs-lookup"><span data-stu-id="38305-143">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="38305-144">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span><span class="sxs-lookup"><span data-stu-id="38305-144">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="38305-145">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38305-145">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="38305-146">Which returns many values, including the following response value:</span><span class="sxs-lookup"><span data-stu-id="38305-146">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="38305-147">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span><span class="sxs-lookup"><span data-stu-id="38305-147">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="38305-148">Which returns many values, including the following object:</span><span class="sxs-lookup"><span data-stu-id="38305-148">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="38305-149">Waiting before sending next request</span><span class="sxs-lookup"><span data-stu-id="38305-149">Waiting before sending next request</span></span>
<span data-ttu-id="38305-150">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span><span class="sxs-lookup"><span data-stu-id="38305-150">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="38305-151">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span><span class="sxs-lookup"><span data-stu-id="38305-151">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="38305-152">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span><span class="sxs-lookup"><span data-stu-id="38305-152">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38305-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="38305-153">Next steps</span></span>

* <span data-ttu-id="38305-154">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="38305-154">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="38305-155">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="38305-155">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
