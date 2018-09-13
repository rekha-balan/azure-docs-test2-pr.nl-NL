---
title: Tenant Resource Usage API | Microsoft Docs
description: Reference for resource usage API, which retrieve Azure Stack usage information.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.reviewer: alfredop
ms.openlocfilehash: ab5dad550e590cd70f54ad5c8d4727d0f6370190
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821215"
---
# <a name="tenant-resource-usage-api"></a><span data-ttu-id="83fcb-103">Tenant Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="83fcb-103">Tenant Resource Usage API</span></span>

<span data-ttu-id="83fcb-104">A tenant can use the Tenant API to view the tenant’s own resource usage data.</span><span class="sxs-lookup"><span data-stu-id="83fcb-104">A tenant can use the Tenant API to view the tenant’s own resource usage data.</span></span> <span data-ttu-id="83fcb-105">This API is consistent with the Azure Usage API (currently in private preview).</span><span class="sxs-lookup"><span data-stu-id="83fcb-105">This API is consistent with the Azure Usage API (currently in private preview).</span></span>

<span data-ttu-id="83fcb-106">You can use the Windows PowerShell cmdlet **Get-UsageAggregates** to get usage data like in Azure.</span><span class="sxs-lookup"><span data-stu-id="83fcb-106">You can use the Windows PowerShell cmdlet **Get-UsageAggregates** to get usage data like in Azure.</span></span>

## <a name="api-call"></a><span data-ttu-id="83fcb-107">API call</span><span class="sxs-lookup"><span data-stu-id="83fcb-107">API call</span></span>
### <a name="request"></a><span data-ttu-id="83fcb-108">Request</span><span class="sxs-lookup"><span data-stu-id="83fcb-108">Request</span></span>
<span data-ttu-id="83fcb-109">The request gets consumption details for the requested subscriptions and for the requested time frame.</span><span class="sxs-lookup"><span data-stu-id="83fcb-109">The request gets consumption details for the requested subscriptions and for the requested time frame.</span></span> <span data-ttu-id="83fcb-110">There is no request body.</span><span class="sxs-lookup"><span data-stu-id="83fcb-110">There is no request body.</span></span>

