---
title: Azure Application Insights Telemetry Data Model - Telemetry Context | Microsoft Docs
description: Application Insights telemetry context data model
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 05/15/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: b6cfae20f09b19a57cf411777e78abb1dbbf0484
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855935"
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="7ca76-103">Telemetry context: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="7ca76-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="7ca76-104">Every telemetry item may have a strongly typed context fields.</span><span class="sxs-lookup"><span data-stu-id="7ca76-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="7ca76-105">Every field enables a specific monitoring scenario.</span><span class="sxs-lookup"><span data-stu-id="7ca76-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="7ca76-106">Use the custom properties collection to store custom or application-specific contextual information.</span><span class="sxs-lookup"><span data-stu-id="7ca76-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


## <a name="application-version"></a><span data-ttu-id="7ca76-107">Application version</span><span class="sxs-lookup"><span data-stu-id="7ca76-107">Application version</span></span>

<span data-ttu-id="7ca76-108">Information in the application context fields is always about the application that is sending the telemetry.</span><span class="sxs-lookup"><span data-stu-id="7ca76-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="7ca76-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span><span class="sxs-lookup"><span data-stu-id="7ca76-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="7ca76-110">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="7ca76-110">Max length: 1024</span></span>


## <a name="client-ip-address"></a><span data-ttu-id="7ca76-111">Client IP address</span><span class="sxs-lookup"><span data-stu-id="7ca76-111">Client IP address</span></span>

<span data-ttu-id="7ca76-112">The IP address of the client device.</span><span class="sxs-lookup"><span data-stu-id="7ca76-112">The IP address of the client device.</span></span> <span data-ttu-id="7ca76-113">IPv4 and IPv6 are supported.</span><span class="sxs-lookup"><span data-stu-id="7ca76-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="7ca76-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span><span class="sxs-lookup"><span data-stu-id="7ca76-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="7ca76-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span><span class="sxs-lookup"><span data-stu-id="7ca76-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="7ca76-116">So client IP by itself cannot be used as end-user identifiable information.</span><span class="sxs-lookup"><span data-stu-id="7ca76-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="7ca76-117">Max length: 46</span><span class="sxs-lookup"><span data-stu-id="7ca76-117">Max length: 46</span></span>


## <a name="device-type"></a><span data-ttu-id="7ca76-118">Device type</span><span class="sxs-lookup"><span data-stu-id="7ca76-118">Device type</span></span>

<span data-ttu-id="7ca76-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span><span class="sxs-lookup"><span data-stu-id="7ca76-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="7ca76-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span><span class="sxs-lookup"><span data-stu-id="7ca76-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="7ca76-121">Max length: 64</span><span class="sxs-lookup"><span data-stu-id="7ca76-121">Max length: 64</span></span>


## <a name="operation-id"></a><span data-ttu-id="7ca76-122">Operation id</span><span class="sxs-lookup"><span data-stu-id="7ca76-122">Operation id</span></span>

<span data-ttu-id="7ca76-123">A unique identifier of the root operation.</span><span class="sxs-lookup"><span data-stu-id="7ca76-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="7ca76-124">This identifier allows to group telemetry across multiple components.</span><span class="sxs-lookup"><span data-stu-id="7ca76-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="7ca76-125">See [telemetry correlation](application-insights-correlation.md) for details.</span><span class="sxs-lookup"><span data-stu-id="7ca76-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="7ca76-126">The operation id is created by either a request or a page view.</span><span class="sxs-lookup"><span data-stu-id="7ca76-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="7ca76-127">All other telemetry sets this field to the value for the containing request or page view.</span><span class="sxs-lookup"><span data-stu-id="7ca76-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="7ca76-128">Max length: 128</span><span class="sxs-lookup"><span data-stu-id="7ca76-128">Max length: 128</span></span>


## <a name="parent-operation-id"></a><span data-ttu-id="7ca76-129">Parent operation ID</span><span class="sxs-lookup"><span data-stu-id="7ca76-129">Parent operation ID</span></span>

