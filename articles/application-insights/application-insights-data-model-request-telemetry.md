---
title: Azure Application Insights Telemetry Data Model - Request Telemetry | Microsoft Docs
description: Application Insights data model for request telemetry
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/25/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: 6cee6db66fc4146e9c799394e40c72ab2ce665dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868115"
---
# <a name="request-telemetry-application-insights-data-model"></a><span data-ttu-id="79d31-103">Request telemetry: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="79d31-103">Request telemetry: Application Insights data model</span></span>

<span data-ttu-id="79d31-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents the logical sequence of execution triggered by an external request to your application.</span><span class="sxs-lookup"><span data-stu-id="79d31-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents the logical sequence of execution triggered by an external request to your application.</span></span> <span data-ttu-id="79d31-105">Every request execution is identified by unique `ID` and `url` containing all the execution parameters.</span><span class="sxs-lookup"><span data-stu-id="79d31-105">Every request execution is identified by unique `ID` and `url` containing all the execution parameters.</span></span> <span data-ttu-id="79d31-106">You can group requests by logical `name` and define the `source` of this request.</span><span class="sxs-lookup"><span data-stu-id="79d31-106">You can group requests by logical `name` and define the `source` of this request.</span></span> <span data-ttu-id="79d31-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span><span class="sxs-lookup"><span data-stu-id="79d31-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span></span> <span data-ttu-id="79d31-108">Both success and failure executions may be grouped further by `resultCode`.</span><span class="sxs-lookup"><span data-stu-id="79d31-108">Both success and failure executions may be grouped further by `resultCode`.</span></span> <span data-ttu-id="79d31-109">Start time for the request telemetry defined on the envelope level.</span><span class="sxs-lookup"><span data-stu-id="79d31-109">Start time for the request telemetry defined on the envelope level.</span></span>

<span data-ttu-id="79d31-110">Request telemetry supports the standard extensibility model using custom `properties` and `measurements`.</span><span class="sxs-lookup"><span data-stu-id="79d31-110">Request telemetry supports the standard extensibility model using custom `properties` and `measurements`.</span></span>

## <a name="name"></a><span data-ttu-id="79d31-111">Name</span><span class="sxs-lookup"><span data-stu-id="79d31-111">Name</span></span>

<span data-ttu-id="79d31-112">Name of the request represents code path taken to process the request.</span><span class="sxs-lookup"><span data-stu-id="79d31-112">Name of the request represents code path taken to process the request.</span></span> <span data-ttu-id="79d31-113">Low cardinality value to allow better grouping of requests.</span><span class="sxs-lookup"><span data-stu-id="79d31-113">Low cardinality value to allow better grouping of requests.</span></span> <span data-ttu-id="79d31-114">For HTTP requests it represents the HTTP method and URL path template like `GET /values/{id}` without the actual `id` value.</span><span class="sxs-lookup"><span data-stu-id="79d31-114">For HTTP requests it represents the HTTP method and URL path template like `GET /values/{id}` without the actual `id` value.</span></span>

