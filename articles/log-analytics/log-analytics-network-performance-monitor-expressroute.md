---
title: Network Performance Monitor solution in Azure Log Analytics | Microsoft Docs
description: Use the ExpressRoute Monitor capability in Network Performance Monitor to monitor end-to-end connectivity and performance between your branch offices and Azure, over Azure ExpressRoute.
services: log-analytics
documentationcenter: ''
author: abshamsft
manager: carmonm
editor: ''
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 02/20/2018
ms.author: abshamsft
ms.component: na
ms.openlocfilehash: 27169193a468d98be879164b80e63fffde419002
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966739"
---
# <a name="expressroute-monitor"></a><span data-ttu-id="534f8-103">ExpressRoute Monitor</span><span class="sxs-lookup"><span data-stu-id="534f8-103">ExpressRoute Monitor</span></span>

<span data-ttu-id="534f8-104">You can use the Azure ExpressRoute Monitor capability in [Network Performance Monitor](log-analytics-network-performance-monitor.md) to monitor end-to-end connectivity and performance between your branch offices and Azure, over Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="534f8-104">You can use the Azure ExpressRoute Monitor capability in [Network Performance Monitor](log-analytics-network-performance-monitor.md) to monitor end-to-end connectivity and performance between your branch offices and Azure, over Azure ExpressRoute.</span></span> <span data-ttu-id="534f8-105">Key advantages are:</span><span class="sxs-lookup"><span data-stu-id="534f8-105">Key advantages are:</span></span> 

- <span data-ttu-id="534f8-106">Autodetection of ExpressRoute circuits associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="534f8-106">Autodetection of ExpressRoute circuits associated with your subscription.</span></span>
- <span data-ttu-id="534f8-107">Tracking of bandwidth utilization, loss and latency at the circuit, peering, and Azure Virtual Network level for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="534f8-107">Tracking of bandwidth utilization, loss and latency at the circuit, peering, and Azure Virtual Network level for ExpressRoute.</span></span>
- <span data-ttu-id="534f8-108">Discovery of network topology of your ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="534f8-108">Discovery of network topology of your ExpressRoute circuits.</span></span>

![ExpressRoute Monitor](media/log-analytics-network-performance-monitor/expressroute-intro.png)

## <a name="configuration"></a><span data-ttu-id="534f8-110">Configuration</span><span class="sxs-lookup"><span data-stu-id="534f8-110">Configuration</span></span> 
<span data-ttu-id="534f8-111">To open the configuration for Network Performance Monitor, open the [Network Performance Monitor solution](log-analytics-network-performance-monitor.md) and select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="534f8-111">To open the configuration for Network Performance Monitor, open the [Network Performance Monitor solution](log-analytics-network-performance-monitor.md) and select **Configure**.</span></span>

### <a name="configure-network-security-group-rules"></a><span data-ttu-id="534f8-112">Configure network security group rules</span><span class="sxs-lookup"><span data-stu-id="534f8-112">Configure network security group rules</span></span> 
<span data-ttu-id="534f8-113">For the servers in Azure that are used for monitoring via Network Performance Monitor, configure network security group (NSG) rules to allow TCP traffic on the port used by Network Performance Monitor for synthetic transactions.</span><span class="sxs-lookup"><span data-stu-id="534f8-113">For the servers in Azure that are used for monitoring via Network Performance Monitor, configure network security group (NSG) rules to allow TCP traffic on the port used by Network Performance Monitor for synthetic transactions.</span></span> <span data-ttu-id="534f8-114">The default port is 8084.</span><span class="sxs-lookup"><span data-stu-id="534f8-114">The default port is 8084.</span></span> <span data-ttu-id="534f8-115">This configuration allows the Operations Management Suite agent installed on Azure VMs to communicate with an on-premises monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="534f8-115">This configuration allows the Operations Management Suite agent installed on Azure VMs to communicate with an on-premises monitoring agent.</span></span> 

<span data-ttu-id="534f8-116">For more information about NSGs, see [Network security groups](../virtual-network/manage-network-security-group.md).</span><span class="sxs-lookup"><span data-stu-id="534f8-116">For more information about NSGs, see [Network security groups](../virtual-network/manage-network-security-group.md).</span></span> 

>[!NOTE]
> <span data-ttu-id="534f8-117">Before you continue with this step, install the on-premises server agent and the Azure server agent, and run the EnableRules.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="534f8-117">Before you continue with this step, install the on-premises server agent and the Azure server agent, and run the EnableRules.ps1 PowerShell script.</span></span> 

 
### <a name="discover-expressroute-peering-connections"></a><span data-ttu-id="534f8-118">Discover ExpressRoute peering connections</span><span class="sxs-lookup"><span data-stu-id="534f8-118">Discover ExpressRoute peering connections</span></span> 
 
