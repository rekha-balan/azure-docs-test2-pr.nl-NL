---
title: IP addresses used by Application Insights and Log Analytics | Microsoft Docs
description: Server firewall exceptions required by Application Insights
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/23/2018
ms.author: mbullwin
ms.openlocfilehash: 724cdb82f601805ffd93f1afd0c27983cc1ef96b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783151"
---
# <a name="ip-addresses-used-by-application-insights-and-log-analytics"></a><span data-ttu-id="d5ff7-103">IP addresses used by Application Insights and Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d5ff7-103">IP addresses used by Application Insights and Log Analytics</span></span>
<span data-ttu-id="d5ff7-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-104">The [Azure Application Insights](app-insights-overview.md) service uses a number of IP addresses.</span></span> <span data-ttu-id="d5ff7-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-105">You might need to know these addresses if the app that you are monitoring is hosted behind a firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="d5ff7-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-106">Although these addresses are static, it's possible that we will need to change them from time to time.</span></span>
> 
> 

> [!TIP]
> <span data-ttu-id="d5ff7-107">Subscribe to this page as a RSS feed by adding https://github.com/MicrosoftDocs/azure-docs/commits/master/articles/application-insights/app-insights-ip-addresses.md.atom to your favorite RSS/ATOM reader to get notified of the latest changes.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-107">Subscribe to this page as a RSS feed by adding https://github.com/MicrosoftDocs/azure-docs/commits/master/articles/application-insights/app-insights-ip-addresses.md.atom to your favorite RSS/ATOM reader to get notified of the latest changes.</span></span>
> 
> 

## <a name="outgoing-ports"></a><span data-ttu-id="d5ff7-108">Outgoing ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-108">Outgoing ports</span></span>
<span data-ttu-id="d5ff7-109">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span><span class="sxs-lookup"><span data-stu-id="d5ff7-109">You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:</span></span>

| <span data-ttu-id="d5ff7-110">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-110">Purpose</span></span> | <span data-ttu-id="d5ff7-111">URL</span><span class="sxs-lookup"><span data-stu-id="d5ff7-111">URL</span></span> | <span data-ttu-id="d5ff7-112">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-112">IP</span></span> | <span data-ttu-id="d5ff7-113">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-113">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-114">Telemetry</span><span class="sxs-lookup"><span data-stu-id="d5ff7-114">Telemetry</span></span> |<span data-ttu-id="d5ff7-115">dc.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-115">dc.services.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-116">dc.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-116">dc.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d5ff7-117">40.114.241.141</span><span class="sxs-lookup"><span data-stu-id="d5ff7-117">40.114.241.141</span></span><br/><span data-ttu-id="d5ff7-118">104.45.136.42</span><span class="sxs-lookup"><span data-stu-id="d5ff7-118">104.45.136.42</span></span><br/><span data-ttu-id="d5ff7-119">40.84.189.107</span><span class="sxs-lookup"><span data-stu-id="d5ff7-119">40.84.189.107</span></span><br/><span data-ttu-id="d5ff7-120">168.63.242.221</span><span class="sxs-lookup"><span data-stu-id="d5ff7-120">168.63.242.221</span></span><br/><span data-ttu-id="d5ff7-121">52.167.221.184</span><span class="sxs-lookup"><span data-stu-id="d5ff7-121">52.167.221.184</span></span><br/><span data-ttu-id="d5ff7-122">52.169.64.244</span><span class="sxs-lookup"><span data-stu-id="d5ff7-122">52.169.64.244</span></span><br/><span data-ttu-id="d5ff7-123">40.85.218.175</span><span class="sxs-lookup"><span data-stu-id="d5ff7-123">40.85.218.175</span></span><br/><span data-ttu-id="d5ff7-124">104.211.92.54</span><span class="sxs-lookup"><span data-stu-id="d5ff7-124">104.211.92.54</span></span><br/><span data-ttu-id="d5ff7-125">52.175.198.74</span><span class="sxs-lookup"><span data-stu-id="d5ff7-125">52.175.198.74</span></span> | <span data-ttu-id="d5ff7-126">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-126">443</span></span> |
| <span data-ttu-id="d5ff7-127">Live Metrics Stream</span><span class="sxs-lookup"><span data-stu-id="d5ff7-127">Live Metrics Stream</span></span> |<span data-ttu-id="d5ff7-128">rt.services.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-128">rt.services.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-129">rt.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-129">rt.applicationinsights.microsoft.com</span></span> |<span data-ttu-id="d5ff7-130">23.96.28.38</span><span class="sxs-lookup"><span data-stu-id="d5ff7-130">23.96.28.38</span></span><br/><span data-ttu-id="d5ff7-131">13.92.40.198</span><span class="sxs-lookup"><span data-stu-id="d5ff7-131">13.92.40.198</span></span> |<span data-ttu-id="d5ff7-132">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-132">443</span></span> |