<span data-ttu-id="79d31-115">Application Insights web SDK sends request name "as is" with regards to letter case.</span><span class="sxs-lookup"><span data-stu-id="79d31-115">Application Insights web SDK sends request name "as is" with regards to letter case.</span></span> <span data-ttu-id="79d31-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in the same controller and action execution.</span><span class="sxs-lookup"><span data-stu-id="79d31-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in the same controller and action execution.</span></span> <span data-ttu-id="79d31-117">The reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span><span class="sxs-lookup"><span data-stu-id="79d31-117">The reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span></span> <span data-ttu-id="79d31-118">You may want to see if all `404` happened for the urls typed in uppercase.</span><span class="sxs-lookup"><span data-stu-id="79d31-118">You may want to see if all `404` happened for the urls typed in uppercase.</span></span> <span data-ttu-id="79d31-119">You can read more on request name collection by ASP.Net Web SDK in the [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span><span class="sxs-lookup"><span data-stu-id="79d31-119">You can read more on request name collection by ASP.Net Web SDK in the [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span></span>

<span data-ttu-id="79d31-120">Max length: 1024 characters</span><span class="sxs-lookup"><span data-stu-id="79d31-120">Max length: 1024 characters</span></span>

## <a name="id"></a><span data-ttu-id="79d31-121">ID</span><span class="sxs-lookup"><span data-stu-id="79d31-121">ID</span></span>

<span data-ttu-id="79d31-122">Identifier of a request call instance.</span><span class="sxs-lookup"><span data-stu-id="79d31-122">Identifier of a request call instance.</span></span> <span data-ttu-id="79d31-123">Used for correlation between request and other telemetry items.</span><span class="sxs-lookup"><span data-stu-id="79d31-123">Used for correlation between request and other telemetry items.</span></span> <span data-ttu-id="79d31-124">ID should be globally unique.</span><span class="sxs-lookup"><span data-stu-id="79d31-124">ID should be globally unique.</span></span> <span data-ttu-id="79d31-125">For more information, see [correlation](application-insights-correlation.md) page.</span><span class="sxs-lookup"><span data-stu-id="79d31-125">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="79d31-126">Max length: 128 characters</span><span class="sxs-lookup"><span data-stu-id="79d31-126">Max length: 128 characters</span></span>

## <a name="url"></a><span data-ttu-id="79d31-127">Url</span><span class="sxs-lookup"><span data-stu-id="79d31-127">Url</span></span>

<span data-ttu-id="79d31-128">Request URL with all query string parameters.</span><span class="sxs-lookup"><span data-stu-id="79d31-128">Request URL with all query string parameters.</span></span>

<span data-ttu-id="79d31-129">Max length: 2048 characters</span><span class="sxs-lookup"><span data-stu-id="79d31-129">Max length: 2048 characters</span></span>

## <a name="source"></a><span data-ttu-id="79d31-130">Source</span><span class="sxs-lookup"><span data-stu-id="79d31-130">Source</span></span>

<span data-ttu-id="79d31-131">Source of the request.</span><span class="sxs-lookup"><span data-stu-id="79d31-131">Source of the request.</span></span> <span data-ttu-id="79d31-132">Examples are the instrumentation key of the caller or the ip address of the caller.</span><span class="sxs-lookup"><span data-stu-id="79d31-132">Examples are the instrumentation key of the caller or the ip address of the caller.</span></span> <span data-ttu-id="79d31-133">For more information, see [correlation](application-insights-correlation.md) page.</span><span class="sxs-lookup"><span data-stu-id="79d31-133">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="79d31-134">Max length: 1024 characters</span><span class="sxs-lookup"><span data-stu-id="79d31-134">Max length: 1024 characters</span></span>

## <a name="duration"></a><span data-ttu-id="79d31-135">Duration</span><span class="sxs-lookup"><span data-stu-id="79d31-135">Duration</span></span>

<span data-ttu-id="79d31-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="79d31-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="79d31-137">Must be positive and less than `1000` days.</span><span class="sxs-lookup"><span data-stu-id="79d31-137">Must be positive and less than `1000` days.</span></span> <span data-ttu-id="79d31-138">This field is required as request telemetry represents the operation with the beginning and the end.</span><span class="sxs-lookup"><span data-stu-id="79d31-138">This field is required as request telemetry represents the operation with the beginning and the end.</span></span>

## <a name="response-code"></a><span data-ttu-id="79d31-139">Response code</span><span class="sxs-lookup"><span data-stu-id="79d31-139">Response code</span></span>

<span data-ttu-id="79d31-140">Result of a request execution.</span><span class="sxs-lookup"><span data-stu-id="79d31-140">Result of a request execution.</span></span> <span data-ttu-id="79d31-141">HTTP status code for HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="79d31-141">HTTP status code for HTTP requests.</span></span> <span data-ttu-id="79d31-142">It may be `HRESULT` value or exception type for other request types.</span><span class="sxs-lookup"><span data-stu-id="79d31-142">It may be `HRESULT` value or exception type for other request types.</span></span>

<span data-ttu-id="79d31-143">Max length: 1024 characters</span><span class="sxs-lookup"><span data-stu-id="79d31-143">Max length: 1024 characters</span></span>

## <a name="success"></a><span data-ttu-id="79d31-144">Success</span><span class="sxs-lookup"><span data-stu-id="79d31-144">Success</span></span>

<span data-ttu-id="79d31-145">Indication of successful or unsuccessful call.</span><span class="sxs-lookup"><span data-stu-id="79d31-145">Indication of successful or unsuccessful call.</span></span> <span data-ttu-id="79d31-146">This field is required.</span><span class="sxs-lookup"><span data-stu-id="79d31-146">This field is required.</span></span> <span data-ttu-id="79d31-147">When not set explicitly to `false` - request considered to be successful.</span><span class="sxs-lookup"><span data-stu-id="79d31-147">When not set explicitly to `false` - request considered to be successful.</span></span> <span data-ttu-id="79d31-148">Set this value to `false` if operation was interrupted by exception or returned error result code.</span><span class="sxs-lookup"><span data-stu-id="79d31-148">Set this value to `false` if operation was interrupted by exception or returned error result code.</span></span>

<span data-ttu-id="79d31-149">For the web applications, Application Insights define request as failed when the response code is less the `400` or equal to `401`.</span><span class="sxs-lookup"><span data-stu-id="79d31-149">For the web applications, Application Insights define request as failed when the response code is less the `400` or equal to `401`.</span></span> <span data-ttu-id="79d31-150">However there are cases when this default mapping does not match the semantic of the application.</span><span class="sxs-lookup"><span data-stu-id="79d31-150">However there are cases when this default mapping does not match the semantic of the application.</span></span> <span data-ttu-id="79d31-151">Response code `404` may indicate "no records", which can be part of regular flow.</span><span class="sxs-lookup"><span data-stu-id="79d31-151">Response code `404` may indicate "no records", which can be part of regular flow.</span></span> <span data-ttu-id="79d31-152">It also may indicate a broken link.</span><span class="sxs-lookup"><span data-stu-id="79d31-152">It also may indicate a broken link.</span></span> <span data-ttu-id="79d31-153">For the broken links, you can even implement more advanced logic.</span><span class="sxs-lookup"><span data-stu-id="79d31-153">For the broken links, you can even implement more advanced logic.</span></span> <span data-ttu-id="79d31-154">You can mark broken links as failures only when those links are located on the same site by analyzing url referrer.</span><span class="sxs-lookup"><span data-stu-id="79d31-154">You can mark broken links as failures only when those links are located on the same site by analyzing url referrer.</span></span> <span data-ttu-id="79d31-155">Or mark them as failures when accessed from the company's mobile application.</span><span class="sxs-lookup"><span data-stu-id="79d31-155">Or mark them as failures when accessed from the company's mobile application.</span></span> <span data-ttu-id="79d31-156">Similarly `301` and `302` indicates failure when accessed from the client that doesn't support redirect.</span><span class="sxs-lookup"><span data-stu-id="79d31-156">Similarly `301` and `302` indicates failure when accessed from the client that doesn't support redirect.</span></span>

<span data-ttu-id="79d31-157">Partially accepted content `206` may indicate a failure of an overall request.</span><span class="sxs-lookup"><span data-stu-id="79d31-157">Partially accepted content `206` may indicate a failure of an overall request.</span></span> <span data-ttu-id="79d31-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span><span class="sxs-lookup"><span data-stu-id="79d31-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span></span> <span data-ttu-id="79d31-159">It returns `206` when some items in the batch were not processed successfully.</span><span class="sxs-lookup"><span data-stu-id="79d31-159">It returns `206` when some items in the batch were not processed successfully.</span></span> <span data-ttu-id="79d31-160">Increasing rate of `206` indicates a problem that needs to be investigated.</span><span class="sxs-lookup"><span data-stu-id="79d31-160">Increasing rate of `206` indicates a problem that needs to be investigated.</span></span> <span data-ttu-id="79d31-161">Similar logic applies to `207` Multi-Status where the success may be the worst of separate response codes.</span><span class="sxs-lookup"><span data-stu-id="79d31-161">Similar logic applies to `207` Multi-Status where the success may be the worst of separate response codes.</span></span>

<span data-ttu-id="79d31-162">You can read more on request result code and status code in the [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span><span class="sxs-lookup"><span data-stu-id="79d31-162">You can read more on request result code and status code in the [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span></span>

## <a name="custom-properties"></a><span data-ttu-id="79d31-163">Custom properties</span><span class="sxs-lookup"><span data-stu-id="79d31-163">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="79d31-164">Custom measurements</span><span class="sxs-lookup"><span data-stu-id="79d31-164">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="79d31-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="79d31-165">Next steps</span></span>

- [<span data-ttu-id="79d31-166">Write custom request telemetry</span><span class="sxs-lookup"><span data-stu-id="79d31-166">Write custom request telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackrequest)
- <span data-ttu-id="79d31-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="79d31-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="79d31-168">Learn how to [configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span><span class="sxs-lookup"><span data-stu-id="79d31-168">Learn how to [configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span></span>
- <span data-ttu-id="79d31-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="79d31-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