1. <span data-ttu-id="534f8-119">Select the **ExpressRoute Peerings** view.</span><span class="sxs-lookup"><span data-stu-id="534f8-119">Select the **ExpressRoute Peerings** view.</span></span>
2. <span data-ttu-id="534f8-120">Select **Discover Now** to discover all the ExpressRoute private peerings that are connected to the virtual networks in the Azure subscription linked with this Azure Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="534f8-120">Select **Discover Now** to discover all the ExpressRoute private peerings that are connected to the virtual networks in the Azure subscription linked with this Azure Log Analytics workspace.</span></span>

    >[!NOTE]
    > <span data-ttu-id="534f8-121">The solution currently discovers only ExpressRoute private peerings.</span><span class="sxs-lookup"><span data-stu-id="534f8-121">The solution currently discovers only ExpressRoute private peerings.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="534f8-122">Only private peerings connected to the virtual networks associated with the subscription linked with this Log Analytics workspace are discovered.</span><span class="sxs-lookup"><span data-stu-id="534f8-122">Only private peerings connected to the virtual networks associated with the subscription linked with this Log Analytics workspace are discovered.</span></span> <span data-ttu-id="534f8-123">If ExpressRoute is connected to virtual networks outside of the subscription linked to this workspace, create a Log Analytics workspace in those subscriptions.</span><span class="sxs-lookup"><span data-stu-id="534f8-123">If ExpressRoute is connected to virtual networks outside of the subscription linked to this workspace, create a Log Analytics workspace in those subscriptions.</span></span> <span data-ttu-id="534f8-124">Then use Network Performance Monitor to monitor those peerings.</span><span class="sxs-lookup"><span data-stu-id="534f8-124">Then use Network Performance Monitor to monitor those peerings.</span></span> 

    ![ExpressRoute Monitor configuration](media/log-analytics-network-performance-monitor/expressroute-configure.png)
 
 <span data-ttu-id="534f8-126">After the discovery is complete, the discovered private peering connections are listed in a table.</span><span class="sxs-lookup"><span data-stu-id="534f8-126">After the discovery is complete, the discovered private peering connections are listed in a table.</span></span> <span data-ttu-id="534f8-127">The monitoring for these peerings is initially in a disabled state.</span><span class="sxs-lookup"><span data-stu-id="534f8-127">The monitoring for these peerings is initially in a disabled state.</span></span> 

### <a name="enable-monitoring-of-the-expressroute-peering-connections"></a><span data-ttu-id="534f8-128">Enable monitoring of the ExpressRoute peering connections</span><span class="sxs-lookup"><span data-stu-id="534f8-128">Enable monitoring of the ExpressRoute peering connections</span></span> 

1. <span data-ttu-id="534f8-129">Select the private peering connection you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="534f8-129">Select the private peering connection you want to monitor.</span></span>
2. <span data-ttu-id="534f8-130">In the pane on the right, select the **Monitor this Peering** check box.</span><span class="sxs-lookup"><span data-stu-id="534f8-130">In the pane on the right, select the **Monitor this Peering** check box.</span></span> 
3. <span data-ttu-id="534f8-131">If you intend to create health events for this connection, select **Enable Health Monitoring for this peering**.</span><span class="sxs-lookup"><span data-stu-id="534f8-131">If you intend to create health events for this connection, select **Enable Health Monitoring for this peering**.</span></span> 
4. <span data-ttu-id="534f8-132">Choose monitoring conditions.</span><span class="sxs-lookup"><span data-stu-id="534f8-132">Choose monitoring conditions.</span></span> <span data-ttu-id="534f8-133">You can set custom thresholds for health event generation by entering threshold values.</span><span class="sxs-lookup"><span data-stu-id="534f8-133">You can set custom thresholds for health event generation by entering threshold values.</span></span> <span data-ttu-id="534f8-134">Whenever the value of the condition goes above its selected threshold for the peering connection, a health event is generated.</span><span class="sxs-lookup"><span data-stu-id="534f8-134">Whenever the value of the condition goes above its selected threshold for the peering connection, a health event is generated.</span></span> 
5. <span data-ttu-id="534f8-135">Select **Add Agents** to choose the monitoring agents you intend to use for monitoring this peering connection.</span><span class="sxs-lookup"><span data-stu-id="534f8-135">Select **Add Agents** to choose the monitoring agents you intend to use for monitoring this peering connection.</span></span> <span data-ttu-id="534f8-136">Make sure that you add agents on both ends of the connection.</span><span class="sxs-lookup"><span data-stu-id="534f8-136">Make sure that you add agents on both ends of the connection.</span></span> <span data-ttu-id="534f8-137">You need at least one agent in the virtual network connected to this peering.</span><span class="sxs-lookup"><span data-stu-id="534f8-137">You need at least one agent in the virtual network connected to this peering.</span></span> <span data-ttu-id="534f8-138">You also need at least one on-premises agent connected to this peering.</span><span class="sxs-lookup"><span data-stu-id="534f8-138">You also need at least one on-premises agent connected to this peering.</span></span> 
6. <span data-ttu-id="534f8-139">Select **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="534f8-139">Select **Save** to save the configuration.</span></span> 

   ![ExpressRoute monitoring configuration](media/log-analytics-network-performance-monitor/expressroute-configure-discovery.png)


