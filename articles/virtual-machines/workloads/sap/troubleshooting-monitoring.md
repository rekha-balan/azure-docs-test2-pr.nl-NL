---
title: Troubleshooting and Monitoring of SAP HANA on Azure (Large Instances) | Microsoft Docs
description: Troubleshoot and monitor SAP HANA on an Azure (Large Instances).
services: virtual-machines-linux
documentationcenter: ''
author: RicksterCDN
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8eab74cc64ad8495864887953d7e9b395bf8d21f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554866"
---
# <a name="how-to-troubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a><span data-ttu-id="167e6-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span><span class="sxs-lookup"><span data-stu-id="167e6-103">How to troubleshoot and monitor SAP HANA (large instances) on Azure</span></span>


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a><span data-ttu-id="167e6-104">Monitoring in SAP HANA on Azure (Large Instances)</span><span class="sxs-lookup"><span data-stu-id="167e6-104">Monitoring in SAP HANA on Azure (Large Instances)</span></span>

<span data-ttu-id="167e6-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span><span class="sxs-lookup"><span data-stu-id="167e6-105">SAP HANA on Azure (Large Instances) is no different from any other IaaS deployment — you need to monitor what the OS and the application is doing and how these consume the following resources:</span></span>

- <span data-ttu-id="167e6-106">CPU</span><span class="sxs-lookup"><span data-stu-id="167e6-106">CPU</span></span>
- <span data-ttu-id="167e6-107">Memory</span><span class="sxs-lookup"><span data-stu-id="167e6-107">Memory</span></span>
- <span data-ttu-id="167e6-108">Network bandwidth</span><span class="sxs-lookup"><span data-stu-id="167e6-108">Network bandwidth</span></span>
- <span data-ttu-id="167e6-109">Disk space</span><span class="sxs-lookup"><span data-stu-id="167e6-109">Disk space</span></span>

<span data-ttu-id="167e6-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span><span class="sxs-lookup"><span data-stu-id="167e6-110">As with Azure Virtual Machines you need to figure out whether the resource classes named above are sufficient, or whether these get depleted.</span></span> <span data-ttu-id="167e6-111">Here is more detail on each of the different classes:</span><span class="sxs-lookup"><span data-stu-id="167e6-111">Here is more detail on each of the different classes:</span></span>

<span data-ttu-id="167e6-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span><span class="sxs-lookup"><span data-stu-id="167e6-112">**CPU resource consumption:** The ratio that SAP defined for certain workload against HANA is enforced to make sure that there should be enough CPU resources available to work through the data that is stored in memory.</span></span> <span data-ttu-id="167e6-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span><span class="sxs-lookup"><span data-stu-id="167e6-113">Nevertheless, there might be cases where HANA consumes a lot of CPU executing queries due to missing indexes or similar issues.</span></span> <span data-ttu-id="167e6-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span><span class="sxs-lookup"><span data-stu-id="167e6-114">This means you should monitor CPU resource consumption of the HANA large instance unit as well as CPU resources consumed by the specific HANA services.</span></span>

<span data-ttu-id="167e6-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span><span class="sxs-lookup"><span data-stu-id="167e6-115">**Memory consumption:** Is important to monitor from within HANA, as well as outside of HANA on the unit.</span></span> <span data-ttu-id="167e6-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span><span class="sxs-lookup"><span data-stu-id="167e6-116">Within HANA, monitor how the data is consuming HANA allocated memory in order to stay within the required sizing guidelines of SAP.</span></span> <span data-ttu-id="167e6-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span><span class="sxs-lookup"><span data-stu-id="167e6-117">You also want to monitor memory consumption on the Large Instance level to make sure that additional installed non-HANA software does not consume too much memory, and therefore compete with HANA for memory.</span></span>

