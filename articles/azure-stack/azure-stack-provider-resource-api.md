---
title: Provider Resource Usage API | Microsoft Docs
description: Reference for resource usage API, which retrieve Azure Stack usage information.
services: azure-stack
documentationcenter: ''
author: AlfredoPizzirani
manager: byronr
editor: ''
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2016
ms.author: alfredop
ms.openlocfilehash: 28b27a7740a299ebcb1055d957e547188cf28e31
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669298"
---
# <a name="provider-resource-usage-api"></a><span data-ttu-id="a6f09-103">Provider Resource Usage API</span><span class="sxs-lookup"><span data-stu-id="a6f09-103">Provider Resource Usage API</span></span>
<span data-ttu-id="a6f09-104">The term provider applies to the service administrator and to any delegated providers.</span><span class="sxs-lookup"><span data-stu-id="a6f09-104">The term provider applies to the service administrator and to any delegated providers.</span></span> <span data-ttu-id="a6f09-105">Service admins and delegated providers can use the Provider Usage API to view the usage of their direct tenants.</span><span class="sxs-lookup"><span data-stu-id="a6f09-105">Service admins and delegated providers can use the Provider Usage API to view the usage of their direct tenants.</span></span> <span data-ttu-id="a6f09-106">For example, P0 can call the Provider API to get usage information on P1's and P2's direct usage, and P1 can call for usage information on P3 and P4.</span><span class="sxs-lookup"><span data-stu-id="a6f09-106">For example, P0 can call the Provider API to get usage information on P1's and P2's direct usage, and P1 can call for usage information on P3 and P4.</span></span>

