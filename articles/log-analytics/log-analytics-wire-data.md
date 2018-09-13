---
title: Wire Data solution in Log Analytics | Microsoft Docs
description: Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager and Windows-connected agents. Network data is combined with your log data to help you correlate data.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 1cd052b0f66b1e785beeeae564caa22aa02c5b5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805121"
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="73d37-104">Wire Data 2.0 (Preview) solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="73d37-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Wire Data symbol](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="73d37-106">Wire data is consolidated network and performance data collected from Windows-connected and Linux-connected computers with the OMS agent, including those monitored by Operations Manager in your environment.</span><span class="sxs-lookup"><span data-stu-id="73d37-106">Wire data is consolidated network and performance data collected from Windows-connected and Linux-connected computers with the OMS agent, including those monitored by Operations Manager in your environment.</span></span> <span data-ttu-id="73d37-107">Network data is combined with your other log data to help you correlate data.</span><span class="sxs-lookup"><span data-stu-id="73d37-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="73d37-108">In addition to the OMS agent, the Wire Data solution uses Microsoft Dependency Agents that you install on computers in your IT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="73d37-108">In addition to the OMS agent, the Wire Data solution uses Microsoft Dependency Agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="73d37-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span><span class="sxs-lookup"><span data-stu-id="73d37-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="73d37-110">Data is then sent to Log Analytics using agents.</span><span class="sxs-lookup"><span data-stu-id="73d37-110">Data is then sent to Log Analytics using agents.</span></span>  

> [!NOTE]
> <span data-ttu-id="73d37-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span><span class="sxs-lookup"><span data-stu-id="73d37-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="73d37-112">If you have the original Wire Data solution enabled, you can continue to use it.</span><span class="sxs-lookup"><span data-stu-id="73d37-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="73d37-113">However, to use Wire Data 2.0, you must first remove the original version.</span><span class="sxs-lookup"><span data-stu-id="73d37-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="73d37-114">By default, Log Analytics logs data for CPU, memory, disk, and network performance data from counters built into Windows and Linux, as well as other performance counters that you can specify.</span><span class="sxs-lookup"><span data-stu-id="73d37-114">By default, Log Analytics logs data for CPU, memory, disk, and network performance data from counters built into Windows and Linux, as well as other performance counters that you can specify.</span></span> <span data-ttu-id="73d37-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span><span class="sxs-lookup"><span data-stu-id="73d37-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span>  <span data-ttu-id="73d37-116">Wire Data looks at network data at the application level, not down at the TCP transport layer.</span><span class="sxs-lookup"><span data-stu-id="73d37-116">Wire Data looks at network data at the application level, not down at the TCP transport layer.</span></span>  <span data-ttu-id="73d37-117">The solution doesn't look at individual ACKs and SYNs.</span><span class="sxs-lookup"><span data-stu-id="73d37-117">The solution doesn't look at individual ACKs and SYNs.</span></span>  <span data-ttu-id="73d37-118">Once the handshake is completed, it is considered a live connection and marked as Connected.</span><span class="sxs-lookup"><span data-stu-id="73d37-118">Once the handshake is completed, it is considered a live connection and marked as Connected.</span></span> <span data-ttu-id="73d37-119">That connection stays live as long as both sides agree the socket is open and data can pass back and forth.</span><span class="sxs-lookup"><span data-stu-id="73d37-119">That connection stays live as long as both sides agree the socket is open and data can pass back and forth.</span></span>  <span data-ttu-id="73d37-120">Once either sides closes the connection, it is marked as Disconnected.</span><span class="sxs-lookup"><span data-stu-id="73d37-120">Once either sides closes the connection, it is marked as Disconnected.</span></span>  <span data-ttu-id="73d37-121">Therefore, it only counts the bandwidth of successfully completed packets, it doesn't report on resends or failed packets.</span><span class="sxs-lookup"><span data-stu-id="73d37-121">Therefore, it only counts the bandwidth of successfully completed packets, it doesn't report on resends or failed packets.</span></span>

<span data-ttu-id="73d37-122">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span><span class="sxs-lookup"><span data-stu-id="73d37-122">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="73d37-123">Some of the types of built-in Log search queries include:</span><span class="sxs-lookup"><span data-stu-id="73d37-123">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="73d37-124">Agents that provide wire data</span><span class="sxs-lookup"><span data-stu-id="73d37-124">Agents that provide wire data</span></span>
- <span data-ttu-id="73d37-125">IP address of agents providing wire data</span><span class="sxs-lookup"><span data-stu-id="73d37-125">IP address of agents providing wire data</span></span>
- <span data-ttu-id="73d37-126">Outbound communications by IP addresses</span><span class="sxs-lookup"><span data-stu-id="73d37-126">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="73d37-127">Number of bytes sent by application protocols</span><span class="sxs-lookup"><span data-stu-id="73d37-127">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="73d37-128">Number of bytes sent by an application service</span><span class="sxs-lookup"><span data-stu-id="73d37-128">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="73d37-129">Bytes received by different protocols</span><span class="sxs-lookup"><span data-stu-id="73d37-129">Bytes received by different protocols</span></span>
- <span data-ttu-id="73d37-130">Total bytes sent and received by IP version</span><span class="sxs-lookup"><span data-stu-id="73d37-130">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="73d37-131">Average latency for connections that were measured reliably</span><span class="sxs-lookup"><span data-stu-id="73d37-131">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="73d37-132">Computer processes that initiated or received network traffic</span><span class="sxs-lookup"><span data-stu-id="73d37-132">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="73d37-133">Amount of network traffic for a process</span><span class="sxs-lookup"><span data-stu-id="73d37-133">Amount of network traffic for a process</span></span>

