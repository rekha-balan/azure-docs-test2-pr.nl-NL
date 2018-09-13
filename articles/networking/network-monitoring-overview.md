---
title: About Network Monitoring in Log Analytics | Microsoft Docs
description: Overview of network monitoring solutions, including NPM, to manage networks across cloud, on-premises, and hybrid environments.
services: monitoring-and-diagnostics
documentationcenter: na
author: agummadi
manager: ''
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2018
ms.author: ajaycode
ms.openlocfilehash: 0656cfcc2dcded284be1a337f797681117f3b313
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857960"
---
# <a name="network-monitoring-solutions"></a><span data-ttu-id="6bd98-103">Network monitoring solutions</span><span class="sxs-lookup"><span data-stu-id="6bd98-103">Network monitoring solutions</span></span> 

<span data-ttu-id="6bd98-104">Azure offers a host of solutions to monitor your networking assets.</span><span class="sxs-lookup"><span data-stu-id="6bd98-104">Azure offers a host of solutions to monitor your networking assets.</span></span> <span data-ttu-id="6bd98-105">Azure has solutions and utilities to monitor network connectivity, the health of ExpressRoute circuits, and analyze network traffic in the cloud.</span><span class="sxs-lookup"><span data-stu-id="6bd98-105">Azure has solutions and utilities to monitor network connectivity, the health of ExpressRoute circuits, and analyze network traffic in the cloud.</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="6bd98-106">Network Performance Monitor (NPM)</span><span class="sxs-lookup"><span data-stu-id="6bd98-106">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="6bd98-107">Network Performance Monitor (NPM) is a suite of capabilities, each of which is geared towards monitoring the health of your network, network connectivity to your applications, and provides insights into the performance of your network.</span><span class="sxs-lookup"><span data-stu-id="6bd98-107">Network Performance Monitor (NPM) is a suite of capabilities, each of which is geared towards monitoring the health of your network, network connectivity to your applications, and provides insights into the performance of your network.</span></span> <span data-ttu-id="6bd98-108">NPM is cloud-based and provides a hybrid network monitoring solution that monitors connectivity between:</span><span class="sxs-lookup"><span data-stu-id="6bd98-108">NPM is cloud-based and provides a hybrid network monitoring solution that monitors connectivity between:</span></span>
 
* <span data-ttu-id="6bd98-109">Cloud deployments and on-premises locations</span><span class="sxs-lookup"><span data-stu-id="6bd98-109">Cloud deployments and on-premises locations</span></span>
* <span data-ttu-id="6bd98-110">Multiple data centers and branch offices</span><span class="sxs-lookup"><span data-stu-id="6bd98-110">Multiple data centers and branch offices</span></span>
* <span data-ttu-id="6bd98-111">Mission critical multi-tier applications/micro-services</span><span class="sxs-lookup"><span data-stu-id="6bd98-111">Mission critical multi-tier applications/micro-services</span></span>
* <span data-ttu-id="6bd98-112">User locations and web-based applications (HTTP/HTTPs)</span><span class="sxs-lookup"><span data-stu-id="6bd98-112">User locations and web-based applications (HTTP/HTTPs)</span></span> 

<span data-ttu-id="6bd98-113">Performance Monitor, ExpressRoute Monitor, and Service Connectivity Monitor are monitoring capabilities within NPM and are described below.</span><span class="sxs-lookup"><span data-stu-id="6bd98-113">Performance Monitor, ExpressRoute Monitor, and Service Connectivity Monitor are monitoring capabilities within NPM and are described below.</span></span>

## <a name="performance-monitor"></a><span data-ttu-id="6bd98-114">Performance Monitor</span><span class="sxs-lookup"><span data-stu-id="6bd98-114">Performance Monitor</span></span>

