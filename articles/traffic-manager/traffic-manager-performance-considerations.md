---
title: Performance considerations for Azure Traffic Manager | Microsoft Docs
description: Understand performance on Traffic Manager and how to test performance of your website when using Traffic Manager
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
editor: ''
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 2ba6fec699315e5a6139dfe26d994c58f78dd8ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661211"
---
# <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="44735-103">Performance considerations for Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="44735-103">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="44735-104">This page explains performance considerations using Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="44735-104">This page explains performance considerations using Traffic Manager.</span></span> <span data-ttu-id="44735-105">Consider the following scenario:</span><span class="sxs-lookup"><span data-stu-id="44735-105">Consider the following scenario:</span></span>

<span data-ttu-id="44735-106">You have instances of your website in the WestUS and EastAsia regions.</span><span class="sxs-lookup"><span data-stu-id="44735-106">You have instances of your website in the WestUS and EastAsia regions.</span></span> <span data-ttu-id="44735-107">One of the instances is failing the health check for the traffic manager probe.</span><span class="sxs-lookup"><span data-stu-id="44735-107">One of the instances is failing the health check for the traffic manager probe.</span></span> <span data-ttu-id="44735-108">Application traffic is directed to the healthy region.</span><span class="sxs-lookup"><span data-stu-id="44735-108">Application traffic is directed to the healthy region.</span></span> <span data-ttu-id="44735-109">This failover is expected but performance can be a problem based on the latency of the traffic now traveling to a distant region.</span><span class="sxs-lookup"><span data-stu-id="44735-109">This failover is expected but performance can be a problem based on the latency of the traffic now traveling to a distant region.</span></span>

## <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="44735-110">Performance considerations for Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="44735-110">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="44735-111">The only performance impact that Traffic Manager can have on your website is the initial DNS lookup.</span><span class="sxs-lookup"><span data-stu-id="44735-111">The only performance impact that Traffic Manager can have on your website is the initial DNS lookup.</span></span> <span data-ttu-id="44735-112">A DNS request for the name of your Traffic Manager profile is handled by the Microsoft DNS root server that hosts the trafficmanager.net zone.</span><span class="sxs-lookup"><span data-stu-id="44735-112">A DNS request for the name of your Traffic Manager profile is handled by the Microsoft DNS root server that hosts the trafficmanager.net zone.</span></span> <span data-ttu-id="44735-113">Traffic Manager populates, and regularly updates, the Microsoft's DNS root servers based on the Traffic Manager policy and the probe results.</span><span class="sxs-lookup"><span data-stu-id="44735-113">Traffic Manager populates, and regularly updates, the Microsoft's DNS root servers based on the Traffic Manager policy and the probe results.</span></span> <span data-ttu-id="44735-114">So even during the initial DNS lookup, no DNS queries are sent to Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="44735-114">So even during the initial DNS lookup, no DNS queries are sent to Traffic Manager.</span></span>

<span data-ttu-id="44735-115">Traffic Manager is made up of several components: DNS name servers, an API service, the storage layer, and an endpoint monitoring service.</span><span class="sxs-lookup"><span data-stu-id="44735-115">Traffic Manager is made up of several components: DNS name servers, an API service, the storage layer, and an endpoint monitoring service.</span></span> <span data-ttu-id="44735-116">If a Traffic Manager service component fails, there is no effect on the DNS name associated with your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="44735-116">If a Traffic Manager service component fails, there is no effect on the DNS name associated with your Traffic Manager profile.</span></span> <span data-ttu-id="44735-117">The records in the Microsoft DNS servers remain unchanged.</span><span class="sxs-lookup"><span data-stu-id="44735-117">The records in the Microsoft DNS servers remain unchanged.</span></span> <span data-ttu-id="44735-118">However, endpoint monitoring and DNS updating do not happen.</span><span class="sxs-lookup"><span data-stu-id="44735-118">However, endpoint monitoring and DNS updating do not happen.</span></span> <span data-ttu-id="44735-119">Therefore, Traffic Manager is not able to update DNS to point to your failover site when your primary site goes down.</span><span class="sxs-lookup"><span data-stu-id="44735-119">Therefore, Traffic Manager is not able to update DNS to point to your failover site when your primary site goes down.</span></span>

<span data-ttu-id="44735-120">DNS name resolution is fast and results are cached.</span><span class="sxs-lookup"><span data-stu-id="44735-120">DNS name resolution is fast and results are cached.</span></span> <span data-ttu-id="44735-121">The speed of the initial DNS lookup depends on the DNS servers the client uses for name resolution.</span><span class="sxs-lookup"><span data-stu-id="44735-121">The speed of the initial DNS lookup depends on the DNS servers the client uses for name resolution.</span></span> <span data-ttu-id="44735-122">Typically, a client can complete a DNS lookup within ~50 ms.</span><span class="sxs-lookup"><span data-stu-id="44735-122">Typically, a client can complete a DNS lookup within ~50 ms.</span></span> <span data-ttu-id="44735-123">The results of the lookup are cached for the duration of the DNS Time-to-live (TTL).</span><span class="sxs-lookup"><span data-stu-id="44735-123">The results of the lookup are cached for the duration of the DNS Time-to-live (TTL).</span></span> <span data-ttu-id="44735-124">The default TTL for Traffic Manager is 300 seconds.</span><span class="sxs-lookup"><span data-stu-id="44735-124">The default TTL for Traffic Manager is 300 seconds.</span></span>