<span data-ttu-id="534f8-141">After you enable the rules and select values and agents, wait 30 to 60 minutes for the values to populate and the **ExpressRoute Monitoring** tiles to appear.</span><span class="sxs-lookup"><span data-stu-id="534f8-141">After you enable the rules and select values and agents, wait 30 to 60 minutes for the values to populate and the **ExpressRoute Monitoring** tiles to appear.</span></span> <span data-ttu-id="534f8-142">When you see the monitoring tiles, your ExpressRoute circuits and connection resources are now monitored by Network Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="534f8-142">When you see the monitoring tiles, your ExpressRoute circuits and connection resources are now monitored by Network Performance Monitor.</span></span> 

>[!NOTE]
> <span data-ttu-id="534f8-143">This capability works reliably on workspaces that have upgraded to the new query language.</span><span class="sxs-lookup"><span data-stu-id="534f8-143">This capability works reliably on workspaces that have upgraded to the new query language.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="534f8-144">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="534f8-144">Walkthrough</span></span> 

<span data-ttu-id="534f8-145">The Network Performance Monitor dashboard shows an overview of the health of ExpressRoute circuits and peering connections.</span><span class="sxs-lookup"><span data-stu-id="534f8-145">The Network Performance Monitor dashboard shows an overview of the health of ExpressRoute circuits and peering connections.</span></span> 

![Network Performance Monitor dashboard](media/log-analytics-network-performance-monitor/npm-dashboard-expressroute.png) 

### <a name="circuits-list"></a><span data-ttu-id="534f8-147">Circuits list</span><span class="sxs-lookup"><span data-stu-id="534f8-147">Circuits list</span></span> 

<span data-ttu-id="534f8-148">To see a list of all monitored ExpressRoute circuits, select the ExpressRoute circuits tile.</span><span class="sxs-lookup"><span data-stu-id="534f8-148">To see a list of all monitored ExpressRoute circuits, select the ExpressRoute circuits tile.</span></span> <span data-ttu-id="534f8-149">You can select a circuit and view its health state, trend charts for packet loss, bandwidth utilization, and latency.</span><span class="sxs-lookup"><span data-stu-id="534f8-149">You can select a circuit and view its health state, trend charts for packet loss, bandwidth utilization, and latency.</span></span> <span data-ttu-id="534f8-150">The charts are interactive.</span><span class="sxs-lookup"><span data-stu-id="534f8-150">The charts are interactive.</span></span> <span data-ttu-id="534f8-151">You can select a custom time window for plotting the charts.</span><span class="sxs-lookup"><span data-stu-id="534f8-151">You can select a custom time window for plotting the charts.</span></span> <span data-ttu-id="534f8-152">Drag the mouse over an area on the chart to zoom in and see fine-grained data points.</span><span class="sxs-lookup"><span data-stu-id="534f8-152">Drag the mouse over an area on the chart to zoom in and see fine-grained data points.</span></span> 

![ExpressRoute circuits list](media/log-analytics-network-performance-monitor/expressroute-circuits.png) 

### <a name="trends-of-loss-latency-and-throughput"></a><span data-ttu-id="534f8-154">Trends of loss, latency, and throughput</span><span class="sxs-lookup"><span data-stu-id="534f8-154">Trends of loss, latency, and throughput</span></span> 