<span data-ttu-id="73d37-134">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span><span class="sxs-lookup"><span data-stu-id="73d37-134">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="73d37-135">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span><span class="sxs-lookup"><span data-stu-id="73d37-135">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="73d37-136">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="73d37-136">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="73d37-137">Wire data in Log Analytics is not a full capture of network data.</span><span class="sxs-lookup"><span data-stu-id="73d37-137">Wire data in Log Analytics is not a full capture of network data.</span></span>  <span data-ttu-id="73d37-138">It is not intended for deep packet-level troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="73d37-138">It is not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="73d37-139">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span><span class="sxs-lookup"><span data-stu-id="73d37-139">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="73d37-140">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span><span class="sxs-lookup"><span data-stu-id="73d37-140">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="73d37-141">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span><span class="sxs-lookup"><span data-stu-id="73d37-141">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="73d37-142">Connected sources</span><span class="sxs-lookup"><span data-stu-id="73d37-142">Connected sources</span></span>

<span data-ttu-id="73d37-143">Wire Data gets its data from the Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-143">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="73d37-144">The Dependency Agent depends on the Log Analytics agent for its connections to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="73d37-144">The Dependency Agent depends on the Log Analytics agent for its connections to Log Analytics.</span></span> <span data-ttu-id="73d37-145">This means that a server must have the Log Analytics agent installed and configured with the Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-145">This means that a server must have the Log Analytics agent installed and configured with the Dependency agent.</span></span> <span data-ttu-id="73d37-146">The following table describes the connected sources that the Wire Data solution supports.</span><span class="sxs-lookup"><span data-stu-id="73d37-146">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="73d37-147">**Connected source**</span><span class="sxs-lookup"><span data-stu-id="73d37-147">**Connected source**</span></span> | <span data-ttu-id="73d37-148">**Supported**</span><span class="sxs-lookup"><span data-stu-id="73d37-148">**Supported**</span></span> | <span data-ttu-id="73d37-149">**Description**</span><span class="sxs-lookup"><span data-stu-id="73d37-149">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73d37-150">Windows agents</span><span class="sxs-lookup"><span data-stu-id="73d37-150">Windows agents</span></span> | <span data-ttu-id="73d37-151">Yes</span><span class="sxs-lookup"><span data-stu-id="73d37-151">Yes</span></span> | <span data-ttu-id="73d37-152">Wire Data analyzes and collects data from Windows agent computers.</span><span class="sxs-lookup"><span data-stu-id="73d37-152">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="73d37-153">In addition to the [Log Analytics agent for Windows](log-analytics-windows-agent.md), Windows agents require the Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-153">In addition to the [Log Analytics agent for Windows](log-analytics-windows-agent.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="73d37-154">See the [supported operating systems](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) for a complete list of operating system versions.</span><span class="sxs-lookup"><span data-stu-id="73d37-154">See the [supported operating systems](../monitoring/monitoring-service-map-configure.md#supported-windows-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="73d37-155">Linux agents</span><span class="sxs-lookup"><span data-stu-id="73d37-155">Linux agents</span></span> | <span data-ttu-id="73d37-156">Yes</span><span class="sxs-lookup"><span data-stu-id="73d37-156">Yes</span></span> | <span data-ttu-id="73d37-157">Wire Data analyzes and collects data from Linux agent computers.</span><span class="sxs-lookup"><span data-stu-id="73d37-157">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="73d37-158">In addition to the [Log Analytics agent for Linux](log-analytics-quick-collect-linux-computer.md), Linux agents require the Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-158">In addition to the [Log Analytics agent for Linux](log-analytics-quick-collect-linux-computer.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="73d37-159">See the [supported operating systems](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) for a complete list of operating system versions.</span><span class="sxs-lookup"><span data-stu-id="73d37-159">See the [supported operating systems](../monitoring/monitoring-service-map-configure.md#supported-linux-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="73d37-160">System Center Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="73d37-160">System Center Operations Manager management group</span></span> | <span data-ttu-id="73d37-161">Yes</span><span class="sxs-lookup"><span data-stu-id="73d37-161">Yes</span></span> | <span data-ttu-id="73d37-162">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="73d37-162">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="73d37-163">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span><span class="sxs-lookup"><span data-stu-id="73d37-163">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> |
| <span data-ttu-id="73d37-164">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="73d37-164">Azure storage account</span></span> | <span data-ttu-id="73d37-165">No</span><span class="sxs-lookup"><span data-stu-id="73d37-165">No</span></span> | <span data-ttu-id="73d37-166">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="73d37-166">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="73d37-167">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span><span class="sxs-lookup"><span data-stu-id="73d37-167">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="73d37-168">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics agent, MMA, or Direct Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-168">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="73d37-169">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span><span class="sxs-lookup"><span data-stu-id="73d37-169">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="73d37-170">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span><span class="sxs-lookup"><span data-stu-id="73d37-170">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="73d37-171">On Linux, the Log Analytics agent for Linux gathers and sends data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="73d37-171">On Linux, the Log Analytics agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="73d37-172">You can use Wire Data on servers with agents directly connected to Log Analytics, or on servers that are connecting to Log Analytics via System Center Operations Manager management groups.</span><span class="sxs-lookup"><span data-stu-id="73d37-172">You can use Wire Data on servers with agents directly connected to Log Analytics, or on servers that are connecting to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="73d37-173">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span><span class="sxs-lookup"><span data-stu-id="73d37-173">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="73d37-174">The data in Wire Data is always transmitted by the Log Analytics agent to Log Analytics, either directly or through the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="73d37-174">The data in Wire Data is always transmitted by the Log Analytics agent to Log Analytics, either directly or through the OMS Gateway.</span></span>

![agent diagram](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="73d37-176">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="73d37-176">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="73d37-177">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="73d37-177">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="73d37-178">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span><span class="sxs-lookup"><span data-stu-id="73d37-178">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="73d37-179">If your Windows or Linux computers cannot directly connect to the service, you need to configure the Log Analytics agent to connect to Log Analytics using the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="73d37-179">If your Windows or Linux computers cannot directly connect to the service, you need to configure the Log Analytics agent to connect to Log Analytics using the OMS Gateway.</span></span> <span data-ttu-id="73d37-180">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="73d37-180">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73d37-181">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="73d37-181">Prerequisites</span></span>

- <span data-ttu-id="73d37-182">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span><span class="sxs-lookup"><span data-stu-id="73d37-182">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="73d37-183">If you're using the previous version of the Wire Data solution, you must first remove it.</span><span class="sxs-lookup"><span data-stu-id="73d37-183">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="73d37-184">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span><span class="sxs-lookup"><span data-stu-id="73d37-184">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="73d37-185">Administrator privileges are required to install or uninstall the Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-185">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="73d37-186">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span><span class="sxs-lookup"><span data-stu-id="73d37-186">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="73d37-187">Operating systems</span><span class="sxs-lookup"><span data-stu-id="73d37-187">Operating systems</span></span>

<span data-ttu-id="73d37-188">The following sections list the supported operating systems for the Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-188">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="73d37-189">Wire Data doesn't support 32-bit architectures for any operating system.</span><span class="sxs-lookup"><span data-stu-id="73d37-189">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="73d37-190">Windows Server</span><span class="sxs-lookup"><span data-stu-id="73d37-190">Windows Server</span></span>

- <span data-ttu-id="73d37-191">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="73d37-191">Windows Server 2016</span></span>
- <span data-ttu-id="73d37-192">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="73d37-192">Windows Server 2012 R2</span></span>
- <span data-ttu-id="73d37-193">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="73d37-193">Windows Server 2012</span></span>
- <span data-ttu-id="73d37-194">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="73d37-194">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="73d37-195">Windows desktop</span><span class="sxs-lookup"><span data-stu-id="73d37-195">Windows desktop</span></span>

- <span data-ttu-id="73d37-196">Windows 10</span><span class="sxs-lookup"><span data-stu-id="73d37-196">Windows 10</span></span>
- <span data-ttu-id="73d37-197">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="73d37-197">Windows 8.1</span></span>
- <span data-ttu-id="73d37-198">Windows 8</span><span class="sxs-lookup"><span data-stu-id="73d37-198">Windows 8</span></span>
- <span data-ttu-id="73d37-199">Windows 7</span><span class="sxs-lookup"><span data-stu-id="73d37-199">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="73d37-200">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span><span class="sxs-lookup"><span data-stu-id="73d37-200">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="73d37-201">Only default and SMP Linux kernel releases are supported.</span><span class="sxs-lookup"><span data-stu-id="73d37-201">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="73d37-202">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="73d37-202">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="73d37-203">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span><span class="sxs-lookup"><span data-stu-id="73d37-203">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="73d37-204">Custom kernels, including recompiles of standard kernels, are not supported.</span><span class="sxs-lookup"><span data-stu-id="73d37-204">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="73d37-205">CentOSPlus kernel is not supported.</span><span class="sxs-lookup"><span data-stu-id="73d37-205">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="73d37-206">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span><span class="sxs-lookup"><span data-stu-id="73d37-206">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="73d37-207">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="73d37-207">Red Hat Linux 7</span></span>

| <span data-ttu-id="73d37-208">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-208">**OS version**</span></span> | <span data-ttu-id="73d37-209">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-209">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-210">7.0</span><span class="sxs-lookup"><span data-stu-id="73d37-210">7.0</span></span> | <span data-ttu-id="73d37-211">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="73d37-211">3.10.0-123</span></span> |
| <span data-ttu-id="73d37-212">7.1</span><span class="sxs-lookup"><span data-stu-id="73d37-212">7.1</span></span> | <span data-ttu-id="73d37-213">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="73d37-213">3.10.0-229</span></span> |
| <span data-ttu-id="73d37-214">7.2</span><span class="sxs-lookup"><span data-stu-id="73d37-214">7.2</span></span> | <span data-ttu-id="73d37-215">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="73d37-215">3.10.0-327</span></span> |
| <span data-ttu-id="73d37-216">7.3</span><span class="sxs-lookup"><span data-stu-id="73d37-216">7.3</span></span> | <span data-ttu-id="73d37-217">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="73d37-217">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="73d37-218">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="73d37-218">Red Hat Linux 6</span></span>

| <span data-ttu-id="73d37-219">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-219">**OS version**</span></span> | <span data-ttu-id="73d37-220">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-220">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-221">6.0</span><span class="sxs-lookup"><span data-stu-id="73d37-221">6.0</span></span> | <span data-ttu-id="73d37-222">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="73d37-222">2.6.32-71</span></span> |
| <span data-ttu-id="73d37-223">6.1</span><span class="sxs-lookup"><span data-stu-id="73d37-223">6.1</span></span> | <span data-ttu-id="73d37-224">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="73d37-224">2.6.32-131</span></span> |
| <span data-ttu-id="73d37-225">6.2</span><span class="sxs-lookup"><span data-stu-id="73d37-225">6.2</span></span> | <span data-ttu-id="73d37-226">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="73d37-226">2.6.32-220</span></span> |
| <span data-ttu-id="73d37-227">6.3</span><span class="sxs-lookup"><span data-stu-id="73d37-227">6.3</span></span> | <span data-ttu-id="73d37-228">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="73d37-228">2.6.32-279</span></span> |
| <span data-ttu-id="73d37-229">6.4</span><span class="sxs-lookup"><span data-stu-id="73d37-229">6.4</span></span> | <span data-ttu-id="73d37-230">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="73d37-230">2.6.32-358</span></span> |
| <span data-ttu-id="73d37-231">6.5</span><span class="sxs-lookup"><span data-stu-id="73d37-231">6.5</span></span> | <span data-ttu-id="73d37-232">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="73d37-232">2.6.32-431</span></span> |
| <span data-ttu-id="73d37-233">6.6</span><span class="sxs-lookup"><span data-stu-id="73d37-233">6.6</span></span> | <span data-ttu-id="73d37-234">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="73d37-234">2.6.32-504</span></span> |
| <span data-ttu-id="73d37-235">6.7</span><span class="sxs-lookup"><span data-stu-id="73d37-235">6.7</span></span> | <span data-ttu-id="73d37-236">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="73d37-236">2.6.32-573</span></span> |
| <span data-ttu-id="73d37-237">6.8</span><span class="sxs-lookup"><span data-stu-id="73d37-237">6.8</span></span> | <span data-ttu-id="73d37-238">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="73d37-238">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="73d37-239">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="73d37-239">Red Hat Linux 5</span></span>

| <span data-ttu-id="73d37-240">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-240">**OS version**</span></span> | <span data-ttu-id="73d37-241">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-241">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-242">5.8</span><span class="sxs-lookup"><span data-stu-id="73d37-242">5.8</span></span> | <span data-ttu-id="73d37-243">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="73d37-243">2.6.18-308</span></span> |
| <span data-ttu-id="73d37-244">5.9</span><span class="sxs-lookup"><span data-stu-id="73d37-244">5.9</span></span> | <span data-ttu-id="73d37-245">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="73d37-245">2.6.18-348</span></span> |
| <span data-ttu-id="73d37-246">5.10</span><span class="sxs-lookup"><span data-stu-id="73d37-246">5.10</span></span> | <span data-ttu-id="73d37-247">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="73d37-247">2.6.18-371</span></span> |
| <span data-ttu-id="73d37-248">5.11</span><span class="sxs-lookup"><span data-stu-id="73d37-248">5.11</span></span> | <span data-ttu-id="73d37-249">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="73d37-249">2.6.18-398</span></span> <br> <span data-ttu-id="73d37-250">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="73d37-250">2.6.18-400</span></span> <br><span data-ttu-id="73d37-251">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="73d37-251">2.6.18-402</span></span> <br><span data-ttu-id="73d37-252">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="73d37-252">2.6.18-404</span></span> <br><span data-ttu-id="73d37-253">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="73d37-253">2.6.18-406</span></span> <br> <span data-ttu-id="73d37-254">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="73d37-254">2.6.18-407</span></span> <br> <span data-ttu-id="73d37-255">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="73d37-255">2.6.18-408</span></span> <br> <span data-ttu-id="73d37-256">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="73d37-256">2.6.18-409</span></span> <br> <span data-ttu-id="73d37-257">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="73d37-257">2.6.18-410</span></span> <br> <span data-ttu-id="73d37-258">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="73d37-258">2.6.18-411</span></span> <br> <span data-ttu-id="73d37-259">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="73d37-259">2.6.18-412</span></span> <br> <span data-ttu-id="73d37-260">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="73d37-260">2.6.18-416</span></span> <br> <span data-ttu-id="73d37-261">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="73d37-261">2.6.18-417</span></span> <br> <span data-ttu-id="73d37-262">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="73d37-262">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="73d37-263">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="73d37-263">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="73d37-264">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="73d37-264">Oracle Linux 6</span></span>

| <span data-ttu-id="73d37-265">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-265">**OS version**</span></span> | <span data-ttu-id="73d37-266">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-266">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-267">6.2</span><span class="sxs-lookup"><span data-stu-id="73d37-267">6.2</span></span> | <span data-ttu-id="73d37-268">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="73d37-268">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="73d37-269">6.3</span><span class="sxs-lookup"><span data-stu-id="73d37-269">6.3</span></span> | <span data-ttu-id="73d37-270">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="73d37-270">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="73d37-271">6.4</span><span class="sxs-lookup"><span data-stu-id="73d37-271">6.4</span></span> | <span data-ttu-id="73d37-272">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="73d37-272">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="73d37-273">6.5</span><span class="sxs-lookup"><span data-stu-id="73d37-273">6.5</span></span> | <span data-ttu-id="73d37-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="73d37-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="73d37-275">6.6</span><span class="sxs-lookup"><span data-stu-id="73d37-275">6.6</span></span> | <span data-ttu-id="73d37-276">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="73d37-276">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="73d37-277">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="73d37-277">Oracle Linux 5</span></span>

| <span data-ttu-id="73d37-278">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-278">**OS version**</span></span> | <span data-ttu-id="73d37-279">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-279">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-280">5.8</span><span class="sxs-lookup"><span data-stu-id="73d37-280">5.8</span></span> | <span data-ttu-id="73d37-281">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="73d37-281">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="73d37-282">5.9</span><span class="sxs-lookup"><span data-stu-id="73d37-282">5.9</span></span> | <span data-ttu-id="73d37-283">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="73d37-283">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="73d37-284">5.10</span><span class="sxs-lookup"><span data-stu-id="73d37-284">5.10</span></span> | <span data-ttu-id="73d37-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="73d37-285">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="73d37-286">5.11</span><span class="sxs-lookup"><span data-stu-id="73d37-286">5.11</span></span> | <span data-ttu-id="73d37-287">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="73d37-287">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="73d37-288">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="73d37-288">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="73d37-289">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="73d37-289">SUSE Linux 11</span></span>

| <span data-ttu-id="73d37-290">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-290">**OS version**</span></span> | <span data-ttu-id="73d37-291">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-291">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-292">11</span><span class="sxs-lookup"><span data-stu-id="73d37-292">11</span></span> | <span data-ttu-id="73d37-293">2.6.27</span><span class="sxs-lookup"><span data-stu-id="73d37-293">2.6.27</span></span> |
| <span data-ttu-id="73d37-294">11 SP1</span><span class="sxs-lookup"><span data-stu-id="73d37-294">11 SP1</span></span> | <span data-ttu-id="73d37-295">2.6.32</span><span class="sxs-lookup"><span data-stu-id="73d37-295">2.6.32</span></span> |
| <span data-ttu-id="73d37-296">11 SP2</span><span class="sxs-lookup"><span data-stu-id="73d37-296">11 SP2</span></span> | <span data-ttu-id="73d37-297">3.0.13</span><span class="sxs-lookup"><span data-stu-id="73d37-297">3.0.13</span></span> |
| <span data-ttu-id="73d37-298">11 SP3</span><span class="sxs-lookup"><span data-stu-id="73d37-298">11 SP3</span></span> | <span data-ttu-id="73d37-299">3.0.76</span><span class="sxs-lookup"><span data-stu-id="73d37-299">3.0.76</span></span> |
| <span data-ttu-id="73d37-300">11 SP4</span><span class="sxs-lookup"><span data-stu-id="73d37-300">11 SP4</span></span> | <span data-ttu-id="73d37-301">3.0.101</span><span class="sxs-lookup"><span data-stu-id="73d37-301">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="73d37-302">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="73d37-302">SUSE Linux 10</span></span>

| <span data-ttu-id="73d37-303">**OS version**</span><span class="sxs-lookup"><span data-stu-id="73d37-303">**OS version**</span></span> | <span data-ttu-id="73d37-304">**Kernel version**</span><span class="sxs-lookup"><span data-stu-id="73d37-304">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-305">10 SP4</span><span class="sxs-lookup"><span data-stu-id="73d37-305">10 SP4</span></span> | <span data-ttu-id="73d37-306">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="73d37-306">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="73d37-307">Dependency Agent downloads</span><span class="sxs-lookup"><span data-stu-id="73d37-307">Dependency Agent downloads</span></span>

| <span data-ttu-id="73d37-308">**File**</span><span class="sxs-lookup"><span data-stu-id="73d37-308">**File**</span></span> | <span data-ttu-id="73d37-309">**OS**</span><span class="sxs-lookup"><span data-stu-id="73d37-309">**OS**</span></span> | <span data-ttu-id="73d37-310">**Version**</span><span class="sxs-lookup"><span data-stu-id="73d37-310">**Version**</span></span> | <span data-ttu-id="73d37-311">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="73d37-311">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="73d37-312">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="73d37-312">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="73d37-313">Windows</span><span class="sxs-lookup"><span data-stu-id="73d37-313">Windows</span></span> | <span data-ttu-id="73d37-314">9.0.5</span><span class="sxs-lookup"><span data-stu-id="73d37-314">9.0.5</span></span> | <span data-ttu-id="73d37-315">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="73d37-315">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="73d37-316">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="73d37-316">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="73d37-317">Linux</span><span class="sxs-lookup"><span data-stu-id="73d37-317">Linux</span></span> | <span data-ttu-id="73d37-318">9.0.5</span><span class="sxs-lookup"><span data-stu-id="73d37-318">9.0.5</span></span> | <span data-ttu-id="73d37-319">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="73d37-319">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="73d37-320">Configuration</span><span class="sxs-lookup"><span data-stu-id="73d37-320">Configuration</span></span>

<span data-ttu-id="73d37-321">Perform the following steps to configure the Wire Data solution for your workspaces.</span><span class="sxs-lookup"><span data-stu-id="73d37-321">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="73d37-322">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="73d37-322">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="73d37-323">Install the Dependency Agent on each computer where you want to get data.</span><span class="sxs-lookup"><span data-stu-id="73d37-323">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="73d37-324">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span><span class="sxs-lookup"><span data-stu-id="73d37-324">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="73d37-325">Install the Dependency Agent on Windows</span><span class="sxs-lookup"><span data-stu-id="73d37-325">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="73d37-326">Administrator privileges are required to install or uninstall the agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-326">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="73d37-327">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="73d37-327">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="73d37-328">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span><span class="sxs-lookup"><span data-stu-id="73d37-328">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="73d37-329">Use the following steps to install the Dependency Agent on each computer running Windows:</span><span class="sxs-lookup"><span data-stu-id="73d37-329">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="73d37-330">Install the OMS Agent following the steps in [Collect data from Windows computers hosted in your environment](log-analytics-windows-agent.md).</span><span class="sxs-lookup"><span data-stu-id="73d37-330">Install the OMS Agent following the steps in [Collect data from Windows computers hosted in your environment](log-analytics-windows-agent.md).</span></span>
2. <span data-ttu-id="73d37-331">Download the Windows Dependency Agent using the link in the previous section and then run it by using the following command: `InstallDependencyAgent-Windows.exe`</span><span class="sxs-lookup"><span data-stu-id="73d37-331">Download the Windows Dependency Agent using the link in the previous section and then run it by using the following command: `InstallDependencyAgent-Windows.exe`</span></span>
3. <span data-ttu-id="73d37-332">Follow the wizard to install the agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-332">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="73d37-333">If the Dependency Agent fails to start, check the logs for detailed error information.</span><span class="sxs-lookup"><span data-stu-id="73d37-333">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="73d37-334">For Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span><span class="sxs-lookup"><span data-stu-id="73d37-334">For Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="73d37-335">Windows command line</span><span class="sxs-lookup"><span data-stu-id="73d37-335">Windows command line</span></span>

<span data-ttu-id="73d37-336">Use options from the following table to install from a command line.</span><span class="sxs-lookup"><span data-stu-id="73d37-336">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="73d37-337">To see a list of the installation flags, run the installer by using the /?</span><span class="sxs-lookup"><span data-stu-id="73d37-337">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="73d37-338">flag as follows.</span><span class="sxs-lookup"><span data-stu-id="73d37-338">flag as follows.</span></span>

<span data-ttu-id="73d37-339">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="73d37-339">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="73d37-340">**Flag**</span><span class="sxs-lookup"><span data-stu-id="73d37-340">**Flag**</span></span> | <span data-ttu-id="73d37-341">**Description**</span><span class="sxs-lookup"><span data-stu-id="73d37-341">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="73d37-342">Get a list of the command-line options.</span><span class="sxs-lookup"><span data-stu-id="73d37-342">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="73d37-343">Perform a silent installation with no user prompts.</span><span class="sxs-lookup"><span data-stu-id="73d37-343">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="73d37-344">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span><span class="sxs-lookup"><span data-stu-id="73d37-344">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="73d37-345">Install the Dependency Agent on Linux</span><span class="sxs-lookup"><span data-stu-id="73d37-345">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="73d37-346">Root access is required to install or configure the agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-346">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="73d37-347">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span><span class="sxs-lookup"><span data-stu-id="73d37-347">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="73d37-348">You can run the file by using _sh_ or add execute permissions to the file itself.</span><span class="sxs-lookup"><span data-stu-id="73d37-348">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="73d37-349">Use the following steps to install the Dependency Agent on each Linux computer:</span><span class="sxs-lookup"><span data-stu-id="73d37-349">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="73d37-350">Install the OMS Agent following the steps in [Collect data from Linux computers hosted in your environment](log-analytics-quick-collect-linux-computer.md#obtain-workspace-id-and-key).</span><span class="sxs-lookup"><span data-stu-id="73d37-350">Install the OMS Agent following the steps in [Collect data from Linux computers hosted in your environment](log-analytics-quick-collect-linux-computer.md#obtain-workspace-id-and-key).</span></span>
2. <span data-ttu-id="73d37-351">Download the Linux Dependency Agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="73d37-351">Download the Linux Dependency Agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="73d37-352">If the Dependency Agent fails to start, check the logs for detailed error information.</span><span class="sxs-lookup"><span data-stu-id="73d37-352">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="73d37-353">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="73d37-353">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="73d37-354">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span><span class="sxs-lookup"><span data-stu-id="73d37-354">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="73d37-355">**Flag**</span><span class="sxs-lookup"><span data-stu-id="73d37-355">**Flag**</span></span> | <span data-ttu-id="73d37-356">**Description**</span><span class="sxs-lookup"><span data-stu-id="73d37-356">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="73d37-357">Get a list of the command-line options.</span><span class="sxs-lookup"><span data-stu-id="73d37-357">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="73d37-358">Perform a silent installation with no user prompts.</span><span class="sxs-lookup"><span data-stu-id="73d37-358">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="73d37-359">Check permissions and the operating system but do not install the agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-359">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="73d37-360">Files for the Dependency Agent are placed in the following directories:</span><span class="sxs-lookup"><span data-stu-id="73d37-360">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="73d37-361">**Files**</span><span class="sxs-lookup"><span data-stu-id="73d37-361">**Files**</span></span> | <span data-ttu-id="73d37-362">**Location**</span><span class="sxs-lookup"><span data-stu-id="73d37-362">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-363">Core files</span><span class="sxs-lookup"><span data-stu-id="73d37-363">Core files</span></span> | <span data-ttu-id="73d37-364">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="73d37-364">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="73d37-365">Log files</span><span class="sxs-lookup"><span data-stu-id="73d37-365">Log files</span></span> | <span data-ttu-id="73d37-366">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="73d37-366">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="73d37-367">Config files</span><span class="sxs-lookup"><span data-stu-id="73d37-367">Config files</span></span> | <span data-ttu-id="73d37-368">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="73d37-368">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="73d37-369">Service executable files</span><span class="sxs-lookup"><span data-stu-id="73d37-369">Service executable files</span></span> | <span data-ttu-id="73d37-370">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="73d37-370">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="73d37-371">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="73d37-371">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="73d37-372">Binary storage files</span><span class="sxs-lookup"><span data-stu-id="73d37-372">Binary storage files</span></span> | <span data-ttu-id="73d37-373">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="73d37-373">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="73d37-374">Installation script examples</span><span class="sxs-lookup"><span data-stu-id="73d37-374">Installation script examples</span></span>

<span data-ttu-id="73d37-375">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span><span class="sxs-lookup"><span data-stu-id="73d37-375">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="73d37-376">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="73d37-376">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="73d37-377">PowerShell script for Windows</span><span class="sxs-lookup"><span data-stu-id="73d37-377">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="73d37-378">Shell script for Linux</span><span class="sxs-lookup"><span data-stu-id="73d37-378">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="73d37-379">Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="73d37-379">Desired State Configuration</span></span>

<span data-ttu-id="73d37-380">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span><span class="sxs-lookup"><span data-stu-id="73d37-380">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="73d37-381">Uninstall the Dependency Agent</span><span class="sxs-lookup"><span data-stu-id="73d37-381">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="73d37-382">Use the following sections to help you remove the Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-382">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="73d37-383">Uninstall the Dependency Agent on Windows</span><span class="sxs-lookup"><span data-stu-id="73d37-383">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="73d37-384">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span><span class="sxs-lookup"><span data-stu-id="73d37-384">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="73d37-385">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-385">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="73d37-386">Uninstall the Dependency Agent on Linux</span><span class="sxs-lookup"><span data-stu-id="73d37-386">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="73d37-387">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span><span class="sxs-lookup"><span data-stu-id="73d37-387">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="73d37-388">You can uninstall both by using the following single command:</span><span class="sxs-lookup"><span data-stu-id="73d37-388">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="73d37-389">Management packs</span><span class="sxs-lookup"><span data-stu-id="73d37-389">Management packs</span></span>

<span data-ttu-id="73d37-390">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span><span class="sxs-lookup"><span data-stu-id="73d37-390">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="73d37-391">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="73d37-391">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="73d37-392">If the agents are directly connected, Log Analytics delivers the management pack.</span><span class="sxs-lookup"><span data-stu-id="73d37-392">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="73d37-393">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="73d37-393">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="73d37-394">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="73d37-394">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="73d37-395">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="73d37-395">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="73d37-396">Using the solution</span><span class="sxs-lookup"><span data-stu-id="73d37-396">Using the solution</span></span>

<span data-ttu-id="73d37-397">**Installing and configuring the solution**</span><span class="sxs-lookup"><span data-stu-id="73d37-397">**Installing and configuring the solution**</span></span>

<span data-ttu-id="73d37-398">Use the following information to install and configure the solution.</span><span class="sxs-lookup"><span data-stu-id="73d37-398">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="73d37-399">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span><span class="sxs-lookup"><span data-stu-id="73d37-399">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="73d37-400">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span><span class="sxs-lookup"><span data-stu-id="73d37-400">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="73d37-401">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="73d37-401">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="73d37-402">There is no further configuration required.</span><span class="sxs-lookup"><span data-stu-id="73d37-402">There is no further configuration required.</span></span>
- <span data-ttu-id="73d37-403">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span><span class="sxs-lookup"><span data-stu-id="73d37-403">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="73d37-404">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span><span class="sxs-lookup"><span data-stu-id="73d37-404">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

![Wire Data tile](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="73d37-406">Using the Wire Data 2.0 solution</span><span class="sxs-lookup"><span data-stu-id="73d37-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="73d37-407">In the **Overview** page for your Log Analytics workspace in the Azure portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span><span class="sxs-lookup"><span data-stu-id="73d37-407">In the **Overview** page for your Log Analytics workspace in the Azure portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="73d37-408">The dashboard includes the blades in the following table.</span><span class="sxs-lookup"><span data-stu-id="73d37-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="73d37-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span><span class="sxs-lookup"><span data-stu-id="73d37-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="73d37-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span><span class="sxs-lookup"><span data-stu-id="73d37-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="73d37-411">**Blade**</span><span class="sxs-lookup"><span data-stu-id="73d37-411">**Blade**</span></span> | <span data-ttu-id="73d37-412">**Description**</span><span class="sxs-lookup"><span data-stu-id="73d37-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="73d37-413">Agents capturing network traffic</span><span class="sxs-lookup"><span data-stu-id="73d37-413">Agents capturing network traffic</span></span> | <span data-ttu-id="73d37-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span><span class="sxs-lookup"><span data-stu-id="73d37-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="73d37-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="73d37-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="73d37-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span><span class="sxs-lookup"><span data-stu-id="73d37-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="73d37-417">Local Subnets</span><span class="sxs-lookup"><span data-stu-id="73d37-417">Local Subnets</span></span> | <span data-ttu-id="73d37-418">Shows the number of local subnets that agents have discovered.</span><span class="sxs-lookup"><span data-stu-id="73d37-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="73d37-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span><span class="sxs-lookup"><span data-stu-id="73d37-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="73d37-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span><span class="sxs-lookup"><span data-stu-id="73d37-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="73d37-421">Application-level Protocols</span><span class="sxs-lookup"><span data-stu-id="73d37-421">Application-level Protocols</span></span> | <span data-ttu-id="73d37-422">Shows the number of application-level protocols in use, as discovered by agents.</span><span class="sxs-lookup"><span data-stu-id="73d37-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="73d37-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="73d37-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="73d37-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span><span class="sxs-lookup"><span data-stu-id="73d37-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

![Wire Data dashboard](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="73d37-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span><span class="sxs-lookup"><span data-stu-id="73d37-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="73d37-427">This blade can help you easily find the _chattiest_ computer in your environment.</span><span class="sxs-lookup"><span data-stu-id="73d37-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="73d37-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span><span class="sxs-lookup"><span data-stu-id="73d37-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![log search example](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="73d37-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span><span class="sxs-lookup"><span data-stu-id="73d37-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="73d37-431">Users often define subnets around critical areas for their applications.</span><span class="sxs-lookup"><span data-stu-id="73d37-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="73d37-432">This blade offers a view into those areas.</span><span class="sxs-lookup"><span data-stu-id="73d37-432">This blade offers a view into those areas.</span></span>

![log search example](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="73d37-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span><span class="sxs-lookup"><span data-stu-id="73d37-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="73d37-435">For example, you might expect SSH to not be in use in your network environment.</span><span class="sxs-lookup"><span data-stu-id="73d37-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="73d37-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span><span class="sxs-lookup"><span data-stu-id="73d37-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![log search example](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="73d37-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span><span class="sxs-lookup"><span data-stu-id="73d37-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![sh search results](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="73d37-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span><span class="sxs-lookup"><span data-stu-id="73d37-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="73d37-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span><span class="sxs-lookup"><span data-stu-id="73d37-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="73d37-442">Input data</span><span class="sxs-lookup"><span data-stu-id="73d37-442">Input data</span></span>

<span data-ttu-id="73d37-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span><span class="sxs-lookup"><span data-stu-id="73d37-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="73d37-444">Each agent sends data about every 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="73d37-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="73d37-445">Output data</span><span class="sxs-lookup"><span data-stu-id="73d37-445">Output data</span></span>

<span data-ttu-id="73d37-446">A record with a type of _WireData_ is created for each type of input data.</span><span class="sxs-lookup"><span data-stu-id="73d37-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="73d37-447">WireData records have properties shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="73d37-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="73d37-448">Property</span><span class="sxs-lookup"><span data-stu-id="73d37-448">Property</span></span> | <span data-ttu-id="73d37-449">Description</span><span class="sxs-lookup"><span data-stu-id="73d37-449">Description</span></span> |
|---|---|
| <span data-ttu-id="73d37-450">Computer</span><span class="sxs-lookup"><span data-stu-id="73d37-450">Computer</span></span> | <span data-ttu-id="73d37-451">Computer name where data was collected</span><span class="sxs-lookup"><span data-stu-id="73d37-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="73d37-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="73d37-452">TimeGenerated</span></span> | <span data-ttu-id="73d37-453">Time of the record</span><span class="sxs-lookup"><span data-stu-id="73d37-453">Time of the record</span></span> |
| <span data-ttu-id="73d37-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="73d37-454">LocalIP</span></span> | <span data-ttu-id="73d37-455">IP address of the local computer</span><span class="sxs-lookup"><span data-stu-id="73d37-455">IP address of the local computer</span></span> |
| <span data-ttu-id="73d37-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="73d37-456">SessionState</span></span> | <span data-ttu-id="73d37-457">Connected or disconnected</span><span class="sxs-lookup"><span data-stu-id="73d37-457">Connected or disconnected</span></span> |
| <span data-ttu-id="73d37-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="73d37-458">ReceivedBytes</span></span> | <span data-ttu-id="73d37-459">Amount of bytes received</span><span class="sxs-lookup"><span data-stu-id="73d37-459">Amount of bytes received</span></span> |
| <span data-ttu-id="73d37-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="73d37-460">ProtocolName</span></span> | <span data-ttu-id="73d37-461">Name of the network protocol used</span><span class="sxs-lookup"><span data-stu-id="73d37-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="73d37-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="73d37-462">IPVersion</span></span> | <span data-ttu-id="73d37-463">IP version</span><span class="sxs-lookup"><span data-stu-id="73d37-463">IP version</span></span> |
| <span data-ttu-id="73d37-464">Direction</span><span class="sxs-lookup"><span data-stu-id="73d37-464">Direction</span></span> | <span data-ttu-id="73d37-465">Inbound or outbound</span><span class="sxs-lookup"><span data-stu-id="73d37-465">Inbound or outbound</span></span> |
| <span data-ttu-id="73d37-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="73d37-466">MaliciousIP</span></span> | <span data-ttu-id="73d37-467">IP address of a known malicious source</span><span class="sxs-lookup"><span data-stu-id="73d37-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="73d37-468">Severity</span><span class="sxs-lookup"><span data-stu-id="73d37-468">Severity</span></span> | <span data-ttu-id="73d37-469">Suspected malware severity</span><span class="sxs-lookup"><span data-stu-id="73d37-469">Suspected malware severity</span></span> |
| <span data-ttu-id="73d37-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="73d37-470">RemoteIPCountry</span></span> | <span data-ttu-id="73d37-471">Country of the remote IP address</span><span class="sxs-lookup"><span data-stu-id="73d37-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="73d37-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="73d37-472">ManagementGroupName</span></span> | <span data-ttu-id="73d37-473">Name of the Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="73d37-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="73d37-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="73d37-474">SourceSystem</span></span> | <span data-ttu-id="73d37-475">Source where data was collected</span><span class="sxs-lookup"><span data-stu-id="73d37-475">Source where data was collected</span></span> |
| <span data-ttu-id="73d37-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="73d37-476">SessionStartTime</span></span> | <span data-ttu-id="73d37-477">Start time of session</span><span class="sxs-lookup"><span data-stu-id="73d37-477">Start time of session</span></span> |
| <span data-ttu-id="73d37-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="73d37-478">SessionEndTime</span></span> | <span data-ttu-id="73d37-479">End time of session</span><span class="sxs-lookup"><span data-stu-id="73d37-479">End time of session</span></span> |
| <span data-ttu-id="73d37-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="73d37-480">LocalSubnet</span></span> | <span data-ttu-id="73d37-481">Subnet where data was collected</span><span class="sxs-lookup"><span data-stu-id="73d37-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="73d37-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="73d37-482">LocalPortNumber</span></span> | <span data-ttu-id="73d37-483">Local port number</span><span class="sxs-lookup"><span data-stu-id="73d37-483">Local port number</span></span> |
| <span data-ttu-id="73d37-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="73d37-484">RemoteIP</span></span> | <span data-ttu-id="73d37-485">Remote IP address used by the remote computer</span><span class="sxs-lookup"><span data-stu-id="73d37-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="73d37-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="73d37-486">RemotePortNumber</span></span> | <span data-ttu-id="73d37-487">Port number used by the remote IP address</span><span class="sxs-lookup"><span data-stu-id="73d37-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="73d37-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="73d37-488">SessionID</span></span> | <span data-ttu-id="73d37-489">A unique value that identifies communication session between two IP addresses</span><span class="sxs-lookup"><span data-stu-id="73d37-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="73d37-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="73d37-490">SentBytes</span></span> | <span data-ttu-id="73d37-491">Number of bytes sent</span><span class="sxs-lookup"><span data-stu-id="73d37-491">Number of bytes sent</span></span> |
| <span data-ttu-id="73d37-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="73d37-492">TotalBytes</span></span> | <span data-ttu-id="73d37-493">Total number of bytes sent during session</span><span class="sxs-lookup"><span data-stu-id="73d37-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="73d37-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="73d37-494">ApplicationProtocol</span></span> | <span data-ttu-id="73d37-495">Type of network protocol used</span><span class="sxs-lookup"><span data-stu-id="73d37-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="73d37-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="73d37-496">ProcessID</span></span> | <span data-ttu-id="73d37-497">Windows process ID</span><span class="sxs-lookup"><span data-stu-id="73d37-497">Windows process ID</span></span> |
| <span data-ttu-id="73d37-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="73d37-498">ProcessName</span></span> | <span data-ttu-id="73d37-499">Path and file name of the process</span><span class="sxs-lookup"><span data-stu-id="73d37-499">Path and file name of the process</span></span> |
| <span data-ttu-id="73d37-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="73d37-500">RemoteIPLongitude</span></span> | <span data-ttu-id="73d37-501">IP longitude value</span><span class="sxs-lookup"><span data-stu-id="73d37-501">IP longitude value</span></span> |
| <span data-ttu-id="73d37-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="73d37-502">RemoteIPLatitude</span></span> | <span data-ttu-id="73d37-503">IP latitude value</span><span class="sxs-lookup"><span data-stu-id="73d37-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="73d37-504">Next steps</span><span class="sxs-lookup"><span data-stu-id="73d37-504">Next steps</span></span>

- <span data-ttu-id="73d37-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span><span class="sxs-lookup"><span data-stu-id="73d37-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
