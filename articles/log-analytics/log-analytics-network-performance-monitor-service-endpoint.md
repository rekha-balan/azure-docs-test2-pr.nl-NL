---
title: Network Performance Monitor solution in Azure Log Analytics | Microsoft Docs
description: Use the Service Connectivity Monitor capability in Network Performance Monitor to monitor network connectivity to any endpoint that has an open TCP port.
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
ms.openlocfilehash: 3c9352e8e4aee7817b1195c15f74503e86e597ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868799"
---
# <a name="service-connectivity-monitor"></a><span data-ttu-id="d36fd-103">Service Connectivity Monitor</span><span class="sxs-lookup"><span data-stu-id="d36fd-103">Service Connectivity Monitor</span></span>

<span data-ttu-id="d36fd-104">You can use the Service Connectivity Monitor capability in [Network Performance Monitor](log-analytics-network-performance-monitor.md) to monitor network connectivity to any endpoint that has an open TCP port.</span><span class="sxs-lookup"><span data-stu-id="d36fd-104">You can use the Service Connectivity Monitor capability in [Network Performance Monitor](log-analytics-network-performance-monitor.md) to monitor network connectivity to any endpoint that has an open TCP port.</span></span> <span data-ttu-id="d36fd-105">Such endpoints include websites, SaaS applications, PaaS applications, and SQL databases.</span><span class="sxs-lookup"><span data-stu-id="d36fd-105">Such endpoints include websites, SaaS applications, PaaS applications, and SQL databases.</span></span> 

<span data-ttu-id="d36fd-106">You can perform the following functions with Service Connectivity Monitor:</span><span class="sxs-lookup"><span data-stu-id="d36fd-106">You can perform the following functions with Service Connectivity Monitor:</span></span> 

- <span data-ttu-id="d36fd-107">Monitor the network connectivity to your applications and network services from multiple branch offices or locations.</span><span class="sxs-lookup"><span data-stu-id="d36fd-107">Monitor the network connectivity to your applications and network services from multiple branch offices or locations.</span></span> <span data-ttu-id="d36fd-108">Applications and network services include Office 365, Dynamics CRM, internal line-of-business applications, and SQL databases.</span><span class="sxs-lookup"><span data-stu-id="d36fd-108">Applications and network services include Office 365, Dynamics CRM, internal line-of-business applications, and SQL databases.</span></span>
- <span data-ttu-id="d36fd-109">Use built-in tests to monitor network connectivity to Office 365 and Dynamics 365 endpoints.</span><span class="sxs-lookup"><span data-stu-id="d36fd-109">Use built-in tests to monitor network connectivity to Office 365 and Dynamics 365 endpoints.</span></span> 
- <span data-ttu-id="d36fd-110">Determine the response time, network latency, and packet loss experienced when connecting to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="d36fd-110">Determine the response time, network latency, and packet loss experienced when connecting to the endpoint.</span></span>
- <span data-ttu-id="d36fd-111">Determine whether poor application performance is because of the network or because of some issue on the application provider's end.</span><span class="sxs-lookup"><span data-stu-id="d36fd-111">Determine whether poor application performance is because of the network or because of some issue on the application provider's end.</span></span>
- <span data-ttu-id="d36fd-112">Identify hot spots on the network that might be causing poor application performance by viewing the latency contributed by each hop on a topology map.</span><span class="sxs-lookup"><span data-stu-id="d36fd-112">Identify hot spots on the network that might be causing poor application performance by viewing the latency contributed by each hop on a topology map.</span></span>


![Service Connectivity Monitor](media/log-analytics-network-performance-monitor/service-endpoint-intro.png)


## <a name="configuration"></a><span data-ttu-id="d36fd-114">Configuration</span><span class="sxs-lookup"><span data-stu-id="d36fd-114">Configuration</span></span> 
<span data-ttu-id="d36fd-115">To open the configuration for Network Performance Monitor, open the [Network Performance Monitor solution](log-analytics-network-performance-monitor.md) and select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d36fd-115">To open the configuration for Network Performance Monitor, open the [Network Performance Monitor solution](log-analytics-network-performance-monitor.md) and select **Configure**.</span></span>