<span data-ttu-id="6bd98-115">Performance Monitor is part of NPM and is network monitoring for cloud, hybrid, and on-premises environments.</span><span class="sxs-lookup"><span data-stu-id="6bd98-115">Performance Monitor is part of NPM and is network monitoring for cloud, hybrid, and on-premises environments.</span></span> <span data-ttu-id="6bd98-116">You can monitor network connectivity across remote branch and field offices, store locations, data centers, and clouds.</span><span class="sxs-lookup"><span data-stu-id="6bd98-116">You can monitor network connectivity across remote branch and field offices, store locations, data centers, and clouds.</span></span> <span data-ttu-id="6bd98-117">You can detect network issues before your users complain.</span><span class="sxs-lookup"><span data-stu-id="6bd98-117">You can detect network issues before your users complain.</span></span> <span data-ttu-id="6bd98-118">The key advantages are:</span><span class="sxs-lookup"><span data-stu-id="6bd98-118">The key advantages are:</span></span>

* <span data-ttu-id="6bd98-119">Monitor loss and latency across various subnets and set alerts</span><span class="sxs-lookup"><span data-stu-id="6bd98-119">Monitor loss and latency across various subnets and set alerts</span></span>
* <span data-ttu-id="6bd98-120">Monitor all paths (including redundant paths) on the network</span><span class="sxs-lookup"><span data-stu-id="6bd98-120">Monitor all paths (including redundant paths) on the network</span></span>
* <span data-ttu-id="6bd98-121">Troubleshoot transient and point-in-time network issues, that are difficult to replicate</span><span class="sxs-lookup"><span data-stu-id="6bd98-121">Troubleshoot transient and point-in-time network issues, that are difficult to replicate</span></span>
* <span data-ttu-id="6bd98-122">Determine the specific segment on the network, that is responsible for degraded performance</span><span class="sxs-lookup"><span data-stu-id="6bd98-122">Determine the specific segment on the network, that is responsible for degraded performance</span></span>
* <span data-ttu-id="6bd98-123">Monitor the health of the network, without the need for SNMP</span><span class="sxs-lookup"><span data-stu-id="6bd98-123">Monitor the health of the network, without the need for SNMP</span></span>

![NPM topology map](./media/network-monitoring-overview/npm-topology-map.png) 

<span data-ttu-id="6bd98-125">For more information, view the following articles:</span><span class="sxs-lookup"><span data-stu-id="6bd98-125">For more information, view the following articles:</span></span>

