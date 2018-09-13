---
title: Tenant Resource Usage API | Microsoft Docs
description: Reference for resource usage API, which retrieve Azure Stack usage information.
services: azure-stack
documentationcenter: ''
author: AlfredoPizzirani
manager: byronr
editor: ''
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2016
ms.author: alfredop
ms.openlocfilehash: d9b684f25307449332a48299e06e0478d41c1e7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555508"
---
# <a name="tenant-resource-usage-api"></a><span data-ttu-id="fb21d-103">Tenant Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="fb21d-103">Tenant Resource Usage API</span></span>
<span data-ttu-id="fb21d-104">A tenant can use the Tenant API to view the tenant’s own resource usage data.</span><span class="sxs-lookup"><span data-stu-id="fb21d-104">A tenant can use the Tenant API to view the tenant’s own resource usage data.</span></span> <span data-ttu-id="fb21d-105">This API is consistent with the Azure Usage API (currently in private preview).</span><span class="sxs-lookup"><span data-stu-id="fb21d-105">This API is consistent with the Azure Usage API (currently in private preview).</span></span>

<span data-ttu-id="fb21d-106">You can use the Windows PowerShell cmdlet **Get-UsageAggregates** to get usage data like in Azure.</span><span class="sxs-lookup"><span data-stu-id="fb21d-106">You can use the Windows PowerShell cmdlet **Get-UsageAggregates** to get usage data like in Azure.</span></span>

## <a name="api-call"></a><span data-ttu-id="fb21d-107">API call</span><span class="sxs-lookup"><span data-stu-id="fb21d-107">API call</span></span>
### <a name="request"></a><span data-ttu-id="fb21d-108">Request</span><span class="sxs-lookup"><span data-stu-id="fb21d-108">Request</span></span>
<span data-ttu-id="fb21d-109">The request gets consumption details for the requested subscriptions and for the requested time frame.</span><span class="sxs-lookup"><span data-stu-id="fb21d-109">The request gets consumption details for the requested subscriptions and for the requested time frame.</span></span> <span data-ttu-id="fb21d-110">There is no request body.</span><span class="sxs-lookup"><span data-stu-id="fb21d-110">There is no request body.</span></span>

