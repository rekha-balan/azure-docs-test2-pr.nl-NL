---
title: Azure Application Insights Data Model | Microsoft Docs
description: Describes properties exported from continuous export in JSON, and used as filters.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: awills
ms.openlocfilehash: 3084bb344976bc542e78a55a1c27c4dedc111af0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553906"
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="8a36a-103">Application Insights Export Data Model</span><span class="sxs-lookup"><span data-stu-id="8a36a-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="8a36a-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span><span class="sxs-lookup"><span data-stu-id="8a36a-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="8a36a-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="8a36a-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="8a36a-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8a36a-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="8a36a-107">Points to note:</span><span class="sxs-lookup"><span data-stu-id="8a36a-107">Points to note:</span></span>

* <span data-ttu-id="8a36a-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span><span class="sxs-lookup"><span data-stu-id="8a36a-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="8a36a-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span><span class="sxs-lookup"><span data-stu-id="8a36a-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="8a36a-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="8a36a-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="8a36a-111">Example</span><span class="sxs-lookup"><span data-stu-id="8a36a-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="8a36a-112">}</span><span class="sxs-lookup"><span data-stu-id="8a36a-112">}</span></span>

## <a name="context"></a><span data-ttu-id="8a36a-113">Context</span><span class="sxs-lookup"><span data-stu-id="8a36a-113">Context</span></span>
<span data-ttu-id="8a36a-114">All types of telemetry are accompanied by a context section.</span><span class="sxs-lookup"><span data-stu-id="8a36a-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="8a36a-115">Not all of these fields are transmitted with every data point.</span><span class="sxs-lookup"><span data-stu-id="8a36a-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="8a36a-116">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-116">Path</span></span> | <span data-ttu-id="8a36a-117">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-117">Type</span></span> | <span data-ttu-id="8a36a-118">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="8a36a-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="8a36a-120">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8a36a-120">object [ ]</span></span> |<span data-ttu-id="8a36a-121">Key-value string pairs set by custom properties parameter.</span><span class="sxs-lookup"><span data-stu-id="8a36a-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="8a36a-122">Key max length 100, values max length 1024.</span><span class="sxs-lookup"><span data-stu-id="8a36a-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="8a36a-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span><span class="sxs-lookup"><span data-stu-id="8a36a-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="8a36a-124">Max 200 keys per ikey.</span><span class="sxs-lookup"><span data-stu-id="8a36a-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="8a36a-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="8a36a-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="8a36a-126">object [ ]</span><span class="sxs-lookup"><span data-stu-id="8a36a-126">object [ ]</span></span> |<span data-ttu-id="8a36a-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span><span class="sxs-lookup"><span data-stu-id="8a36a-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="8a36a-128">Key max length 100, values may be numeric.</span><span class="sxs-lookup"><span data-stu-id="8a36a-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="8a36a-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="8a36a-129">context.data.eventTime</span></span> |<span data-ttu-id="8a36a-130">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-130">string</span></span> |<span data-ttu-id="8a36a-131">UTC</span><span class="sxs-lookup"><span data-stu-id="8a36a-131">UTC</span></span> |
| <span data-ttu-id="8a36a-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="8a36a-132">context.data.isSynthetic</span></span> |<span data-ttu-id="8a36a-133">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-133">boolean</span></span> |<span data-ttu-id="8a36a-134">Request appears to come from a bot or web test.</span><span class="sxs-lookup"><span data-stu-id="8a36a-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="8a36a-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="8a36a-135">context.data.samplingRate</span></span> |<span data-ttu-id="8a36a-136">number</span><span class="sxs-lookup"><span data-stu-id="8a36a-136">number</span></span> |<span data-ttu-id="8a36a-137">Percentage of telemetry generated by the SDK that is sent to portal.</span><span class="sxs-lookup"><span data-stu-id="8a36a-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="8a36a-138">Range 0.0-100.0.</span><span class="sxs-lookup"><span data-stu-id="8a36a-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="8a36a-139">context.device</span><span class="sxs-lookup"><span data-stu-id="8a36a-139">context.device</span></span> |<span data-ttu-id="8a36a-140">object</span><span class="sxs-lookup"><span data-stu-id="8a36a-140">object</span></span> |<span data-ttu-id="8a36a-141">Client device</span><span class="sxs-lookup"><span data-stu-id="8a36a-141">Client device</span></span> |
| <span data-ttu-id="8a36a-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="8a36a-142">context.device.browser</span></span> |<span data-ttu-id="8a36a-143">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-143">string</span></span> |<span data-ttu-id="8a36a-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="8a36a-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="8a36a-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="8a36a-145">context.device.browserVersion</span></span> |<span data-ttu-id="8a36a-146">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-146">string</span></span> |<span data-ttu-id="8a36a-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="8a36a-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="8a36a-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="8a36a-148">context.device.deviceModel</span></span> |<span data-ttu-id="8a36a-149">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-149">string</span></span> | |
| <span data-ttu-id="8a36a-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="8a36a-150">context.device.deviceName</span></span> |<span data-ttu-id="8a36a-151">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-151">string</span></span> | |
| <span data-ttu-id="8a36a-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="8a36a-152">context.device.id</span></span> |<span data-ttu-id="8a36a-153">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-153">string</span></span> | |
| <span data-ttu-id="8a36a-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="8a36a-154">context.device.locale</span></span> |<span data-ttu-id="8a36a-155">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-155">string</span></span> |<span data-ttu-id="8a36a-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="8a36a-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="8a36a-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="8a36a-157">context.device.network</span></span> |<span data-ttu-id="8a36a-158">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-158">string</span></span> | |
| <span data-ttu-id="8a36a-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="8a36a-159">context.device.oemName</span></span> |<span data-ttu-id="8a36a-160">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-160">string</span></span> | |
| <span data-ttu-id="8a36a-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="8a36a-161">context.device.osVersion</span></span> |<span data-ttu-id="8a36a-162">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-162">string</span></span> |<span data-ttu-id="8a36a-163">Host OS</span><span class="sxs-lookup"><span data-stu-id="8a36a-163">Host OS</span></span> |
| <span data-ttu-id="8a36a-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="8a36a-164">context.device.roleInstance</span></span> |<span data-ttu-id="8a36a-165">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-165">string</span></span> |<span data-ttu-id="8a36a-166">ID of server host</span><span class="sxs-lookup"><span data-stu-id="8a36a-166">ID of server host</span></span> |
| <span data-ttu-id="8a36a-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="8a36a-167">context.device.roleName</span></span> |<span data-ttu-id="8a36a-168">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-168">string</span></span> | |
| <span data-ttu-id="8a36a-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="8a36a-169">context.device.type</span></span> |<span data-ttu-id="8a36a-170">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-170">string</span></span> |<span data-ttu-id="8a36a-171">PC, Browser, ...</span><span class="sxs-lookup"><span data-stu-id="8a36a-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="8a36a-172">context.location</span><span class="sxs-lookup"><span data-stu-id="8a36a-172">context.location</span></span> |<span data-ttu-id="8a36a-173">object</span><span class="sxs-lookup"><span data-stu-id="8a36a-173">object</span></span> |<span data-ttu-id="8a36a-174">Derived from clientip.</span><span class="sxs-lookup"><span data-stu-id="8a36a-174">Derived from clientip.</span></span> |
| <span data-ttu-id="8a36a-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="8a36a-175">context.location.city</span></span> |<span data-ttu-id="8a36a-176">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-176">string</span></span> |<span data-ttu-id="8a36a-177">Derived from clientip, if known</span><span class="sxs-lookup"><span data-stu-id="8a36a-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="8a36a-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="8a36a-178">context.location.clientip</span></span> |<span data-ttu-id="8a36a-179">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-179">string</span></span> |<span data-ttu-id="8a36a-180">Last octagon is anonymized to 0.</span><span class="sxs-lookup"><span data-stu-id="8a36a-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="8a36a-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="8a36a-181">context.location.continent</span></span> |<span data-ttu-id="8a36a-182">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-182">string</span></span> | |
| <span data-ttu-id="8a36a-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="8a36a-183">context.location.country</span></span> |<span data-ttu-id="8a36a-184">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-184">string</span></span> | |
| <span data-ttu-id="8a36a-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="8a36a-185">context.location.province</span></span> |<span data-ttu-id="8a36a-186">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-186">string</span></span> |<span data-ttu-id="8a36a-187">State or province</span><span class="sxs-lookup"><span data-stu-id="8a36a-187">State or province</span></span> |
| <span data-ttu-id="8a36a-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="8a36a-188">context.operation.id</span></span> |<span data-ttu-id="8a36a-189">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-189">string</span></span> |<span data-ttu-id="8a36a-190">Items that have the same operation id are shown as Related Items in the portal.</span><span class="sxs-lookup"><span data-stu-id="8a36a-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="8a36a-191">Usually the request id.</span><span class="sxs-lookup"><span data-stu-id="8a36a-191">Usually the request id.</span></span> |
| <span data-ttu-id="8a36a-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="8a36a-192">context.operation.name</span></span> |<span data-ttu-id="8a36a-193">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-193">string</span></span> |<span data-ttu-id="8a36a-194">url or request name</span><span class="sxs-lookup"><span data-stu-id="8a36a-194">url or request name</span></span> |
| <span data-ttu-id="8a36a-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="8a36a-195">context.operation.parentId</span></span> |<span data-ttu-id="8a36a-196">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-196">string</span></span> |<span data-ttu-id="8a36a-197">Allows nested related items.</span><span class="sxs-lookup"><span data-stu-id="8a36a-197">Allows nested related items.</span></span> |
| <span data-ttu-id="8a36a-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="8a36a-198">context.session.id</span></span> |<span data-ttu-id="8a36a-199">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-199">string</span></span> |<span data-ttu-id="8a36a-200">Id of a group of operations from the same source.</span><span class="sxs-lookup"><span data-stu-id="8a36a-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="8a36a-201">A period of 30 minutes without an operation signals the end of a session.</span><span class="sxs-lookup"><span data-stu-id="8a36a-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="8a36a-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="8a36a-202">context.session.isFirst</span></span> |<span data-ttu-id="8a36a-203">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-203">boolean</span></span> | |
| <span data-ttu-id="8a36a-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8a36a-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="8a36a-205">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-205">string</span></span> | |
| <span data-ttu-id="8a36a-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8a36a-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="8a36a-207">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-207">string</span></span> | |
| <span data-ttu-id="8a36a-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="8a36a-208">context.user.anonId</span></span> |<span data-ttu-id="8a36a-209">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-209">string</span></span> | |
| <span data-ttu-id="8a36a-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="8a36a-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="8a36a-211">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-211">string</span></span> |[<span data-ttu-id="8a36a-212">Authenticated User</span><span class="sxs-lookup"><span data-stu-id="8a36a-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="8a36a-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="8a36a-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="8a36a-214">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-214">boolean</span></span> | |
| <span data-ttu-id="8a36a-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="8a36a-215">internal.data.documentVersion</span></span> |<span data-ttu-id="8a36a-216">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-216">string</span></span> | |
| <span data-ttu-id="8a36a-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="8a36a-217">internal.data.id</span></span> |<span data-ttu-id="8a36a-218">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="8a36a-219">Events</span><span class="sxs-lookup"><span data-stu-id="8a36a-219">Events</span></span>
<span data-ttu-id="8a36a-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="8a36a-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="8a36a-221">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-221">Path</span></span> | <span data-ttu-id="8a36a-222">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-222">Type</span></span> | <span data-ttu-id="8a36a-223">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-224">event [0] count</span></span> |<span data-ttu-id="8a36a-225">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-225">integer</span></span> |<span data-ttu-id="8a36a-226">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-227">For example 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="8a36a-228">event [0] name</span></span> |<span data-ttu-id="8a36a-229">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-229">string</span></span> |<span data-ttu-id="8a36a-230">Event name.</span><span class="sxs-lookup"><span data-stu-id="8a36a-230">Event name.</span></span>  <span data-ttu-id="8a36a-231">Max length 250.</span><span class="sxs-lookup"><span data-stu-id="8a36a-231">Max length 250.</span></span> |
| <span data-ttu-id="8a36a-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="8a36a-232">event [0] url</span></span> |<span data-ttu-id="8a36a-233">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-233">string</span></span> | |
| <span data-ttu-id="8a36a-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8a36a-234">event [0] urlData.base</span></span> |<span data-ttu-id="8a36a-235">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-235">string</span></span> | |
| <span data-ttu-id="8a36a-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8a36a-236">event [0] urlData.host</span></span> |<span data-ttu-id="8a36a-237">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="8a36a-238">Exceptions</span><span class="sxs-lookup"><span data-stu-id="8a36a-238">Exceptions</span></span>
<span data-ttu-id="8a36a-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span><span class="sxs-lookup"><span data-stu-id="8a36a-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="8a36a-240">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-240">Path</span></span> | <span data-ttu-id="8a36a-241">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-241">Type</span></span> | <span data-ttu-id="8a36a-242">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8a36a-243">basicException [0] assembly</span></span> |<span data-ttu-id="8a36a-244">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-244">string</span></span> | |
| <span data-ttu-id="8a36a-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-245">basicException [0] count</span></span> |<span data-ttu-id="8a36a-246">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-246">integer</span></span> |<span data-ttu-id="8a36a-247">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-248">For example 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="8a36a-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="8a36a-250">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-250">string</span></span> | |
| <span data-ttu-id="8a36a-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="8a36a-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="8a36a-252">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-252">string</span></span> | |
| <span data-ttu-id="8a36a-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="8a36a-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="8a36a-254">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-254">string</span></span> | |
| <span data-ttu-id="8a36a-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="8a36a-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="8a36a-256">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-256">string</span></span> | |
| <span data-ttu-id="8a36a-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="8a36a-257">basicException [0] handledAt</span></span> |<span data-ttu-id="8a36a-258">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-258">string</span></span> | |
| <span data-ttu-id="8a36a-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="8a36a-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="8a36a-260">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-260">boolean</span></span> | |
| <span data-ttu-id="8a36a-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="8a36a-261">basicException [0] id</span></span> |<span data-ttu-id="8a36a-262">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-262">string</span></span> | |
| <span data-ttu-id="8a36a-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="8a36a-263">basicException [0] method</span></span> |<span data-ttu-id="8a36a-264">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-264">string</span></span> | |
| <span data-ttu-id="8a36a-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="8a36a-265">basicException [0] message</span></span> |<span data-ttu-id="8a36a-266">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-266">string</span></span> |<span data-ttu-id="8a36a-267">Exception message.</span><span class="sxs-lookup"><span data-stu-id="8a36a-267">Exception message.</span></span> <span data-ttu-id="8a36a-268">Max length 10k.</span><span class="sxs-lookup"><span data-stu-id="8a36a-268">Max length 10k.</span></span> |
| <span data-ttu-id="8a36a-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="8a36a-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="8a36a-270">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-270">string</span></span> | |
| <span data-ttu-id="8a36a-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="8a36a-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="8a36a-272">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-272">string</span></span> | |
| <span data-ttu-id="8a36a-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="8a36a-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="8a36a-274">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-274">string</span></span> | |
| <span data-ttu-id="8a36a-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="8a36a-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="8a36a-276">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-276">string</span></span> | |
| <span data-ttu-id="8a36a-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="8a36a-277">basicException [0] outerId</span></span> |<span data-ttu-id="8a36a-278">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-278">string</span></span> | |
| <span data-ttu-id="8a36a-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="8a36a-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="8a36a-280">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-280">string</span></span> | |
| <span data-ttu-id="8a36a-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="8a36a-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="8a36a-282">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-282">string</span></span> | |
| <span data-ttu-id="8a36a-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="8a36a-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="8a36a-284">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-284">integer</span></span> | |
| <span data-ttu-id="8a36a-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="8a36a-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="8a36a-286">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-286">integer</span></span> | |
| <span data-ttu-id="8a36a-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="8a36a-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="8a36a-288">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-288">string</span></span> | |
| <span data-ttu-id="8a36a-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="8a36a-289">basicException [0] stack</span></span> |<span data-ttu-id="8a36a-290">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-290">string</span></span> |<span data-ttu-id="8a36a-291">Max length 10k</span><span class="sxs-lookup"><span data-stu-id="8a36a-291">Max length 10k</span></span> |
| <span data-ttu-id="8a36a-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="8a36a-292">basicException [0] typeName</span></span> |<span data-ttu-id="8a36a-293">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="8a36a-294">Trace Messages</span><span class="sxs-lookup"><span data-stu-id="8a36a-294">Trace Messages</span></span>
<span data-ttu-id="8a36a-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8a36a-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="8a36a-296">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-296">Path</span></span> | <span data-ttu-id="8a36a-297">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-297">Type</span></span> | <span data-ttu-id="8a36a-298">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="8a36a-299">message [0] loggerName</span></span> |<span data-ttu-id="8a36a-300">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-300">string</span></span> | |
| <span data-ttu-id="8a36a-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="8a36a-301">message [0] parameters</span></span> |<span data-ttu-id="8a36a-302">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-302">string</span></span> | |
| <span data-ttu-id="8a36a-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="8a36a-303">message [0] raw</span></span> |<span data-ttu-id="8a36a-304">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-304">string</span></span> |<span data-ttu-id="8a36a-305">The log message, max length 10k.</span><span class="sxs-lookup"><span data-stu-id="8a36a-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="8a36a-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="8a36a-306">message [0] severityLevel</span></span> |<span data-ttu-id="8a36a-307">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="8a36a-308">Remote dependency</span><span class="sxs-lookup"><span data-stu-id="8a36a-308">Remote dependency</span></span>
<span data-ttu-id="8a36a-309">Sent by TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="8a36a-309">Sent by TrackDependency.</span></span> <span data-ttu-id="8a36a-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span><span class="sxs-lookup"><span data-stu-id="8a36a-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="8a36a-311">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-311">Path</span></span> | <span data-ttu-id="8a36a-312">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-312">Type</span></span> | <span data-ttu-id="8a36a-313">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="8a36a-314">remoteDependency [0] async</span></span> |<span data-ttu-id="8a36a-315">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-315">boolean</span></span> | |
| <span data-ttu-id="8a36a-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="8a36a-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="8a36a-317">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-317">string</span></span> | |
| <span data-ttu-id="8a36a-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="8a36a-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="8a36a-319">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-319">string</span></span> |<span data-ttu-id="8a36a-320">For example "home/index"</span><span class="sxs-lookup"><span data-stu-id="8a36a-320">For example "home/index"</span></span> |
| <span data-ttu-id="8a36a-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-321">remoteDependency [0] count</span></span> |<span data-ttu-id="8a36a-322">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-322">integer</span></span> |<span data-ttu-id="8a36a-323">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-324">For example 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="8a36a-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="8a36a-326">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-326">string</span></span> |<span data-ttu-id="8a36a-327">HTTP, SQL, ...</span><span class="sxs-lookup"><span data-stu-id="8a36a-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="8a36a-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="8a36a-329">number</span><span class="sxs-lookup"><span data-stu-id="8a36a-329">number</span></span> |<span data-ttu-id="8a36a-330">Time from call to completion of response by dependency</span><span class="sxs-lookup"><span data-stu-id="8a36a-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="8a36a-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="8a36a-331">remoteDependency [0] id</span></span> |<span data-ttu-id="8a36a-332">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-332">string</span></span> | |
| <span data-ttu-id="8a36a-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="8a36a-333">remoteDependency [0] name</span></span> |<span data-ttu-id="8a36a-334">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-334">string</span></span> |<span data-ttu-id="8a36a-335">Url.</span><span class="sxs-lookup"><span data-stu-id="8a36a-335">Url.</span></span> <span data-ttu-id="8a36a-336">Max length 250.</span><span class="sxs-lookup"><span data-stu-id="8a36a-336">Max length 250.</span></span> |
| <span data-ttu-id="8a36a-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="8a36a-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="8a36a-338">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-338">string</span></span> |<span data-ttu-id="8a36a-339">from HTTP dependency</span><span class="sxs-lookup"><span data-stu-id="8a36a-339">from HTTP dependency</span></span> |
| <span data-ttu-id="8a36a-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="8a36a-340">remoteDependency [0] success</span></span> |<span data-ttu-id="8a36a-341">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-341">boolean</span></span> | |
| <span data-ttu-id="8a36a-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="8a36a-342">remoteDependency [0] type</span></span> |<span data-ttu-id="8a36a-343">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-343">string</span></span> |<span data-ttu-id="8a36a-344">Http, Sql,...</span><span class="sxs-lookup"><span data-stu-id="8a36a-344">Http, Sql,...</span></span> |
| <span data-ttu-id="8a36a-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="8a36a-345">remoteDependency [0] url</span></span> |<span data-ttu-id="8a36a-346">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-346">string</span></span> |<span data-ttu-id="8a36a-347">Max length 2000</span><span class="sxs-lookup"><span data-stu-id="8a36a-347">Max length 2000</span></span> |
| <span data-ttu-id="8a36a-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8a36a-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="8a36a-349">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-349">string</span></span> |<span data-ttu-id="8a36a-350">Max length 2000</span><span class="sxs-lookup"><span data-stu-id="8a36a-350">Max length 2000</span></span> |
| <span data-ttu-id="8a36a-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8a36a-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="8a36a-352">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-352">string</span></span> | |
| <span data-ttu-id="8a36a-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8a36a-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="8a36a-354">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-354">string</span></span> |<span data-ttu-id="8a36a-355">Max length 200</span><span class="sxs-lookup"><span data-stu-id="8a36a-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="8a36a-356">Requests</span><span class="sxs-lookup"><span data-stu-id="8a36a-356">Requests</span></span>
<span data-ttu-id="8a36a-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="8a36a-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="8a36a-358">The standard modules use this to reports server response time, measured at the server.</span><span class="sxs-lookup"><span data-stu-id="8a36a-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="8a36a-359">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-359">Path</span></span> | <span data-ttu-id="8a36a-360">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-360">Type</span></span> | <span data-ttu-id="8a36a-361">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-362">request [0] count</span></span> |<span data-ttu-id="8a36a-363">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-363">integer</span></span> |<span data-ttu-id="8a36a-364">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-365">For example: 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="8a36a-367">number</span><span class="sxs-lookup"><span data-stu-id="8a36a-367">number</span></span> |<span data-ttu-id="8a36a-368">Time from request arriving to response.</span><span class="sxs-lookup"><span data-stu-id="8a36a-368">Time from request arriving to response.</span></span> <span data-ttu-id="8a36a-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="8a36a-369">1e7 == 1s</span></span> |
| <span data-ttu-id="8a36a-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="8a36a-370">request [0] id</span></span> |<span data-ttu-id="8a36a-371">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-371">string</span></span> |<span data-ttu-id="8a36a-372">Operation id</span><span class="sxs-lookup"><span data-stu-id="8a36a-372">Operation id</span></span> |
| <span data-ttu-id="8a36a-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="8a36a-373">request [0] name</span></span> |<span data-ttu-id="8a36a-374">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-374">string</span></span> |<span data-ttu-id="8a36a-375">GET/POST + url base.</span><span class="sxs-lookup"><span data-stu-id="8a36a-375">GET/POST + url base.</span></span>  <span data-ttu-id="8a36a-376">Max length 250</span><span class="sxs-lookup"><span data-stu-id="8a36a-376">Max length 250</span></span> |
| <span data-ttu-id="8a36a-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="8a36a-377">request [0] responseCode</span></span> |<span data-ttu-id="8a36a-378">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-378">integer</span></span> |<span data-ttu-id="8a36a-379">HTTP response sent to client</span><span class="sxs-lookup"><span data-stu-id="8a36a-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="8a36a-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="8a36a-380">request [0] success</span></span> |<span data-ttu-id="8a36a-381">boolean</span><span class="sxs-lookup"><span data-stu-id="8a36a-381">boolean</span></span> |<span data-ttu-id="8a36a-382">Default == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="8a36a-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="8a36a-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="8a36a-383">request [0] url</span></span> |<span data-ttu-id="8a36a-384">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-384">string</span></span> |<span data-ttu-id="8a36a-385">Not including host</span><span class="sxs-lookup"><span data-stu-id="8a36a-385">Not including host</span></span> |
| <span data-ttu-id="8a36a-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8a36a-386">request [0] urlData.base</span></span> |<span data-ttu-id="8a36a-387">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-387">string</span></span> | |
| <span data-ttu-id="8a36a-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8a36a-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="8a36a-389">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-389">string</span></span> | |
| <span data-ttu-id="8a36a-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8a36a-390">request [0] urlData.host</span></span> |<span data-ttu-id="8a36a-391">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="8a36a-392">Page View Performance</span><span class="sxs-lookup"><span data-stu-id="8a36a-392">Page View Performance</span></span>
<span data-ttu-id="8a36a-393">Sent by the browser.</span><span class="sxs-lookup"><span data-stu-id="8a36a-393">Sent by the browser.</span></span> <span data-ttu-id="8a36a-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span><span class="sxs-lookup"><span data-stu-id="8a36a-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="8a36a-395">Context values show client OS and browser version.</span><span class="sxs-lookup"><span data-stu-id="8a36a-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="8a36a-396">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-396">Path</span></span> | <span data-ttu-id="8a36a-397">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-397">Type</span></span> | <span data-ttu-id="8a36a-398">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="8a36a-400">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-400">integer</span></span> |<span data-ttu-id="8a36a-401">Time from end of receiving the HTML to displaying the page.</span><span class="sxs-lookup"><span data-stu-id="8a36a-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="8a36a-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="8a36a-402">clientPerformance [0] name</span></span> |<span data-ttu-id="8a36a-403">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-403">string</span></span> | |
| <span data-ttu-id="8a36a-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="8a36a-405">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-405">integer</span></span> |<span data-ttu-id="8a36a-406">Time taken to establish a network connection.</span><span class="sxs-lookup"><span data-stu-id="8a36a-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="8a36a-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="8a36a-408">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-408">integer</span></span> |<span data-ttu-id="8a36a-409">Time from end of sending the request to receiving the HTML in reply.</span><span class="sxs-lookup"><span data-stu-id="8a36a-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="8a36a-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="8a36a-411">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-411">integer</span></span> |<span data-ttu-id="8a36a-412">Time from taken to send the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="8a36a-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="8a36a-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="8a36a-414">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-414">integer</span></span> |<span data-ttu-id="8a36a-415">Time from starting to send the request to displaying the page.</span><span class="sxs-lookup"><span data-stu-id="8a36a-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="8a36a-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="8a36a-416">clientPerformance [0] url</span></span> |<span data-ttu-id="8a36a-417">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-417">string</span></span> |<span data-ttu-id="8a36a-418">URL of this request</span><span class="sxs-lookup"><span data-stu-id="8a36a-418">URL of this request</span></span> |
| <span data-ttu-id="8a36a-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8a36a-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="8a36a-420">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-420">string</span></span> | |
| <span data-ttu-id="8a36a-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8a36a-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="8a36a-422">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-422">string</span></span> | |
| <span data-ttu-id="8a36a-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8a36a-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="8a36a-424">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-424">string</span></span> | |
| <span data-ttu-id="8a36a-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="8a36a-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="8a36a-426">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="8a36a-427">Page Views</span><span class="sxs-lookup"><span data-stu-id="8a36a-427">Page Views</span></span>
<span data-ttu-id="8a36a-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="8a36a-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="8a36a-429">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-429">Path</span></span> | <span data-ttu-id="8a36a-430">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-430">Type</span></span> | <span data-ttu-id="8a36a-431">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-432">view [0] count</span></span> |<span data-ttu-id="8a36a-433">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-433">integer</span></span> |<span data-ttu-id="8a36a-434">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-435">For example 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="8a36a-437">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-437">integer</span></span> |<span data-ttu-id="8a36a-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="8a36a-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="8a36a-439">Not the same as clientPerformance values.</span><span class="sxs-lookup"><span data-stu-id="8a36a-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="8a36a-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="8a36a-440">view [0] name</span></span> |<span data-ttu-id="8a36a-441">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-441">string</span></span> |<span data-ttu-id="8a36a-442">Page title.</span><span class="sxs-lookup"><span data-stu-id="8a36a-442">Page title.</span></span>  <span data-ttu-id="8a36a-443">Max length 250</span><span class="sxs-lookup"><span data-stu-id="8a36a-443">Max length 250</span></span> |
| <span data-ttu-id="8a36a-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="8a36a-444">view [0] url</span></span> |<span data-ttu-id="8a36a-445">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-445">string</span></span> | |
| <span data-ttu-id="8a36a-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="8a36a-446">view [0] urlData.base</span></span> |<span data-ttu-id="8a36a-447">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-447">string</span></span> | |
| <span data-ttu-id="8a36a-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="8a36a-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="8a36a-449">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-449">string</span></span> | |
| <span data-ttu-id="8a36a-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="8a36a-450">view [0] urlData.host</span></span> |<span data-ttu-id="8a36a-451">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="8a36a-452">Availability</span><span class="sxs-lookup"><span data-stu-id="8a36a-452">Availability</span></span>
<span data-ttu-id="8a36a-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="8a36a-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="8a36a-454">Path</span><span class="sxs-lookup"><span data-stu-id="8a36a-454">Path</span></span> | <span data-ttu-id="8a36a-455">Type</span><span class="sxs-lookup"><span data-stu-id="8a36a-455">Type</span></span> | <span data-ttu-id="8a36a-456">Notes</span><span class="sxs-lookup"><span data-stu-id="8a36a-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a36a-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="8a36a-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="8a36a-458">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-458">string</span></span> |<span data-ttu-id="8a36a-459">availability</span><span class="sxs-lookup"><span data-stu-id="8a36a-459">availability</span></span> |
| <span data-ttu-id="8a36a-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="8a36a-461">number</span><span class="sxs-lookup"><span data-stu-id="8a36a-461">number</span></span> |<span data-ttu-id="8a36a-462">1.0 or 0.0</span><span class="sxs-lookup"><span data-stu-id="8a36a-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="8a36a-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="8a36a-463">availability [0] count</span></span> |<span data-ttu-id="8a36a-464">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-464">integer</span></span> |<span data-ttu-id="8a36a-465">100/([sampling](app-insights-sampling.md) rate).</span><span class="sxs-lookup"><span data-stu-id="8a36a-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="8a36a-466">For example 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="8a36a-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="8a36a-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="8a36a-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="8a36a-468">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-468">string</span></span> | |
| <span data-ttu-id="8a36a-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="8a36a-470">integer</span><span class="sxs-lookup"><span data-stu-id="8a36a-470">integer</span></span> | |
| <span data-ttu-id="8a36a-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="8a36a-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="8a36a-472">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-472">string</span></span> | |
| <span data-ttu-id="8a36a-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="8a36a-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="8a36a-474">number</span><span class="sxs-lookup"><span data-stu-id="8a36a-474">number</span></span> |<span data-ttu-id="8a36a-475">Duration of test.</span><span class="sxs-lookup"><span data-stu-id="8a36a-475">Duration of test.</span></span> <span data-ttu-id="8a36a-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="8a36a-476">1e7==1s</span></span> |
| <span data-ttu-id="8a36a-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="8a36a-477">availability [0] message</span></span> |<span data-ttu-id="8a36a-478">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-478">string</span></span> |<span data-ttu-id="8a36a-479">Failure diagnostic</span><span class="sxs-lookup"><span data-stu-id="8a36a-479">Failure diagnostic</span></span> |
| <span data-ttu-id="8a36a-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="8a36a-480">availability [0] result</span></span> |<span data-ttu-id="8a36a-481">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-481">string</span></span> |<span data-ttu-id="8a36a-482">Pass/Fail</span><span class="sxs-lookup"><span data-stu-id="8a36a-482">Pass/Fail</span></span> |
| <span data-ttu-id="8a36a-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="8a36a-483">availability [0] runLocation</span></span> |<span data-ttu-id="8a36a-484">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-484">string</span></span> |<span data-ttu-id="8a36a-485">Geo source of http req</span><span class="sxs-lookup"><span data-stu-id="8a36a-485">Geo source of http req</span></span> |
| <span data-ttu-id="8a36a-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="8a36a-486">availability [0] testName</span></span> |<span data-ttu-id="8a36a-487">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-487">string</span></span> | |
| <span data-ttu-id="8a36a-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="8a36a-488">availability [0] testRunId</span></span> |<span data-ttu-id="8a36a-489">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-489">string</span></span> | |
| <span data-ttu-id="8a36a-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="8a36a-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="8a36a-491">string</span><span class="sxs-lookup"><span data-stu-id="8a36a-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="8a36a-492">Metrics</span><span class="sxs-lookup"><span data-stu-id="8a36a-492">Metrics</span></span>
<span data-ttu-id="8a36a-493">Generated by TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="8a36a-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="8a36a-494">The metric value is found in context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="8a36a-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="8a36a-495">For example:</span><span class="sxs-lookup"><span data-stu-id="8a36a-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="8a36a-496">About metric values</span><span class="sxs-lookup"><span data-stu-id="8a36a-496">About metric values</span></span>
<span data-ttu-id="8a36a-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span><span class="sxs-lookup"><span data-stu-id="8a36a-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="8a36a-498">For example:</span><span class="sxs-lookup"><span data-stu-id="8a36a-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="8a36a-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span><span class="sxs-lookup"><span data-stu-id="8a36a-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="8a36a-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span><span class="sxs-lookup"><span data-stu-id="8a36a-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="8a36a-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span><span class="sxs-lookup"><span data-stu-id="8a36a-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="8a36a-502">For example, you could average several successive readings before sending each metric report.</span><span class="sxs-lookup"><span data-stu-id="8a36a-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="8a36a-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span><span class="sxs-lookup"><span data-stu-id="8a36a-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="8a36a-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span><span class="sxs-lookup"><span data-stu-id="8a36a-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="8a36a-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span><span class="sxs-lookup"><span data-stu-id="8a36a-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="8a36a-506">Durations</span><span class="sxs-lookup"><span data-stu-id="8a36a-506">Durations</span></span>
<span data-ttu-id="8a36a-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span><span class="sxs-lookup"><span data-stu-id="8a36a-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="8a36a-508">See also</span><span class="sxs-lookup"><span data-stu-id="8a36a-508">See also</span></span>
* [<span data-ttu-id="8a36a-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="8a36a-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="8a36a-510">Continuous Export</span><span class="sxs-lookup"><span data-stu-id="8a36a-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="8a36a-511">Code samples</span><span class="sxs-lookup"><span data-stu-id="8a36a-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