<span data-ttu-id="534f8-155">The bandwidth utilization, latency, and loss charts are interactive.</span><span class="sxs-lookup"><span data-stu-id="534f8-155">The bandwidth utilization, latency, and loss charts are interactive.</span></span> <span data-ttu-id="534f8-156">You can zoom in to any section of these charts by using mouse controls.</span><span class="sxs-lookup"><span data-stu-id="534f8-156">You can zoom in to any section of these charts by using mouse controls.</span></span> <span data-ttu-id="534f8-157">You also can see the bandwidth, latency, and loss data for other intervals.</span><span class="sxs-lookup"><span data-stu-id="534f8-157">You also can see the bandwidth, latency, and loss data for other intervals.</span></span> <span data-ttu-id="534f8-158">In the upper left under the **Actions** button, select **Date/Time**.</span><span class="sxs-lookup"><span data-stu-id="534f8-158">In the upper left under the **Actions** button, select **Date/Time**.</span></span> 

![ExpressRoute latency](media/log-analytics-network-performance-monitor/expressroute-latency.png) 

### <a name="peerings-list"></a><span data-ttu-id="534f8-160">Peerings list</span><span class="sxs-lookup"><span data-stu-id="534f8-160">Peerings list</span></span> 

<span data-ttu-id="534f8-161">To bring up a list of all connections to virtual networks over private peering, select the **Private Peerings** tile on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="534f8-161">To bring up a list of all connections to virtual networks over private peering, select the **Private Peerings** tile on the dashboard.</span></span> <span data-ttu-id="534f8-162">Here, you can select a virtual network connection and view its health state, trend charts for packet loss, bandwidth utilization, and latency.</span><span class="sxs-lookup"><span data-stu-id="534f8-162">Here, you can select a virtual network connection and view its health state, trend charts for packet loss, bandwidth utilization, and latency.</span></span> 

![ExpressRoute peerings](media/log-analytics-network-performance-monitor/expressroute-peerings.png) 

### <a name="circuit-topology"></a><span data-ttu-id="534f8-164">Circuit topology</span><span class="sxs-lookup"><span data-stu-id="534f8-164">Circuit topology</span></span> 

<span data-ttu-id="534f8-165">To view circuit topology, select the **Topology** tile.</span><span class="sxs-lookup"><span data-stu-id="534f8-165">To view circuit topology, select the **Topology** tile.</span></span> <span data-ttu-id="534f8-166">This action takes you to the topology view of the selected circuit or peering.</span><span class="sxs-lookup"><span data-stu-id="534f8-166">This action takes you to the topology view of the selected circuit or peering.</span></span> <span data-ttu-id="534f8-167">The topology diagram provides the latency for each segment on the network, and each layer 3 hop is represented by a node of the diagram.</span><span class="sxs-lookup"><span data-stu-id="534f8-167">The topology diagram provides the latency for each segment on the network, and each layer 3 hop is represented by a node of the diagram.</span></span> <span data-ttu-id="534f8-168">Selecting a hop reveals more details about the hop.</span><span class="sxs-lookup"><span data-stu-id="534f8-168">Selecting a hop reveals more details about the hop.</span></span> <span data-ttu-id="534f8-169">To increase the level of visibility to include on-premises hops, move the slider bar under **FILTERS**.</span><span class="sxs-lookup"><span data-stu-id="534f8-169">To increase the level of visibility to include on-premises hops, move the slider bar under **FILTERS**.</span></span> <span data-ttu-id="534f8-170">Moving the slider bar to the left or right increases or decreases the number of hops in the topology graph.</span><span class="sxs-lookup"><span data-stu-id="534f8-170">Moving the slider bar to the left or right increases or decreases the number of hops in the topology graph.</span></span> <span data-ttu-id="534f8-171">The latency across each segment is visible, which allows for faster isolation of high-latency segments on your network.</span><span class="sxs-lookup"><span data-stu-id="534f8-171">The latency across each segment is visible, which allows for faster isolation of high-latency segments on your network.</span></span> 

![ExpressRoute topology](media/log-analytics-network-performance-monitor/expressroute-topology.png)

### <a name="detailed-topology-view-of-a-circuit"></a><span data-ttu-id="534f8-173">Detailed topology view of a circuit</span><span class="sxs-lookup"><span data-stu-id="534f8-173">Detailed topology view of a circuit</span></span> 

<span data-ttu-id="534f8-174">This view shows virtual network connections.</span><span class="sxs-lookup"><span data-stu-id="534f8-174">This view shows virtual network connections.</span></span> 

![ExpressRoute virtual network connections](media/log-analytics-network-performance-monitor/expressroute-vnet.png)
 

### <a name="diagnostics"></a><span data-ttu-id="534f8-176">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="534f8-176">Diagnostics</span></span> 