| <span data-ttu-id="fb21d-111">**Method**</span><span class="sxs-lookup"><span data-stu-id="fb21d-111">**Method**</span></span> | <span data-ttu-id="fb21d-112">**Request URI**</span><span class="sxs-lookup"><span data-stu-id="fb21d-112">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="fb21d-113">GET</span><span class="sxs-lookup"><span data-stu-id="fb21d-113">GET</span></span> |<span data-ttu-id="fb21d-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="fb21d-114">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="fb21d-115">Arguments</span><span class="sxs-lookup"><span data-stu-id="fb21d-115">Arguments</span></span>
| <span data-ttu-id="fb21d-116">**Argument**</span><span class="sxs-lookup"><span data-stu-id="fb21d-116">**Argument**</span></span> | <span data-ttu-id="fb21d-117">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb21d-117">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fb21d-118">*Armendpoint*</span><span class="sxs-lookup"><span data-stu-id="fb21d-118">*Armendpoint*</span></span> |<span data-ttu-id="fb21d-119">Azure Resource Manager endpoint of your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="fb21d-119">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="fb21d-120">The Azure Stack convention is that the name of ARM endpoint is in the format `https://management.{domain-name}`.</span><span class="sxs-lookup"><span data-stu-id="fb21d-120">The Azure Stack convention is that the name of ARM endpoint is in the format `https://management.{domain-name}`.</span></span> <span data-ttu-id="fb21d-121">For example, if the domain name is local.azurestack.external, then the Resource Manager  endpoint will be `https://management.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="fb21d-121">For example, if the domain name is local.azurestack.external, then the Resource Manager  endpoint will be `https://management.local.azurestack.external`.</span></span> |
| <span data-ttu-id="fb21d-122">*subId*</span><span class="sxs-lookup"><span data-stu-id="fb21d-122">*subId*</span></span> |<span data-ttu-id="fb21d-123">Subscription ID of the user who is making the call.</span><span class="sxs-lookup"><span data-stu-id="fb21d-123">Subscription ID of the user who is making the call.</span></span> <span data-ttu-id="fb21d-124">You can use this API only to query for a single subscription’s usage.</span><span class="sxs-lookup"><span data-stu-id="fb21d-124">You can use this API only to query for a single subscription’s usage.</span></span> <span data-ttu-id="fb21d-125">Providers can use the Provider Resource Usage API to query usage for all tenants.</span><span class="sxs-lookup"><span data-stu-id="fb21d-125">Providers can use the Provider Resource Usage API to query usage for all tenants.</span></span> |
| <span data-ttu-id="fb21d-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="fb21d-126">*reportedStartTime*</span></span> |<span data-ttu-id="fb21d-127">Start time of the query.</span><span class="sxs-lookup"><span data-stu-id="fb21d-127">Start time of the query.</span></span> <span data-ttu-id="fb21d-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span><span class="sxs-lookup"><span data-stu-id="fb21d-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span></span> <span data-ttu-id="fb21d-129">For daily aggregation, set this value to UTC midnight.</span><span class="sxs-lookup"><span data-stu-id="fb21d-129">For daily aggregation, set this value to UTC midnight.</span></span> <span data-ttu-id="fb21d-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span><span class="sxs-lookup"><span data-stu-id="fb21d-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="fb21d-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="fb21d-131">*reportedEndTime*</span></span> |<span data-ttu-id="fb21d-132">End time of the query.</span><span class="sxs-lookup"><span data-stu-id="fb21d-132">End time of the query.</span></span> <span data-ttu-id="fb21d-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span><span class="sxs-lookup"><span data-stu-id="fb21d-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span></span> <span data-ttu-id="fb21d-134">The value for *reportedEndTime* cannot be in the future.</span><span class="sxs-lookup"><span data-stu-id="fb21d-134">The value for *reportedEndTime* cannot be in the future.</span></span> |
| <span data-ttu-id="fb21d-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="fb21d-135">*aggregationGranularity*</span></span> |<span data-ttu-id="fb21d-136">Optional parameter that has two discrete potential values: daily and hourly.</span><span class="sxs-lookup"><span data-stu-id="fb21d-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="fb21d-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span><span class="sxs-lookup"><span data-stu-id="fb21d-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span></span> <span data-ttu-id="fb21d-138">The daily option is the default.</span><span class="sxs-lookup"><span data-stu-id="fb21d-138">The daily option is the default.</span></span> |
| <span data-ttu-id="fb21d-139">*api-version*</span><span class="sxs-lookup"><span data-stu-id="fb21d-139">*api-version*</span></span> |<span data-ttu-id="fb21d-140">Version of the protocol that is used to make this request.</span><span class="sxs-lookup"><span data-stu-id="fb21d-140">Version of the protocol that is used to make this request.</span></span> <span data-ttu-id="fb21d-141">You must use 2015-06-01-preview.</span><span class="sxs-lookup"><span data-stu-id="fb21d-141">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="fb21d-142">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="fb21d-142">*continuationToken*</span></span> |<span data-ttu-id="fb21d-143">Token retrieved from the last call to the Usage API provider.</span><span class="sxs-lookup"><span data-stu-id="fb21d-143">Token retrieved from the last call to the Usage API provider.</span></span> <span data-ttu-id="fb21d-144">This is needed when a response is greater than 1,000 lines.</span><span class="sxs-lookup"><span data-stu-id="fb21d-144">This is needed when a response is greater than 1,000 lines.</span></span> <span data-ttu-id="fb21d-145">This is the bookmark for progress.</span><span class="sxs-lookup"><span data-stu-id="fb21d-145">This is the bookmark for progress.</span></span> <span data-ttu-id="fb21d-146">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span><span class="sxs-lookup"><span data-stu-id="fb21d-146">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="fb21d-147">Response</span><span class="sxs-lookup"><span data-stu-id="fb21d-147">Response</span></span>
<span data-ttu-id="fb21d-148">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="fb21d-148">GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0</span></span>

