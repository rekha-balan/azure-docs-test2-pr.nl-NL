---
title: Dynamic site acceleration via Azure CDN
description: Azure CDN supports dynamic site acceleration (DSA) optimization for files with dynamic content.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/01/2018
ms.author: rli; v-deasim
ms.openlocfilehash: 8ecb2c1fa4d421907a338e01d24264c2951a1aba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868867"
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a><span data-ttu-id="33dc3-103">Dynamic site acceleration via Azure CDN</span><span class="sxs-lookup"><span data-stu-id="33dc3-103">Dynamic site acceleration via Azure CDN</span></span>

<span data-ttu-id="33dc3-104">With the explosion of social media, electronic commerce, and the hyper-personalized web, a rapidly increasing percentage of the content served to end users is generated in real time.</span><span class="sxs-lookup"><span data-stu-id="33dc3-104">With the explosion of social media, electronic commerce, and the hyper-personalized web, a rapidly increasing percentage of the content served to end users is generated in real time.</span></span> <span data-ttu-id="33dc3-105">Users expect a fast, reliable, and personalized web experience, independent of their browser, location, device, or network.</span><span class="sxs-lookup"><span data-stu-id="33dc3-105">Users expect a fast, reliable, and personalized web experience, independent of their browser, location, device, or network.</span></span> <span data-ttu-id="33dc3-106">However, the very innovations that make these experiences so engaging also slow page downloads and put the quality of the consumer experience at risk.</span><span class="sxs-lookup"><span data-stu-id="33dc3-106">However, the very innovations that make these experiences so engaging also slow page downloads and put the quality of the consumer experience at risk.</span></span> 

<span data-ttu-id="33dc3-107">Standard content delivery network (CDN) capability includes the ability to cache files closer to end users to speed up delivery of static files.</span><span class="sxs-lookup"><span data-stu-id="33dc3-107">Standard content delivery network (CDN) capability includes the ability to cache files closer to end users to speed up delivery of static files.</span></span> <span data-ttu-id="33dc3-108">However, with dynamic web applications, caching that content in edge locations isn't possible because the server generates the content in response to user behavior.</span><span class="sxs-lookup"><span data-stu-id="33dc3-108">However, with dynamic web applications, caching that content in edge locations isn't possible because the server generates the content in response to user behavior.</span></span> <span data-ttu-id="33dc3-109">Speeding up the delivery of such content is more complex than traditional edge caching and requires an end-to-end solution that finely tunes each element along the entire data path from inception to delivery.</span><span class="sxs-lookup"><span data-stu-id="33dc3-109">Speeding up the delivery of such content is more complex than traditional edge caching and requires an end-to-end solution that finely tunes each element along the entire data path from inception to delivery.</span></span> <span data-ttu-id="33dc3-110">With Azure CDN dynamic site acceleration (DSA) optimization, the performance of web pages with dynamic content is measurably improved.</span><span class="sxs-lookup"><span data-stu-id="33dc3-110">With Azure CDN dynamic site acceleration (DSA) optimization, the performance of web pages with dynamic content is measurably improved.</span></span>

<span data-ttu-id="33dc3-111">**Azure CDN from Akamai** and **Azure CDN from Verizon** both offer DSA optimization through the **Optimized for** menu during endpoint creation.</span><span class="sxs-lookup"><span data-stu-id="33dc3-111">**Azure CDN from Akamai** and **Azure CDN from Verizon** both offer DSA optimization through the **Optimized for** menu during endpoint creation.</span></span>

> [!Important]
> <span data-ttu-id="33dc3-112">For **Azure CDN from Akamai** profiles, you are allowed to change the optimization of a CDN endpoint after it has been created.</span><span class="sxs-lookup"><span data-stu-id="33dc3-112">For **Azure CDN from Akamai** profiles, you are allowed to change the optimization of a CDN endpoint after it has been created.</span></span>
>   
> <span data-ttu-id="33dc3-113">For **Azure CDN from Verizon** profiles, you cannot change the optimization of a CDN endpoint after it has been created.</span><span class="sxs-lookup"><span data-stu-id="33dc3-113">For **Azure CDN from Verizon** profiles, you cannot change the optimization of a CDN endpoint after it has been created.</span></span>

