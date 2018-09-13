---
title: IP addresses used by Application Insights | Microsoft Docs
description: Server firewall exceptions required by Application Insights
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: douge
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: awills
ms.openlocfilehash: a11d03c370995347b94220d0fbb7b02ee1361aae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556118"
---
# <a name="ip-addresses-used-by-application-insights"></a><span data-ttu-id="3b3da-103">IP addresses used by Application Insights</span><span class="sxs-lookup"><span data-stu-id="3b3da-103">IP addresses used by Application Insights</span></span>
<span data-ttu-id="3b3da-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="3b3da-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="3b3da-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span><span class="sxs-lookup"><span data-stu-id="3b3da-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3da-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span><span class="sxs-lookup"><span data-stu-id="3b3da-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="3b3da-107">Outgoing ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-107">Outgoing ports</span></span>
<span data-ttu-id="3b3da-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span><span class="sxs-lookup"><span data-stu-id="3b3da-108">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="3b3da-109">Purpose</span><span class="sxs-lookup"><span data-stu-id="3b3da-109">Purpose</span></span> | <span data-ttu-id="3b3da-110">URL</span><span class="sxs-lookup"><span data-stu-id="3b3da-110">URL</span></span> | <span data-ttu-id="3b3da-111">IP</span><span class="sxs-lookup"><span data-stu-id="3b3da-111">IP</span></span> | <span data-ttu-id="3b3da-112">Ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-112">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3da-113">Telemetry</span><span class="sxs-lookup"><span data-stu-id="3b3da-113">Telemetry</span></span> |<span data-ttu-id="3b3da-114">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-114">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="3b3da-115">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-115">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="3b3da-116">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="3b3da-116">40.114.241.141</span></span><br/><span data-ttu-id="3b3da-117">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="3b3da-117">104.45.136.42</span></span><br/><span data-ttu-id="3b3da-118">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="3b3da-118">40.84.189.107</span></span><br/><span data-ttu-id="3b3da-119">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="3b3da-119">168.63.242.221</span></span> |<span data-ttu-id="3b3da-120">443</span><span class="sxs-lookup"><span data-stu-id="3b3da-120">443</span></span> |
| <span data-ttu-id="3b3da-121">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="3b3da-121">Live Metrics Stream</span></span> |<span data-ttu-id="3b3da-122">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-122">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="3b3da-123">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-123">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="3b3da-124">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="3b3da-124">23.96.28.38</span></span><br/><span data-ttu-id="3b3da-125">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="3b3da-125">13.92.40.198</span></span> |<span data-ttu-id="3b3da-126">443</span><span class="sxs-lookup"><span data-stu-id="3b3da-126">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="3b3da-127">Status Monitor</span><span class="sxs-lookup"><span data-stu-id="3b3da-127">Status Monitor</span></span>
<span data-ttu-id="3b3da-128">Status Monitor Configuration - needed only when making changes.</span><span class="sxs-lookup"><span data-stu-id="3b3da-128">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="3b3da-129">Purpose</span><span class="sxs-lookup"><span data-stu-id="3b3da-129">Purpose</span></span> | <span data-ttu-id="3b3da-130">URL</span><span class="sxs-lookup"><span data-stu-id="3b3da-130">URL</span></span> | <span data-ttu-id="3b3da-131">IP</span><span class="sxs-lookup"><span data-stu-id="3b3da-131">IP</span></span> | <span data-ttu-id="3b3da-132">Ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-132">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3da-133">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-133">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="3b3da-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-134">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="3b3da-135">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-135">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="3b3da-136">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-136">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="3b3da-137">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-137">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="3b3da-138">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-138">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="3b3da-139">Configuration</span><span class="sxs-lookup"><span data-stu-id="3b3da-139">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="3b3da-140">Installation</span><span class="sxs-lookup"><span data-stu-id="3b3da-140">Installation</span></span> |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a><span data-ttu-id="3b3da-141">HockeyApp</span><span class="sxs-lookup"><span data-stu-id="3b3da-141">HockeyApp</span></span>
| <span data-ttu-id="3b3da-142">Purpose</span><span class="sxs-lookup"><span data-stu-id="3b3da-142">Purpose</span></span> | <span data-ttu-id="3b3da-143">URL</span><span class="sxs-lookup"><span data-stu-id="3b3da-143">URL</span></span> | <span data-ttu-id="3b3da-144">IP</span><span class="sxs-lookup"><span data-stu-id="3b3da-144">IP</span></span> | <span data-ttu-id="3b3da-145">Ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-145">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3da-146">Crash data</span><span class="sxs-lookup"><span data-stu-id="3b3da-146">Crash data</span></span> |<span data-ttu-id="3b3da-147">gate.hockeyapp.net</span><span class="sxs-lookup"><span data-stu-id="3b3da-147">gate.hockeyapp.net</span></span> |<span data-ttu-id="3b3da-148">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="3b3da-148">104.45.136.42</span></span> |<span data-ttu-id="3b3da-149">80, 443</span><span class="sxs-lookup"><span data-stu-id="3b3da-149">80, 443</span></span> |

## <a name="availability-tests"></a><span data-ttu-id="3b3da-150">Availability tests</span><span class="sxs-lookup"><span data-stu-id="3b3da-150">Availability tests</span></span>
<span data-ttu-id="3b3da-151">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span><span class="sxs-lookup"><span data-stu-id="3b3da-151">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="3b3da-152">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span><span class="sxs-lookup"><span data-stu-id="3b3da-152">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="3b3da-153">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses:</span><span class="sxs-lookup"><span data-stu-id="3b3da-153">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses:</span></span>