<span data-ttu-id="7ca76-130">The unique identifier of the telemetry item's immediate parent.</span><span class="sxs-lookup"><span data-stu-id="7ca76-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="7ca76-131">See [telemetry correlation](application-insights-correlation.md) for details.</span><span class="sxs-lookup"><span data-stu-id="7ca76-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="7ca76-132">Max length: 128</span><span class="sxs-lookup"><span data-stu-id="7ca76-132">Max length: 128</span></span>


## <a name="operation-name"></a><span data-ttu-id="7ca76-133">Operation name</span><span class="sxs-lookup"><span data-stu-id="7ca76-133">Operation name</span></span>

<span data-ttu-id="7ca76-134">The name (group) of the operation.</span><span class="sxs-lookup"><span data-stu-id="7ca76-134">The name (group) of the operation.</span></span> <span data-ttu-id="7ca76-135">The operation name is created by either a request or a page view.</span><span class="sxs-lookup"><span data-stu-id="7ca76-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="7ca76-136">All other telemetry items set this field to the value for the containing request or page view.</span><span class="sxs-lookup"><span data-stu-id="7ca76-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="7ca76-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span><span class="sxs-lookup"><span data-stu-id="7ca76-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="7ca76-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span><span class="sxs-lookup"><span data-stu-id="7ca76-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="7ca76-139">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="7ca76-139">Max length: 1024</span></span>


## <a name="synthetic-source-of-the-operation"></a><span data-ttu-id="7ca76-140">Synthetic source of the operation</span><span class="sxs-lookup"><span data-stu-id="7ca76-140">Synthetic source of the operation</span></span>

<span data-ttu-id="7ca76-141">Name of synthetic source.</span><span class="sxs-lookup"><span data-stu-id="7ca76-141">Name of synthetic source.</span></span> <span data-ttu-id="7ca76-142">Some telemetry from the application may represent synthetic traffic.</span><span class="sxs-lookup"><span data-stu-id="7ca76-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="7ca76-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span><span class="sxs-lookup"><span data-stu-id="7ca76-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="7ca76-144">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="7ca76-144">Max length: 1024</span></span>


## <a name="session-id"></a><span data-ttu-id="7ca76-145">Session id</span><span class="sxs-lookup"><span data-stu-id="7ca76-145">Session id</span></span>

<span data-ttu-id="7ca76-146">Session ID - the instance of the user's interaction with the app.</span><span class="sxs-lookup"><span data-stu-id="7ca76-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="7ca76-147">Information in the session context fields is always about the end user.</span><span class="sxs-lookup"><span data-stu-id="7ca76-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="7ca76-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span><span class="sxs-lookup"><span data-stu-id="7ca76-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="7ca76-149">Max length: 64</span><span class="sxs-lookup"><span data-stu-id="7ca76-149">Max length: 64</span></span>


## <a name="anonymous-user-id"></a><span data-ttu-id="7ca76-150">Anonymous user id</span><span class="sxs-lookup"><span data-stu-id="7ca76-150">Anonymous user id</span></span>

<span data-ttu-id="7ca76-151">Anonymous user id. Represents the end user of the application.</span><span class="sxs-lookup"><span data-stu-id="7ca76-151">Anonymous user id. Represents the end user of the application.</span></span> <span data-ttu-id="7ca76-152">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span><span class="sxs-lookup"><span data-stu-id="7ca76-152">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="7ca76-153">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span><span class="sxs-lookup"><span data-stu-id="7ca76-153">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="7ca76-154">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span><span class="sxs-lookup"><span data-stu-id="7ca76-154">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="7ca76-155">Anonymous user id is used for sampling score generation.</span><span class="sxs-lookup"><span data-stu-id="7ca76-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="7ca76-156">So anonymous user id should be a random enough value.</span><span class="sxs-lookup"><span data-stu-id="7ca76-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="7ca76-157">Using anonymous user id to store user name is a misuse of the field.</span><span class="sxs-lookup"><span data-stu-id="7ca76-157">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="7ca76-158">Use Authenticated user id.</span><span class="sxs-lookup"><span data-stu-id="7ca76-158">Use Authenticated user id.</span></span>

<span data-ttu-id="7ca76-159">Max length: 128</span><span class="sxs-lookup"><span data-stu-id="7ca76-159">Max length: 128</span></span>