## <a name="status-monitor"></a><span data-ttu-id="d5ff7-133">Status Monitor</span><span class="sxs-lookup"><span data-stu-id="d5ff7-133">Status Monitor</span></span>
<span data-ttu-id="d5ff7-134">Status Monitor Configuration - needed only when making changes.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-134">Status Monitor Configuration - needed only when making changes.</span></span>

| <span data-ttu-id="d5ff7-135">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-135">Purpose</span></span> | <span data-ttu-id="d5ff7-136">URL</span><span class="sxs-lookup"><span data-stu-id="d5ff7-136">URL</span></span> | <span data-ttu-id="d5ff7-137">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-137">IP</span></span> | <span data-ttu-id="d5ff7-138">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-138">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-139">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-139">Configuration</span></span> |`management.core.windows.net` | |`443` |
| <span data-ttu-id="d5ff7-140">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-140">Configuration</span></span> |`management.azure.com` | |`443` |
| <span data-ttu-id="d5ff7-141">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-141">Configuration</span></span> |`login.windows.net` | |`443` |
| <span data-ttu-id="d5ff7-142">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-142">Configuration</span></span> |`login.microsoftonline.com` | |`443` |
| <span data-ttu-id="d5ff7-143">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-143">Configuration</span></span> |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| <span data-ttu-id="d5ff7-144">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-144">Configuration</span></span> |`auth.gfx.ms` | |`443` |
| <span data-ttu-id="d5ff7-145">Configuration</span><span class="sxs-lookup"><span data-stu-id="d5ff7-145">Configuration</span></span> |`login.live.com` | |`443` |
| <span data-ttu-id="d5ff7-146">Installation</span><span class="sxs-lookup"><span data-stu-id="d5ff7-146">Installation</span></span> |<span data-ttu-id="d5ff7-147">`packages.nuget.org` , `nuget.org`, `api.nuget.org`, `az320820.vo.msecnd.net` (NuGet Downloads)</span><span class="sxs-lookup"><span data-stu-id="d5ff7-147">`packages.nuget.org` , `nuget.org`, `api.nuget.org`, `az320820.vo.msecnd.net` (NuGet Downloads)</span></span> | |`443` |

## <a name="availability-tests"></a><span data-ttu-id="d5ff7-148">Availability tests</span><span class="sxs-lookup"><span data-stu-id="d5ff7-148">Availability tests</span></span>
<span data-ttu-id="d5ff7-149">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-149">This is the list of addresses from which [availability web tests](app-insights-monitor-web-app-availability.md) are run.</span></span> <span data-ttu-id="d5ff7-150">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-150">If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.</span></span>

<span data-ttu-id="d5ff7-151">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span><span class="sxs-lookup"><span data-stu-id="d5ff7-151">Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):</span></span>

