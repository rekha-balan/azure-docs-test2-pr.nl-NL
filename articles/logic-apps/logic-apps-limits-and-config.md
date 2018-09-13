---
title: Logic App limits and configuration | Microsoft Docs
description: Overview of the service limits and configuration values available for Logic Apps.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: jehollan
ms.openlocfilehash: f09c231baecf2452a6e3abd196748629f13885ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551679"
---
# <a name="logic-app-limits-and-configuration"></a><span data-ttu-id="fed08-103">Logic App limits and configuration</span><span class="sxs-lookup"><span data-stu-id="fed08-103">Logic App limits and configuration</span></span>

<span data-ttu-id="fed08-104">Below are information on the current limits and configuration details for Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="fed08-104">Below are information on the current limits and configuration details for Azure Logic Apps.</span></span>

## <a name="limits"></a><span data-ttu-id="fed08-105">Limits</span><span class="sxs-lookup"><span data-stu-id="fed08-105">Limits</span></span>

### <a name="http-request-limits"></a><span data-ttu-id="fed08-106">HTTP request limits</span><span class="sxs-lookup"><span data-stu-id="fed08-106">HTTP request limits</span></span>

<span data-ttu-id="fed08-107">These are limits for a single HTTP request and/or connector call</span><span class="sxs-lookup"><span data-stu-id="fed08-107">These are limits for a single HTTP request and/or connector call</span></span>

#### <a name="timeout"></a><span data-ttu-id="fed08-108">Timeout</span><span class="sxs-lookup"><span data-stu-id="fed08-108">Timeout</span></span>

|<span data-ttu-id="fed08-109">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-109">Name</span></span>|<span data-ttu-id="fed08-110">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-110">Limit</span></span>|<span data-ttu-id="fed08-111">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-111">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-112">Request Timeout</span><span class="sxs-lookup"><span data-stu-id="fed08-112">Request Timeout</span></span>|<span data-ttu-id="fed08-113">120 Seconds</span><span class="sxs-lookup"><span data-stu-id="fed08-113">120 Seconds</span></span>|<span data-ttu-id="fed08-114">An [async pattern](../logic-apps/logic-apps-create-api-app.md) or [until loop](logic-apps-loops-and-scopes.md) can compensate as needed</span><span class="sxs-lookup"><span data-stu-id="fed08-114">An [async pattern](../logic-apps/logic-apps-create-api-app.md) or [until loop](logic-apps-loops-and-scopes.md) can compensate as needed</span></span>|

#### <a name="message-size"></a><span data-ttu-id="fed08-115">Message size</span><span class="sxs-lookup"><span data-stu-id="fed08-115">Message size</span></span>

|<span data-ttu-id="fed08-116">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-116">Name</span></span>|<span data-ttu-id="fed08-117">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-117">Limit</span></span>|<span data-ttu-id="fed08-118">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-118">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-119">Message size</span><span class="sxs-lookup"><span data-stu-id="fed08-119">Message size</span></span>|<span data-ttu-id="fed08-120">100 MB</span><span class="sxs-lookup"><span data-stu-id="fed08-120">100 MB</span></span>|<span data-ttu-id="fed08-121">Some connectors and APIs may not support 100MB</span><span class="sxs-lookup"><span data-stu-id="fed08-121">Some connectors and APIs may not support 100MB</span></span> |
|<span data-ttu-id="fed08-122">Expression evaluation limit</span><span class="sxs-lookup"><span data-stu-id="fed08-122">Expression evaluation limit</span></span>|<span data-ttu-id="fed08-123">131,072 characters</span><span class="sxs-lookup"><span data-stu-id="fed08-123">131,072 characters</span></span>|<span data-ttu-id="fed08-124">`@concat()`, `@base64()`, `string` cannot be longer than this</span><span class="sxs-lookup"><span data-stu-id="fed08-124">`@concat()`, `@base64()`, `string` cannot be longer than this</span></span>|

#### <a name="retry-policy"></a><span data-ttu-id="fed08-125">Retry policy</span><span class="sxs-lookup"><span data-stu-id="fed08-125">Retry policy</span></span>