<span data-ttu-id="167e6-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span><span class="sxs-lookup"><span data-stu-id="167e6-118">**Network bandwidth:** The Azure VNet gateway is limited in bandwidth of data moving into the Azure VNet, so it is helpful to monitor the data received by all the Azure VMs within a VNet to figure out how close you are to the limits of the Azure gateway SKU you selected.</span></span> <span data-ttu-id="167e6-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span><span class="sxs-lookup"><span data-stu-id="167e6-119">On the HANA Large Instance unit, it does make sense to monitor incoming and outgoing network traffic as well, and to keep track of the volumes that are handled over time.</span></span>

<span data-ttu-id="167e6-120">**Disk space:** Disk space consumption usually increases over time.</span><span class="sxs-lookup"><span data-stu-id="167e6-120">**Disk space:** Disk space consumption usually increases over time.</span></span> <span data-ttu-id="167e6-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="167e6-121">There are many reasons for this, but most of all are: data volume increases, execution of transaction log backups, storing trace files, and performing storage snapshots.</span></span> <span data-ttu-id="167e6-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span><span class="sxs-lookup"><span data-stu-id="167e6-122">Therefore, it is important to monitor disk space usage and manage the disk space associated with the HANA Large Instance unit.</span></span>

## <a name="monitoring-and-troubleshooting-from-hana-side"></a><span data-ttu-id="167e6-123">Monitoring and troubleshooting from HANA side</span><span class="sxs-lookup"><span data-stu-id="167e6-123">Monitoring and troubleshooting from HANA side</span></span>

<span data-ttu-id="167e6-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span><span class="sxs-lookup"><span data-stu-id="167e6-124">In order to effectively analyze problems related to SAP HANA on Azure (Large Instances), it is useful to narrow down the root cause of a problem.</span></span> <span data-ttu-id="167e6-125">SAP has published a large amount of documentation to help you.</span><span class="sxs-lookup"><span data-stu-id="167e6-125">SAP has published a large amount of documentation to help you.</span></span>

<span data-ttu-id="167e6-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span><span class="sxs-lookup"><span data-stu-id="167e6-126">Applicable FAQs related to SAP HANA performance can be found in the following SAP Notes:</span></span>