```
Australia East
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
Brazil South
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
France South
52.136.140.221
52.136.140.222
52.136.140.223
52.136.140.226
France Central
52.143.140.242
52.143.140.246
52.143.140.247
52.143.140.249
40.89.137.100
40.89.142.126
40.89.131.237
40.89.136.180
East Asia
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
North Europe
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
40.112.90.148
40.112.94.212
104.46.15.57
40.115.125.114
Japan East
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
West Europe
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
23.100.10.236
23.100.6.155
52.232.113.84
51.144.113.219
UK South
51.140.79.229
51.140.84.172
51.140.87.211
51.140.105.74
UK West
51.141.25.219
51.141.32.101
51.141.35.167
51.141.54.177
51.140.240.239
51.140.205.236
51.140.245.132
51.140.203.56
Southeast Asia
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
West US
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
104.42.39.222
104.42.145.220
104.42.60.160
104.42.248.11
40.83.163.29
104.42.195.57
40.78.19.163
40.78.23.43
Central US
52.165.130.58
52.173.142.229
52.173.147.190
52.173.17.41
52.173.204.247
52.173.244.190
52.173.36.222
52.176.1.226
104.43.251.84
40.113.236.73
40.113.230.234
40.113.195.109
104.43.215.218
104.43.240.112
North Central US
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
65.52.205.196
23.100.75.146
65.52.63.179
157.55.143.58
South Central US
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
40.124.36.120
104.210.216.32
104.215.75.92
104.215.77.186
East US
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26
104.41.133.69
137.117.103.13
40.114.75.45
40.121.8.31
168.62.41.234
168.62.168.66

```  

## <a name="application-insights-api"></a><span data-ttu-id="d5ff7-152">Application Insights API</span><span class="sxs-lookup"><span data-stu-id="d5ff7-152">Application Insights API</span></span>
| <span data-ttu-id="d5ff7-153">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-153">Purpose</span></span> | <span data-ttu-id="d5ff7-154">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-154">URI</span></span> | <span data-ttu-id="d5ff7-155">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-155">IP</span></span> | <span data-ttu-id="d5ff7-156">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-156">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-157">API</span><span class="sxs-lookup"><span data-stu-id="d5ff7-157">API</span></span> |<span data-ttu-id="d5ff7-158">api.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-158">api.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-159">api1.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-159">api1.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-160">api2.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-160">api2.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-161">api3.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-161">api3.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-162">api4.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-162">api4.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-163">api5.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-163">api5.applicationinsights.io</span></span> |<span data-ttu-id="d5ff7-164">13.82.26.252</span><span class="sxs-lookup"><span data-stu-id="d5ff7-164">13.82.26.252</span></span><br/><span data-ttu-id="d5ff7-165">40.76.213.73</span><span class="sxs-lookup"><span data-stu-id="d5ff7-165">40.76.213.73</span></span> |<span data-ttu-id="d5ff7-166">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-166">80,443</span></span> |
| <span data-ttu-id="d5ff7-167">API docs</span><span class="sxs-lookup"><span data-stu-id="d5ff7-167">API docs</span></span> |<span data-ttu-id="d5ff7-168">dev.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-168">dev.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-169">dev.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-169">dev.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d5ff7-170">dev.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-170">dev.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-171">www.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-171">www.applicationinsights.io</span></span><br/><span data-ttu-id="d5ff7-172">www.applicationinsights.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-172">www.applicationinsights.microsoft.com</span></span><br/><span data-ttu-id="d5ff7-173">www.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-173">www.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d5ff7-174">13.82.24.149</span><span class="sxs-lookup"><span data-stu-id="d5ff7-174">13.82.24.149</span></span><br/><span data-ttu-id="d5ff7-175">40.114.82.10</span><span class="sxs-lookup"><span data-stu-id="d5ff7-175">40.114.82.10</span></span> |<span data-ttu-id="d5ff7-176">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-176">80,443</span></span> |
| <span data-ttu-id="d5ff7-177">Internal API</span><span class="sxs-lookup"><span data-stu-id="d5ff7-177">Internal API</span></span> |<span data-ttu-id="d5ff7-178">aigs.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-178">aigs.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-179">aigs1.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-179">aigs1.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-180">aigs2.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-180">aigs2.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-181">aigs3.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-181">aigs3.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-182">aigs4.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-182">aigs4.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-183">aigs5.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-183">aigs5.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-184">aigs6.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-184">aigs6.aisvc.visualstudio.com</span></span> |<span data-ttu-id="d5ff7-185">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-185">dynamic</span></span>|<span data-ttu-id="d5ff7-186">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-186">443</span></span> |