|<span data-ttu-id="fed08-126">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-126">Name</span></span>|<span data-ttu-id="fed08-127">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-127">Limit</span></span>|<span data-ttu-id="fed08-128">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-128">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-129">Retry attempts</span><span class="sxs-lookup"><span data-stu-id="fed08-129">Retry attempts</span></span>|<span data-ttu-id="fed08-130">4</span><span class="sxs-lookup"><span data-stu-id="fed08-130">4</span></span>|<span data-ttu-id="fed08-131">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span><span class="sxs-lookup"><span data-stu-id="fed08-131">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span></span>|
|<span data-ttu-id="fed08-132">Retry max delay</span><span class="sxs-lookup"><span data-stu-id="fed08-132">Retry max delay</span></span>|<span data-ttu-id="fed08-133">1 hour</span><span class="sxs-lookup"><span data-stu-id="fed08-133">1 hour</span></span>|<span data-ttu-id="fed08-134">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span><span class="sxs-lookup"><span data-stu-id="fed08-134">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span></span>|
|<span data-ttu-id="fed08-135">Retry min delay</span><span class="sxs-lookup"><span data-stu-id="fed08-135">Retry min delay</span></span>|<span data-ttu-id="fed08-136">5 sec</span><span class="sxs-lookup"><span data-stu-id="fed08-136">5 sec</span></span>|<span data-ttu-id="fed08-137">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span><span class="sxs-lookup"><span data-stu-id="fed08-137">Can configure with the [retry policy parameter](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)</span></span>|

### <a name="run-duration-and-retention"></a><span data-ttu-id="fed08-138">Run duration and retention</span><span class="sxs-lookup"><span data-stu-id="fed08-138">Run duration and retention</span></span>

<span data-ttu-id="fed08-139">These are the limits for a single logic app run.</span><span class="sxs-lookup"><span data-stu-id="fed08-139">These are the limits for a single logic app run.</span></span>

|<span data-ttu-id="fed08-140">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-140">Name</span></span>|<span data-ttu-id="fed08-141">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-141">Limit</span></span>|<span data-ttu-id="fed08-142">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-142">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-143">Run duration</span><span class="sxs-lookup"><span data-stu-id="fed08-143">Run duration</span></span>|<span data-ttu-id="fed08-144">90 days</span><span class="sxs-lookup"><span data-stu-id="fed08-144">90 days</span></span>||
|<span data-ttu-id="fed08-145">Storage retention</span><span class="sxs-lookup"><span data-stu-id="fed08-145">Storage retention</span></span>|<span data-ttu-id="fed08-146">90 days</span><span class="sxs-lookup"><span data-stu-id="fed08-146">90 days</span></span>|<span data-ttu-id="fed08-147">This is from the run start time</span><span class="sxs-lookup"><span data-stu-id="fed08-147">This is from the run start time</span></span>|
|<span data-ttu-id="fed08-148">Min recurrence interval</span><span class="sxs-lookup"><span data-stu-id="fed08-148">Min recurrence interval</span></span>|<span data-ttu-id="fed08-149">1 sec</span><span class="sxs-lookup"><span data-stu-id="fed08-149">1 sec</span></span>|| <span data-ttu-id="fed08-150">15 seconds for logic apps with App Service Plan</span><span class="sxs-lookup"><span data-stu-id="fed08-150">15 seconds for logic apps with App Service Plan</span></span>
|<span data-ttu-id="fed08-151">Max recurrence interval</span><span class="sxs-lookup"><span data-stu-id="fed08-151">Max recurrence interval</span></span>|<span data-ttu-id="fed08-152">500 days</span><span class="sxs-lookup"><span data-stu-id="fed08-152">500 days</span></span>||


### <a name="looping-and-debatching-limits"></a><span data-ttu-id="fed08-153">Looping and debatching limits</span><span class="sxs-lookup"><span data-stu-id="fed08-153">Looping and debatching limits</span></span>

<span data-ttu-id="fed08-154">These are limits for a single logic app run.</span><span class="sxs-lookup"><span data-stu-id="fed08-154">These are limits for a single logic app run.</span></span>