* [<span data-ttu-id="6bd98-126">Configure a Network Performance Monitor Solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6bd98-126">Configure a Network Performance Monitor Solution in Log Analytics</span></span>](../log-analytics/log-analytics-network-performance-monitor.md) 
* [<span data-ttu-id="6bd98-127">Use cases</span><span class="sxs-lookup"><span data-stu-id="6bd98-127">Use cases</span></span>](https://blogs.technet.microsoft.com/msoms/2016/08/30/monitor-on-premises-cloud-iaas-and-hybrid-networks-using-oms-network-performance-monitor/)
*  <span data-ttu-id="6bd98-128">Product Updates: [February 2017](https://blogs.technet.microsoft.com/msoms/2017/02/27/oms-network-performance-monitor-is-now-generally-available/), [August 2017](https://blogs.technet.microsoft.com/msoms/2017/08/14/improvements-to-oms-network-performance-monitor/)</span><span class="sxs-lookup"><span data-stu-id="6bd98-128">Product Updates: [February 2017](https://blogs.technet.microsoft.com/msoms/2017/02/27/oms-network-performance-monitor-is-now-generally-available/), [August 2017](https://blogs.technet.microsoft.com/msoms/2017/08/14/improvements-to-oms-network-performance-monitor/)</span></span>

## <a name="expressroute-monitor"></a><span data-ttu-id="6bd98-129">ExpressRoute Monitor</span><span class="sxs-lookup"><span data-stu-id="6bd98-129">ExpressRoute Monitor</span></span>

<span data-ttu-id="6bd98-130">NPM for ExpressRoute offers comprehensive ExpressRoute monitoring for Azure Private peering and Microsoft peering connections.</span><span class="sxs-lookup"><span data-stu-id="6bd98-130">NPM for ExpressRoute offers comprehensive ExpressRoute monitoring for Azure Private peering and Microsoft peering connections.</span></span> <span data-ttu-id="6bd98-131">You can monitor E2E connectivity and performance between your branch offices and Azure over ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6bd98-131">You can monitor E2E connectivity and performance between your branch offices and Azure over ExpressRoute.</span></span> <span data-ttu-id="6bd98-132">The key capabilities are:</span><span class="sxs-lookup"><span data-stu-id="6bd98-132">The key capabilities are:</span></span>

* <span data-ttu-id="6bd98-133">Auto-detection of ER circuits associated with your subscription</span><span class="sxs-lookup"><span data-stu-id="6bd98-133">Auto-detection of ER circuits associated with your subscription</span></span>
* <span data-ttu-id="6bd98-134">Detection of network topology  from on-premises to your cloud applications</span><span class="sxs-lookup"><span data-stu-id="6bd98-134">Detection of network topology  from on-premises to your cloud applications</span></span>
* <span data-ttu-id="6bd98-135">Capacity planning,  bandwidth utilization analysis</span><span class="sxs-lookup"><span data-stu-id="6bd98-135">Capacity planning,  bandwidth utilization analysis</span></span>
* <span data-ttu-id="6bd98-136">Monitoring and alerting on both primary and secondary paths</span><span class="sxs-lookup"><span data-stu-id="6bd98-136">Monitoring and alerting on both primary and secondary paths</span></span>
* <span data-ttu-id="6bd98-137">Monitoring connectivity to Azure services such as Office 365, Dynamics 365, ... over ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6bd98-137">Monitoring connectivity to Azure services such as Office 365, Dynamics 365, ... over ExpressRoute</span></span>
* <span data-ttu-id="6bd98-138">Detect degradation of connectivity to VNets</span><span class="sxs-lookup"><span data-stu-id="6bd98-138">Detect degradation of connectivity to VNets</span></span>

![Geo-map showing traffic across regions](./media/network-monitoring-overview/expressroute-topology-map.png) 

<span data-ttu-id="6bd98-140">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="6bd98-140">For more information, see the following articles:</span></span>

* [<span data-ttu-id="6bd98-141">Configure Network Performance Monitor for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6bd98-141">Configure Network Performance Monitor for ExpressRoute</span></span>](../expressroute/how-to-npm.md)
* [<span data-ttu-id="6bd98-142">Blog post</span><span class="sxs-lookup"><span data-stu-id="6bd98-142">Blog post</span></span>](https://aka.ms/NPMExRmonitorGA)

## <a name="service-connectivity-monitor"></a><span data-ttu-id="6bd98-143">Service Connectivity Monitor</span><span class="sxs-lookup"><span data-stu-id="6bd98-143">Service Connectivity Monitor</span></span>

<span data-ttu-id="6bd98-144">With Service Connectivity monitoring, you can now test reachability of applications and detect performance bottlenecks across on-premises, carrier networks and cloud/private data centers.</span><span class="sxs-lookup"><span data-stu-id="6bd98-144">With Service Connectivity monitoring, you can now test reachability of applications and detect performance bottlenecks across on-premises, carrier networks and cloud/private data centers.</span></span>

* <span data-ttu-id="6bd98-145">Monitor end-to-end network connectivity to applications</span><span class="sxs-lookup"><span data-stu-id="6bd98-145">Monitor end-to-end network connectivity to applications</span></span>
* <span data-ttu-id="6bd98-146">Correlate application delivery with network performance, detect precise location of degradation along the path between the user and the application</span><span class="sxs-lookup"><span data-stu-id="6bd98-146">Correlate application delivery with network performance, detect precise location of degradation along the path between the user and the application</span></span>
* <span data-ttu-id="6bd98-147">Test application reachability from multiple user locations across the globe</span><span class="sxs-lookup"><span data-stu-id="6bd98-147">Test application reachability from multiple user locations across the globe</span></span>
* <span data-ttu-id="6bd98-148">Determine network latency and packet loss for your line of business and SaaS applications</span><span class="sxs-lookup"><span data-stu-id="6bd98-148">Determine network latency and packet loss for your line of business and SaaS applications</span></span>
* <span data-ttu-id="6bd98-149">Determine hot spots on the network, that may be causing poor application performance</span><span class="sxs-lookup"><span data-stu-id="6bd98-149">Determine hot spots on the network, that may be causing poor application performance</span></span>
* <span data-ttu-id="6bd98-150">Monitor reachability to  Office 365 applications, using built-in tests for Microsoft Office 365, Dynamics 365, Skype for Business and other Microsoft services</span><span class="sxs-lookup"><span data-stu-id="6bd98-150">Monitor reachability to  Office 365 applications, using built-in tests for Microsoft Office 365, Dynamics 365, Skype for Business and other Microsoft services</span></span>

<span data-ttu-id="6bd98-151">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="6bd98-151">For more information, see the following articles:</span></span>

* [<span data-ttu-id="6bd98-152">Configure Network Performance Monitor for monitoring Service Endpoints</span><span class="sxs-lookup"><span data-stu-id="6bd98-152">Configure Network Performance Monitor for monitoring Service Endpoints</span></span>](https://aka.ms/applicationconnectivitymonitorguide)
* [<span data-ttu-id="6bd98-153">Blog post</span><span class="sxs-lookup"><span data-stu-id="6bd98-153">Blog post</span></span>](https://aka.ms/svcendptmonitor)

## <a name="traffic-analytics"></a><span data-ttu-id="6bd98-154">Traffic Analytics</span><span class="sxs-lookup"><span data-stu-id="6bd98-154">Traffic Analytics</span></span>
<span data-ttu-id="6bd98-155">Traffic Analytics is a cloud-based solution that provides  visibility into user and application activity on your cloud networks.</span><span class="sxs-lookup"><span data-stu-id="6bd98-155">Traffic Analytics is a cloud-based solution that provides  visibility into user and application activity on your cloud networks.</span></span> <span data-ttu-id="6bd98-156">NSG Flow logs are analyzed to provide insights into:</span><span class="sxs-lookup"><span data-stu-id="6bd98-156">NSG Flow logs are analyzed to provide insights into:</span></span>

* <span data-ttu-id="6bd98-157">Traffic flows across your networks between Azure and Internet,  public cloud regions, VNETs, and subnets</span><span class="sxs-lookup"><span data-stu-id="6bd98-157">Traffic flows across your networks between Azure and Internet,  public cloud regions, VNETs, and subnets</span></span>
* <span data-ttu-id="6bd98-158">Applications and protocols on your network, without the need for sniffers or dedicated flow collector appliances</span><span class="sxs-lookup"><span data-stu-id="6bd98-158">Applications and protocols on your network, without the need for sniffers or dedicated flow collector appliances</span></span>
* <span data-ttu-id="6bd98-159">Top talkers, chatty applications, VM conversations in the cloud, traffic hotspots</span><span class="sxs-lookup"><span data-stu-id="6bd98-159">Top talkers, chatty applications, VM conversations in the cloud, traffic hotspots</span></span>
* <span data-ttu-id="6bd98-160">Sources and destinations of traffic across VNETs, inter-relationships between critical business services and applications</span><span class="sxs-lookup"><span data-stu-id="6bd98-160">Sources and destinations of traffic across VNETs, inter-relationships between critical business services and applications</span></span>
* <span data-ttu-id="6bd98-161">Security – malicious traffic, ports open to the Internet,  applications or VMs attempting Internet access…</span><span class="sxs-lookup"><span data-stu-id="6bd98-161">Security – malicious traffic, ports open to the Internet,  applications or VMs attempting Internet access…</span></span>
* <span data-ttu-id="6bd98-162">Capacity utilization - helps you eliminate issues of over-provisioning or underutilization by monitoring utilization trends of VPN gateways and other services</span><span class="sxs-lookup"><span data-stu-id="6bd98-162">Capacity utilization - helps you eliminate issues of over-provisioning or underutilization by monitoring utilization trends of VPN gateways and other services</span></span>

<span data-ttu-id="6bd98-163">Traffic Analytics equips you with actionable information that helps you audit your organization’s network activity, secure applications and data,  optimize workload performance and stay compliant.</span><span class="sxs-lookup"><span data-stu-id="6bd98-163">Traffic Analytics equips you with actionable information that helps you audit your organization’s network activity, secure applications and data,  optimize workload performance and stay compliant.</span></span>

![Geo-map showing traffic across regions](../network-watcher/media/traffic-analytics/geo-map-view-showcasing-traffic-distribution-to-countries-and-continents.png) 

<span data-ttu-id="6bd98-165">Related links:</span><span class="sxs-lookup"><span data-stu-id="6bd98-165">Related links:</span></span>
* <span data-ttu-id="6bd98-166">[Blog post](https://aka.ms/trafficanalytics), [Documentation](https://aka.ms/trafficanalyticsdocs), [FAQ](https://docs.microsoft.com/azure/network-watcher/traffic-analytics-faq)</span><span class="sxs-lookup"><span data-stu-id="6bd98-166">[Blog post](https://aka.ms/trafficanalytics), [Documentation](https://aka.ms/trafficanalyticsdocs), [FAQ](https://docs.microsoft.com/azure/network-watcher/traffic-analytics-faq)</span></span>

## <a name="dns-analytics"></a><span data-ttu-id="6bd98-167">DNS Analytics</span><span class="sxs-lookup"><span data-stu-id="6bd98-167">DNS Analytics</span></span>
<span data-ttu-id="6bd98-168">Built for DNS Administrators, this solution collects, analyzes, and correlates DNS logs to provide security, operations, and performance-related insights.</span><span class="sxs-lookup"><span data-stu-id="6bd98-168">Built for DNS Administrators, this solution collects, analyzes, and correlates DNS logs to provide security, operations, and performance-related insights.</span></span>  <span data-ttu-id="6bd98-169">Some of the capabilities are:</span><span class="sxs-lookup"><span data-stu-id="6bd98-169">Some of the capabilities are:</span></span>

* <span data-ttu-id="6bd98-170">Identification of clients that try to resolve to malicious domains</span><span class="sxs-lookup"><span data-stu-id="6bd98-170">Identification of clients that try to resolve to malicious domains</span></span>
* <span data-ttu-id="6bd98-171">Identification of stale resource records</span><span class="sxs-lookup"><span data-stu-id="6bd98-171">Identification of stale resource records</span></span>
* <span data-ttu-id="6bd98-172">Visibility into frequently queried domain names and talkative DNS clients</span><span class="sxs-lookup"><span data-stu-id="6bd98-172">Visibility into frequently queried domain names and talkative DNS clients</span></span>
* <span data-ttu-id="6bd98-173">Visibility into the request load on DNS servers</span><span class="sxs-lookup"><span data-stu-id="6bd98-173">Visibility into the request load on DNS servers</span></span>
* <span data-ttu-id="6bd98-174">Monitoring of dynamic DNS registration failures</span><span class="sxs-lookup"><span data-stu-id="6bd98-174">Monitoring of dynamic DNS registration failures</span></span>

![DNS Analytics Dashboard](./media/network-monitoring-overview/dns-analytics-overview.png) 

<span data-ttu-id="6bd98-176">Related links:</span><span class="sxs-lookup"><span data-stu-id="6bd98-176">Related links:</span></span>
* <span data-ttu-id="6bd98-177">[Blog post](https://blogs.technet.microsoft.com/msoms/2017/04/19/introducing-oms-dns-analytics/), [Documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-dns)</span><span class="sxs-lookup"><span data-stu-id="6bd98-177">[Blog post](https://blogs.technet.microsoft.com/msoms/2017/04/19/introducing-oms-dns-analytics/), [Documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-dns)</span></span>

## <a name="miscellaneous"></a><span data-ttu-id="6bd98-178">Miscellaneous</span><span class="sxs-lookup"><span data-stu-id="6bd98-178">Miscellaneous</span></span>

* [<span data-ttu-id="6bd98-179">New Pricing</span><span class="sxs-lookup"><span data-stu-id="6bd98-179">New Pricing</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor-pricing-faq)