## <a name="log-analytics-api"></a><span data-ttu-id="d5ff7-187">Log Analytics API</span><span class="sxs-lookup"><span data-stu-id="d5ff7-187">Log Analytics API</span></span>
| <span data-ttu-id="d5ff7-188">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-188">Purpose</span></span> | <span data-ttu-id="d5ff7-189">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-189">URI</span></span> | <span data-ttu-id="d5ff7-190">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-190">IP</span></span> | <span data-ttu-id="d5ff7-191">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-191">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-192">API</span><span class="sxs-lookup"><span data-stu-id="d5ff7-192">API</span></span> |<span data-ttu-id="d5ff7-193">api.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-193">api.loganalytics.io</span></span><br/><span data-ttu-id="d5ff7-194">\*.api.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-194">\*.api.loganalytics.io</span></span> |<span data-ttu-id="d5ff7-195">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-195">dynamic</span></span> |<span data-ttu-id="d5ff7-196">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-196">80,443</span></span> |
| <span data-ttu-id="d5ff7-197">API docs</span><span class="sxs-lookup"><span data-stu-id="d5ff7-197">API docs</span></span> |<span data-ttu-id="d5ff7-198">dev.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-198">dev.loganalytics.io</span></span><br/><span data-ttu-id="d5ff7-199">docs.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-199">docs.loganalytics.io</span></span><br/><span data-ttu-id="d5ff7-200">www.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-200">www.loganalytics.io</span></span> |<span data-ttu-id="d5ff7-201">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-201">dynamic</span></span> |<span data-ttu-id="d5ff7-202">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-202">80,443</span></span> |

## <a name="application-insights-analytics"></a><span data-ttu-id="d5ff7-203">Application Insights Analytics</span><span class="sxs-lookup"><span data-stu-id="d5ff7-203">Application Insights Analytics</span></span>

| <span data-ttu-id="d5ff7-204">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-204">Purpose</span></span> | <span data-ttu-id="d5ff7-205">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-205">URI</span></span> | <span data-ttu-id="d5ff7-206">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-206">IP</span></span> | <span data-ttu-id="d5ff7-207">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-207">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-208">Analytics Portal</span><span class="sxs-lookup"><span data-stu-id="d5ff7-208">Analytics Portal</span></span> | <span data-ttu-id="d5ff7-209">analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-209">analytics.applicationinsights.io</span></span> | <span data-ttu-id="d5ff7-210">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-210">dynamic</span></span> | <span data-ttu-id="d5ff7-211">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-211">80,443</span></span> |
| <span data-ttu-id="d5ff7-212">CDN</span><span class="sxs-lookup"><span data-stu-id="d5ff7-212">CDN</span></span> | <span data-ttu-id="d5ff7-213">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-213">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="d5ff7-214">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-214">dynamic</span></span> | <span data-ttu-id="d5ff7-215">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-215">80,443</span></span> |
| <span data-ttu-id="d5ff7-216">Media CDN</span><span class="sxs-lookup"><span data-stu-id="d5ff7-216">Media CDN</span></span> | <span data-ttu-id="d5ff7-217">applicationanalyticsmedia.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-217">applicationanalyticsmedia.azureedge.net</span></span> | <span data-ttu-id="d5ff7-218">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-218">dynamic</span></span> | <span data-ttu-id="d5ff7-219">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-219">80,443</span></span> |

<span data-ttu-id="d5ff7-220">Note: \*.applicationinsights.io domain is owned by Application Insights team.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-220">Note: \*.applicationinsights.io domain is owned by Application Insights team.</span></span>

## <a name="log-analytics-portal"></a><span data-ttu-id="d5ff7-221">Log Analytics Portal</span><span class="sxs-lookup"><span data-stu-id="d5ff7-221">Log Analytics Portal</span></span>