<span data-ttu-id="fb21d-149">{</span><span class="sxs-lookup"><span data-stu-id="fb21d-149">{</span></span>

<span data-ttu-id="fb21d-150">"value": \[</span><span class="sxs-lookup"><span data-stu-id="fb21d-150">"value": \[</span></span>

<span data-ttu-id="fb21d-151">{</span><span class="sxs-lookup"><span data-stu-id="fb21d-151">{</span></span>

<span data-ttu-id="fb21d-152">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="fb21d-152">"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",</span></span>

<span data-ttu-id="fb21d-153">"name": "sub1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="fb21d-153">"name": "sub1-meterID1",</span></span>

<span data-ttu-id="fb21d-154">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="fb21d-154">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="fb21d-155">"properties": {</span><span class="sxs-lookup"><span data-stu-id="fb21d-155">"properties": {</span></span>

<span data-ttu-id="fb21d-156">"subscriptionId":"sub1",</span><span class="sxs-lookup"><span data-stu-id="fb21d-156">"subscriptionId":"sub1",</span></span>

<span data-ttu-id="fb21d-157">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="fb21d-157">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="fb21d-158">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="fb21d-158">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="fb21d-159">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="fb21d-159">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="fb21d-160">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="fb21d-160">"quantity":2.4000000000,</span></span>

<span data-ttu-id="fb21d-161">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="fb21d-161">"meterId":"meterID1"</span></span>

<span data-ttu-id="fb21d-162">}</span><span class="sxs-lookup"><span data-stu-id="fb21d-162">}</span></span>

<span data-ttu-id="fb21d-163">},</span><span class="sxs-lookup"><span data-stu-id="fb21d-163">},</span></span>

<span data-ttu-id="fb21d-164">…</span><span class="sxs-lookup"><span data-stu-id="fb21d-164">…</span></span>

### <a name="response-details"></a><span data-ttu-id="fb21d-165">Response details</span><span class="sxs-lookup"><span data-stu-id="fb21d-165">Response details</span></span>
| <span data-ttu-id="fb21d-166">**Argument**</span><span class="sxs-lookup"><span data-stu-id="fb21d-166">**Argument**</span></span> | <span data-ttu-id="fb21d-167">**Description**</span><span class="sxs-lookup"><span data-stu-id="fb21d-167">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fb21d-168">*id*</span><span class="sxs-lookup"><span data-stu-id="fb21d-168">*id*</span></span> |<span data-ttu-id="fb21d-169">Unique ID of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="fb21d-169">Unique ID of the usage aggregate</span></span> |
| <span data-ttu-id="fb21d-170">*name*</span><span class="sxs-lookup"><span data-stu-id="fb21d-170">*name*</span></span> |<span data-ttu-id="fb21d-171">Name of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="fb21d-171">Name of the usage aggregate</span></span> |
| <span data-ttu-id="fb21d-172">*type*</span><span class="sxs-lookup"><span data-stu-id="fb21d-172">*type*</span></span> |<span data-ttu-id="fb21d-173">Resource definition</span><span class="sxs-lookup"><span data-stu-id="fb21d-173">Resource definition</span></span> |
| <span data-ttu-id="fb21d-174">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="fb21d-174">*subscriptionId*</span></span> |<span data-ttu-id="fb21d-175">Subscription identifier of the Azure user</span><span class="sxs-lookup"><span data-stu-id="fb21d-175">Subscription identifier of the Azure user</span></span> |
| <span data-ttu-id="fb21d-176">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="fb21d-176">*usageStartTime*</span></span> |<span data-ttu-id="fb21d-177">UTC start time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="fb21d-177">UTC start time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="fb21d-178">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="fb21d-178">*usageEndTime*</span></span> |<span data-ttu-id="fb21d-179">UTC end time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="fb21d-179">UTC end time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="fb21d-180">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="fb21d-180">*instanceData*</span></span> |<span data-ttu-id="fb21d-181">Key-value pairs of instance details (in a new format):</span><span class="sxs-lookup"><span data-stu-id="fb21d-181">Key-value pairs of instance details (in a new format):</span></span><br>  <span data-ttu-id="fb21d-182">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span><span class="sxs-lookup"><span data-stu-id="fb21d-182">*resourceUri*: Fully qualified resource ID, including resource groups and instance name</span></span> <br>  <span data-ttu-id="fb21d-183">*location*: Region in which this service was run</span><span class="sxs-lookup"><span data-stu-id="fb21d-183">*location*: Region in which this service was run</span></span> <br>  <span data-ttu-id="fb21d-184">*tags*: Resource tags that the user specifies</span><span class="sxs-lookup"><span data-stu-id="fb21d-184">*tags*: Resource tags that the user specifies</span></span> <br>  <span data-ttu-id="fb21d-185">*additionalInfo*: More details about the resource being consumed, for example, OS version or image type</span><span class="sxs-lookup"><span data-stu-id="fb21d-185">*additionalInfo*: More details about the resource being consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="fb21d-186">*quantity*</span><span class="sxs-lookup"><span data-stu-id="fb21d-186">*quantity*</span></span> |<span data-ttu-id="fb21d-187">Amount of resource consumption that occurred in this time frame</span><span class="sxs-lookup"><span data-stu-id="fb21d-187">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="fb21d-188">*meterId*</span><span class="sxs-lookup"><span data-stu-id="fb21d-188">*meterId*</span></span> |<span data-ttu-id="fb21d-189">Unique ID for the resource that was consumed (also called *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="fb21d-189">Unique ID for the resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb21d-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb21d-190">Next steps</span></span>
[<span data-ttu-id="fb21d-191">Provider resource usage API</span><span class="sxs-lookup"><span data-stu-id="fb21d-191">Provider resource usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="fb21d-192">Usage-related FAQ</span><span class="sxs-lookup"><span data-stu-id="fb21d-192">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

