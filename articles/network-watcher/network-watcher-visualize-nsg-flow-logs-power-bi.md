---
title: Visualizing Azure Network Security Group flow logs with Power BI | Microsoft Docs
description: This page describes how to visualize NSG flow logs with Power BI.
services: network-watcher
documentationcenter: na
author: mattreatMSFT
manager: vitinnan
editor: ''
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: mareat
ms.openlocfilehash: 8f5bb54e12348fd915b2c4413bbacdc083a2a879
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811784"
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="ff83f-103">Visualizing Network Security Group flow logs with Power BI</span><span class="sxs-lookup"><span data-stu-id="ff83f-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="ff83f-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="ff83f-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="ff83f-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="ff83f-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="ff83f-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span><span class="sxs-lookup"><span data-stu-id="ff83f-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="ff83f-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span><span class="sxs-lookup"><span data-stu-id="ff83f-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="ff83f-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="ff83f-108">Scenario</span></span>

<span data-ttu-id="ff83f-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span><span class="sxs-lookup"><span data-stu-id="ff83f-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="ff83f-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span><span class="sxs-lookup"><span data-stu-id="ff83f-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="ff83f-111">Using the visuals supplied in the template you can examine:</span><span class="sxs-lookup"><span data-stu-id="ff83f-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="ff83f-112">Top Talkers</span><span class="sxs-lookup"><span data-stu-id="ff83f-112">Top Talkers</span></span>
* <span data-ttu-id="ff83f-113">Time Series Flow Data by direction and rule decision</span><span class="sxs-lookup"><span data-stu-id="ff83f-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="ff83f-114">Flows by Network Interface MAC address</span><span class="sxs-lookup"><span data-stu-id="ff83f-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="ff83f-115">Flows by NSG and Rule</span><span class="sxs-lookup"><span data-stu-id="ff83f-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="ff83f-116">Flows by Destination Port</span><span class="sxs-lookup"><span data-stu-id="ff83f-116">Flows by Destination Port</span></span>

<span data-ttu-id="ff83f-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="ff83f-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="ff83f-118">Setup</span><span class="sxs-lookup"><span data-stu-id="ff83f-118">Setup</span></span>

<span data-ttu-id="ff83f-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span><span class="sxs-lookup"><span data-stu-id="ff83f-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="ff83f-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ff83f-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="ff83f-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span><span class="sxs-lookup"><span data-stu-id="ff83f-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Visio diagram][1]

### <a name="steps"></a><span data-ttu-id="ff83f-123">Steps</span><span class="sxs-lookup"><span data-stu-id="ff83f-123">Steps</span></span>

1. <span data-ttu-id="ff83f-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="ff83f-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="ff83f-125">Enter the required Query parameters</span><span class="sxs-lookup"><span data-stu-id="ff83f-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="ff83f-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span><span class="sxs-lookup"><span data-stu-id="ff83f-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="ff83f-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span><span class="sxs-lookup"><span data-stu-id="ff83f-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="ff83f-128">For example, if 50 is specified, the 50 latest log files.</span><span class="sxs-lookup"><span data-stu-id="ff83f-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="ff83f-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span><span class="sxs-lookup"><span data-stu-id="ff83f-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![power BI main][2]

1. <span data-ttu-id="ff83f-131">Enter the Access Key for your storage account.</span><span class="sxs-lookup"><span data-stu-id="ff83f-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="ff83f-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span><span class="sxs-lookup"><span data-stu-id="ff83f-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="ff83f-133">Click **Connect** then apply changes.</span><span class="sxs-lookup"><span data-stu-id="ff83f-133">Click **Connect** then apply changes.</span></span>

    ![access keys][3]

    ![access key 2][4]

4.  <span data-ttu-id="ff83f-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span><span class="sxs-lookup"><span data-stu-id="ff83f-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="ff83f-137">Understanding the visuals</span><span class="sxs-lookup"><span data-stu-id="ff83f-137">Understanding the visuals</span></span>

<span data-ttu-id="ff83f-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span><span class="sxs-lookup"><span data-stu-id="ff83f-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="ff83f-139">The following images show a sample of what the dashboard looks like when populated with data.</span><span class="sxs-lookup"><span data-stu-id="ff83f-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="ff83f-140">Below we examine each visual in greater detail</span><span class="sxs-lookup"><span data-stu-id="ff83f-140">Below we examine each visual in greater detail</span></span> 

![powerbi][5]
 
<span data-ttu-id="ff83f-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span><span class="sxs-lookup"><span data-stu-id="ff83f-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="ff83f-143">The size of the boxes corresponds to the relative number of connections.</span><span class="sxs-lookup"><span data-stu-id="ff83f-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="ff83f-145">The following time series graphs show the number of flows over the period.</span><span class="sxs-lookup"><span data-stu-id="ff83f-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="ff83f-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span><span class="sxs-lookup"><span data-stu-id="ff83f-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="ff83f-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span><span class="sxs-lookup"><span data-stu-id="ff83f-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="ff83f-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span><span class="sxs-lookup"><span data-stu-id="ff83f-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="ff83f-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="ff83f-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="ff83f-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span><span class="sxs-lookup"><span data-stu-id="ff83f-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="ff83f-153">With this information, you can view the most commonly used destination ports used within the specified period.</span><span class="sxs-lookup"><span data-stu-id="ff83f-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![donut][9]

<span data-ttu-id="ff83f-155">The following bar chart shows the Flow by NSG and Rule.</span><span class="sxs-lookup"><span data-stu-id="ff83f-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="ff83f-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span><span class="sxs-lookup"><span data-stu-id="ff83f-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="ff83f-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span><span class="sxs-lookup"><span data-stu-id="ff83f-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="ff83f-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span><span class="sxs-lookup"><span data-stu-id="ff83f-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="ff83f-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span><span class="sxs-lookup"><span data-stu-id="ff83f-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="ff83f-163">You can filter on your resource groups, NSGs, and rules.</span><span class="sxs-lookup"><span data-stu-id="ff83f-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="ff83f-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span><span class="sxs-lookup"><span data-stu-id="ff83f-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![slicers][13]

## <a name="conclusion"></a><span data-ttu-id="ff83f-166">Conclusion</span><span class="sxs-lookup"><span data-stu-id="ff83f-166">Conclusion</span></span>

<span data-ttu-id="ff83f-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span><span class="sxs-lookup"><span data-stu-id="ff83f-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="ff83f-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span><span class="sxs-lookup"><span data-stu-id="ff83f-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="ff83f-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span><span class="sxs-lookup"><span data-stu-id="ff83f-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="ff83f-170">Feel free to customize this template for your needs.</span><span class="sxs-lookup"><span data-stu-id="ff83f-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="ff83f-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span><span class="sxs-lookup"><span data-stu-id="ff83f-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="ff83f-172">Notes</span><span class="sxs-lookup"><span data-stu-id="ff83f-172">Notes</span></span>

* <span data-ttu-id="ff83f-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="ff83f-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="ff83f-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span><span class="sxs-lookup"><span data-stu-id="ff83f-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="ff83f-175">The provided template is not recommended for use with more than 1 GB of logs.</span><span class="sxs-lookup"><span data-stu-id="ff83f-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="ff83f-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span><span class="sxs-lookup"><span data-stu-id="ff83f-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff83f-177">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ff83f-177">Next Steps</span></span>

<span data-ttu-id="ff83f-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ff83f-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