| <span data-ttu-id="d5ff7-222">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-222">Purpose</span></span> | <span data-ttu-id="d5ff7-223">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-223">URI</span></span> | <span data-ttu-id="d5ff7-224">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-224">IP</span></span> | <span data-ttu-id="d5ff7-225">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-225">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-226">Portal</span><span class="sxs-lookup"><span data-stu-id="d5ff7-226">Portal</span></span> | <span data-ttu-id="d5ff7-227">portal.loganalytics.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-227">portal.loganalytics.io</span></span> | <span data-ttu-id="d5ff7-228">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-228">dynamic</span></span> | <span data-ttu-id="d5ff7-229">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-229">80,443</span></span> |
| <span data-ttu-id="d5ff7-230">CDN</span><span class="sxs-lookup"><span data-stu-id="d5ff7-230">CDN</span></span> | <span data-ttu-id="d5ff7-231">applicationanalytics.azureedge.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-231">applicationanalytics.azureedge.net</span></span> | <span data-ttu-id="d5ff7-232">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-232">dynamic</span></span> | <span data-ttu-id="d5ff7-233">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-233">80,443</span></span> |

<span data-ttu-id="d5ff7-234">Note: \*.loganalytics.io domain is owned by the Log Analytics team.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-234">Note: \*.loganalytics.io domain is owned by the Log Analytics team.</span></span>

## <a name="application-insights-azure-portal-extension"></a><span data-ttu-id="d5ff7-235">Application Insights Azure portal Extension</span><span class="sxs-lookup"><span data-stu-id="d5ff7-235">Application Insights Azure portal Extension</span></span>

| <span data-ttu-id="d5ff7-236">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-236">Purpose</span></span> | <span data-ttu-id="d5ff7-237">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-237">URI</span></span> | <span data-ttu-id="d5ff7-238">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-238">IP</span></span> | <span data-ttu-id="d5ff7-239">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-239">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-240">Application Insights Extension</span><span class="sxs-lookup"><span data-stu-id="d5ff7-240">Application Insights Extension</span></span> | <span data-ttu-id="d5ff7-241">stamp2.app.insightsportal.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-241">stamp2.app.insightsportal.visualstudio.com</span></span> | <span data-ttu-id="d5ff7-242">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-242">dynamic</span></span> | <span data-ttu-id="d5ff7-243">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-243">80,443</span></span> |
| <span data-ttu-id="d5ff7-244">Application Insights Extension CDN</span><span class="sxs-lookup"><span data-stu-id="d5ff7-244">Application Insights Extension CDN</span></span> | <span data-ttu-id="d5ff7-245">insightsportal-prod2-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-245">insightsportal-prod2-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-246">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span><span class="sxs-lookup"><span data-stu-id="d5ff7-246">insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com</span></span><br/><span data-ttu-id="d5ff7-247">insightsportal-cdn-aimon.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="d5ff7-247">insightsportal-cdn-aimon.applicationinsights.io</span></span> | <span data-ttu-id="d5ff7-248">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-248">dynamic</span></span> | <span data-ttu-id="d5ff7-249">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-249">80,443</span></span> |

## <a name="application-insights-sdks"></a><span data-ttu-id="d5ff7-250">Application Insights SDKs</span><span class="sxs-lookup"><span data-stu-id="d5ff7-250">Application Insights SDKs</span></span>

| <span data-ttu-id="d5ff7-251">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-251">Purpose</span></span> | <span data-ttu-id="d5ff7-252">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-252">URI</span></span> | <span data-ttu-id="d5ff7-253">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-253">IP</span></span> | <span data-ttu-id="d5ff7-254">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-254">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-255">Application Insights JS SDK CDN</span><span class="sxs-lookup"><span data-stu-id="d5ff7-255">Application Insights JS SDK CDN</span></span> | <span data-ttu-id="d5ff7-256">az416426.vo.msecnd.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-256">az416426.vo.msecnd.net</span></span> | <span data-ttu-id="d5ff7-257">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-257">dynamic</span></span> | <span data-ttu-id="d5ff7-258">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-258">80,443</span></span> |
| <span data-ttu-id="d5ff7-259">Application Insights Java SDK</span><span class="sxs-lookup"><span data-stu-id="d5ff7-259">Application Insights Java SDK</span></span> | <span data-ttu-id="d5ff7-260">aijavasdk.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-260">aijavasdk.blob.core.windows.net</span></span> | <span data-ttu-id="d5ff7-261">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-261">dynamic</span></span> | <span data-ttu-id="d5ff7-262">80,443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-262">80,443</span></span> |