<span data-ttu-id="534f8-177">Network Performance Monitor helps you diagnose several circuit connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="534f8-177">Network Performance Monitor helps you diagnose several circuit connectivity issues.</span></span> <span data-ttu-id="534f8-178">Some of the issues are listed here.</span><span class="sxs-lookup"><span data-stu-id="534f8-178">Some of the issues are listed here.</span></span> 

<span data-ttu-id="534f8-179">**Circuit is down.**</span><span class="sxs-lookup"><span data-stu-id="534f8-179">**Circuit is down.**</span></span> <span data-ttu-id="534f8-180">Network Performance Monitor notifies you as soon as the connectivity between your on-premises resources and Azure virtual networks is lost.</span><span class="sxs-lookup"><span data-stu-id="534f8-180">Network Performance Monitor notifies you as soon as the connectivity between your on-premises resources and Azure virtual networks is lost.</span></span> <span data-ttu-id="534f8-181">This notification helps you take proactive action before you receive user escalations and reduce downtime.</span><span class="sxs-lookup"><span data-stu-id="534f8-181">This notification helps you take proactive action before you receive user escalations and reduce downtime.</span></span>

![ExpressRoute circuit is down](media/log-analytics-network-performance-monitor/expressroute-circuit-down.png)
 

<span data-ttu-id="534f8-183">**Traffic not flowing through intended circuit.**</span><span class="sxs-lookup"><span data-stu-id="534f8-183">**Traffic not flowing through intended circuit.**</span></span> <span data-ttu-id="534f8-184">Network Performance Monitor notifies you whenever traffic isn't flowing through the intended ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="534f8-184">Network Performance Monitor notifies you whenever traffic isn't flowing through the intended ExpressRoute circuit.</span></span> <span data-ttu-id="534f8-185">This issue can happen if the circuit is down and traffic is flowing through the backup route.</span><span class="sxs-lookup"><span data-stu-id="534f8-185">This issue can happen if the circuit is down and traffic is flowing through the backup route.</span></span> <span data-ttu-id="534f8-186">It also can happen if there's a routing issue.</span><span class="sxs-lookup"><span data-stu-id="534f8-186">It also can happen if there's a routing issue.</span></span> <span data-ttu-id="534f8-187">This information helps you proactively manage any configuration issues in your routing policies and make sure that the most optimal and secure route is used.</span><span class="sxs-lookup"><span data-stu-id="534f8-187">This information helps you proactively manage any configuration issues in your routing policies and make sure that the most optimal and secure route is used.</span></span> 

 

<span data-ttu-id="534f8-188">**Traffic not flowing through primary circuit.**</span><span class="sxs-lookup"><span data-stu-id="534f8-188">**Traffic not flowing through primary circuit.**</span></span> <span data-ttu-id="534f8-189">Network Performance Monitor notifies you when traffic is flowing through the secondary ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="534f8-189">Network Performance Monitor notifies you when traffic is flowing through the secondary ExpressRoute circuit.</span></span> <span data-ttu-id="534f8-190">Even though you won't experience any connectivity issues in this case, proactively troubleshooting the issues with the primary circuit makes you better prepared.</span><span class="sxs-lookup"><span data-stu-id="534f8-190">Even though you won't experience any connectivity issues in this case, proactively troubleshooting the issues with the primary circuit makes you better prepared.</span></span> 

 
![ExpressRoute traffic flow](media/log-analytics-network-performance-monitor/expressroute-traffic-flow.png)


<span data-ttu-id="534f8-192">**Degradation due to peak utilization.**</span><span class="sxs-lookup"><span data-stu-id="534f8-192">**Degradation due to peak utilization.**</span></span> <span data-ttu-id="534f8-193">You can correlate the bandwidth utilization trend with the latency trend to identify whether the Azure workload degradation is due to a peak in bandwidth utilization or not.</span><span class="sxs-lookup"><span data-stu-id="534f8-193">You can correlate the bandwidth utilization trend with the latency trend to identify whether the Azure workload degradation is due to a peak in bandwidth utilization or not.</span></span> <span data-ttu-id="534f8-194">Then you can take action accordingly.</span><span class="sxs-lookup"><span data-stu-id="534f8-194">Then you can take action accordingly.</span></span>

![ExpressRoute bandwidth utilization](media/log-analytics-network-performance-monitor/expressroute-peak-utilization.png)

 

## <a name="next-steps"></a><span data-ttu-id="534f8-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="534f8-196">Next steps</span></span>
<span data-ttu-id="534f8-197">[Search logs](log-analytics-log-searches.md) to view detailed network performance data records.</span><span class="sxs-lookup"><span data-stu-id="534f8-197">[Search logs](log-analytics-log-searches.md) to view detailed network performance data records.</span></span>