## <a name="authenticated-user-id"></a><span data-ttu-id="7ca76-160">Authenticated user id</span><span class="sxs-lookup"><span data-stu-id="7ca76-160">Authenticated user id</span></span>

<span data-ttu-id="7ca76-161">Authenticated user id. The opposite of anonymous user id, this field represents the user with a friendly name.</span><span class="sxs-lookup"><span data-stu-id="7ca76-161">Authenticated user id. The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="7ca76-162">Since its PII information it is not collected by default by most SDK.</span><span class="sxs-lookup"><span data-stu-id="7ca76-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="7ca76-163">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="7ca76-163">Max length: 1024</span></span>


## <a name="account-id"></a><span data-ttu-id="7ca76-164">Account id</span><span class="sxs-lookup"><span data-stu-id="7ca76-164">Account id</span></span>

<span data-ttu-id="7ca76-165">In multi-tenant applications this is the account ID or name, which the user is acting with.</span><span class="sxs-lookup"><span data-stu-id="7ca76-165">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="7ca76-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span><span class="sxs-lookup"><span data-stu-id="7ca76-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="7ca76-167">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="7ca76-167">Max length: 1024</span></span>


## <a name="cloud-role"></a><span data-ttu-id="7ca76-168">Cloud role</span><span class="sxs-lookup"><span data-stu-id="7ca76-168">Cloud role</span></span>

<span data-ttu-id="7ca76-169">Name of the role the application is a part of.</span><span class="sxs-lookup"><span data-stu-id="7ca76-169">Name of the role the application is a part of.</span></span> <span data-ttu-id="7ca76-170">Maps directly to the role name in azure.</span><span class="sxs-lookup"><span data-stu-id="7ca76-170">Maps directly to the role name in azure.</span></span> <span data-ttu-id="7ca76-171">Can also be used to distinguish micro services, which are part of a single application.</span><span class="sxs-lookup"><span data-stu-id="7ca76-171">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="7ca76-172">Max length: 256</span><span class="sxs-lookup"><span data-stu-id="7ca76-172">Max length: 256</span></span>


## <a name="cloud-role-instance"></a><span data-ttu-id="7ca76-173">Cloud role instance</span><span class="sxs-lookup"><span data-stu-id="7ca76-173">Cloud role instance</span></span>

<span data-ttu-id="7ca76-174">Name of the instance where the application is running.</span><span class="sxs-lookup"><span data-stu-id="7ca76-174">Name of the instance where the application is running.</span></span> <span data-ttu-id="7ca76-175">Computer name for on-premises, instance name for Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca76-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="7ca76-176">Max length: 256</span><span class="sxs-lookup"><span data-stu-id="7ca76-176">Max length: 256</span></span>


## <a name="internal-sdk-version"></a><span data-ttu-id="7ca76-177">Internal: SDK version</span><span class="sxs-lookup"><span data-stu-id="7ca76-177">Internal: SDK version</span></span>

<span data-ttu-id="7ca76-178">SDK version.</span><span class="sxs-lookup"><span data-stu-id="7ca76-178">SDK version.</span></span> <span data-ttu-id="7ca76-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span><span class="sxs-lookup"><span data-stu-id="7ca76-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="7ca76-180">Max length: 64</span><span class="sxs-lookup"><span data-stu-id="7ca76-180">Max length: 64</span></span>


## <a name="internal-node-name"></a><span data-ttu-id="7ca76-181">Internal: Node name</span><span class="sxs-lookup"><span data-stu-id="7ca76-181">Internal: Node name</span></span>

<span data-ttu-id="7ca76-182">This field represents the node name used for billing purposes.</span><span class="sxs-lookup"><span data-stu-id="7ca76-182">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="7ca76-183">Use it to override the standard detection of nodes.</span><span class="sxs-lookup"><span data-stu-id="7ca76-183">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="7ca76-184">Max length: 256</span><span class="sxs-lookup"><span data-stu-id="7ca76-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ca76-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ca76-185">Next steps</span></span>

- <span data-ttu-id="7ca76-186">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7ca76-186">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="7ca76-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="7ca76-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="7ca76-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="7ca76-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