![Configure Network Performance Monitor](media/log-analytics-network-performance-monitor/npm-configure-button.png)


### <a name="configure-operations-management-suite-agents-for-monitoring"></a><span data-ttu-id="d36fd-117">Configure Operations Management Suite agents for monitoring</span><span class="sxs-lookup"><span data-stu-id="d36fd-117">Configure Operations Management Suite agents for monitoring</span></span>
<span data-ttu-id="d36fd-118">Enable the following firewall rules on the nodes used for monitoring so that the solution can discover the topology from your nodes to the service endpoint:</span><span class="sxs-lookup"><span data-stu-id="d36fd-118">Enable the following firewall rules on the nodes used for monitoring so that the solution can discover the topology from your nodes to the service endpoint:</span></span> 

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow 
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow 
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow 
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow 
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow 
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow 
```

### <a name="create-service-connectivity-monitor-tests"></a><span data-ttu-id="d36fd-119">Create Service Connectivity Monitor tests</span><span class="sxs-lookup"><span data-stu-id="d36fd-119">Create Service Connectivity Monitor tests</span></span> 

<span data-ttu-id="d36fd-120">Start creating your tests to monitor network connectivity to the service endpoints.</span><span class="sxs-lookup"><span data-stu-id="d36fd-120">Start creating your tests to monitor network connectivity to the service endpoints.</span></span>

1. <span data-ttu-id="d36fd-121">Select the **Service Connectivity Monitor** tab.</span><span class="sxs-lookup"><span data-stu-id="d36fd-121">Select the **Service Connectivity Monitor** tab.</span></span>
2. <span data-ttu-id="d36fd-122">Select **Add Test**, and enter the test name and description.</span><span class="sxs-lookup"><span data-stu-id="d36fd-122">Select **Add Test**, and enter the test name and description.</span></span> 
3. <span data-ttu-id="d36fd-123">Select the type of test:</span><span class="sxs-lookup"><span data-stu-id="d36fd-123">Select the type of test:</span></span><br>

    * <span data-ttu-id="d36fd-124">Select **Web** to monitor connectivity to a service that responds to HTTP/S requests, such as outlook.office365.com or bing.com.</span><span class="sxs-lookup"><span data-stu-id="d36fd-124">Select **Web** to monitor connectivity to a service that responds to HTTP/S requests, such as outlook.office365.com or bing.com.</span></span><br>
    * <span data-ttu-id="d36fd-125">Select **Network** to monitor connectivity to a service that responds to TCP requests but doesn't respond to HTTP/S requests, such as a SQL server, FTP server, or SSH port.</span><span class="sxs-lookup"><span data-stu-id="d36fd-125">Select **Network** to monitor connectivity to a service that responds to TCP requests but doesn't respond to HTTP/S requests, such as a SQL server, FTP server, or SSH port.</span></span> 
4. <span data-ttu-id="d36fd-126">If you don't want to perform network measurements, such as network latency, packet loss, and topology discovery, clear the **Perform network measurements** check box.</span><span class="sxs-lookup"><span data-stu-id="d36fd-126">If you don't want to perform network measurements, such as network latency, packet loss, and topology discovery, clear the **Perform network measurements** check box.</span></span> <span data-ttu-id="d36fd-127">Keep it selected to get maximum benefit from the capability.</span><span class="sxs-lookup"><span data-stu-id="d36fd-127">Keep it selected to get maximum benefit from the capability.</span></span> 
5. <span data-ttu-id="d36fd-128">In **Target**, enter the URL/FQDN/IP address to which you want to monitor network connectivity.</span><span class="sxs-lookup"><span data-stu-id="d36fd-128">In **Target**, enter the URL/FQDN/IP address to which you want to monitor network connectivity.</span></span>
6. <span data-ttu-id="d36fd-129">In **Port number**, enter the port number of the target service.</span><span class="sxs-lookup"><span data-stu-id="d36fd-129">In **Port number**, enter the port number of the target service.</span></span> 
7. <span data-ttu-id="d36fd-130">In **Test Frequency**, enter a value for how frequently you want the test to run.</span><span class="sxs-lookup"><span data-stu-id="d36fd-130">In **Test Frequency**, enter a value for how frequently you want the test to run.</span></span> 
8. <span data-ttu-id="d36fd-131">Select the nodes from which you want to monitor the network connectivity to service.</span><span class="sxs-lookup"><span data-stu-id="d36fd-131">Select the nodes from which you want to monitor the network connectivity to service.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="d36fd-132">For Windows server-based nodes, the capability uses TCP-based requests to perform the network measurements.</span><span class="sxs-lookup"><span data-stu-id="d36fd-132">For Windows server-based nodes, the capability uses TCP-based requests to perform the network measurements.</span></span> <span data-ttu-id="d36fd-133">For Windows client-based nodes, the capability uses ICMP-based requests to perform the network measurements.</span><span class="sxs-lookup"><span data-stu-id="d36fd-133">For Windows client-based nodes, the capability uses ICMP-based requests to perform the network measurements.</span></span> <span data-ttu-id="d36fd-134">In some cases, the target application blocks incoming ICMP-based requests when the nodes are Windows client-based.</span><span class="sxs-lookup"><span data-stu-id="d36fd-134">In some cases, the target application blocks incoming ICMP-based requests when the nodes are Windows client-based.</span></span> <span data-ttu-id="d36fd-135">The solution is unable to perform network measurements.</span><span class="sxs-lookup"><span data-stu-id="d36fd-135">The solution is unable to perform network measurements.</span></span> <span data-ttu-id="d36fd-136">We recommend that you use Windows server-based nodes in such cases.</span><span class="sxs-lookup"><span data-stu-id="d36fd-136">We recommend that you use Windows server-based nodes in such cases.</span></span> 

9. <span data-ttu-id="d36fd-137">If you don't want to create health events for the items you select, clear **Enable Health Monitoring in the targets covered by this test**.</span><span class="sxs-lookup"><span data-stu-id="d36fd-137">If you don't want to create health events for the items you select, clear **Enable Health Monitoring in the targets covered by this test**.</span></span> 
10. <span data-ttu-id="d36fd-138">Choose monitoring conditions.</span><span class="sxs-lookup"><span data-stu-id="d36fd-138">Choose monitoring conditions.</span></span> <span data-ttu-id="d36fd-139">You can set custom thresholds for health-event generation by entering threshold values.</span><span class="sxs-lookup"><span data-stu-id="d36fd-139">You can set custom thresholds for health-event generation by entering threshold values.</span></span> <span data-ttu-id="d36fd-140">Whenever the value of the condition goes above its selected threshold for the selected network or subnetwork pair, a health event is generated.</span><span class="sxs-lookup"><span data-stu-id="d36fd-140">Whenever the value of the condition goes above its selected threshold for the selected network or subnetwork pair, a health event is generated.</span></span> 
11. <span data-ttu-id="d36fd-141">Select **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="d36fd-141">Select **Save** to save the configuration.</span></span> 

    ![Service Connectivity Monitor test configurations](media/log-analytics-network-performance-monitor/service-endpoint-configuration.png)



## <a name="walkthrough"></a><span data-ttu-id="d36fd-143">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="d36fd-143">Walkthrough</span></span> 

<span data-ttu-id="d36fd-144">Go to the Network Performance Monitor dashboard view.</span><span class="sxs-lookup"><span data-stu-id="d36fd-144">Go to the Network Performance Monitor dashboard view.</span></span> <span data-ttu-id="d36fd-145">To get a summary of the health of the different tests you created, look at the **Service Connectivity Monitor** page.</span><span class="sxs-lookup"><span data-stu-id="d36fd-145">To get a summary of the health of the different tests you created, look at the **Service Connectivity Monitor** page.</span></span> 

![Service Connectivity Monitor page](media/log-analytics-network-performance-monitor/service-endpoint-blade.png)

<span data-ttu-id="d36fd-147">Select the tile to view the details of the tests on the **Tests** page.</span><span class="sxs-lookup"><span data-stu-id="d36fd-147">Select the tile to view the details of the tests on the **Tests** page.</span></span> <span data-ttu-id="d36fd-148">In the table on the left, you can view the point-in-time health and value of the service response time, network latency, and packet loss for all the tests.</span><span class="sxs-lookup"><span data-stu-id="d36fd-148">In the table on the left, you can view the point-in-time health and value of the service response time, network latency, and packet loss for all the tests.</span></span> <span data-ttu-id="d36fd-149">Use the Network State Recorder control to view the network snapshot at another time in the past.</span><span class="sxs-lookup"><span data-stu-id="d36fd-149">Use the Network State Recorder control to view the network snapshot at another time in the past.</span></span> <span data-ttu-id="d36fd-150">Select the test in the table that you want to investigate.</span><span class="sxs-lookup"><span data-stu-id="d36fd-150">Select the test in the table that you want to investigate.</span></span> <span data-ttu-id="d36fd-151">In the charts in the pane on the right, you can view the historical trend of the loss, latency, and response time values.</span><span class="sxs-lookup"><span data-stu-id="d36fd-151">In the charts in the pane on the right, you can view the historical trend of the loss, latency, and response time values.</span></span> <span data-ttu-id="d36fd-152">Select the **Test Details** link to view the performance from each node.</span><span class="sxs-lookup"><span data-stu-id="d36fd-152">Select the **Test Details** link to view the performance from each node.</span></span>

![Service Connectivity Monitor tests](media/log-analytics-network-performance-monitor/service-endpoint-tests.png)

<span data-ttu-id="d36fd-154">In the **Test Nodes** view, you can observe the network connectivity from each node.</span><span class="sxs-lookup"><span data-stu-id="d36fd-154">In the **Test Nodes** view, you can observe the network connectivity from each node.</span></span> <span data-ttu-id="d36fd-155">Select the node that has performance degradation.</span><span class="sxs-lookup"><span data-stu-id="d36fd-155">Select the node that has performance degradation.</span></span> <span data-ttu-id="d36fd-156">This is the node where the application is observed to be running slow.</span><span class="sxs-lookup"><span data-stu-id="d36fd-156">This is the node where the application is observed to be running slow.</span></span>

<span data-ttu-id="d36fd-157">Determine whether poor application performance is because of the network or an issue on the application provider's end by observing the correlation between the response time of the application and the network latency.</span><span class="sxs-lookup"><span data-stu-id="d36fd-157">Determine whether poor application performance is because of the network or an issue on the application provider's end by observing the correlation between the response time of the application and the network latency.</span></span> 

* <span data-ttu-id="d36fd-158">**Application issue:** A spike in the response time but consistency in the network latency suggests that the network is working fine and the problem might be due to an issue on the application end.</span><span class="sxs-lookup"><span data-stu-id="d36fd-158">**Application issue:** A spike in the response time but consistency in the network latency suggests that the network is working fine and the problem might be due to an issue on the application end.</span></span> 

    ![Service Connectivity Monitor application issue](media/log-analytics-network-performance-monitor/service-endpoint-application-issue.png)

* <span data-ttu-id="d36fd-160">**Network issue:** A spike in response time accompanied with a corresponding spike in network latency suggests that the increase in response time might be due to an increase in network latency.</span><span class="sxs-lookup"><span data-stu-id="d36fd-160">**Network issue:** A spike in response time accompanied with a corresponding spike in network latency suggests that the increase in response time might be due to an increase in network latency.</span></span> 

    ![Service Connectivity Monitor network issue](media/log-analytics-network-performance-monitor/service-endpoint-network-issue.png)

<span data-ttu-id="d36fd-162">After you determine that the problem is because of the network, select the **Topology** view link to identify the troublesome hop on the topology map.</span><span class="sxs-lookup"><span data-stu-id="d36fd-162">After you determine that the problem is because of the network, select the **Topology** view link to identify the troublesome hop on the topology map.</span></span> <span data-ttu-id="d36fd-163">An example is shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="d36fd-163">An example is shown in the following image.</span></span> <span data-ttu-id="d36fd-164">Out of the 105-ms total latency between the node and the application endpoint, 96 ms is because of the hop marked in red.</span><span class="sxs-lookup"><span data-stu-id="d36fd-164">Out of the 105-ms total latency between the node and the application endpoint, 96 ms is because of the hop marked in red.</span></span> <span data-ttu-id="d36fd-165">After you identify the troublesome hop, you can take corrective action.</span><span class="sxs-lookup"><span data-stu-id="d36fd-165">After you identify the troublesome hop, you can take corrective action.</span></span> 

![Service Connectivity Monitor tests](media/log-analytics-network-performance-monitor/service-endpoint-topology.png)

## <a name="diagnostics"></a><span data-ttu-id="d36fd-167">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d36fd-167">Diagnostics</span></span> 

<span data-ttu-id="d36fd-168">If you observe an abnormality, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d36fd-168">If you observe an abnormality, follow these steps:</span></span>

* <span data-ttu-id="d36fd-169">If the service response time, network loss, and latency are shown as NA, one or more of the following reasons might be the cause:</span><span class="sxs-lookup"><span data-stu-id="d36fd-169">If the service response time, network loss, and latency are shown as NA, one or more of the following reasons might be the cause:</span></span>

    - <span data-ttu-id="d36fd-170">The application is down.</span><span class="sxs-lookup"><span data-stu-id="d36fd-170">The application is down.</span></span>
    - <span data-ttu-id="d36fd-171">The node used for checking network connectivity to the service is down.</span><span class="sxs-lookup"><span data-stu-id="d36fd-171">The node used for checking network connectivity to the service is down.</span></span>
    - <span data-ttu-id="d36fd-172">The target entered in the test configuration is incorrect.</span><span class="sxs-lookup"><span data-stu-id="d36fd-172">The target entered in the test configuration is incorrect.</span></span>
    - <span data-ttu-id="d36fd-173">The node doesn't have any network connectivity.</span><span class="sxs-lookup"><span data-stu-id="d36fd-173">The node doesn't have any network connectivity.</span></span>

* <span data-ttu-id="d36fd-174">If a valid service response time is shown but network loss as well as latency are shown as NA, one or more of the following reasons might be the cause:</span><span class="sxs-lookup"><span data-stu-id="d36fd-174">If a valid service response time is shown but network loss as well as latency are shown as NA, one or more of the following reasons might be the cause:</span></span>

    - <span data-ttu-id="d36fd-175">If the node used for checking network connectivity to the service is a Windows client machine, either the target service is blocking ICMP requests or a network firewall is blocking ICMP requests that originate from the node.</span><span class="sxs-lookup"><span data-stu-id="d36fd-175">If the node used for checking network connectivity to the service is a Windows client machine, either the target service is blocking ICMP requests or a network firewall is blocking ICMP requests that originate from the node.</span></span>
    - <span data-ttu-id="d36fd-176">The **Perform network measurements** check box is blank in the test configuration.</span><span class="sxs-lookup"><span data-stu-id="d36fd-176">The **Perform network measurements** check box is blank in the test configuration.</span></span> 

* <span data-ttu-id="d36fd-177">If the service response time is NA but network loss as well as latency are valid, the target service might not be a web application.</span><span class="sxs-lookup"><span data-stu-id="d36fd-177">If the service response time is NA but network loss as well as latency are valid, the target service might not be a web application.</span></span> <span data-ttu-id="d36fd-178">Edit the test configuration, and choose the test type as **Network** instead of **Web**.</span><span class="sxs-lookup"><span data-stu-id="d36fd-178">Edit the test configuration, and choose the test type as **Network** instead of **Web**.</span></span> 

* <span data-ttu-id="d36fd-179">If the application is running slow, determine whether poor application performance is because of the network or an issue on the application provider's end.</span><span class="sxs-lookup"><span data-stu-id="d36fd-179">If the application is running slow, determine whether poor application performance is because of the network or an issue on the application provider's end.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d36fd-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="d36fd-180">Next steps</span></span>
<span data-ttu-id="d36fd-181">[Search logs](log-analytics-log-searches.md) to view detailed network performance data records.</span><span class="sxs-lookup"><span data-stu-id="d36fd-181">[Search logs](log-analytics-log-searches.md) to view detailed network performance data records.</span></span>