```
13.106.106.20
13.106.106.21
13.106.106.22
13.106.106.23
13.106.106.24
13.106.106.25
13.106.106.26
13.106.106.27
13.106.106.28
13.106.106.29
157.55.14.43
157.55.14.44
157.55.14.47
157.55.14.49
157.55.14.50
157.55.14.60
157.55.14.61
157.55.14.62
157.55.14.64
157.55.14.65
202.89.228.57
202.89.228.67
202.89.228.68
202.89.228.69
207.46.14.51
207.46.14.52
207.46.14.55
207.46.14.56
207.46.14.60
207.46.14.61
207.46.14.62
207.46.14.63
207.46.14.64
207.46.14.65
207.46.14.67
207.46.14.68
207.46.56.57
207.46.56.58
207.46.56.59
207.46.56.61
207.46.56.62
207.46.56.63
207.46.56.64
207.46.56.67
207.46.71.37
207.46.71.38
207.46.71.51
207.46.71.52
207.46.71.54
207.46.71.55
207.46.71.57
207.46.71.58
207.46.98.152
207.46.98.153
207.46.98.156
207.46.98.157
207.46.98.158
207.46.98.159
207.46.98.160
207.46.98.162
207.46.98.169
207.46.98.170
207.46.98.171
207.46.98.172
213.199.178.54
213.199.178.55
213.199.178.56
213.199.178.57
213.199.178.58
213.199.178.59
213.199.178.60
213.199.178.61
213.199.178.63
213.199.178.64
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
65.54.66.56
65.54.66.57
65.54.66.58
65.54.66.61
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
65.55.82.77
65.55.82.78
65.55.82.81
65.55.82.84
65.55.82.85
65.55.82.86
65.55.82.87
65.55.82.88
65.55.82.89
65.55.82.90
65.55.82.91
65.55.82.92
70.37.147.43
70.37.147.44
70.37.147.45
70.37.147.48
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38


```  

## <a name="data-access-api"></a><span data-ttu-id="3b3da-154">Data access API</span><span class="sxs-lookup"><span data-stu-id="3b3da-154">Data access API</span></span>
| <span data-ttu-id="3b3da-155">Purpose</span><span class="sxs-lookup"><span data-stu-id="3b3da-155">Purpose</span></span> | <span data-ttu-id="3b3da-156">URI</span><span class="sxs-lookup"><span data-stu-id="3b3da-156">URI</span></span> | <span data-ttu-id="3b3da-157">IP</span><span class="sxs-lookup"><span data-stu-id="3b3da-157">IP</span></span> | <span data-ttu-id="3b3da-158">Ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-158">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3da-159">API</span><span class="sxs-lookup"><span data-stu-id="3b3da-159">API</span></span> |<span data-ttu-id="3b3da-160">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-160">api.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-161">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-161">api1.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-162">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-162">api2.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-163">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-163">api3.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-164">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-164">api4.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-165">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-165">api5.applicationinsights.io</span></span> |<span data-ttu-id="3b3da-166">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="3b3da-166">13.82.26.252</span></span><br/><span data-ttu-id="3b3da-167">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="3b3da-167">40.76.213.73</span></span> |<span data-ttu-id="3b3da-168">80,443</span><span class="sxs-lookup"><span data-stu-id="3b3da-168">80,443</span></span> |
| <span data-ttu-id="3b3da-169">API docs</span><span class="sxs-lookup"><span data-stu-id="3b3da-169">API docs</span></span> |<span data-ttu-id="3b3da-170">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-170">dev.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-171">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-171">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="3b3da-172">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-172">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="3b3da-173">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="3b3da-173">www.applicationinsights.io</span></span><br/><span data-ttu-id="3b3da-174">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-174">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="3b3da-175">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="3b3da-175">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="3b3da-176">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="3b3da-176">13.82.24.149</span></span><br/><span data-ttu-id="3b3da-177">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="3b3da-177">40.114.82.10</span></span> |<span data-ttu-id="3b3da-178">80,443</span><span class="sxs-lookup"><span data-stu-id="3b3da-178">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="3b3da-179">Profiler</span><span class="sxs-lookup"><span data-stu-id="3b3da-179">Profiler</span></span>

| <span data-ttu-id="3b3da-180">Purpose</span><span class="sxs-lookup"><span data-stu-id="3b3da-180">Purpose</span></span> | <span data-ttu-id="3b3da-181">URI</span><span class="sxs-lookup"><span data-stu-id="3b3da-181">URI</span></span> | <span data-ttu-id="3b3da-182">IP</span><span class="sxs-lookup"><span data-stu-id="3b3da-182">IP</span></span> | <span data-ttu-id="3b3da-183">Ports</span><span class="sxs-lookup"><span data-stu-id="3b3da-183">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3da-184">Agent</span><span class="sxs-lookup"><span data-stu-id="3b3da-184">Agent</span></span> | <span data-ttu-id="3b3da-185">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="3b3da-185">agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="3b3da-186">dynamic</span><span class="sxs-lookup"><span data-stu-id="3b3da-186">dynamic</span></span> | <span data-ttu-id="3b3da-187">443</span><span class="sxs-lookup"><span data-stu-id="3b3da-187">443</span></span>
| <span data-ttu-id="3b3da-188">Portal</span><span class="sxs-lookup"><span data-stu-id="3b3da-188">Portal</span></span> | <span data-ttu-id="3b3da-189">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="3b3da-189">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="3b3da-190">dynamic</span><span class="sxs-lookup"><span data-stu-id="3b3da-190">dynamic</span></span> | <span data-ttu-id="3b3da-191">443</span><span class="sxs-lookup"><span data-stu-id="3b3da-191">443</span></span>