| <span data-ttu-id="83fcb-111">**Method**</span><span class="sxs-lookup"><span data-stu-id="83fcb-111">**Method**</span></span> | <span data-ttu-id="83fcb-112">**Request URI**</span><span class="sxs-lookup"><span data-stu-id="83fcb-112">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="83fcb-113">GET</span><span class="sxs-lookup"><span data-stu-id="83fcb-113">GET</span></span> |<span data-ttu-id="83fcb-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="83fcb-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="83fcb-115">Arguments</span><span class="sxs-lookup"><span data-stu-id="83fcb-115">Arguments</span></span>
| <span data-ttu-id="83fcb-116">**Argument**</span><span class="sxs-lookup"><span data-stu-id="83fcb-116">**Argument**</span></span> | <span data-ttu-id="83fcb-117">**Description**</span><span class="sxs-lookup"><span data-stu-id="83fcb-117">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="83fcb-118">*Armendpoint*</span><span class="sxs-lookup"><span data-stu-id="83fcb-118">*Armendpoint*</span></span> |<span data-ttu-id="83fcb-119">Azure Resource Manager endpoint of your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="83fcb-119">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="83fcb-120">The Azure Stack convention is that the name of Azure Resource Manager endpoint is in the format `https://management.{domain-name}`.</span><span class="sxs-lookup"><span data-stu-id="83fcb-120">The Azure Stack convention is that the name of Azure Resource Manager endpoint is in the format `https://management.{domain-name}`.</span></span> <span data-ttu-id="83fcb-121">For example, for the development kit, the domain name is local.azurestack.external, then the Resource Manager  endpoint is `https://management.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="83fcb-121">For example, for the development kit, the domain name is local.azurestack.external, then the Resource Manager  endpoint is `https://management.local.azurestack.external`.</span></span> |
| <span data-ttu-id="83fcb-122">*subId*</span><span class="sxs-lookup"><span data-stu-id="83fcb-122">*subId*</span></span> |<span data-ttu-id="83fcb-123">Subscription ID of the user who is making the call.</span><span class="sxs-lookup"><span data-stu-id="83fcb-123">Subscription ID of the user who is making the call.</span></span> <span data-ttu-id="83fcb-124">You can use this API only to query for a single subscription’s usage.</span><span class="sxs-lookup"><span data-stu-id="83fcb-124">You can use this API only to query for a single subscription’s usage.</span></span> <span data-ttu-id="83fcb-125">Providers can use the Provider Resource Usage API to query usage for all tenants.</span><span class="sxs-lookup"><span data-stu-id="83fcb-125">Providers can use the Provider Resource Usage API to query usage for all tenants.</span></span> |
| <span data-ttu-id="83fcb-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="83fcb-126">*reportedStartTime*</span></span> |<span data-ttu-id="83fcb-127">Start time of the query.</span><span class="sxs-lookup"><span data-stu-id="83fcb-127">Start time of the query.</span></span> <span data-ttu-id="83fcb-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span><span class="sxs-lookup"><span data-stu-id="83fcb-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span></span> <span data-ttu-id="83fcb-129">For daily aggregation, set this value to UTC midnight.</span><span class="sxs-lookup"><span data-stu-id="83fcb-129">For daily aggregation, set this value to UTC midnight.</span></span> <span data-ttu-id="83fcb-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span><span class="sxs-lookup"><span data-stu-id="83fcb-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="83fcb-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="83fcb-131">*reportedEndTime*</span></span> |<span data-ttu-id="83fcb-132">End time of the query.</span><span class="sxs-lookup"><span data-stu-id="83fcb-132">End time of the query.</span></span> <span data-ttu-id="83fcb-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span><span class="sxs-lookup"><span data-stu-id="83fcb-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span></span> <span data-ttu-id="83fcb-134">The value for *reportedEndTime* cannot be in the future.</span><span class="sxs-lookup"><span data-stu-id="83fcb-134">The value for *reportedEndTime* cannot be in the future.</span></span> |
| <span data-ttu-id="83fcb-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="83fcb-135">*aggregationGranularity*</span></span> |<span data-ttu-id="83fcb-136">Optional parameter that has two discrete potential values: daily and hourly.</span><span class="sxs-lookup"><span data-stu-id="83fcb-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="83fcb-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span><span class="sxs-lookup"><span data-stu-id="83fcb-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span></span> <span data-ttu-id="83fcb-138">The daily option is the default.</span><span class="sxs-lookup"><span data-stu-id="83fcb-138">The daily option is the default.</span></span> |
| <span data-ttu-id="83fcb-139">*api-version*</span><span class="sxs-lookup"><span data-stu-id="83fcb-139">*api-version*</span></span> |<span data-ttu-id="83fcb-140">Version of the protocol that is used to make this request.</span><span class="sxs-lookup"><span data-stu-id="83fcb-140">Version of the protocol that is used to make this request.</span></span> <span data-ttu-id="83fcb-141">You must use 2015-06-01-preview.</span><span class="sxs-lookup"><span data-stu-id="83fcb-141">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="83fcb-142">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="83fcb-142">*continuationToken*</span></span> |<span data-ttu-id="83fcb-143">Token retrieved from the last call to the Usage API provider.</span><span class="sxs-lookup"><span data-stu-id="83fcb-143">Token retrieved from the last call to the Usage API provider.</span></span> <span data-ttu-id="83fcb-144">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for progress.</span><span class="sxs-lookup"><span data-stu-id="83fcb-144">This token is needed when a response is greater than 1,000 lines and it acts as a bookmark for progress.</span></span> <span data-ttu-id="83fcb-145">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span><span class="sxs-lookup"><span data-stu-id="83fcb-145">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="83fcb-146">Response</span><span class="sxs-lookup"><span data-stu-id="83fcb-146">Response</span></span>
<span data-ttu-id="83fcb-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="83fcb-147">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span></span>

```json
{
"value": [
{

"id":
"/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",
"name": "sub1-meterID1",
"type": "Microsoft.Commerce/UsageAggregate",

"properties": {
"subscriptionId":"sub1",
"usageStartTime": "2015-03-03T00:00:00+00:00",
"usageEndTime": "2015-03-04T00:00:00+00:00",
"instanceData":"{\"Microsoft.Resources\":{\"resourceUri\":\"resourceUri1\",\"location\":\"Alaska\",\"tags\":null,\"additionalInfo\":null}}",
"quantity":2.4000000000,
"meterId":"meterID1"

}
},

…
```