|<span data-ttu-id="fed08-155">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-155">Name</span></span>|<span data-ttu-id="fed08-156">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-156">Limit</span></span>|<span data-ttu-id="fed08-157">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-157">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-158">ForEach items</span><span class="sxs-lookup"><span data-stu-id="fed08-158">ForEach items</span></span>|<span data-ttu-id="fed08-159">100,000</span><span class="sxs-lookup"><span data-stu-id="fed08-159">100,000</span></span>|<span data-ttu-id="fed08-160">You can use the [query action](../connectors/connectors-native-query.md) to filter larger arrays as needed</span><span class="sxs-lookup"><span data-stu-id="fed08-160">You can use the [query action](../connectors/connectors-native-query.md) to filter larger arrays as needed</span></span>|
|<span data-ttu-id="fed08-161">Until iterations</span><span class="sxs-lookup"><span data-stu-id="fed08-161">Until iterations</span></span>|<span data-ttu-id="fed08-162">5,000</span><span class="sxs-lookup"><span data-stu-id="fed08-162">5,000</span></span>||
|<span data-ttu-id="fed08-163">SplitOn items</span><span class="sxs-lookup"><span data-stu-id="fed08-163">SplitOn items</span></span>|<span data-ttu-id="fed08-164">100,000</span><span class="sxs-lookup"><span data-stu-id="fed08-164">100,000</span></span>||
|<span data-ttu-id="fed08-165">ForEach Parallelism</span><span class="sxs-lookup"><span data-stu-id="fed08-165">ForEach Parallelism</span></span>|<span data-ttu-id="fed08-166">20</span><span class="sxs-lookup"><span data-stu-id="fed08-166">20</span></span>|<span data-ttu-id="fed08-167">You can set to a sequential foreach by adding `"operationOptions": "Sequential"` to the `foreach` action</span><span class="sxs-lookup"><span data-stu-id="fed08-167">You can set to a sequential foreach by adding `"operationOptions": "Sequential"` to the `foreach` action</span></span>|


### <a name="throughput-limits"></a><span data-ttu-id="fed08-168">Throughput limits</span><span class="sxs-lookup"><span data-stu-id="fed08-168">Throughput limits</span></span>

<span data-ttu-id="fed08-169">These are limits for a single logic app instance.</span><span class="sxs-lookup"><span data-stu-id="fed08-169">These are limits for a single logic app instance.</span></span> 

|<span data-ttu-id="fed08-170">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-170">Name</span></span>|<span data-ttu-id="fed08-171">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-171">Limit</span></span>|<span data-ttu-id="fed08-172">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-172">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-173">Actions executions per 5 minutes</span><span class="sxs-lookup"><span data-stu-id="fed08-173">Actions executions per 5 minutes</span></span> |<span data-ttu-id="fed08-174">100,000</span><span class="sxs-lookup"><span data-stu-id="fed08-174">100,000</span></span>|<span data-ttu-id="fed08-175">Can distribute workload across multiple apps as needed</span><span class="sxs-lookup"><span data-stu-id="fed08-175">Can distribute workload across multiple apps as needed</span></span>|