## <a name="cdn-endpoint-configuration-to-accelerate-delivery-of-dynamic-files"></a><span data-ttu-id="33dc3-114">CDN endpoint configuration to accelerate delivery of dynamic files</span><span class="sxs-lookup"><span data-stu-id="33dc3-114">CDN endpoint configuration to accelerate delivery of dynamic files</span></span>

<span data-ttu-id="33dc3-115">To configure a CDN endpoint to optimize delivery of dynamic files, you can either use the Azure portal, the REST APIs, or any of the client SDKs to do the same thing programmatically.</span><span class="sxs-lookup"><span data-stu-id="33dc3-115">To configure a CDN endpoint to optimize delivery of dynamic files, you can either use the Azure portal, the REST APIs, or any of the client SDKs to do the same thing programmatically.</span></span> 

<span data-ttu-id="33dc3-116">**To configure a CDN endpoint for DSA optimization by using the Azure portal:**</span><span class="sxs-lookup"><span data-stu-id="33dc3-116">**To configure a CDN endpoint for DSA optimization by using the Azure portal:**</span></span>

1. <span data-ttu-id="33dc3-117">In the **CDN profile** page, select **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-117">In the **CDN profile** page, select **Endpoint**.</span></span>

   ![Add a new CDN endpoint](./media/cdn-dynamic-site-acceleration/cdn-endpoint-profile.png) 

   <span data-ttu-id="33dc3-119">The **Add an endpoint** pane appears.</span><span class="sxs-lookup"><span data-stu-id="33dc3-119">The **Add an endpoint** pane appears.</span></span>

2. <span data-ttu-id="33dc3-120">Under **Optimized for**, select **Dynamic site acceleration**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-120">Under **Optimized for**, select **Dynamic site acceleration**.</span></span>

    ![Create a new CDN endpoint with DSA](./media/cdn-dynamic-site-acceleration/cdn-endpoint-dsa.png)

3. <span data-ttu-id="33dc3-122">For **Probe path**, enter a valid path to a file.</span><span class="sxs-lookup"><span data-stu-id="33dc3-122">For **Probe path**, enter a valid path to a file.</span></span>

    <span data-ttu-id="33dc3-123">Probe path is a feature specific to DSA, and a valid path is required for creation.</span><span class="sxs-lookup"><span data-stu-id="33dc3-123">Probe path is a feature specific to DSA, and a valid path is required for creation.</span></span> <span data-ttu-id="33dc3-124">DSA uses a small *probe path* file placed on the origin server to optimize network routing configurations for the CDN.</span><span class="sxs-lookup"><span data-stu-id="33dc3-124">DSA uses a small *probe path* file placed on the origin server to optimize network routing configurations for the CDN.</span></span> <span data-ttu-id="33dc3-125">For the probe path file, you can download and upload the sample file to your site, or use an existing asset on your origin that is about 10 KB in size.</span><span class="sxs-lookup"><span data-stu-id="33dc3-125">For the probe path file, you can download and upload the sample file to your site, or use an existing asset on your origin that is about 10 KB in size.</span></span>