<span data-ttu-id="44735-125">Traffic does NOT flow through Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="44735-125">Traffic does NOT flow through Traffic Manager.</span></span> <span data-ttu-id="44735-126">Once the DNS lookup completes, the client has an IP address for an instance of your web site.</span><span class="sxs-lookup"><span data-stu-id="44735-126">Once the DNS lookup completes, the client has an IP address for an instance of your web site.</span></span> <span data-ttu-id="44735-127">The client connects directly to that address and does not pass through Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="44735-127">The client connects directly to that address and does not pass through Traffic Manager.</span></span> <span data-ttu-id="44735-128">The Traffic Manager policy you choose has no influence on the DNS performance.</span><span class="sxs-lookup"><span data-stu-id="44735-128">The Traffic Manager policy you choose has no influence on the DNS performance.</span></span> <span data-ttu-id="44735-129">However, a Performance routing-method can negatively impact the application experience.</span><span class="sxs-lookup"><span data-stu-id="44735-129">However, a Performance routing-method can negatively impact the application experience.</span></span> <span data-ttu-id="44735-130">For example, if your policy redirects traffic from North America to an instance hosted in Asia, the network latency for those sessions may be a performance issue.</span><span class="sxs-lookup"><span data-stu-id="44735-130">For example, if your policy redirects traffic from North America to an instance hosted in Asia, the network latency for those sessions may be a performance issue.</span></span>

## <a name="measuring-traffic-manager-performance"></a><span data-ttu-id="44735-131">Measuring Traffic Manager Performance</span><span class="sxs-lookup"><span data-stu-id="44735-131">Measuring Traffic Manager Performance</span></span>

<span data-ttu-id="44735-132">There are several websites you can use to understand the performance and behavior of a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="44735-132">There are several websites you can use to understand the performance and behavior of a Traffic Manager profile.</span></span> <span data-ttu-id="44735-133">Many of these sites are free but may have limitations.</span><span class="sxs-lookup"><span data-stu-id="44735-133">Many of these sites are free but may have limitations.</span></span> <span data-ttu-id="44735-134">Some sites offer enhanced monitoring and reporting for a fee.</span><span class="sxs-lookup"><span data-stu-id="44735-134">Some sites offer enhanced monitoring and reporting for a fee.</span></span>

<span data-ttu-id="44735-135">The tools on these sites measure DNS latencies and display the resolved IP addresses for client locations around the world.</span><span class="sxs-lookup"><span data-stu-id="44735-135">The tools on these sites measure DNS latencies and display the resolved IP addresses for client locations around the world.</span></span> <span data-ttu-id="44735-136">Most of these tools do not cache the DNS results.</span><span class="sxs-lookup"><span data-stu-id="44735-136">Most of these tools do not cache the DNS results.</span></span> <span data-ttu-id="44735-137">Therefore, the tools show the full DNS lookup each time a test is run.</span><span class="sxs-lookup"><span data-stu-id="44735-137">Therefore, the tools show the full DNS lookup each time a test is run.</span></span> <span data-ttu-id="44735-138">When you test from your own client, you only experience the full DNS lookup performance once during the TTL duration.</span><span class="sxs-lookup"><span data-stu-id="44735-138">When you test from your own client, you only experience the full DNS lookup performance once during the TTL duration.</span></span>

## <a name="sample-tools-to-measure-dns-performance"></a><span data-ttu-id="44735-139">Sample tools to measure DNS performance</span><span class="sxs-lookup"><span data-stu-id="44735-139">Sample tools to measure DNS performance</span></span>

