---
title: Pricing FAQ for Azure Network Performance Monitor | Microsoft Docs
description: Frequently asked questions - Azure Network Performance Monitor
services: monitoring-and-diagnostics
documentationcenter: na
author: agummadi
manager: cherylmc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/02/2018
ms.author: ajaycode
ms.component: na
ms.openlocfilehash: 96eb26d6a4faf8c6907d23ebf21f2446722c913b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870363"
---
# <a name="pricing-changes-for-azure-network-performance-monitor"></a><span data-ttu-id="5cb8f-103">Pricing changes for Azure Network Performance Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-103">Pricing changes for Azure Network Performance Monitor</span></span>

<span data-ttu-id="5cb8f-104">We have listened to your feedback and recently introduced a [new pricing experience](https://azure.microsoft.com/blog/introducing-a-new-way-to-purchase-azure-monitoring-services/) for various monitoring services across Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-104">We have listened to your feedback and recently introduced a [new pricing experience](https://azure.microsoft.com/blog/introducing-a-new-way-to-purchase-azure-monitoring-services/) for various monitoring services across Azure.</span></span> <span data-ttu-id="5cb8f-105">This article captures the pricing changes related to Azure [Network Performance Monitor](https://docs.microsoft.com/azure/networking/network-monitoring-overview) (NPM) in an easy-to-read question and answer format.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-105">This article captures the pricing changes related to Azure [Network Performance Monitor](https://docs.microsoft.com/azure/networking/network-monitoring-overview) (NPM) in an easy-to-read question and answer format.</span></span>

<span data-ttu-id="5cb8f-106">Network Performance Monitor consists of three components:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-106">Network Performance Monitor consists of three components:</span></span>
* [<span data-ttu-id="5cb8f-107">Performance Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-107">Performance Monitor</span></span>](https://docs.microsoft.com/azure/networking/network-monitoring-overview#performance-monitor)
* [<span data-ttu-id="5cb8f-108">Service Endpoint Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-108">Service Endpoint Monitor</span></span>](https://docs.microsoft.com/azure/networking/network-monitoring-overview#service-endpoint-monitor)
* [<span data-ttu-id="5cb8f-109">ExpressRoute Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-109">ExpressRoute Monitor</span></span>](https://docs.microsoft.com/azure/networking/network-monitoring-overview#expressroute-monitor)

<span data-ttu-id="5cb8f-110">The following sections explain the pricing changes for the NPM components.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-110">The following sections explain the pricing changes for the NPM components.</span></span>

## <a name="performance-monitor"></a><span data-ttu-id="5cb8f-111">Performance Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-111">Performance Monitor</span></span>

<span data-ttu-id="5cb8f-112">**How was usage of Performance Monitor billed in the old model?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-112">**How was usage of Performance Monitor billed in the old model?**</span></span>

<span data-ttu-id="5cb8f-113">The billing for NPM was based on the usage and consumption of two components:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-113">The billing for NPM was based on the usage and consumption of two components:</span></span>
* <span data-ttu-id="5cb8f-114">**Nodes**: All synthetic transactions originate and terminate at the nodes.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-114">**Nodes**: All synthetic transactions originate and terminate at the nodes.</span></span> <span data-ttu-id="5cb8f-115">Nodes are also referred to as agents or Microsoft Management Agents.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-115">Nodes are also referred to as agents or Microsoft Management Agents.</span></span>
* <span data-ttu-id="5cb8f-116">**Data**: The results of the various network tests are stored in the Azure Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-116">**Data**: The results of the various network tests are stored in the Azure Log Analytics repository.</span></span>

<span data-ttu-id="5cb8f-117">Under the old model, the bill was computed based on the number of nodes and the volume of data generated.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-117">Under the old model, the bill was computed based on the number of nodes and the volume of data generated.</span></span> 

<span data-ttu-id="5cb8f-118">**How is usage of Performance Monitor charged under the new model?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-118">**How is usage of Performance Monitor charged under the new model?**</span></span>

<span data-ttu-id="5cb8f-119">The Performance Monitor feature in NPM is now billed based on a combination of:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-119">The Performance Monitor feature in NPM is now billed based on a combination of:</span></span> 

* <span data-ttu-id="5cb8f-120">Subnet links monitored</span><span class="sxs-lookup"><span data-stu-id="5cb8f-120">Subnet links monitored</span></span>
* <span data-ttu-id="5cb8f-121">Data volume</span><span class="sxs-lookup"><span data-stu-id="5cb8f-121">Data volume</span></span>

<span data-ttu-id="5cb8f-122">**What is a subnet link?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-122">**What is a subnet link?**</span></span>

<span data-ttu-id="5cb8f-123">Performance Monitor monitors connectivity between two or more locations on the network.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-123">Performance Monitor monitors connectivity between two or more locations on the network.</span></span> <span data-ttu-id="5cb8f-124">The connection between a group of nodes or agents on one subnet, and a group of nodes on another subnet, is called a subnet link.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-124">The connection between a group of nodes or agents on one subnet, and a group of nodes on another subnet, is called a subnet link.</span></span>

<span data-ttu-id="5cb8f-125">**I have two subnets (A and B), and I have several agents on each subnet. Performance Monitor monitors connectivity from all agents on subnet A to all agents on subnet B. Will I be charged based on the number of inter-subnet connections?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-125">**I have two subnets (A and B), and I have several agents on each subnet. Performance Monitor monitors connectivity from all agents on subnet A to all agents on subnet B. Will I be charged based on the number of inter-subnet connections?**</span></span>

<span data-ttu-id="5cb8f-126">No.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-126">No.</span></span> <span data-ttu-id="5cb8f-127">For billing purposes, all connections from subnet A to subnet B are grouped together into one subnet link.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-127">For billing purposes, all connections from subnet A to subnet B are grouped together into one subnet link.</span></span> <span data-ttu-id="5cb8f-128">You're billed for a single connection.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-128">You're billed for a single connection.</span></span> <span data-ttu-id="5cb8f-129">Performance Monitor continues to monitor connectivity between various agents on each subnet.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-129">Performance Monitor continues to monitor connectivity between various agents on each subnet.</span></span>

<span data-ttu-id="5cb8f-130">**What are the costs for monitoring a subnet link?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-130">**What are the costs for monitoring a subnet link?**</span></span>

<span data-ttu-id="5cb8f-131">For the cost of monitoring a single subnet link for the entire month, see the [Ping Mesh](https://azure.microsoft.com/pricing/details/network-watcher/) section.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-131">For the cost of monitoring a single subnet link for the entire month, see the [Ping Mesh](https://azure.microsoft.com/pricing/details/network-watcher/) section.</span></span>

<span data-ttu-id="5cb8f-132">**What are the charges for data that Performance Monitor generates?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-132">**What are the charges for data that Performance Monitor generates?**</span></span>

<span data-ttu-id="5cb8f-133">The charge for ingestion (data upload to Log Analytics, processing, and indexing) is available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/) for Log Analytics, in the Data Ingestion section.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-133">The charge for ingestion (data upload to Log Analytics, processing, and indexing) is available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/) for Log Analytics, in the Data Ingestion section.</span></span> <span data-ttu-id="5cb8f-134">The charge for data retention (that is, data retained at customer's option, beyond the first month) is also available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/), in the Data Retention section.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-134">The charge for data retention (that is, data retained at customer's option, beyond the first month) is also available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/), in the Data Retention section.</span></span>


## <a name="expressroute-monitor"></a><span data-ttu-id="5cb8f-135">ExpressRoute Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-135">ExpressRoute Monitor</span></span>

<span data-ttu-id="5cb8f-136">**What are the charges for usage of ExpressRoute Monitor?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-136">**What are the charges for usage of ExpressRoute Monitor?**</span></span>

<span data-ttu-id="5cb8f-137">Charges for ExpressRoute Monitor are billed based on the volume of data generated during monitoring.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-137">Charges for ExpressRoute Monitor are billed based on the volume of data generated during monitoring.</span></span> <span data-ttu-id="5cb8f-138">For more information, see "What are the charges for data that Performance Monitor generates?"</span><span class="sxs-lookup"><span data-stu-id="5cb8f-138">For more information, see "What are the charges for data that Performance Monitor generates?"</span></span>

<span data-ttu-id="5cb8f-139">**I use ExpressRoute Monitor to monitor multiple ExpressRoute circuits. Am I charged based on the number of circuits being monitored?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-139">**I use ExpressRoute Monitor to monitor multiple ExpressRoute circuits. Am I charged based on the number of circuits being monitored?**</span></span>

<span data-ttu-id="5cb8f-140">You are not charged based on either the number of circuits or the type of peering (for example, private peering, Microsoft peering).</span><span class="sxs-lookup"><span data-stu-id="5cb8f-140">You are not charged based on either the number of circuits or the type of peering (for example, private peering, Microsoft peering).</span></span> <span data-ttu-id="5cb8f-141">You are charged based on the volume of data, as explained previously.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-141">You are charged based on the volume of data, as explained previously.</span></span>

<span data-ttu-id="5cb8f-142">**What is the volume of data generated when ExpressRoute monitors a single circuit?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-142">**What is the volume of data generated when ExpressRoute monitors a single circuit?**</span></span>

<span data-ttu-id="5cb8f-143">The volume of data generated per month, when ExpressRoute monitors a private peering connection, is as follows:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-143">The volume of data generated per month, when ExpressRoute monitors a private peering connection, is as follows:</span></span>

|<span data-ttu-id="5cb8f-144">Percentile</span><span class="sxs-lookup"><span data-stu-id="5cb8f-144">Percentile</span></span>      |<span data-ttu-id="5cb8f-145">Data/month (MB)</span><span class="sxs-lookup"><span data-stu-id="5cb8f-145">Data/month (MB)</span></span>|
| :---:          |           ---:|
|<span data-ttu-id="5cb8f-146">50<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-146">50<sup>th</sup></span></span> |            <span data-ttu-id="5cb8f-147">192</span><span class="sxs-lookup"><span data-stu-id="5cb8f-147">192</span></span>|
|<span data-ttu-id="5cb8f-148">60<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-148">60<sup>th</sup></span></span> |            <span data-ttu-id="5cb8f-149">256</span><span class="sxs-lookup"><span data-stu-id="5cb8f-149">256</span></span>|
|<span data-ttu-id="5cb8f-150">70<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-150">70<sup>th</sup></span></span> |            <span data-ttu-id="5cb8f-151">360</span><span class="sxs-lookup"><span data-stu-id="5cb8f-151">360</span></span>|
|<span data-ttu-id="5cb8f-152">80<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-152">80<sup>th</sup></span></span> |            <span data-ttu-id="5cb8f-153">498</span><span class="sxs-lookup"><span data-stu-id="5cb8f-153">498</span></span>|
|<span data-ttu-id="5cb8f-154">90<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-154">90<sup>th</sup></span></span> |            <span data-ttu-id="5cb8f-155">870</span><span class="sxs-lookup"><span data-stu-id="5cb8f-155">870</span></span>|
|<span data-ttu-id="5cb8f-156">95<sup>th</sup></span><span class="sxs-lookup"><span data-stu-id="5cb8f-156">95<sup>th</sup></span></span> |           <span data-ttu-id="5cb8f-157">1560</span><span class="sxs-lookup"><span data-stu-id="5cb8f-157">1560</span></span>|


<span data-ttu-id="5cb8f-158">According to this table, customers at the 50th percentile pay for 192 MB of data.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-158">According to this table, customers at the 50th percentile pay for 192 MB of data.</span></span> <span data-ttu-id="5cb8f-159">At USD $2.30/GB for the first month, the cost incurred for monitoring a circuit is USD $0.43 (= 192 \* 2.30 / 1024).</span><span class="sxs-lookup"><span data-stu-id="5cb8f-159">At USD $2.30/GB for the first month, the cost incurred for monitoring a circuit is USD $0.43 (= 192 \* 2.30 / 1024).</span></span>

<span data-ttu-id="5cb8f-160">**What are some reasons for variations in the volume of data?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-160">**What are some reasons for variations in the volume of data?**</span></span>

<span data-ttu-id="5cb8f-161">The volume of monitoring data generated depends on several factors, such as:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-161">The volume of monitoring data generated depends on several factors, such as:</span></span>
* <span data-ttu-id="5cb8f-162">Number of agents.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-162">Number of agents.</span></span> <span data-ttu-id="5cb8f-163">The accuracy of fault isolation increases with an increase in the number of agents.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-163">The accuracy of fault isolation increases with an increase in the number of agents.</span></span>
* <span data-ttu-id="5cb8f-164">Number of hops on the network.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-164">Number of hops on the network.</span></span>
* <span data-ttu-id="5cb8f-165">Number of paths between the source and the destination.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-165">Number of paths between the source and the destination.</span></span>

<span data-ttu-id="5cb8f-166">Customers at the higher percentiles (in the preceding table) usually monitor their circuits from several vantage points on their on-premises network.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-166">Customers at the higher percentiles (in the preceding table) usually monitor their circuits from several vantage points on their on-premises network.</span></span> <span data-ttu-id="5cb8f-167">Multiple agents are also placed deeper in the network, farther from the service provider edge router.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-167">Multiple agents are also placed deeper in the network, farther from the service provider edge router.</span></span> <span data-ttu-id="5cb8f-168">The agents are often placed at several user sites, branches, and racks in datacenters.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-168">The agents are often placed at several user sites, branches, and racks in datacenters.</span></span>

## <a name="service-endpoint-monitor"></a><span data-ttu-id="5cb8f-169">Service Endpoint Monitor</span><span class="sxs-lookup"><span data-stu-id="5cb8f-169">Service Endpoint Monitor</span></span>

<span data-ttu-id="5cb8f-170">**What are the charges for usage of Service Endpoint Monitor?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-170">**What are the charges for usage of Service Endpoint Monitor?**</span></span>

<span data-ttu-id="5cb8f-171">Charges for usage of Service Endpoint Monitor are computed based on:</span><span class="sxs-lookup"><span data-stu-id="5cb8f-171">Charges for usage of Service Endpoint Monitor are computed based on:</span></span>
* <span data-ttu-id="5cb8f-172">Number of connections</span><span class="sxs-lookup"><span data-stu-id="5cb8f-172">Number of connections</span></span>
* <span data-ttu-id="5cb8f-173">Volume of data</span><span class="sxs-lookup"><span data-stu-id="5cb8f-173">Volume of data</span></span>

<span data-ttu-id="5cb8f-174">**What is a connection?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-174">**What is a connection?**</span></span>

<span data-ttu-id="5cb8f-175">A connection is a test of reachability to one endpoint (URL or network service) from a single agent for the entire month.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-175">A connection is a test of reachability to one endpoint (URL or network service) from a single agent for the entire month.</span></span> <span data-ttu-id="5cb8f-176">For example, monitoring a connection to bing.com from three agents constitutes three connections.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-176">For example, monitoring a connection to bing.com from three agents constitutes three connections.</span></span>

<span data-ttu-id="5cb8f-177">**What are the costs for Service Endpoint Monitor?**</span><span class="sxs-lookup"><span data-stu-id="5cb8f-177">**What are the costs for Service Endpoint Monitor?**</span></span>

<span data-ttu-id="5cb8f-178">Refer to the [Connection Monitoring](https://azure.microsoft.com/pricing/details/network-watcher/) section for the cost of monitoring an endpoint for the entire month.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-178">Refer to the [Connection Monitoring](https://azure.microsoft.com/pricing/details/network-watcher/) section for the cost of monitoring an endpoint for the entire month.</span></span> <span data-ttu-id="5cb8f-179">The charge for data is available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/) for Log Analytics, in the Data Ingestion section.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-179">The charge for data is available on the [pricing page](https://azure.microsoft.com/pricing/details/log-analytics/) for Log Analytics, in the Data Ingestion section.</span></span>

## <a name="references"></a><span data-ttu-id="5cb8f-180">References</span><span class="sxs-lookup"><span data-stu-id="5cb8f-180">References</span></span>

<span data-ttu-id="5cb8f-181">[Log Analytics Pricing FAQ](https://azure.microsoft.com/pricing/details/log-analytics/): The FAQ section has information on free tier, per node pricing and other pricing details.</span><span class="sxs-lookup"><span data-stu-id="5cb8f-181">[Log Analytics Pricing FAQ](https://azure.microsoft.com/pricing/details/log-analytics/): The FAQ section has information on free tier, per node pricing and other pricing details.</span></span>