4. <span data-ttu-id="33dc3-126">Enter the other required endpoint options (for more information, see [Create a new CDN endpoint](cdn-create-new-endpoint.md#create-a-new-cdn-endpoint)), then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-126">Enter the other required endpoint options (for more information, see [Create a new CDN endpoint](cdn-create-new-endpoint.md#create-a-new-cdn-endpoint)), then select **Add**.</span></span>

   <span data-ttu-id="33dc3-127">After the CDN endpoint is created, it applies the DSA optimizations for all files that match certain criteria.</span><span class="sxs-lookup"><span data-stu-id="33dc3-127">After the CDN endpoint is created, it applies the DSA optimizations for all files that match certain criteria.</span></span> 


<span data-ttu-id="33dc3-128">**To configure an existing endpoint for DSA (Azure CDN from Akamai profiles only):**</span><span class="sxs-lookup"><span data-stu-id="33dc3-128">**To configure an existing endpoint for DSA (Azure CDN from Akamai profiles only):**</span></span>

1. <span data-ttu-id="33dc3-129">In the **CDN profile** page, select the endpoint you want to modify.</span><span class="sxs-lookup"><span data-stu-id="33dc3-129">In the **CDN profile** page, select the endpoint you want to modify.</span></span>

2. <span data-ttu-id="33dc3-130">From the left pane, select **Optimization**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-130">From the left pane, select **Optimization**.</span></span> 

   <span data-ttu-id="33dc3-131">The **Optimization** page appears.</span><span class="sxs-lookup"><span data-stu-id="33dc3-131">The **Optimization** page appears.</span></span>

3. <span data-ttu-id="33dc3-132">Under **Optimized for**, select **Dynamic site acceleration**, then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-132">Under **Optimized for**, select **Dynamic site acceleration**, then select **Save**.</span></span>

> [!Note]
> <span data-ttu-id="33dc3-133">DSA incurs extra charges.</span><span class="sxs-lookup"><span data-stu-id="33dc3-133">DSA incurs extra charges.</span></span> <span data-ttu-id="33dc3-134">For more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span><span class="sxs-lookup"><span data-stu-id="33dc3-134">For more information, see [Content Delivery Network pricing](https://azure.microsoft.com/pricing/details/cdn/).</span></span>

## <a name="dsa-optimization-using-azure-cdn"></a><span data-ttu-id="33dc3-135">DSA Optimization using Azure CDN</span><span class="sxs-lookup"><span data-stu-id="33dc3-135">DSA Optimization using Azure CDN</span></span>

<span data-ttu-id="33dc3-136">Dynamic Site Acceleration on Azure CDN speeds up delivery of dynamic assets by using the following techniques:</span><span class="sxs-lookup"><span data-stu-id="33dc3-136">Dynamic Site Acceleration on Azure CDN speeds up delivery of dynamic assets by using the following techniques:</span></span>

-   [<span data-ttu-id="33dc3-137">Route optimization</span><span class="sxs-lookup"><span data-stu-id="33dc3-137">Route optimization</span></span>](#route-optimization)
-   [<span data-ttu-id="33dc3-138">TCP optimizations</span><span class="sxs-lookup"><span data-stu-id="33dc3-138">TCP optimizations</span></span>](#tcp-optimizations)
-   [<span data-ttu-id="33dc3-139">Object prefetch (Azure CDN from Akamai only)</span><span class="sxs-lookup"><span data-stu-id="33dc3-139">Object prefetch (Azure CDN from Akamai only)</span></span>](#object-prefetch-azure-cdn-from-akamai-only)
-   [<span data-ttu-id="33dc3-140">Adaptive image compression (Azure CDN from Akamai only)</span><span class="sxs-lookup"><span data-stu-id="33dc3-140">Adaptive image compression (Azure CDN from Akamai only)</span></span>](#adaptive-image-compression-azure-cdn-from-akamai-only)

### <a name="route-optimization"></a><span data-ttu-id="33dc3-141">Route Optimization</span><span class="sxs-lookup"><span data-stu-id="33dc3-141">Route Optimization</span></span>

<span data-ttu-id="33dc3-142">Route optimization is important because the Internet is a dynamic place, where traffic and temporarily outages are constantly changing the network topology.</span><span class="sxs-lookup"><span data-stu-id="33dc3-142">Route optimization is important because the Internet is a dynamic place, where traffic and temporarily outages are constantly changing the network topology.</span></span> <span data-ttu-id="33dc3-143">The Border Gateway Protocol (BGP) is the routing protocol of the Internet, but there may be faster routes via intermediary Point of Presence (PoP) servers.</span><span class="sxs-lookup"><span data-stu-id="33dc3-143">The Border Gateway Protocol (BGP) is the routing protocol of the Internet, but there may be faster routes via intermediary Point of Presence (PoP) servers.</span></span> 

<span data-ttu-id="33dc3-144">Route optimization chooses the most optimal path to the origin so that a site is continuously accessible and dynamic content is delivered to end users via the fastest and most reliable route possible.</span><span class="sxs-lookup"><span data-stu-id="33dc3-144">Route optimization chooses the most optimal path to the origin so that a site is continuously accessible and dynamic content is delivered to end users via the fastest and most reliable route possible.</span></span> 

<span data-ttu-id="33dc3-145">The Akamai network uses techniques to collect real-time data and compare various paths through different nodes in the Akamai server, as well as the default BGP route across the open Internet to determine the fastest route between the origin and the CDN edge.</span><span class="sxs-lookup"><span data-stu-id="33dc3-145">The Akamai network uses techniques to collect real-time data and compare various paths through different nodes in the Akamai server, as well as the default BGP route across the open Internet to determine the fastest route between the origin and the CDN edge.</span></span> <span data-ttu-id="33dc3-146">These techniques avoid Internet congestion points and long routes.</span><span class="sxs-lookup"><span data-stu-id="33dc3-146">These techniques avoid Internet congestion points and long routes.</span></span> 

<span data-ttu-id="33dc3-147">Similarly, the Verizon network uses a combination of Anycast DNS, high capacity support PoPs, and health checks, to determine the best gateways to best route data from the client to the origin.</span><span class="sxs-lookup"><span data-stu-id="33dc3-147">Similarly, the Verizon network uses a combination of Anycast DNS, high capacity support PoPs, and health checks, to determine the best gateways to best route data from the client to the origin.</span></span>
 
<span data-ttu-id="33dc3-148">As a result, fully dynamic and transactional content is delivered more quickly and more reliably to end users, even when it is uncacheable.</span><span class="sxs-lookup"><span data-stu-id="33dc3-148">As a result, fully dynamic and transactional content is delivered more quickly and more reliably to end users, even when it is uncacheable.</span></span> 

### <a name="tcp-optimizations"></a><span data-ttu-id="33dc3-149">TCP Optimizations</span><span class="sxs-lookup"><span data-stu-id="33dc3-149">TCP Optimizations</span></span>

<span data-ttu-id="33dc3-150">Transmission Control Protocol (TCP) is the standard of the Internet protocol suite used to deliver information between applications on an IP network.</span><span class="sxs-lookup"><span data-stu-id="33dc3-150">Transmission Control Protocol (TCP) is the standard of the Internet protocol suite used to deliver information between applications on an IP network.</span></span>  <span data-ttu-id="33dc3-151">By default, several back-and-forth requests are required to set up a TCP connection, as well as limits to avoid network congestions, which result in inefficiencies at scale.</span><span class="sxs-lookup"><span data-stu-id="33dc3-151">By default, several back-and-forth requests are required to set up a TCP connection, as well as limits to avoid network congestions, which result in inefficiencies at scale.</span></span> <span data-ttu-id="33dc3-152">**Azure CDN from Akamai** handles this problem by optimizing in three areas:</span><span class="sxs-lookup"><span data-stu-id="33dc3-152">**Azure CDN from Akamai** handles this problem by optimizing in three areas:</span></span> 

 - [<span data-ttu-id="33dc3-153">Eliminating TCP slow start</span><span class="sxs-lookup"><span data-stu-id="33dc3-153">Eliminating TCP slow start</span></span>](#eliminating-tcp-slow-start)
 - [<span data-ttu-id="33dc3-154">Leveraging persistent connections</span><span class="sxs-lookup"><span data-stu-id="33dc3-154">Leveraging persistent connections</span></span>](#leveraging-persistent-connections)
 - [<span data-ttu-id="33dc3-155">Tuning TCP packet parameters</span><span class="sxs-lookup"><span data-stu-id="33dc3-155">Tuning TCP packet parameters</span></span>](#tuning-tcp-packet-parameters)

#### <a name="eliminating-tcp-slow-start"></a><span data-ttu-id="33dc3-156">Eliminating TCP slow start</span><span class="sxs-lookup"><span data-stu-id="33dc3-156">Eliminating TCP slow start</span></span>

<span data-ttu-id="33dc3-157">TCP *slow start* is an algorithm of the TCP protocol that prevents network congestion by limiting the amount of data sent over the network.</span><span class="sxs-lookup"><span data-stu-id="33dc3-157">TCP *slow start* is an algorithm of the TCP protocol that prevents network congestion by limiting the amount of data sent over the network.</span></span> <span data-ttu-id="33dc3-158">It starts off with small congestion window sizes between sender and receiver until the maximum is reached or packet loss is detected.</span><span class="sxs-lookup"><span data-stu-id="33dc3-158">It starts off with small congestion window sizes between sender and receiver until the maximum is reached or packet loss is detected.</span></span>

 <span data-ttu-id="33dc3-159">Both **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles eliminate TCP slow start with the following three steps:</span><span class="sxs-lookup"><span data-stu-id="33dc3-159">Both **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles eliminate TCP slow start with the following three steps:</span></span>

1. <span data-ttu-id="33dc3-160">Health and bandwidth monitoring is used to measure the bandwidth of connections between edge PoP servers.</span><span class="sxs-lookup"><span data-stu-id="33dc3-160">Health and bandwidth monitoring is used to measure the bandwidth of connections between edge PoP servers.</span></span>
    
2. <span data-ttu-id="33dc3-161">Metrics are shared between edge PoP servers so that each server is aware of the network conditions and server health of the other PoPs around them.</span><span class="sxs-lookup"><span data-stu-id="33dc3-161">Metrics are shared between edge PoP servers so that each server is aware of the network conditions and server health of the other PoPs around them.</span></span>  
    
3. <span data-ttu-id="33dc3-162">The CDN edge servers make assumptions about some transmission parameters, such as what the optimal window size should be when communicating with other CDN edge servers in its proximity.</span><span class="sxs-lookup"><span data-stu-id="33dc3-162">The CDN edge servers make assumptions about some transmission parameters, such as what the optimal window size should be when communicating with other CDN edge servers in its proximity.</span></span> <span data-ttu-id="33dc3-163">This step means that the initial congestion window size can be increased if the health of the connection between the CDN edge servers is capable of higher packet data transfers.</span><span class="sxs-lookup"><span data-stu-id="33dc3-163">This step means that the initial congestion window size can be increased if the health of the connection between the CDN edge servers is capable of higher packet data transfers.</span></span>  

#### <a name="leveraging-persistent-connections"></a><span data-ttu-id="33dc3-164">Leveraging persistent connections</span><span class="sxs-lookup"><span data-stu-id="33dc3-164">Leveraging persistent connections</span></span>

<span data-ttu-id="33dc3-165">Using a CDN, fewer unique machines connect to your origin server directly compared with users connecting directly to your origin.</span><span class="sxs-lookup"><span data-stu-id="33dc3-165">Using a CDN, fewer unique machines connect to your origin server directly compared with users connecting directly to your origin.</span></span> <span data-ttu-id="33dc3-166">Azure CDN also pools user requests together to establish fewer connections with the origin.</span><span class="sxs-lookup"><span data-stu-id="33dc3-166">Azure CDN also pools user requests together to establish fewer connections with the origin.</span></span>

<span data-ttu-id="33dc3-167">As previously mentioned, several handshake requests are required to establish a TCP connection.</span><span class="sxs-lookup"><span data-stu-id="33dc3-167">As previously mentioned, several handshake requests are required to establish a TCP connection.</span></span> <span data-ttu-id="33dc3-168">Persistent connections, which are implemented by the `Keep-Alive` HTTP header, reuse existing TCP connections for multiple HTTP requests to save round-trip times and speed up delivery.</span><span class="sxs-lookup"><span data-stu-id="33dc3-168">Persistent connections, which are implemented by the `Keep-Alive` HTTP header, reuse existing TCP connections for multiple HTTP requests to save round-trip times and speed up delivery.</span></span> 

<span data-ttu-id="33dc3-169">**Azure CDN from Verizon** also sends periodic keep-alive packets over the TCP connection to prevent an open connection from being closed.</span><span class="sxs-lookup"><span data-stu-id="33dc3-169">**Azure CDN from Verizon** also sends periodic keep-alive packets over the TCP connection to prevent an open connection from being closed.</span></span>

#### <a name="tuning-tcp-packet-parameters"></a><span data-ttu-id="33dc3-170">Tuning TCP packet parameters</span><span class="sxs-lookup"><span data-stu-id="33dc3-170">Tuning TCP packet parameters</span></span>

<span data-ttu-id="33dc3-171">**Azure CDN from Akamai** tunes the parameters that govern server-to-server connections and reduces the amount of long-haul round trips required to retrieve content embedded in the site by using the following techniques:</span><span class="sxs-lookup"><span data-stu-id="33dc3-171">**Azure CDN from Akamai** tunes the parameters that govern server-to-server connections and reduces the amount of long-haul round trips required to retrieve content embedded in the site by using the following techniques:</span></span>

- <span data-ttu-id="33dc3-172">Increasing the initial congestion window so that more packets can be sent without waiting for an acknowledgement.</span><span class="sxs-lookup"><span data-stu-id="33dc3-172">Increasing the initial congestion window so that more packets can be sent without waiting for an acknowledgement.</span></span>
- <span data-ttu-id="33dc3-173">Decreasing the initial retransmit timeout so that a loss is detected, and retransmission occurs more quickly.</span><span class="sxs-lookup"><span data-stu-id="33dc3-173">Decreasing the initial retransmit timeout so that a loss is detected, and retransmission occurs more quickly.</span></span>
- <span data-ttu-id="33dc3-174">Decreasing the minimum and maximum retransmit timeout to reduce the wait time before assuming packets were lost in transmission.</span><span class="sxs-lookup"><span data-stu-id="33dc3-174">Decreasing the minimum and maximum retransmit timeout to reduce the wait time before assuming packets were lost in transmission.</span></span>

### <a name="object-prefetch-azure-cdn-from-akamai-only"></a><span data-ttu-id="33dc3-175">Object prefetch (Azure CDN from Akamai only)</span><span class="sxs-lookup"><span data-stu-id="33dc3-175">Object prefetch (Azure CDN from Akamai only)</span></span>

<span data-ttu-id="33dc3-176">Most websites consist of an HTML page, which references various other resources such as images and scripts.</span><span class="sxs-lookup"><span data-stu-id="33dc3-176">Most websites consist of an HTML page, which references various other resources such as images and scripts.</span></span> <span data-ttu-id="33dc3-177">Typically, when a client requests a webpage, the browser first downloads and parses the HTML object, and then makes additional requests to linked assets that are required to fully load the page.</span><span class="sxs-lookup"><span data-stu-id="33dc3-177">Typically, when a client requests a webpage, the browser first downloads and parses the HTML object, and then makes additional requests to linked assets that are required to fully load the page.</span></span> 

<span data-ttu-id="33dc3-178">*Prefetch* is a technique to retrieve images and scripts embedded in the HTML page while the HTML is served to the browser, and before the browser even makes these object requests.</span><span class="sxs-lookup"><span data-stu-id="33dc3-178">*Prefetch* is a technique to retrieve images and scripts embedded in the HTML page while the HTML is served to the browser, and before the browser even makes these object requests.</span></span> 

<span data-ttu-id="33dc3-179">With the prefetch option turned on at the time when the CDN serves the HTML base page to the client’s browser, the CDN parses the HTML file and make additional requests for any linked resources and store it in its cache.</span><span class="sxs-lookup"><span data-stu-id="33dc3-179">With the prefetch option turned on at the time when the CDN serves the HTML base page to the client’s browser, the CDN parses the HTML file and make additional requests for any linked resources and store it in its cache.</span></span> <span data-ttu-id="33dc3-180">When the client makes the requests for the linked assets, the CDN edge server already has the requested objects and can serve them immediately without a round trip to the origin.</span><span class="sxs-lookup"><span data-stu-id="33dc3-180">When the client makes the requests for the linked assets, the CDN edge server already has the requested objects and can serve them immediately without a round trip to the origin.</span></span> <span data-ttu-id="33dc3-181">This optimization benefits both cacheable and non-cacheable content.</span><span class="sxs-lookup"><span data-stu-id="33dc3-181">This optimization benefits both cacheable and non-cacheable content.</span></span>

### <a name="adaptive-image-compression-azure-cdn-from-akamai-only"></a><span data-ttu-id="33dc3-182">Adaptive image compression (Azure CDN from Akamai only)</span><span class="sxs-lookup"><span data-stu-id="33dc3-182">Adaptive image compression (Azure CDN from Akamai only)</span></span>

<span data-ttu-id="33dc3-183">Some devices, especially mobile ones, experience slower network speeds from time to time.</span><span class="sxs-lookup"><span data-stu-id="33dc3-183">Some devices, especially mobile ones, experience slower network speeds from time to time.</span></span> <span data-ttu-id="33dc3-184">In these scenarios, it is more beneficial for the user to receive smaller images in their webpage more quickly rather than waiting a long time for full resolution images.</span><span class="sxs-lookup"><span data-stu-id="33dc3-184">In these scenarios, it is more beneficial for the user to receive smaller images in their webpage more quickly rather than waiting a long time for full resolution images.</span></span>

<span data-ttu-id="33dc3-185">This feature automatically monitors network quality, and employs standard JPEG compression methods when network speeds are slower to improve delivery time.</span><span class="sxs-lookup"><span data-stu-id="33dc3-185">This feature automatically monitors network quality, and employs standard JPEG compression methods when network speeds are slower to improve delivery time.</span></span>

<span data-ttu-id="33dc3-186">Adaptive Image Compression</span><span class="sxs-lookup"><span data-stu-id="33dc3-186">Adaptive Image Compression</span></span> | <span data-ttu-id="33dc3-187">File Extensions</span><span class="sxs-lookup"><span data-stu-id="33dc3-187">File Extensions</span></span>  
--- | ---  
<span data-ttu-id="33dc3-188">JPEG compression</span><span class="sxs-lookup"><span data-stu-id="33dc3-188">JPEG compression</span></span> | <span data-ttu-id="33dc3-189">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span><span class="sxs-lookup"><span data-stu-id="33dc3-189">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span></span>

## <a name="caching"></a><span data-ttu-id="33dc3-190">Caching</span><span class="sxs-lookup"><span data-stu-id="33dc3-190">Caching</span></span>

<span data-ttu-id="33dc3-191">With DSA, caching is turned off by default on the CDN, even when the origin includes `Cache-Control` or `Expires` headers in the response.</span><span class="sxs-lookup"><span data-stu-id="33dc3-191">With DSA, caching is turned off by default on the CDN, even when the origin includes `Cache-Control` or `Expires` headers in the response.</span></span> <span data-ttu-id="33dc3-192">DSA is typically used for dynamic assets that should not be cached because they are unique to each client.</span><span class="sxs-lookup"><span data-stu-id="33dc3-192">DSA is typically used for dynamic assets that should not be cached because they are unique to each client.</span></span> <span data-ttu-id="33dc3-193">Caching can break this behavior.</span><span class="sxs-lookup"><span data-stu-id="33dc3-193">Caching can break this behavior.</span></span>

<span data-ttu-id="33dc3-194">If you have a website with a mix of static and dynamic assets, it is best to take a hybrid approach to get the best performance.</span><span class="sxs-lookup"><span data-stu-id="33dc3-194">If you have a website with a mix of static and dynamic assets, it is best to take a hybrid approach to get the best performance.</span></span> 

<span data-ttu-id="33dc3-195">For **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles, you can turn on caching for specific DSA endpoints by using [caching rules](cdn-caching-rules.md).</span><span class="sxs-lookup"><span data-stu-id="33dc3-195">For **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles, you can turn on caching for specific DSA endpoints by using [caching rules](cdn-caching-rules.md).</span></span>

<span data-ttu-id="33dc3-196">To access caching rules:</span><span class="sxs-lookup"><span data-stu-id="33dc3-196">To access caching rules:</span></span>

1. <span data-ttu-id="33dc3-197">From the **CDN profile** page, under settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-197">From the **CDN profile** page, under settings, select **Caching rules**.</span></span>  
    
    ![CDN Caching rules button](./media/cdn-dynamic-site-acceleration/cdn-caching-rules-btn.png)

    <span data-ttu-id="33dc3-199">The **Caching rules** page opens.</span><span class="sxs-lookup"><span data-stu-id="33dc3-199">The **Caching rules** page opens.</span></span>

2. <span data-ttu-id="33dc3-200">Create a global or custom caching rule to turn on caching for your DSA endpoint.</span><span class="sxs-lookup"><span data-stu-id="33dc3-200">Create a global or custom caching rule to turn on caching for your DSA endpoint.</span></span> 

<span data-ttu-id="33dc3-201">For **Azure CDN Premium from Verizon** profiles only, you turn on caching for specific DSA endpoints by using the [rules engine](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="33dc3-201">For **Azure CDN Premium from Verizon** profiles only, you turn on caching for specific DSA endpoints by using the [rules engine](cdn-rules-engine.md).</span></span> <span data-ttu-id="33dc3-202">Any rules that are created affect only those endpoints of your profile that are optimized for DSA.</span><span class="sxs-lookup"><span data-stu-id="33dc3-202">Any rules that are created affect only those endpoints of your profile that are optimized for DSA.</span></span> 

<span data-ttu-id="33dc3-203">To access the rules engine:</span><span class="sxs-lookup"><span data-stu-id="33dc3-203">To access the rules engine:</span></span>
    
1. <span data-ttu-id="33dc3-204">From the **CDN profile** page, select **Manage**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-204">From the **CDN profile** page, select **Manage**.</span></span>  
    
    ![CDN profile manage button](./media/cdn-dynamic-site-acceleration/cdn-manage-btn.png)

    <span data-ttu-id="33dc3-206">The CDN management portal opens.</span><span class="sxs-lookup"><span data-stu-id="33dc3-206">The CDN management portal opens.</span></span>

2. <span data-ttu-id="33dc3-207">From the CDN management portal, select **ADN**, then select **Rules Engine**.</span><span class="sxs-lookup"><span data-stu-id="33dc3-207">From the CDN management portal, select **ADN**, then select **Rules Engine**.</span></span> 

    ![Rules engine for DSA](./media/cdn-dynamic-site-acceleration/cdn-dsa-rules-engine.png)



<span data-ttu-id="33dc3-209">Alternatively, you can use two CDN endpoints: one endpoint optimized with DSA to deliver dynamic assets and another endpoint optimized with a static optimization type, such as general web delivery, to delivery cacheable assets.</span><span class="sxs-lookup"><span data-stu-id="33dc3-209">Alternatively, you can use two CDN endpoints: one endpoint optimized with DSA to deliver dynamic assets and another endpoint optimized with a static optimization type, such as general web delivery, to delivery cacheable assets.</span></span> <span data-ttu-id="33dc3-210">Modify your webpage URLs to link directly to the asset on the CDN endpoint you plan to use.</span><span class="sxs-lookup"><span data-stu-id="33dc3-210">Modify your webpage URLs to link directly to the asset on the CDN endpoint you plan to use.</span></span> 

<span data-ttu-id="33dc3-211">For example: `mydynamic.azureedge.net/index.html` is a dynamic page and is loaded from the DSA endpoint.</span><span class="sxs-lookup"><span data-stu-id="33dc3-211">For example: `mydynamic.azureedge.net/index.html` is a dynamic page and is loaded from the DSA endpoint.</span></span>  <span data-ttu-id="33dc3-212">The html page references multiple static assets such as JavaScript libraries or images that are loaded from the static CDN endpoint, such as `mystatic.azureedge.net/banner.jpg` and `mystatic.azureedge.net/scripts.js`.</span><span class="sxs-lookup"><span data-stu-id="33dc3-212">The html page references multiple static assets such as JavaScript libraries or images that are loaded from the static CDN endpoint, such as `mystatic.azureedge.net/banner.jpg` and `mystatic.azureedge.net/scripts.js`.</span></span> 