![Conceptual model of provider hierarchy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a><span data-ttu-id="a6f09-108">API call reference</span><span class="sxs-lookup"><span data-stu-id="a6f09-108">API call reference</span></span>
### <a name="request"></a><span data-ttu-id="a6f09-109">Request</span><span class="sxs-lookup"><span data-stu-id="a6f09-109">Request</span></span>
<span data-ttu-id="a6f09-110">The request gets consumption details for the requested subscriptions and for the requested time frame.</span><span class="sxs-lookup"><span data-stu-id="a6f09-110">The request gets consumption details for the requested subscriptions and for the requested time frame.</span></span> <span data-ttu-id="a6f09-111">There is no request body.</span><span class="sxs-lookup"><span data-stu-id="a6f09-111">There is no request body.</span></span>

<span data-ttu-id="a6f09-112">This usage API is a Provider API, so the caller must be assigned an Owner, Contributor, or Reader role in the provider’s subscription.</span><span class="sxs-lookup"><span data-stu-id="a6f09-112">This usage API is a Provider API, so the caller must be assigned an Owner, Contributor, or Reader role in the provider’s subscription.</span></span>

| <span data-ttu-id="a6f09-113">**Method**</span><span class="sxs-lookup"><span data-stu-id="a6f09-113">**Method**</span></span> | <span data-ttu-id="a6f09-114">**Request URI**</span><span class="sxs-lookup"><span data-stu-id="a6f09-114">**Request URI**</span></span> |
| --- | --- |
| <span data-ttu-id="a6f09-115">GET</span><span class="sxs-lookup"><span data-stu-id="a6f09-115">GET</span></span> |<span data-ttu-id="a6f09-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span><span class="sxs-lookup"><span data-stu-id="a6f09-116">https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value}</span></span> |

### <a name="arguments"></a><span data-ttu-id="a6f09-117">Arguments</span><span class="sxs-lookup"><span data-stu-id="a6f09-117">Arguments</span></span>
| <span data-ttu-id="a6f09-118">**Argument**</span><span class="sxs-lookup"><span data-stu-id="a6f09-118">**Argument**</span></span> | <span data-ttu-id="a6f09-119">**Description**</span><span class="sxs-lookup"><span data-stu-id="a6f09-119">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a6f09-120">*armendpoint*</span><span class="sxs-lookup"><span data-stu-id="a6f09-120">*armendpoint*</span></span> |<span data-ttu-id="a6f09-121">Azure Resource Manager endpoint of your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="a6f09-121">Azure Resource Manager endpoint of your Azure Stack environment.</span></span> <span data-ttu-id="a6f09-122">The Azure Stack convention is that the name of ARM endpoint is in the format `https://adminmanagement.{domain-name}`.</span><span class="sxs-lookup"><span data-stu-id="a6f09-122">The Azure Stack convention is that the name of ARM endpoint is in the format `https://adminmanagement.{domain-name}`.</span></span> <span data-ttu-id="a6f09-123">For example, if the domain name is local.azurestack.external, then the Resource Manager endpoint will be `https://adminmanagement.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="a6f09-123">For example, if the domain name is local.azurestack.external, then the Resource Manager endpoint will be `https://adminmanagement.local.azurestack.external`.</span></span> |
| <span data-ttu-id="a6f09-124">*subId*</span><span class="sxs-lookup"><span data-stu-id="a6f09-124">*subId*</span></span> |<span data-ttu-id="a6f09-125">Subscription ID of the user who is making the call.</span><span class="sxs-lookup"><span data-stu-id="a6f09-125">Subscription ID of the user who is making the call.</span></span> |
| <span data-ttu-id="a6f09-126">*reportedStartTime*</span><span class="sxs-lookup"><span data-stu-id="a6f09-126">*reportedStartTime*</span></span> |<span data-ttu-id="a6f09-127">Start time of the query.</span><span class="sxs-lookup"><span data-stu-id="a6f09-127">Start time of the query.</span></span> <span data-ttu-id="a6f09-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span><span class="sxs-lookup"><span data-stu-id="a6f09-128">The value for *DateTime* should be in UTC and at the beginning of the hour, for example, 13:00.</span></span> <span data-ttu-id="a6f09-129">For daily aggregation, set this value to UTC midnight.</span><span class="sxs-lookup"><span data-stu-id="a6f09-129">For daily aggregation, set this value to UTC midnight.</span></span> <span data-ttu-id="a6f09-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span><span class="sxs-lookup"><span data-stu-id="a6f09-130">The format is *escaped* ISO 8601, for example, 2015-06-16T18%3a53%3a11%2b00%3a00Z, where colon is escaped to %3a and plus is escaped to %2b so that it is URI friendly.</span></span> |
| <span data-ttu-id="a6f09-131">*reportedEndTime*</span><span class="sxs-lookup"><span data-stu-id="a6f09-131">*reportedEndTime*</span></span> |<span data-ttu-id="a6f09-132">End time of the query.</span><span class="sxs-lookup"><span data-stu-id="a6f09-132">End time of the query.</span></span> <span data-ttu-id="a6f09-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span><span class="sxs-lookup"><span data-stu-id="a6f09-133">The constraints that apply to *reportedStartTime* also apply to this argument.</span></span> <span data-ttu-id="a6f09-134">The value for *reportedEndTime* cannot be in the future.</span><span class="sxs-lookup"><span data-stu-id="a6f09-134">The value for *reportedEndTime* cannot be in the future.</span></span> |
| <span data-ttu-id="a6f09-135">*aggregationGranularity*</span><span class="sxs-lookup"><span data-stu-id="a6f09-135">*aggregationGranularity*</span></span> |<span data-ttu-id="a6f09-136">Optional parameter that has two discrete potential values: daily and hourly.</span><span class="sxs-lookup"><span data-stu-id="a6f09-136">Optional parameter that has two discrete potential values: daily and hourly.</span></span> <span data-ttu-id="a6f09-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span><span class="sxs-lookup"><span data-stu-id="a6f09-137">As the values suggest, one returns the data in daily granularity, and the other is an hourly resolution.</span></span> <span data-ttu-id="a6f09-138">The daily option is the default.</span><span class="sxs-lookup"><span data-stu-id="a6f09-138">The daily option is the default.</span></span> |
| <span data-ttu-id="a6f09-139">*subscriberId*</span><span class="sxs-lookup"><span data-stu-id="a6f09-139">*subscriberId*</span></span> |<span data-ttu-id="a6f09-140">Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="a6f09-140">Subscription ID.</span></span> <span data-ttu-id="a6f09-141">To get filtered data, the subscription ID of a direct tenant of the provider is required.</span><span class="sxs-lookup"><span data-stu-id="a6f09-141">To get filtered data, the subscription ID of a direct tenant of the provider is required.</span></span> <span data-ttu-id="a6f09-142">If no subscription ID parameter is specified, the call returns usage data for all the provider’s direct tenants.</span><span class="sxs-lookup"><span data-stu-id="a6f09-142">If no subscription ID parameter is specified, the call returns usage data for all the provider’s direct tenants.</span></span> |
| <span data-ttu-id="a6f09-143">*api-version*</span><span class="sxs-lookup"><span data-stu-id="a6f09-143">*api-version*</span></span> |<span data-ttu-id="a6f09-144">Version of the protocol that is used to make this request.</span><span class="sxs-lookup"><span data-stu-id="a6f09-144">Version of the protocol that is used to make this request.</span></span> <span data-ttu-id="a6f09-145">You must use 2015-06-01-preview.</span><span class="sxs-lookup"><span data-stu-id="a6f09-145">You must use 2015-06-01-preview.</span></span> |
| <span data-ttu-id="a6f09-146">*continuationToken*</span><span class="sxs-lookup"><span data-stu-id="a6f09-146">*continuationToken*</span></span> |<span data-ttu-id="a6f09-147">Token retrieved from the last call to the Usage API provider.</span><span class="sxs-lookup"><span data-stu-id="a6f09-147">Token retrieved from the last call to the Usage API provider.</span></span> <span data-ttu-id="a6f09-148">This is needed when a response is greater than 1,000 lines.</span><span class="sxs-lookup"><span data-stu-id="a6f09-148">This is needed when a response is greater than 1,000 lines.</span></span> <span data-ttu-id="a6f09-149">This is the bookmark for progress.</span><span class="sxs-lookup"><span data-stu-id="a6f09-149">This is the bookmark for progress.</span></span> <span data-ttu-id="a6f09-150">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span><span class="sxs-lookup"><span data-stu-id="a6f09-150">If not present, the data is retrieved from the beginning of the day or hour, based on the granularity passed in.</span></span> |

### <a name="response"></a><span data-ttu-id="a6f09-151">Response</span><span class="sxs-lookup"><span data-stu-id="a6f09-151">Response</span></span>
<span data-ttu-id="a6f09-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span><span class="sxs-lookup"><span data-stu-id="a6f09-152">GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0</span></span>

<span data-ttu-id="a6f09-153">{</span><span class="sxs-lookup"><span data-stu-id="a6f09-153">{</span></span>

<span data-ttu-id="a6f09-154">"value": \[</span><span class="sxs-lookup"><span data-stu-id="a6f09-154">"value": \[</span></span>

<span data-ttu-id="a6f09-155">{</span><span class="sxs-lookup"><span data-stu-id="a6f09-155">{</span></span>

<span data-ttu-id="a6f09-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span><span class="sxs-lookup"><span data-stu-id="a6f09-156">"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-</span></span>

<span data-ttu-id="a6f09-157">meterID1",</span><span class="sxs-lookup"><span data-stu-id="a6f09-157">meterID1",</span></span>

<span data-ttu-id="a6f09-158">"name": "sub1.1-meterID1",</span><span class="sxs-lookup"><span data-stu-id="a6f09-158">"name": "sub1.1-meterID1",</span></span>

<span data-ttu-id="a6f09-159">"type": "Microsoft.Commerce/UsageAggregate",</span><span class="sxs-lookup"><span data-stu-id="a6f09-159">"type": "Microsoft.Commerce/UsageAggregate",</span></span>

<span data-ttu-id="a6f09-160">"properties": {</span><span class="sxs-lookup"><span data-stu-id="a6f09-160">"properties": {</span></span>

<span data-ttu-id="a6f09-161">"subscriptionId":"sub1.1",</span><span class="sxs-lookup"><span data-stu-id="a6f09-161">"subscriptionId":"sub1.1",</span></span>

<span data-ttu-id="a6f09-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="a6f09-162">"usageStartTime": "2015-03-03T00:00:00+00:00",</span></span>

<span data-ttu-id="a6f09-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span><span class="sxs-lookup"><span data-stu-id="a6f09-163">"usageEndTime": "2015-03-04T00:00:00+00:00",</span></span>

<span data-ttu-id="a6f09-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span><span class="sxs-lookup"><span data-stu-id="a6f09-164">"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\</span></span>

<span data-ttu-id="a6f09-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span><span class="sxs-lookup"><span data-stu-id="a6f09-165">":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",</span></span>

<span data-ttu-id="a6f09-166">"quantity":2.4000000000,</span><span class="sxs-lookup"><span data-stu-id="a6f09-166">"quantity":2.4000000000,</span></span>

<span data-ttu-id="a6f09-167">"meterId":"meterID1"</span><span class="sxs-lookup"><span data-stu-id="a6f09-167">"meterId":"meterID1"</span></span>

<span data-ttu-id="a6f09-168">}</span><span class="sxs-lookup"><span data-stu-id="a6f09-168">}</span></span>

<span data-ttu-id="a6f09-169">},</span><span class="sxs-lookup"><span data-stu-id="a6f09-169">},</span></span>

<span data-ttu-id="a6f09-170">…</span><span class="sxs-lookup"><span data-stu-id="a6f09-170">…</span></span>

### <a name="response-details"></a><span data-ttu-id="a6f09-171">Response details</span><span class="sxs-lookup"><span data-stu-id="a6f09-171">Response details</span></span>
| <span data-ttu-id="a6f09-172">**Argument**</span><span class="sxs-lookup"><span data-stu-id="a6f09-172">**Argument**</span></span> | <span data-ttu-id="a6f09-173">**Description**</span><span class="sxs-lookup"><span data-stu-id="a6f09-173">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a6f09-174">*id*</span><span class="sxs-lookup"><span data-stu-id="a6f09-174">*id*</span></span> |<span data-ttu-id="a6f09-175">Unique ID of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="a6f09-175">Unique ID of the usage aggregate</span></span> |
| <span data-ttu-id="a6f09-176">*name*</span><span class="sxs-lookup"><span data-stu-id="a6f09-176">*name*</span></span> |<span data-ttu-id="a6f09-177">Name of the usage aggregate</span><span class="sxs-lookup"><span data-stu-id="a6f09-177">Name of the usage aggregate</span></span> |
| <span data-ttu-id="a6f09-178">*type*</span><span class="sxs-lookup"><span data-stu-id="a6f09-178">*type*</span></span> |<span data-ttu-id="a6f09-179">Resource definition</span><span class="sxs-lookup"><span data-stu-id="a6f09-179">Resource definition</span></span> |
| <span data-ttu-id="a6f09-180">*subscriptionId*</span><span class="sxs-lookup"><span data-stu-id="a6f09-180">*subscriptionId*</span></span> |<span data-ttu-id="a6f09-181">Subscription identifier of the Azure Stack user</span><span class="sxs-lookup"><span data-stu-id="a6f09-181">Subscription identifier of the Azure Stack user</span></span> |
| <span data-ttu-id="a6f09-182">*usageStartTime*</span><span class="sxs-lookup"><span data-stu-id="a6f09-182">*usageStartTime*</span></span> |<span data-ttu-id="a6f09-183">UTC start time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="a6f09-183">UTC start time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="a6f09-184">*usageEndTime*</span><span class="sxs-lookup"><span data-stu-id="a6f09-184">*usageEndTime*</span></span> |<span data-ttu-id="a6f09-185">UTC end time of the usage bucket to which this usage aggregate belongs</span><span class="sxs-lookup"><span data-stu-id="a6f09-185">UTC end time of the usage bucket to which this usage aggregate belongs</span></span> |
| <span data-ttu-id="a6f09-186">*instanceData*</span><span class="sxs-lookup"><span data-stu-id="a6f09-186">*instanceData*</span></span> |<span data-ttu-id="a6f09-187">Key-value pairs of instance details (in a new format):</span><span class="sxs-lookup"><span data-stu-id="a6f09-187">Key-value pairs of instance details (in a new format):</span></span><br> <span data-ttu-id="a6f09-188">*resourceUri*: Fully qualified resource ID, which includes the resource groups and the instance name</span><span class="sxs-lookup"><span data-stu-id="a6f09-188">*resourceUri*: Fully qualified resource ID, which includes the resource groups and the instance name</span></span> <br> <span data-ttu-id="a6f09-189">*location*: Region in which this service was run</span><span class="sxs-lookup"><span data-stu-id="a6f09-189">*location*: Region in which this service was run</span></span> <br> <span data-ttu-id="a6f09-190">*tags*: Resource tags that are specified by the user</span><span class="sxs-lookup"><span data-stu-id="a6f09-190">*tags*: Resource tags that are specified by the user</span></span> <br> <span data-ttu-id="a6f09-191">*additionalInfo*: More details about the resource being consumed, for example, OS version or image type</span><span class="sxs-lookup"><span data-stu-id="a6f09-191">*additionalInfo*: More details about the resource being consumed, for example, OS version or image type</span></span> |
| <span data-ttu-id="a6f09-192">*quantity*</span><span class="sxs-lookup"><span data-stu-id="a6f09-192">*quantity*</span></span> |<span data-ttu-id="a6f09-193">Amount of resource consumption that occurred in this time frame</span><span class="sxs-lookup"><span data-stu-id="a6f09-193">Amount of resource consumption that occurred in this time frame</span></span> |
| <span data-ttu-id="a6f09-194">*meterId*</span><span class="sxs-lookup"><span data-stu-id="a6f09-194">*meterId*</span></span> |<span data-ttu-id="a6f09-195">Unique ID for the resource that was consumed (also called *ResourceID*)</span><span class="sxs-lookup"><span data-stu-id="a6f09-195">Unique ID for the resource that was consumed (also called *ResourceID*)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6f09-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6f09-196">Next steps</span></span>
[<span data-ttu-id="a6f09-197">Tenant resource usage API reference</span><span class="sxs-lookup"><span data-stu-id="a6f09-197">Tenant resource usage API reference</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="a6f09-198">Usage-related FAQ</span><span class="sxs-lookup"><span data-stu-id="a6f09-198">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)