* [<span data-ttu-id="44735-140">SolveDNS</span><span class="sxs-lookup"><span data-stu-id="44735-140">SolveDNS</span></span>](http://www.solvedns.com/dns-comparison/)

    <span data-ttu-id="44735-141">SolveDNS offers many performance tools.</span><span class="sxs-lookup"><span data-stu-id="44735-141">SolveDNS offers many performance tools.</span></span> <span data-ttu-id="44735-142">The DNS Comparison tool can show you how long it takes to resolve your DNS name and how that compares to other DNS service providers.</span><span class="sxs-lookup"><span data-stu-id="44735-142">The DNS Comparison tool can show you how long it takes to resolve your DNS name and how that compares to other DNS service providers.</span></span>

* [<span data-ttu-id="44735-143">WebSitePulse</span><span class="sxs-lookup"><span data-stu-id="44735-143">WebSitePulse</span></span>](http://www.websitepulse.com/help/tools.php)

    <span data-ttu-id="44735-144">One of the simplest tools is WebSitePulse.</span><span class="sxs-lookup"><span data-stu-id="44735-144">One of the simplest tools is WebSitePulse.</span></span> <span data-ttu-id="44735-145">Enter the URL to see DNS resolution time, First Byte, Last Byte, and other performance statistics.</span><span class="sxs-lookup"><span data-stu-id="44735-145">Enter the URL to see DNS resolution time, First Byte, Last Byte, and other performance statistics.</span></span> <span data-ttu-id="44735-146">You can choose from three different test locations.</span><span class="sxs-lookup"><span data-stu-id="44735-146">You can choose from three different test locations.</span></span> <span data-ttu-id="44735-147">In this example, you see that the first execution shows that DNS lookup takes 0.204 sec.</span><span class="sxs-lookup"><span data-stu-id="44735-147">In this example, you see that the first execution shows that DNS lookup takes 0.204 sec.</span></span>

    ![pulse1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    <span data-ttu-id="44735-149">Because the results are cached, the second test for the same Traffic Manager endpoint the DNS lookup takes 0.002 sec.</span><span class="sxs-lookup"><span data-stu-id="44735-149">Because the results are cached, the second test for the same Traffic Manager endpoint the DNS lookup takes 0.002 sec.</span></span>

    ![pulse2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [<span data-ttu-id="44735-151">CA App Synthetic Monitor</span><span class="sxs-lookup"><span data-stu-id="44735-151">CA App Synthetic Monitor</span></span>](https://asm.ca.com/en/checkit.php)

    <span data-ttu-id="44735-152">Formerly known as the Watchmouse Check Website tool, this site show you the DNS resolution time from multiple geographic regions simultaneously.</span><span class="sxs-lookup"><span data-stu-id="44735-152">Formerly known as the Watchmouse Check Website tool, this site show you the DNS resolution time from multiple geographic regions simultaneously.</span></span> <span data-ttu-id="44735-153">Enter the URL to see DNS resolution time, connection time, and speed from several geographic locations.</span><span class="sxs-lookup"><span data-stu-id="44735-153">Enter the URL to see DNS resolution time, connection time, and speed from several geographic locations.</span></span> <span data-ttu-id="44735-154">Use this test to see which hosted service is returned for different locations around the world.</span><span class="sxs-lookup"><span data-stu-id="44735-154">Use this test to see which hosted service is returned for different locations around the world.</span></span>

    ![pulse1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [<span data-ttu-id="44735-156">Pingdom</span><span class="sxs-lookup"><span data-stu-id="44735-156">Pingdom</span></span>](http://tools.pingdom.com/)

    <span data-ttu-id="44735-157">This tool provides performance statistics for each element of a web page.</span><span class="sxs-lookup"><span data-stu-id="44735-157">This tool provides performance statistics for each element of a web page.</span></span> <span data-ttu-id="44735-158">The Page Analysis tab shows the percentage of time spent on DNS lookup.</span><span class="sxs-lookup"><span data-stu-id="44735-158">The Page Analysis tab shows the percentage of time spent on DNS lookup.</span></span>

* [<span data-ttu-id="44735-159">What's My DNS?</span><span class="sxs-lookup"><span data-stu-id="44735-159">What's My DNS?</span></span>](http://www.whatsmydns.net/)

    <span data-ttu-id="44735-160">This site does a DNS lookup from 20 different locations and displays the results on a map.</span><span class="sxs-lookup"><span data-stu-id="44735-160">This site does a DNS lookup from 20 different locations and displays the results on a map.</span></span>

* [<span data-ttu-id="44735-161">Dig Web Interface</span><span class="sxs-lookup"><span data-stu-id="44735-161">Dig Web Interface</span></span>](http://www.digwebinterface.com)

    <span data-ttu-id="44735-162">This site shows more detailed DNS information including CNAMEs and A records.</span><span class="sxs-lookup"><span data-stu-id="44735-162">This site shows more detailed DNS information including CNAMEs and A records.</span></span> <span data-ttu-id="44735-163">Make sure you check the 'Colorize output' and 'Stats' under options, and select 'All' under Nameservers.</span><span class="sxs-lookup"><span data-stu-id="44735-163">Make sure you check the 'Colorize output' and 'Stats' under options, and select 'All' under Nameservers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44735-164">Next Steps</span><span class="sxs-lookup"><span data-stu-id="44735-164">Next Steps</span></span>

[<span data-ttu-id="44735-165">About Traffic Manager traffic routing methods</span><span class="sxs-lookup"><span data-stu-id="44735-165">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="44735-166">Test your Traffic Manager settings</span><span class="sxs-lookup"><span data-stu-id="44735-166">Test your Traffic Manager settings</span></span>](traffic-manager-testing-settings.md)

[<span data-ttu-id="44735-167">Operations on Traffic Manager (REST API Reference)</span><span class="sxs-lookup"><span data-stu-id="44735-167">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

[<span data-ttu-id="44735-168">Azure Traffic Manager Cmdlets</span><span class="sxs-lookup"><span data-stu-id="44735-168">Azure Traffic Manager Cmdlets</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=400769)