### <a name="response-details"></a><span data-ttu-id="83fcb-148">Response details</span><span class="sxs-lookup"><span data-stu-id="83fcb-148">Response details</span></span>
| <span data-ttu-id="83fcb-149">**Argument**</span><span class="sxs-lookup"><span data-stu-id="83fcb-149">**Argument**</span></span> | <span data-ttu-id="83fcb-150">**Description**</span><span class="sxs-lookup"><span data-stu-id="83fcb-150">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="83fcb-151">*id*</span><span class="sxs-lookup"><span data-stu-id="83fcb-151">*id*</span></span> |<span data-ttu-id="83fcb-152">Unique ID of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="83fcb-152">Unique ID of the usage aggregate</span></span> |
| <span data-ttu-id="83fcb-153">*name*</span><span class="sxs-lookup"><span data-stu-id="83fcb-153">*name*</span></span> |<span data-ttu-id="83fcb-154">Name of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="83fcb-154">Name of the usage aggregate</span></span> |
| <span data-ttu-id="83fcb-155">*type*</span><span class="sxs-lookup"><span data-stu-id="83fcb-155">*type*</span></span> |<span data-ttu-id="83fcb-156">Resource definition</span><span class="sxs-lookup"><span data-stu-id="83fcb-156">Resource definition</span></span> |
| <span data-ttu-id="83fcb-157">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="83fcb-157">*subscriptionId*</span></span> |<span data-ttu-id="83fcb-158">Subscription identifier of the Azure user</span><span class="sxs-lookup"><span data-stu-id="83fcb-158">Subscription identifier of the Azure user</span></span> |
| <span data-ttu-id="83fcb-159">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="83fcb-159">*usageStartTime*</span></span> |<span data-ttu-id="83fcb-160">UTC start time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="83fcb-160">UTC start time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="83fcb-161">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="83fcb-161">*usageEndTime*</span></span> |<span data-ttu-id="83fcb-162">UTC end time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="83fcb-162">UTC end time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="83fcb-163">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="83fcb-163">*instanceData*</span></span> |<span data-ttu-id="83fcb-164">Key-value pairs of instance details (in a new format):</span><span class="sxs-lookup"><span data-stu-id="83fcb-164">Key-value pairs of instance details (in a new format):</span></span><br>  <span data-ttu-id="83fcb-165">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span><span class="sxs-lookup"><span data-stu-id="83fcb-165">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span></span> <br>  <span data-ttu-id="83fcb-166">*location*: Region in which this service was run</span><span class="sxs-lookup"><span data-stu-id="83fcb-166">*location*: Region in which this service was run</span></span> <br>  <span data-ttu-id="83fcb-167">*tags*: Resource tags that the user specifies</span><span class="sxs-lookup"><span data-stu-id="83fcb-167">*tags*: Resource tags that the user specifies</span></span> <br>  <span data-ttu-id="83fcb-168">*additionalInfo*: More details about the resource that was consumed, for example, OS version or image type</span><span class="sxs-lookup"><span data-stu-id="83fcb-168">*additionalInfo*: More details about the resource that was consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="83fcb-169">*quantity*</span><span class="sxs-lookup"><span data-stu-id="83fcb-169">*quantity*</span></span> |<span data-ttu-id="83fcb-170">Amount of resource consumption that occurred in this time frame</span><span class="sxs-lookup"><span data-stu-id="83fcb-170">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="83fcb-171">*meterId*</span><span class="sxs-lookup"><span data-stu-id="83fcb-171">*meterId*</span></span> |<span data-ttu-id="83fcb-172">Unique ID for the resource that was consumed (also called *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="83fcb-172">Unique ID for the resource that was consumed (also called *ResourceID*)</span></span> |


## <a name="next-steps"></a><span data-ttu-id="83fcb-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="83fcb-173">Next steps</span></span>
[<span data-ttu-id="83fcb-174">Provider resource usage API</span><span class="sxs-lookup"><span data-stu-id="83fcb-174">Provider resource usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="83fcb-175">Usage-related FAQ</span><span class="sxs-lookup"><span data-stu-id="83fcb-175">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