- [<span data-ttu-id="167e6-127">SAP Note #2222200 – FAQ: SAP HANA Network</span><span class="sxs-lookup"><span data-stu-id="167e6-127">SAP Note #2222200 – FAQ: SAP HANA Network</span></span>](https://launchpad.support.sap.com/#/notes/2222200)
- [<span data-ttu-id="167e6-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span><span class="sxs-lookup"><span data-stu-id="167e6-128">SAP Note #2100040 – FAQ: SAP HANA CPU</span></span>](https://launchpad.support.sap.com/#/notes/0002100040)
- [<span data-ttu-id="167e6-129">SAP Note #199997 – FAQ: SAP HANA Memory</span><span class="sxs-lookup"><span data-stu-id="167e6-129">SAP Note #199997 – FAQ: SAP HANA Memory</span></span>](https://launchpad.support.sap.com/#/notes/2177064)
- [<span data-ttu-id="167e6-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span><span class="sxs-lookup"><span data-stu-id="167e6-130">SAP Note #200000 – FAQ: SAP HANA Performance Optimization</span></span>](https://launchpad.support.sap.com/#/notes/2000000)
- [<span data-ttu-id="167e6-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span><span class="sxs-lookup"><span data-stu-id="167e6-131">SAP Note #199930 – FAQ: SAP HANA I/O Analysis</span></span>](https://launchpad.support.sap.com/#/notes/1999930)
- [<span data-ttu-id="167e6-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span><span class="sxs-lookup"><span data-stu-id="167e6-132">SAP Note #2177064 – FAQ: SAP HANA Service Restart and Crashes</span></span>](https://launchpad.support.sap.com/#/notes/2177064)

<span data-ttu-id="167e6-133">**SAP HANA Alerts**</span><span class="sxs-lookup"><span data-stu-id="167e6-133">**SAP HANA Alerts**</span></span>

<span data-ttu-id="167e6-134">As a first step, check the current SAP HANA alert logs.</span><span class="sxs-lookup"><span data-stu-id="167e6-134">As a first step, check the current SAP HANA alert logs.</span></span> <span data-ttu-id="167e6-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span><span class="sxs-lookup"><span data-stu-id="167e6-135">In SAP HANA Studio, go to **Administration Console: Alerts: Show: all alerts**.</span></span> <span data-ttu-id="167e6-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span><span class="sxs-lookup"><span data-stu-id="167e6-136">This tab will show all SAP HANA alerts for specific values (free physical memory, CPU utilization, etc.) that fall outside of the set minimum and maximum thresholds.</span></span> <span data-ttu-id="167e6-137">By default, checks are auto-refreshed every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="167e6-137">By default, checks are auto-refreshed every 15 minutes.</span></span>

![In SAP HANA Studio, go to Administration Console: Alerts: Show: all alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image1-show-alerts.png)

<span data-ttu-id="167e6-139">**CPU**</span><span class="sxs-lookup"><span data-stu-id="167e6-139">**CPU**</span></span>

<span data-ttu-id="167e6-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span><span class="sxs-lookup"><span data-stu-id="167e6-140">For an alert triggered due to improper threshold setting, a resolution is to reset to the default value or a more reasonable threshold value.</span></span>

![Reset to the default value or a more reasonable threshold value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image2-cpu-utilization.png)

<span data-ttu-id="167e6-142">The following alerts may indicate CPU resource problems:</span><span class="sxs-lookup"><span data-stu-id="167e6-142">The following alerts may indicate CPU resource problems:</span></span>

- <span data-ttu-id="167e6-143">Host CPU Usage (Alert 5)</span><span class="sxs-lookup"><span data-stu-id="167e6-143">Host CPU Usage (Alert 5)</span></span>
- <span data-ttu-id="167e6-144">Most recent savepoint operation (Alert 28)</span><span class="sxs-lookup"><span data-stu-id="167e6-144">Most recent savepoint operation (Alert 28)</span></span>
- <span data-ttu-id="167e6-145">Savepoint duration (Alert 54)</span><span class="sxs-lookup"><span data-stu-id="167e6-145">Savepoint duration (Alert 54)</span></span>

<span data-ttu-id="167e6-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span><span class="sxs-lookup"><span data-stu-id="167e6-146">You may notice high CPU consumption on your SAP HANA database from one of the following:</span></span>

- <span data-ttu-id="167e6-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span><span class="sxs-lookup"><span data-stu-id="167e6-147">Alert 5 (Host CPU usage) is raised for current or past CPU usage</span></span>
- <span data-ttu-id="167e6-148">The displayed CPU usage on the overview screen</span><span class="sxs-lookup"><span data-stu-id="167e6-148">The displayed CPU usage on the overview screen</span></span>

![Displayed CPU usage on the overview screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image3-cpu-usage.png)

<span data-ttu-id="167e6-150">The Load graph might show high CPU consumption, or high consumption in the past:</span><span class="sxs-lookup"><span data-stu-id="167e6-150">The Load graph might show high CPU consumption, or high consumption in the past:</span></span>

![The Load graph might show high CPU consumption, or high consumption in the past](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image4-load-graph.png)

<span data-ttu-id="167e6-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span><span class="sxs-lookup"><span data-stu-id="167e6-152">An alert triggered due to high CPU utilization could be caused by several reasons, including, but not limited to: execution of certain transactions, data loading, hanging of jobs, long running SQL statements, and bad query performance (for example, with BW on HANA cubes).</span></span>

<span data-ttu-id="167e6-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="167e6-153">Refer to the [SAP HANA Troubleshooting: CPU Related Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="167e6-154">**Operating System**</span><span class="sxs-lookup"><span data-stu-id="167e6-154">**Operating System**</span></span>

<span data-ttu-id="167e6-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span><span class="sxs-lookup"><span data-stu-id="167e6-155">One of the most important checks for SAP HANA on Linux is to make sure that Transparent Huge Pages are disabled, see [SAP Note #2131662 – Transparent Huge Pages (THP) on SAP HANA Servers](https://launchpad.support.sap.com/#/notes/2131662).</span></span>

- <span data-ttu-id="167e6-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span><span class="sxs-lookup"><span data-stu-id="167e6-156">You can check if Transparent Huge Pages are enabled through the following Linux command: **cat /sys/kernel/mm/transparent\_hugepage/enabled**</span></span>
- <span data-ttu-id="167e6-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span><span class="sxs-lookup"><span data-stu-id="167e6-157">If _always_ is enclosed in brackets as below, it means that the Transparent Huge Pages are enabled: [always] madvise never; if _never_ is enclosed in brackets as below, it means that the Transparent Huge Pages are disabled: always madvise [never]</span></span>

<span data-ttu-id="167e6-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span><span class="sxs-lookup"><span data-stu-id="167e6-158">The following Linux command should return nothing: **rpm -qa | grep ulimit.**</span></span> <span data-ttu-id="167e6-159">If it appears _ulimit_ is installed, uninstall it immediately.</span><span class="sxs-lookup"><span data-stu-id="167e6-159">If it appears _ulimit_ is installed, uninstall it immediately.</span></span>

<span data-ttu-id="167e6-160">**Memory**</span><span class="sxs-lookup"><span data-stu-id="167e6-160">**Memory**</span></span>

<span data-ttu-id="167e6-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span><span class="sxs-lookup"><span data-stu-id="167e6-161">You may observe that the amount of memory allocated by the SAP HANA database is higher than expected.</span></span> <span data-ttu-id="167e6-162">The following alerts indicate issues with high memory usage:</span><span class="sxs-lookup"><span data-stu-id="167e6-162">The following alerts indicate issues with high memory usage:</span></span>

- <span data-ttu-id="167e6-163">Host physical memory usage (Alert 1)</span><span class="sxs-lookup"><span data-stu-id="167e6-163">Host physical memory usage (Alert 1)</span></span>
- <span data-ttu-id="167e6-164">Memory usage of name server (Alert 12)</span><span class="sxs-lookup"><span data-stu-id="167e6-164">Memory usage of name server (Alert 12)</span></span>
- <span data-ttu-id="167e6-165">Total memory usage of Column Store tables (Alert 40)</span><span class="sxs-lookup"><span data-stu-id="167e6-165">Total memory usage of Column Store tables (Alert 40)</span></span>
- <span data-ttu-id="167e6-166">Memory usage of services (Alert 43)</span><span class="sxs-lookup"><span data-stu-id="167e6-166">Memory usage of services (Alert 43)</span></span>
- <span data-ttu-id="167e6-167">Memory usage of main storage of Column Store tables (Alert 45)</span><span class="sxs-lookup"><span data-stu-id="167e6-167">Memory usage of main storage of Column Store tables (Alert 45)</span></span>
- <span data-ttu-id="167e6-168">Runtime dump files (Alert 46)</span><span class="sxs-lookup"><span data-stu-id="167e6-168">Runtime dump files (Alert 46)</span></span>

<span data-ttu-id="167e6-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="167e6-169">Refer to the [SAP HANA Troubleshooting: Memory Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="167e6-170">**Network**</span><span class="sxs-lookup"><span data-stu-id="167e6-170">**Network**</span></span>

<span data-ttu-id="167e6-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span><span class="sxs-lookup"><span data-stu-id="167e6-171">Refer to [SAP Note #2081065 – Troubleshooting SAP HANA Network](https://launchpad.support.sap.com/#/notes/2081065) and perform the network troubleshooting steps in this SAP Note.</span></span>

1. <span data-ttu-id="167e6-172">Analyzing round-trip time between server and client.</span><span class="sxs-lookup"><span data-stu-id="167e6-172">Analyzing round-trip time between server and client.</span></span>
  <span data-ttu-id="167e6-173">A.</span><span class="sxs-lookup"><span data-stu-id="167e6-173">A.</span></span> <span data-ttu-id="167e6-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="167e6-174">Run the SQL script [_HANA\_Network\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>
  
2. <span data-ttu-id="167e6-175">Analyze internode communication.</span><span class="sxs-lookup"><span data-stu-id="167e6-175">Analyze internode communication.</span></span>
  <span data-ttu-id="167e6-176">A.</span><span class="sxs-lookup"><span data-stu-id="167e6-176">A.</span></span> <span data-ttu-id="167e6-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span><span class="sxs-lookup"><span data-stu-id="167e6-177">Run SQL script [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._</span></span>

3. <span data-ttu-id="167e6-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span><span class="sxs-lookup"><span data-stu-id="167e6-178">Run Linux command **ifconfig** (the output shows if any packet losses are occurring).</span></span>
4. <span data-ttu-id="167e6-179">Run Linux command **tcpdump**.</span><span class="sxs-lookup"><span data-stu-id="167e6-179">Run Linux command **tcpdump**.</span></span>

<span data-ttu-id="167e6-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span><span class="sxs-lookup"><span data-stu-id="167e6-180">Also, use the open source [IPERF](https://iperf.fr/) tool (or similar) to measure real application network performance.</span></span>

<span data-ttu-id="167e6-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="167e6-181">Refer to the [SAP HANA Troubleshooting: Networking Performance and Connectivity Problems](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="167e6-182">**Storage**</span><span class="sxs-lookup"><span data-stu-id="167e6-182">**Storage**</span></span>

<span data-ttu-id="167e6-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span><span class="sxs-lookup"><span data-stu-id="167e6-183">From an end-user perspective, an application (or the system as a whole) runs sluggishly, is unresponsive, or can even seem to hang if there are issues with I/O performance.</span></span> <span data-ttu-id="167e6-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span><span class="sxs-lookup"><span data-stu-id="167e6-184">In the **Volumes** tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service.</span></span>

![In the Volumes tab in SAP HANA Studio, you can see the attached volumes, and what volumes are used by each service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image5-volumes-tab-a.png)

<span data-ttu-id="167e6-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span><span class="sxs-lookup"><span data-stu-id="167e6-186">Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics.</span></span>

![Attached volumes in the lower part of the screen you can see details of the volumes, such as files and I/O statistics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image6-volumes-tab-b.png)

<span data-ttu-id="167e6-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="167e6-188">Refer to the [SAP HANA Troubleshooting: I/O Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) and [SAP HANA Troubleshooting: Disk Related Root Causes and Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site for detailed troubleshooting steps.</span></span>

<span data-ttu-id="167e6-189">**Diagnostic Tools**</span><span class="sxs-lookup"><span data-stu-id="167e6-189">**Diagnostic Tools**</span></span>

<span data-ttu-id="167e6-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span><span class="sxs-lookup"><span data-stu-id="167e6-190">Perform an SAP HANA Health Check through HANA\_Configuration\_Minichecks.</span></span> <span data-ttu-id="167e6-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="167e6-191">This tool returns potentially critical technical issues that should have already been raised as alerts in SAP HANA Studio.</span></span>

<span data-ttu-id="167e6-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span><span class="sxs-lookup"><span data-stu-id="167e6-192">Refer to [SAP Note #1969700 – SQL statement collection for SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) and download the SQL Statements.zip file attached to that note.</span></span> <span data-ttu-id="167e6-193">Store this .zip file on the local hard drive.</span><span class="sxs-lookup"><span data-stu-id="167e6-193">Store this .zip file on the local hard drive.</span></span>

<span data-ttu-id="167e6-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span><span class="sxs-lookup"><span data-stu-id="167e6-194">In SAP HANA Studio, on the **System Information** tab, right-click in the **Name** column and select **Import SQL Statements**.</span></span>

![In SAP HANA Studio, on the System Information tab, right-click in the Name column and select Import SQL Statements](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image7-import-statements-a.png)

<span data-ttu-id="167e6-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span><span class="sxs-lookup"><span data-stu-id="167e6-196">Select the SQL Statements.zip file stored locally, and a folder with the corresponding SQL statements will be imported.</span></span> <span data-ttu-id="167e6-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span><span class="sxs-lookup"><span data-stu-id="167e6-197">At this point, the many different diagnostic checks can be run with these SQL statements.</span></span>

<span data-ttu-id="167e6-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span><span class="sxs-lookup"><span data-stu-id="167e6-198">For example, to test SAP HANA System Replication bandwidth requirements, right-click the **Bandwidth** statement under **Replication: Bandwidth** and select **Open** in SQL Console.</span></span>

<span data-ttu-id="167e6-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span><span class="sxs-lookup"><span data-stu-id="167e6-199">The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed.</span></span>

![The complete SQL statement opens allowing input parameters (modification section) to be changed and then executed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image8-import-statements-b.png)

<span data-ttu-id="167e6-201">Another example is right-clicking on the statements under **Replication: Overview**.</span><span class="sxs-lookup"><span data-stu-id="167e6-201">Another example is right-clicking on the statements under **Replication: Overview**.</span></span> <span data-ttu-id="167e6-202">Select **Execute** from the context menu:</span><span class="sxs-lookup"><span data-stu-id="167e6-202">Select **Execute** from the context menu:</span></span>

![Another example is right-clicking on the statements under Replication: Overview.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image9-import-statements-c.png)

<span data-ttu-id="167e6-205">This results in information that helps with troubleshooting:</span><span class="sxs-lookup"><span data-stu-id="167e6-205">This results in information that helps with troubleshooting:</span></span>

![This will result in information that will help with troubleshooting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image10-import-statements-d.png)

<span data-ttu-id="167e6-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span><span class="sxs-lookup"><span data-stu-id="167e6-207">Do the same for HANA\_Configuration\_Minichecks and check for any _X_ marks in the _C_ (Critical) column.</span></span>

<span data-ttu-id="167e6-208">Sample outputs:</span><span class="sxs-lookup"><span data-stu-id="167e6-208">Sample outputs:</span></span>

<span data-ttu-id="167e6-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span><span class="sxs-lookup"><span data-stu-id="167e6-209">**HANA\_Configuration\_MiniChecks\_Rev102.01+1** for general SAP HANA checks.</span></span>

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 for general SAP HANA checks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image11-configuration-minichecks.png)

<span data-ttu-id="167e6-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span><span class="sxs-lookup"><span data-stu-id="167e6-211">**HANA\_Services\_Overview** for an overview of what SAP HANA services are currently running.</span></span>

![HANA\_Services\_Overview for an overview of what SAP HANA services are currently running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image12-services-overview.png)

<span data-ttu-id="167e6-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span><span class="sxs-lookup"><span data-stu-id="167e6-213">**HANA\_Services\_Statistics** for SAP HANA service information (CPU, memory, etc.).</span></span>

![<span data-ttu-id="167e6-214">HANA\_Services\_Statistics for SAP HANA service information</span><span class="sxs-lookup"><span data-stu-id="167e6-214">HANA\_Services\_Statistics for SAP HANA service information</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image13-services-statistics.png)

<span data-ttu-id="167e6-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="167e6-215">**HANA\_Configuration\_Overview\_Rev110+** for general information on the SAP HANA instance.</span></span>

![HANA\_Configuration\_Overview\_Rev110+ for general information on the SAP HANA instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image14-configuration-overview.png)

<span data-ttu-id="167e6-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span><span class="sxs-lookup"><span data-stu-id="167e6-217">**HANA\_Configuration\_Parameters\_Rev70+** to check SAP HANA parameters.</span></span>

![HANA\_Configuration\_Parameters\_Rev70+ to check SAP HANA parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/troubleshooting-monitoring/image15-configuration-parameters.png)
