<span data-ttu-id="fed08-176">If you expect to exceed this limit in normal processing or wish to run load testing that may exceed this limit for a period of time please [contact us](mailto://logicappsemail@microsoft.com) so that we can help with your requirements.</span><span class="sxs-lookup"><span data-stu-id="fed08-176">If you expect to exceed this limit in normal processing or wish to run load testing that may exceed this limit for a period of time please [contact us](mailto://logicappsemail@microsoft.com) so that we can help with your requirements.</span></span>

### <a name="definition-limits"></a><span data-ttu-id="fed08-177">Definition limits</span><span class="sxs-lookup"><span data-stu-id="fed08-177">Definition limits</span></span>

<span data-ttu-id="fed08-178">These are limits for a single logic app definition.</span><span class="sxs-lookup"><span data-stu-id="fed08-178">These are limits for a single logic app definition.</span></span>

|<span data-ttu-id="fed08-179">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-179">Name</span></span>|<span data-ttu-id="fed08-180">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-180">Limit</span></span>|<span data-ttu-id="fed08-181">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-181">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-182">Actions per workflow</span><span class="sxs-lookup"><span data-stu-id="fed08-182">Actions per workflow</span></span>|<span data-ttu-id="fed08-183">250</span><span class="sxs-lookup"><span data-stu-id="fed08-183">250</span></span>|<span data-ttu-id="fed08-184">You can add nested workflows to extend this as needed</span><span class="sxs-lookup"><span data-stu-id="fed08-184">You can add nested workflows to extend this as needed</span></span>|
|<span data-ttu-id="fed08-185">Allowed action nesting depth</span><span class="sxs-lookup"><span data-stu-id="fed08-185">Allowed action nesting depth</span></span>|<span data-ttu-id="fed08-186">5</span><span class="sxs-lookup"><span data-stu-id="fed08-186">5</span></span>|<span data-ttu-id="fed08-187">You can add nested workflows to extend this as needed</span><span class="sxs-lookup"><span data-stu-id="fed08-187">You can add nested workflows to extend this as needed</span></span>|
|<span data-ttu-id="fed08-188">Workflows per region per subscription</span><span class="sxs-lookup"><span data-stu-id="fed08-188">Workflows per region per subscription</span></span>|<span data-ttu-id="fed08-189">1000</span><span class="sxs-lookup"><span data-stu-id="fed08-189">1000</span></span>||
|<span data-ttu-id="fed08-190">Triggers per workflow</span><span class="sxs-lookup"><span data-stu-id="fed08-190">Triggers per workflow</span></span>|<span data-ttu-id="fed08-191">10</span><span class="sxs-lookup"><span data-stu-id="fed08-191">10</span></span>||
|<span data-ttu-id="fed08-192">Max characters per expression</span><span class="sxs-lookup"><span data-stu-id="fed08-192">Max characters per expression</span></span>|<span data-ttu-id="fed08-193">8,192</span><span class="sxs-lookup"><span data-stu-id="fed08-193">8,192</span></span>||
|<span data-ttu-id="fed08-194">Max `trackedProperties` size in characters</span><span class="sxs-lookup"><span data-stu-id="fed08-194">Max `trackedProperties` size in characters</span></span>|<span data-ttu-id="fed08-195">16,000</span><span class="sxs-lookup"><span data-stu-id="fed08-195">16,000</span></span>|
|<span data-ttu-id="fed08-196">`action`/`trigger` name limit</span><span class="sxs-lookup"><span data-stu-id="fed08-196">`action`/`trigger` name limit</span></span>|<span data-ttu-id="fed08-197">80</span><span class="sxs-lookup"><span data-stu-id="fed08-197">80</span></span>||
|<span data-ttu-id="fed08-198">`description` length limit</span><span class="sxs-lookup"><span data-stu-id="fed08-198">`description` length limit</span></span>|<span data-ttu-id="fed08-199">256</span><span class="sxs-lookup"><span data-stu-id="fed08-199">256</span></span>||
|<span data-ttu-id="fed08-200">`parameters` limit</span><span class="sxs-lookup"><span data-stu-id="fed08-200">`parameters` limit</span></span>|<span data-ttu-id="fed08-201">50</span><span class="sxs-lookup"><span data-stu-id="fed08-201">50</span></span>||
|<span data-ttu-id="fed08-202">`outputs` limit</span><span class="sxs-lookup"><span data-stu-id="fed08-202">`outputs` limit</span></span>|<span data-ttu-id="fed08-203">10</span><span class="sxs-lookup"><span data-stu-id="fed08-203">10</span></span>||

### <a name="integration-account-limits"></a><span data-ttu-id="fed08-204">Integration Account limits</span><span class="sxs-lookup"><span data-stu-id="fed08-204">Integration Account limits</span></span>

<span data-ttu-id="fed08-205">These are limits for artifacts added to integration Account</span><span class="sxs-lookup"><span data-stu-id="fed08-205">These are limits for artifacts added to integration Account</span></span>

|<span data-ttu-id="fed08-206">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-206">Name</span></span>|<span data-ttu-id="fed08-207">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-207">Limit</span></span>|<span data-ttu-id="fed08-208">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-208">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-209">Schema</span><span class="sxs-lookup"><span data-stu-id="fed08-209">Schema</span></span>|<span data-ttu-id="fed08-210">8MB</span><span class="sxs-lookup"><span data-stu-id="fed08-210">8MB</span></span>|<span data-ttu-id="fed08-211">You can use [blob URI](logic-apps-enterprise-integration-schemas.md) to upload files larger than 2 MB</span><span class="sxs-lookup"><span data-stu-id="fed08-211">You can use [blob URI](logic-apps-enterprise-integration-schemas.md) to upload files larger than 2 MB</span></span> |
|<span data-ttu-id="fed08-212">Map (XSLT file)</span><span class="sxs-lookup"><span data-stu-id="fed08-212">Map (XSLT file)</span></span>|<span data-ttu-id="fed08-213">2MB</span><span class="sxs-lookup"><span data-stu-id="fed08-213">2MB</span></span>| |

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a><span data-ttu-id="fed08-214">B2B protocols (AS2, X12, EDIFACT) message size</span><span class="sxs-lookup"><span data-stu-id="fed08-214">B2B protocols (AS2, X12, EDIFACT) message size</span></span>

<span data-ttu-id="fed08-215">These are the limits for B2B protocols</span><span class="sxs-lookup"><span data-stu-id="fed08-215">These are the limits for B2B protocols</span></span>

|<span data-ttu-id="fed08-216">Name</span><span class="sxs-lookup"><span data-stu-id="fed08-216">Name</span></span>|<span data-ttu-id="fed08-217">Limit</span><span class="sxs-lookup"><span data-stu-id="fed08-217">Limit</span></span>|<span data-ttu-id="fed08-218">Notes</span><span class="sxs-lookup"><span data-stu-id="fed08-218">Notes</span></span>|
|----|----|----|
|<span data-ttu-id="fed08-219">AS2</span><span class="sxs-lookup"><span data-stu-id="fed08-219">AS2</span></span>|<span data-ttu-id="fed08-220">50MB</span><span class="sxs-lookup"><span data-stu-id="fed08-220">50MB</span></span>|<span data-ttu-id="fed08-221">Applicable to decode and encode</span><span class="sxs-lookup"><span data-stu-id="fed08-221">Applicable to decode and encode</span></span>|
|<span data-ttu-id="fed08-222">X12</span><span class="sxs-lookup"><span data-stu-id="fed08-222">X12</span></span>|<span data-ttu-id="fed08-223">50MB</span><span class="sxs-lookup"><span data-stu-id="fed08-223">50MB</span></span>|<span data-ttu-id="fed08-224">Applicable to decode and encode</span><span class="sxs-lookup"><span data-stu-id="fed08-224">Applicable to decode and encode</span></span>|
|<span data-ttu-id="fed08-225">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="fed08-225">EDIFACT</span></span>|<span data-ttu-id="fed08-226">50MB</span><span class="sxs-lookup"><span data-stu-id="fed08-226">50MB</span></span>|<span data-ttu-id="fed08-227">Applicable to decode and encode</span><span class="sxs-lookup"><span data-stu-id="fed08-227">Applicable to decode and encode</span></span>|

## <a name="configuration"></a><span data-ttu-id="fed08-228">Configuration</span><span class="sxs-lookup"><span data-stu-id="fed08-228">Configuration</span></span>

### <a name="ip-address"></a><span data-ttu-id="fed08-229">IP Address</span><span class="sxs-lookup"><span data-stu-id="fed08-229">IP Address</span></span>

#### <a name="logic-app-service"></a><span data-ttu-id="fed08-230">Logic App Service</span><span class="sxs-lookup"><span data-stu-id="fed08-230">Logic App Service</span></span>

<span data-ttu-id="fed08-231">Calls made from a logic app directly (i.e. via [HTTP](../connectors/connectors-native-http.md) or [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) or other HTTP requests will come from the IP Address specified below:</span><span class="sxs-lookup"><span data-stu-id="fed08-231">Calls made from a logic app directly (i.e. via [HTTP](../connectors/connectors-native-http.md) or [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) or other HTTP requests will come from the IP Address specified below:</span></span>

|<span data-ttu-id="fed08-232">Logic App Region</span><span class="sxs-lookup"><span data-stu-id="fed08-232">Logic App Region</span></span>|<span data-ttu-id="fed08-233">Outbound IP</span><span class="sxs-lookup"><span data-stu-id="fed08-233">Outbound IP</span></span>|
|-----|----|
|<span data-ttu-id="fed08-234">Australia East</span><span class="sxs-lookup"><span data-stu-id="fed08-234">Australia East</span></span>|<span data-ttu-id="fed08-235">13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241</span><span class="sxs-lookup"><span data-stu-id="fed08-235">13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241</span></span>|
|<span data-ttu-id="fed08-236">Australia Southeast</span><span class="sxs-lookup"><span data-stu-id="fed08-236">Australia Southeast</span></span>|<span data-ttu-id="fed08-237">13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205</span><span class="sxs-lookup"><span data-stu-id="fed08-237">13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205</span></span>|
|<span data-ttu-id="fed08-238">Brazil South</span><span class="sxs-lookup"><span data-stu-id="fed08-238">Brazil South</span></span>|<span data-ttu-id="fed08-239">191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26</span><span class="sxs-lookup"><span data-stu-id="fed08-239">191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26</span></span>|
|<span data-ttu-id="fed08-240">Canada Central</span><span class="sxs-lookup"><span data-stu-id="fed08-240">Canada Central</span></span>|<span data-ttu-id="fed08-241">52.233.29.92,52.228.39.241,52.228.39.244</span><span class="sxs-lookup"><span data-stu-id="fed08-241">52.233.29.92,52.228.39.241,52.228.39.244</span></span>|
|<span data-ttu-id="fed08-242">Canada East</span><span class="sxs-lookup"><span data-stu-id="fed08-242">Canada East</span></span>|<span data-ttu-id="fed08-243">52.232.128.155,52.229.120.45,52.229.126.25</span><span class="sxs-lookup"><span data-stu-id="fed08-243">52.232.128.155,52.229.120.45,52.229.126.25</span></span>|
|<span data-ttu-id="fed08-244">Central India</span><span class="sxs-lookup"><span data-stu-id="fed08-244">Central India</span></span>|<span data-ttu-id="fed08-245">52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79</span><span class="sxs-lookup"><span data-stu-id="fed08-245">52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79</span></span>|
|<span data-ttu-id="fed08-246">Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-246">Central US</span></span>|<span data-ttu-id="fed08-247">13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198</span><span class="sxs-lookup"><span data-stu-id="fed08-247">13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198</span></span>|
|<span data-ttu-id="fed08-248">East Asia</span><span class="sxs-lookup"><span data-stu-id="fed08-248">East Asia</span></span>|<span data-ttu-id="fed08-249">168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254</span><span class="sxs-lookup"><span data-stu-id="fed08-249">168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254</span></span>|
|<span data-ttu-id="fed08-250">East US</span><span class="sxs-lookup"><span data-stu-id="fed08-250">East US</span></span>|<span data-ttu-id="fed08-251">137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191</span><span class="sxs-lookup"><span data-stu-id="fed08-251">137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191</span></span>|
|<span data-ttu-id="fed08-252">East US 2</span><span class="sxs-lookup"><span data-stu-id="fed08-252">East US 2</span></span>|<span data-ttu-id="fed08-253">40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174</span><span class="sxs-lookup"><span data-stu-id="fed08-253">40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174</span></span>|
|<span data-ttu-id="fed08-254">Japan East</span><span class="sxs-lookup"><span data-stu-id="fed08-254">Japan East</span></span>|<span data-ttu-id="fed08-255">13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120</span><span class="sxs-lookup"><span data-stu-id="fed08-255">13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120</span></span>|
|<span data-ttu-id="fed08-256">Japan West</span><span class="sxs-lookup"><span data-stu-id="fed08-256">Japan West</span></span>|<span data-ttu-id="fed08-257">40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45</span><span class="sxs-lookup"><span data-stu-id="fed08-257">40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45</span></span>|
|<span data-ttu-id="fed08-258">North Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-258">North Central US</span></span>|<span data-ttu-id="fed08-259">168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238</span><span class="sxs-lookup"><span data-stu-id="fed08-259">168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238</span></span>|
|<span data-ttu-id="fed08-260">North Europe</span><span class="sxs-lookup"><span data-stu-id="fed08-260">North Europe</span></span>|<span data-ttu-id="fed08-261">13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21</span><span class="sxs-lookup"><span data-stu-id="fed08-261">13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21</span></span>|
|<span data-ttu-id="fed08-262">South Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-262">South Central US</span></span>|<span data-ttu-id="fed08-263">13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232</span><span class="sxs-lookup"><span data-stu-id="fed08-263">13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232</span></span>|
|<span data-ttu-id="fed08-264">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="fed08-264">Southeast Asia</span></span>|<span data-ttu-id="fed08-265">52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166</span><span class="sxs-lookup"><span data-stu-id="fed08-265">52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166</span></span>|
|<span data-ttu-id="fed08-266">South India</span><span class="sxs-lookup"><span data-stu-id="fed08-266">South India</span></span>|<span data-ttu-id="fed08-267">52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0</span><span class="sxs-lookup"><span data-stu-id="fed08-267">52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0</span></span>|
|<span data-ttu-id="fed08-268">West Europe</span><span class="sxs-lookup"><span data-stu-id="fed08-268">West Europe</span></span>|<span data-ttu-id="fed08-269">13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65</span><span class="sxs-lookup"><span data-stu-id="fed08-269">13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65</span></span>|
|<span data-ttu-id="fed08-270">West India</span><span class="sxs-lookup"><span data-stu-id="fed08-270">West India</span></span>|<span data-ttu-id="fed08-271">104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136</span><span class="sxs-lookup"><span data-stu-id="fed08-271">104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136</span></span>|
|<span data-ttu-id="fed08-272">West US</span><span class="sxs-lookup"><span data-stu-id="fed08-272">West US</span></span>|<span data-ttu-id="fed08-273">52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243</span><span class="sxs-lookup"><span data-stu-id="fed08-273">52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243</span></span>|

#### <a name="connectors"></a><span data-ttu-id="fed08-274">Connectors</span><span class="sxs-lookup"><span data-stu-id="fed08-274">Connectors</span></span>

<span data-ttu-id="fed08-275">Calls made from a [connector](../connectors/apis-list.md) will come from the IP Address specified below:</span><span class="sxs-lookup"><span data-stu-id="fed08-275">Calls made from a [connector](../connectors/apis-list.md) will come from the IP Address specified below:</span></span>

|<span data-ttu-id="fed08-276">Logic App Region</span><span class="sxs-lookup"><span data-stu-id="fed08-276">Logic App Region</span></span>|<span data-ttu-id="fed08-277">Outbound IP</span><span class="sxs-lookup"><span data-stu-id="fed08-277">Outbound IP</span></span>|
|-----|----|
|<span data-ttu-id="fed08-278">Australia East</span><span class="sxs-lookup"><span data-stu-id="fed08-278">Australia East</span></span>|<span data-ttu-id="fed08-279">40.126.251.213</span><span class="sxs-lookup"><span data-stu-id="fed08-279">40.126.251.213</span></span>|
|<span data-ttu-id="fed08-280">Australia Southeast</span><span class="sxs-lookup"><span data-stu-id="fed08-280">Australia Southeast</span></span>|<span data-ttu-id="fed08-281">40.127.80.34</span><span class="sxs-lookup"><span data-stu-id="fed08-281">40.127.80.34</span></span>|
|<span data-ttu-id="fed08-282">Brazil South</span><span class="sxs-lookup"><span data-stu-id="fed08-282">Brazil South</span></span>|<span data-ttu-id="fed08-283">191.232.38.129</span><span class="sxs-lookup"><span data-stu-id="fed08-283">191.232.38.129</span></span>|
|<span data-ttu-id="fed08-284">Canada Central</span><span class="sxs-lookup"><span data-stu-id="fed08-284">Canada Central</span></span>|<span data-ttu-id="fed08-285">52.233.31.197,52.228.42.205,52.228.33.76,52.228.34.13</span><span class="sxs-lookup"><span data-stu-id="fed08-285">52.233.31.197,52.228.42.205,52.228.33.76,52.228.34.13</span></span>|
|<span data-ttu-id="fed08-286">Canada East</span><span class="sxs-lookup"><span data-stu-id="fed08-286">Canada East</span></span>|<span data-ttu-id="fed08-287">52.229.123.98,52.229.120.178,52.229.126.202,52.229.120.52</span><span class="sxs-lookup"><span data-stu-id="fed08-287">52.229.123.98,52.229.120.178,52.229.126.202,52.229.120.52</span></span>|
|<span data-ttu-id="fed08-288">Central India</span><span class="sxs-lookup"><span data-stu-id="fed08-288">Central India</span></span>|<span data-ttu-id="fed08-289">104.211.98.164</span><span class="sxs-lookup"><span data-stu-id="fed08-289">104.211.98.164</span></span>|
|<span data-ttu-id="fed08-290">Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-290">Central US</span></span>|<span data-ttu-id="fed08-291">40.122.49.51</span><span class="sxs-lookup"><span data-stu-id="fed08-291">40.122.49.51</span></span>|
|<span data-ttu-id="fed08-292">East Asia</span><span class="sxs-lookup"><span data-stu-id="fed08-292">East Asia</span></span>|<span data-ttu-id="fed08-293">23.99.116.181</span><span class="sxs-lookup"><span data-stu-id="fed08-293">23.99.116.181</span></span>|
|<span data-ttu-id="fed08-294">East US</span><span class="sxs-lookup"><span data-stu-id="fed08-294">East US</span></span>|<span data-ttu-id="fed08-295">191.237.41.52</span><span class="sxs-lookup"><span data-stu-id="fed08-295">191.237.41.52</span></span>|
|<span data-ttu-id="fed08-296">East US 2</span><span class="sxs-lookup"><span data-stu-id="fed08-296">East US 2</span></span>|<span data-ttu-id="fed08-297">104.208.233.100</span><span class="sxs-lookup"><span data-stu-id="fed08-297">104.208.233.100</span></span>|
|<span data-ttu-id="fed08-298">Japan East</span><span class="sxs-lookup"><span data-stu-id="fed08-298">Japan East</span></span>|<span data-ttu-id="fed08-299">40.115.186.96</span><span class="sxs-lookup"><span data-stu-id="fed08-299">40.115.186.96</span></span>|
|<span data-ttu-id="fed08-300">Japan West</span><span class="sxs-lookup"><span data-stu-id="fed08-300">Japan West</span></span>|<span data-ttu-id="fed08-301">40.74.130.77</span><span class="sxs-lookup"><span data-stu-id="fed08-301">40.74.130.77</span></span>|
|<span data-ttu-id="fed08-302">North Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-302">North Central US</span></span>|<span data-ttu-id="fed08-303">65.52.218.230</span><span class="sxs-lookup"><span data-stu-id="fed08-303">65.52.218.230</span></span>|
|<span data-ttu-id="fed08-304">North Europe</span><span class="sxs-lookup"><span data-stu-id="fed08-304">North Europe</span></span>|<span data-ttu-id="fed08-305">104.45.93.9</span><span class="sxs-lookup"><span data-stu-id="fed08-305">104.45.93.9</span></span>|
|<span data-ttu-id="fed08-306">South Central US</span><span class="sxs-lookup"><span data-stu-id="fed08-306">South Central US</span></span>|<span data-ttu-id="fed08-307">104.214.70.191</span><span class="sxs-lookup"><span data-stu-id="fed08-307">104.214.70.191</span></span>|
|<span data-ttu-id="fed08-308">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="fed08-308">Southeast Asia</span></span>|<span data-ttu-id="fed08-309">13.76.231.68</span><span class="sxs-lookup"><span data-stu-id="fed08-309">13.76.231.68</span></span>|
|<span data-ttu-id="fed08-310">South India</span><span class="sxs-lookup"><span data-stu-id="fed08-310">South India</span></span>|<span data-ttu-id="fed08-311">104.211.227.225</span><span class="sxs-lookup"><span data-stu-id="fed08-311">104.211.227.225</span></span>|
|<span data-ttu-id="fed08-312">West Europe</span><span class="sxs-lookup"><span data-stu-id="fed08-312">West Europe</span></span>|<span data-ttu-id="fed08-313">40.115.50.13</span><span class="sxs-lookup"><span data-stu-id="fed08-313">40.115.50.13</span></span>|
|<span data-ttu-id="fed08-314">West India</span><span class="sxs-lookup"><span data-stu-id="fed08-314">West India</span></span>|<span data-ttu-id="fed08-315">104.211.161.203</span><span class="sxs-lookup"><span data-stu-id="fed08-315">104.211.161.203</span></span>|
|<span data-ttu-id="fed08-316">West US</span><span class="sxs-lookup"><span data-stu-id="fed08-316">West US</span></span>|<span data-ttu-id="fed08-317">104.40.51.248</span><span class="sxs-lookup"><span data-stu-id="fed08-317">104.40.51.248</span></span>|


## <a name="next-steps"></a><span data-ttu-id="fed08-318">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fed08-318">Next Steps</span></span>  

- <span data-ttu-id="fed08-319">To get started with Logic Apps, follow the [create a Logic App](../logic-apps/logic-apps-create-a-logic-app.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="fed08-319">To get started with Logic Apps, follow the [create a Logic App](../logic-apps/logic-apps-create-a-logic-app.md) tutorial.</span></span>  
- [<span data-ttu-id="fed08-320">View common examples and scenarios</span><span class="sxs-lookup"><span data-stu-id="fed08-320">View common examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
- [<span data-ttu-id="fed08-321">You can automate business processes with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fed08-321">You can automate business processes with Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694) 
- [<span data-ttu-id="fed08-322">Learn How to Integrate your systems with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fed08-322">Learn How to Integrate your systems with Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
