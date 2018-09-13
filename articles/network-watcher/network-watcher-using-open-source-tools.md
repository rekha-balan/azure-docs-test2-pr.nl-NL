---
title: Visualize network traffic patterns with Azure Network Watcher and open source tools | Microsoft Docs
description: This page describes how to use Network Watcher packet capture with Capanalysis to visualize traffic patterns to and from your VMs.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 33714f7849312a15261c5ec9a261a0e4e7c32272
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553456"
---
# <a name="visualize-network-traffic-patterns-to-and-from-your-vms-using-open-source-tools"></a><span data-ttu-id="bc1d8-103">Visualize network traffic patterns to and from your VMs using open source tools</span><span class="sxs-lookup"><span data-stu-id="bc1d8-103">Visualize network traffic patterns to and from your VMs using open source tools</span></span>

<span data-ttu-id="bc1d8-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-104">Packet captures contain network data that allow you to perform network forensics and deep packet inspection.</span></span> <span data-ttu-id="bc1d8-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-105">There are many opens source tools you can use to analyze packet captures to gain insights about your network.</span></span> <span data-ttu-id="bc1d8-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="bc1d8-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-107">Visualizing packet capture data is a valuable way to quickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="bc1d8-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="bc1d8-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-109">Azure’s Network Watcher provides you the ability to capture this valuable data by allowing you to perform packet captures on your network.</span></span> <span data-ttu-id="bc1d8-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-110">In this article, we provide a walkthrough of how to visualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="bc1d8-111">Scenario</span><span class="sxs-lookup"><span data-stu-id="bc1d8-111">Scenario</span></span>

<span data-ttu-id="bc1d8-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-112">You have a simple web application deployed on a VM in Azure want to use open source tools to visualize its network traffic to quickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="bc1d8-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="bc1d8-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-114">CapAnalysis can then ingest the packet capture directly from the storage blob and visualize its contents.</span></span>

![scenario][1]

## <a name="steps"></a><span data-ttu-id="bc1d8-116">Steps</span><span class="sxs-lookup"><span data-stu-id="bc1d8-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="bc1d8-117">Install CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="bc1d8-117">Install CapAnalysis</span></span>

<span data-ttu-id="bc1d8-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-118">To install CapAnalysis on a virtual machine, you can refer to the official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="bc1d8-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-119">In order access CapAnalysis remotely, we need to open port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="bc1d8-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="bc1d8-120">For more about creating rules in Network Security Groups, refer to [Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="bc1d8-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="bc1d8-121">Once the rule has been successfully added, you should be able to access CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-to-start-a-packet-capture-session"></a><span data-ttu-id="bc1d8-122">Use Azure Network Watcher to start a packet capture session</span><span class="sxs-lookup"><span data-stu-id="bc1d8-122">Use Azure Network Watcher to start a packet capture session</span></span>

<span data-ttu-id="bc1d8-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-123">Network Watcher allows you to capture packets to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="bc1d8-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-124">You can refer to the instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) to start a packet capture session.</span></span> <span data-ttu-id="bc1d8-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-125">This packet capture can be stored in a storage blob to be accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-to-capanalysis"></a><span data-ttu-id="bc1d8-126">Upload a packet capture to CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="bc1d8-126">Upload a packet capture to CapAnalysis</span></span>
<span data-ttu-id="bc1d8-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-127">You can directly upload a packet capture taken by network watcher using the “Import from URL” tab and providing a link to the storage blob where the packet capture is stored.</span></span>

<span data-ttu-id="bc1d8-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-128">When providing a link to CapAnalysis, make sure to append a SAS token to the storage blob URL.</span></span>  <span data-ttu-id="bc1d8-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-129">To do this, navigate to Shared access signature from the storage account, designate the allowed permissions, and press the Generate SAS button to create a token.</span></span> <span data-ttu-id="bc1d8-130">You can then append this SAS token to the packet capture storage blob URL.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-130">You can then append this SAS token to the packet capture storage blob URL.</span></span>

<span data-ttu-id="bc1d8-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="bc1d8-131">The resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="bc1d8-132">Analyzing packet captures</span><span class="sxs-lookup"><span data-stu-id="bc1d8-132">Analyzing packet captures</span></span>

<span data-ttu-id="bc1d8-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-133">CapAnalysis offers various options to visualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="bc1d8-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="bc1d8-135">A few of these features are shown in the following list:</span><span class="sxs-lookup"><span data-stu-id="bc1d8-135">A few of these features are shown in the following list:</span></span>

1. <span data-ttu-id="bc1d8-136">Flow Tables</span><span class="sxs-lookup"><span data-stu-id="bc1d8-136">Flow Tables</span></span>

    <span data-ttu-id="bc1d8-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-137">This table gives you the list of flows in the packet data, the time stamp associated with the flows and the various protocols associated with the flow, as well as source and destination IP.</span></span>

    ![capanalysis flow page][5]

1. <span data-ttu-id="bc1d8-139">Protocol Overview</span><span class="sxs-lookup"><span data-stu-id="bc1d8-139">Protocol Overview</span></span>

    <span data-ttu-id="bc1d8-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-140">This pane allows you to quickly see the distribution of network traffic over the various protocols and geographies.</span></span>

    ![capanalysis protocol overview][6]

1. <span data-ttu-id="bc1d8-142">Statistics</span><span class="sxs-lookup"><span data-stu-id="bc1d8-142">Statistics</span></span>

    <span data-ttu-id="bc1d8-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-143">This pane allows you to view network traffic statistics – bytes sent and received from source and destination IPs, flows for each of the source and destination IPs, protocol used for various flows, and the duration of flows.</span></span>

    ![capanalysis statistics][7]

1. <span data-ttu-id="bc1d8-145">Geomap</span><span class="sxs-lookup"><span data-stu-id="bc1d8-145">Geomap</span></span>

    <span data-ttu-id="bc1d8-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-146">This pane provides you with a map view of your network traffic, with colors scaling to the volume of traffic from each country.</span></span> <span data-ttu-id="bc1d8-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-147">You can select highlighted countries to view additional flow statistics such as the proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="bc1d8-149">Filters</span><span class="sxs-lookup"><span data-stu-id="bc1d8-149">Filters</span></span>

    <span data-ttu-id="bc1d8-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="bc1d8-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-151">For example, you can choose to filter the data by protocol to gain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="bc1d8-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) to learn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bc1d8-154">Conclusion</span><span class="sxs-lookup"><span data-stu-id="bc1d8-154">Conclusion</span></span>

<span data-ttu-id="bc1d8-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-155">Network Watcher’s packet capture feature allows you to capture the data necessary to perform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="bc1d8-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="bc1d8-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span><span class="sxs-lookup"><span data-stu-id="bc1d8-157">By using open source tools such as CapAnalysis to visualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1d8-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc1d8-158">Next steps</span></span>

<span data-ttu-id="bc1d8-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bc1d8-159">To learn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="bc1d8-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references--></span><span class="sxs-lookup"><span data-stu-id="bc1d8-160">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references--></span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-using-open-source-tools/figure11.png