## <a name="profiler"></a><span data-ttu-id="d5ff7-263">Profiler</span><span class="sxs-lookup"><span data-stu-id="d5ff7-263">Profiler</span></span>

| <span data-ttu-id="d5ff7-264">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-264">Purpose</span></span> | <span data-ttu-id="d5ff7-265">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-265">URI</span></span> | <span data-ttu-id="d5ff7-266">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-266">IP</span></span> | <span data-ttu-id="d5ff7-267">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-267">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-268">Agent</span><span class="sxs-lookup"><span data-stu-id="d5ff7-268">Agent</span></span> | <span data-ttu-id="d5ff7-269">agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-269">agent.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d5ff7-270">\*.agent.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-270">\*.agent.azureserviceprofiler.net</span></span> | <span data-ttu-id="d5ff7-271">51.143.96.206</span><span class="sxs-lookup"><span data-stu-id="d5ff7-271">51.143.96.206</span></span><br/><span data-ttu-id="d5ff7-272">51.143.98.157</span><span class="sxs-lookup"><span data-stu-id="d5ff7-272">51.143.98.157</span></span><br/><span data-ttu-id="d5ff7-273">52.161.8.88</span><span class="sxs-lookup"><span data-stu-id="d5ff7-273">52.161.8.88</span></span><br/><span data-ttu-id="d5ff7-274">52.161.29.225</span><span class="sxs-lookup"><span data-stu-id="d5ff7-274">52.161.29.225</span></span><br/><span data-ttu-id="d5ff7-275">52.178.149.106</span><span class="sxs-lookup"><span data-stu-id="d5ff7-275">52.178.149.106</span></span><br/><span data-ttu-id="d5ff7-276">52.178.147.66</span><span class="sxs-lookup"><span data-stu-id="d5ff7-276">52.178.147.66</span></span><br/><span data-ttu-id="d5ff7-277">40.68.32.221</span><span class="sxs-lookup"><span data-stu-id="d5ff7-277">40.68.32.221</span></span><br/><span data-ttu-id="d5ff7-278">104.40.217.71</span><span class="sxs-lookup"><span data-stu-id="d5ff7-278">104.40.217.71</span></span><br/><span data-ttu-id="d5ff7-279">52.230.124.46</span><span class="sxs-lookup"><span data-stu-id="d5ff7-279">52.230.124.46</span></span><br/><span data-ttu-id="d5ff7-280">52.230.122.9</span><span class="sxs-lookup"><span data-stu-id="d5ff7-280">52.230.122.9</span></span> | <span data-ttu-id="d5ff7-281">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-281">443</span></span>
| <span data-ttu-id="d5ff7-282">Portal</span><span class="sxs-lookup"><span data-stu-id="d5ff7-282">Portal</span></span> | <span data-ttu-id="d5ff7-283">gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-283">gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d5ff7-284">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-284">dynamic</span></span> | <span data-ttu-id="d5ff7-285">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-285">443</span></span>
| <span data-ttu-id="d5ff7-286">Storage</span><span class="sxs-lookup"><span data-stu-id="d5ff7-286">Storage</span></span> | <span data-ttu-id="d5ff7-287">\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-287">\*.core.windows.net</span></span> | <span data-ttu-id="d5ff7-288">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-288">dynamic</span></span> | <span data-ttu-id="d5ff7-289">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-289">443</span></span>

## <a name="snapshot-debugger"></a><span data-ttu-id="d5ff7-290">Snapshot Debugger</span><span class="sxs-lookup"><span data-stu-id="d5ff7-290">Snapshot Debugger</span></span>

> [!NOTE]
> <span data-ttu-id="d5ff7-291">Profiler and Snapshot Debugger share the same set of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="d5ff7-291">Profiler and Snapshot Debugger share the same set of IP addresses.</span></span>

| <span data-ttu-id="d5ff7-292">Purpose</span><span class="sxs-lookup"><span data-stu-id="d5ff7-292">Purpose</span></span> | <span data-ttu-id="d5ff7-293">URI</span><span class="sxs-lookup"><span data-stu-id="d5ff7-293">URI</span></span> | <span data-ttu-id="d5ff7-294">IP</span><span class="sxs-lookup"><span data-stu-id="d5ff7-294">IP</span></span> | <span data-ttu-id="d5ff7-295">Ports</span><span class="sxs-lookup"><span data-stu-id="d5ff7-295">Ports</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5ff7-296">Agent</span><span class="sxs-lookup"><span data-stu-id="d5ff7-296">Agent</span></span> | <span data-ttu-id="d5ff7-297">ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-297">ppe.azureserviceprofiler.net</span></span><br/><span data-ttu-id="d5ff7-298">\*.ppe.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-298">\*.ppe.azureserviceprofiler.net</span></span> | <span data-ttu-id="d5ff7-299">51.143.96.206</span><span class="sxs-lookup"><span data-stu-id="d5ff7-299">51.143.96.206</span></span><br/><span data-ttu-id="d5ff7-300">51.143.98.157</span><span class="sxs-lookup"><span data-stu-id="d5ff7-300">51.143.98.157</span></span><br/><span data-ttu-id="d5ff7-301">52.161.8.88</span><span class="sxs-lookup"><span data-stu-id="d5ff7-301">52.161.8.88</span></span><br/><span data-ttu-id="d5ff7-302">52.161.29.225</span><span class="sxs-lookup"><span data-stu-id="d5ff7-302">52.161.29.225</span></span><br/><span data-ttu-id="d5ff7-303">52.178.149.106</span><span class="sxs-lookup"><span data-stu-id="d5ff7-303">52.178.149.106</span></span><br/><span data-ttu-id="d5ff7-304">52.178.147.66</span><span class="sxs-lookup"><span data-stu-id="d5ff7-304">52.178.147.66</span></span><br/><span data-ttu-id="d5ff7-305">40.68.32.221</span><span class="sxs-lookup"><span data-stu-id="d5ff7-305">40.68.32.221</span></span><br/><span data-ttu-id="d5ff7-306">104.40.217.71</span><span class="sxs-lookup"><span data-stu-id="d5ff7-306">104.40.217.71</span></span><br/><span data-ttu-id="d5ff7-307">52.230.124.46</span><span class="sxs-lookup"><span data-stu-id="d5ff7-307">52.230.124.46</span></span><br/><span data-ttu-id="d5ff7-308">52.230.122.9</span><span class="sxs-lookup"><span data-stu-id="d5ff7-308">52.230.122.9</span></span> | <span data-ttu-id="d5ff7-309">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-309">443</span></span>
| <span data-ttu-id="d5ff7-310">Portal</span><span class="sxs-lookup"><span data-stu-id="d5ff7-310">Portal</span></span> | <span data-ttu-id="d5ff7-311">ppe.gateway.azureserviceprofiler.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-311">ppe.gateway.azureserviceprofiler.net</span></span> | <span data-ttu-id="d5ff7-312">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-312">dynamic</span></span> | <span data-ttu-id="d5ff7-313">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-313">443</span></span>
| <span data-ttu-id="d5ff7-314">Storage</span><span class="sxs-lookup"><span data-stu-id="d5ff7-314">Storage</span></span> | <span data-ttu-id="d5ff7-315">\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d5ff7-315">\*.core.windows.net</span></span> | <span data-ttu-id="d5ff7-316">dynamic</span><span class="sxs-lookup"><span data-stu-id="d5ff7-316">dynamic</span></span> | <span data-ttu-id="d5ff7-317">443</span><span class="sxs-lookup"><span data-stu-id="d5ff7-317">443</span></span>
