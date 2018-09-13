---
title: Packet inspection with Azure Network Watcher | Microsoft Docs
description: This article describes how to use Network Watcher to perform deep packet inspection collected from a VM
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fa5e79c893e68e859708d7d55de6c02afe997a4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669072"
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="5c021-103">Packet inspection with Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5c021-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="5c021-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span><span class="sxs-lookup"><span data-stu-id="5c021-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span></span> <span data-ttu-id="5c021-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span><span class="sxs-lookup"><span data-stu-id="5c021-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span></span> <span data-ttu-id="5c021-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span><span class="sxs-lookup"><span data-stu-id="5c021-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="5c021-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span><span class="sxs-lookup"><span data-stu-id="5c021-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="5c021-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span><span class="sxs-lookup"><span data-stu-id="5c021-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="5c021-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span><span class="sxs-lookup"><span data-stu-id="5c021-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5c021-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5c021-110">Before you begin</span></span>

<span data-ttu-id="5c021-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span><span class="sxs-lookup"><span data-stu-id="5c021-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="5c021-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span><span class="sxs-lookup"><span data-stu-id="5c021-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="5c021-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span><span class="sxs-lookup"><span data-stu-id="5c021-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span></span>

<span data-ttu-id="5c021-114">This scenario assumes you already ran a packet capture on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5c021-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="5c021-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="5c021-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="5c021-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="5c021-116">Scenario</span></span>

<span data-ttu-id="5c021-117">In this scenario, you:</span><span class="sxs-lookup"><span data-stu-id="5c021-117">In this scenario, you:</span></span>

* <span data-ttu-id="5c021-118">Review a packet capture</span><span class="sxs-lookup"><span data-stu-id="5c021-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="5c021-119">Calculate network latency</span><span class="sxs-lookup"><span data-stu-id="5c021-119">Calculate network latency</span></span>

<span data-ttu-id="5c021-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span><span class="sxs-lookup"><span data-stu-id="5c021-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="5c021-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span><span class="sxs-lookup"><span data-stu-id="5c021-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span></span> <span data-ttu-id="5c021-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span><span class="sxs-lookup"><span data-stu-id="5c021-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span></span> <span data-ttu-id="5c021-123">This latency is referred to as the Round Trip Time (RTT).</span><span class="sxs-lookup"><span data-stu-id="5c021-123">This latency is referred to as the Round Trip Time (RTT).</span></span> <span data-ttu-id="5c021-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span><span class="sxs-lookup"><span data-stu-id="5c021-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span></span> <span data-ttu-id="5c021-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="5c021-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="5c021-126">Step 1</span><span class="sxs-lookup"><span data-stu-id="5c021-126">Step 1</span></span>

<span data-ttu-id="5c021-127">Launch WireShark</span><span class="sxs-lookup"><span data-stu-id="5c021-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="5c021-128">Step 2</span><span class="sxs-lookup"><span data-stu-id="5c021-128">Step 2</span></span>

<span data-ttu-id="5c021-129">Load the **.cap** file from your packet capture.</span><span class="sxs-lookup"><span data-stu-id="5c021-129">Load the **.cap** file from your packet capture.</span></span> <span data-ttu-id="5c021-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span><span class="sxs-lookup"><span data-stu-id="5c021-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="5c021-131">Step 3</span><span class="sxs-lookup"><span data-stu-id="5c021-131">Step 3</span></span>

<span data-ttu-id="5c021-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span><span class="sxs-lookup"><span data-stu-id="5c021-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span></span> <span data-ttu-id="5c021-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span><span class="sxs-lookup"><span data-stu-id="5c021-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="5c021-134">They are named for flags set in the TCP header.</span><span class="sxs-lookup"><span data-stu-id="5c021-134">They are named for flags set in the TCP header.</span></span> <span data-ttu-id="5c021-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span><span class="sxs-lookup"><span data-stu-id="5c021-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="5c021-136">The [SYN] packet is sent by the client.</span><span class="sxs-lookup"><span data-stu-id="5c021-136">The [SYN] packet is sent by the client.</span></span> <span data-ttu-id="5c021-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span><span class="sxs-lookup"><span data-stu-id="5c021-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span></span> <span data-ttu-id="5c021-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span><span class="sxs-lookup"><span data-stu-id="5c021-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span></span>

<span data-ttu-id="5c021-139">Using WireShark this value is calculated for us.</span><span class="sxs-lookup"><span data-stu-id="5c021-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="5c021-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span><span class="sxs-lookup"><span data-stu-id="5c021-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span></span>

<span data-ttu-id="5c021-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span><span class="sxs-lookup"><span data-stu-id="5c021-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span></span>

<span data-ttu-id="5c021-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span><span class="sxs-lookup"><span data-stu-id="5c021-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span></span>

![figure 7][7]

### <a name="step-4"></a><span data-ttu-id="5c021-144">Step 4</span><span class="sxs-lookup"><span data-stu-id="5c021-144">Step 4</span></span>

<span data-ttu-id="5c021-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span><span class="sxs-lookup"><span data-stu-id="5c021-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span></span> <span data-ttu-id="5c021-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span><span class="sxs-lookup"><span data-stu-id="5c021-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="5c021-147">You will then see the RTT displayed.</span><span class="sxs-lookup"><span data-stu-id="5c021-147">You will then see the RTT displayed.</span></span> <span data-ttu-id="5c021-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="5c021-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![figure 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="5c021-150">Unwanted protocols</span><span class="sxs-lookup"><span data-stu-id="5c021-150">Unwanted protocols</span></span>

<span data-ttu-id="5c021-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="5c021-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="5c021-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span><span class="sxs-lookup"><span data-stu-id="5c021-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span></span> <span data-ttu-id="5c021-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span><span class="sxs-lookup"><span data-stu-id="5c021-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span></span>

<span data-ttu-id="5c021-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span><span class="sxs-lookup"><span data-stu-id="5c021-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="5c021-155">Step 1</span><span class="sxs-lookup"><span data-stu-id="5c021-155">Step 1</span></span>

<span data-ttu-id="5c021-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span><span class="sxs-lookup"><span data-stu-id="5c021-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![protocol hierarchy menu][2]

<span data-ttu-id="5c021-158">The protocol hierarchy window appears.</span><span class="sxs-lookup"><span data-stu-id="5c021-158">The protocol hierarchy window appears.</span></span> <span data-ttu-id="5c021-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span><span class="sxs-lookup"><span data-stu-id="5c021-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span></span> <span data-ttu-id="5c021-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span><span class="sxs-lookup"><span data-stu-id="5c021-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![protocol hierachy opened][3]

<span data-ttu-id="5c021-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span><span class="sxs-lookup"><span data-stu-id="5c021-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span></span> <span data-ttu-id="5c021-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span><span class="sxs-lookup"><span data-stu-id="5c021-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="5c021-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span><span class="sxs-lookup"><span data-stu-id="5c021-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="5c021-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span><span class="sxs-lookup"><span data-stu-id="5c021-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="5c021-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="5c021-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="5c021-167">Finding top destinations and ports</span><span class="sxs-lookup"><span data-stu-id="5c021-167">Finding top destinations and ports</span></span>

<span data-ttu-id="5c021-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span><span class="sxs-lookup"><span data-stu-id="5c021-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="5c021-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span><span class="sxs-lookup"><span data-stu-id="5c021-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="5c021-170">Step 1</span><span class="sxs-lookup"><span data-stu-id="5c021-170">Step 1</span></span>

<span data-ttu-id="5c021-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span><span class="sxs-lookup"><span data-stu-id="5c021-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![packet capture window][4]

### <a name="step-2"></a><span data-ttu-id="5c021-173">Step 2</span><span class="sxs-lookup"><span data-stu-id="5c021-173">Step 2</span></span>

<span data-ttu-id="5c021-174">As we look through the results a line stands out, there were multiple connections on port 111.</span><span class="sxs-lookup"><span data-stu-id="5c021-174">As we look through the results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="5c021-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span><span class="sxs-lookup"><span data-stu-id="5c021-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="5c021-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span><span class="sxs-lookup"><span data-stu-id="5c021-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span></span>

![figure 5][5]

### <a name="step-3"></a><span data-ttu-id="5c021-178">Step 3</span><span class="sxs-lookup"><span data-stu-id="5c021-178">Step 3</span></span>

<span data-ttu-id="5c021-179">Now that we have determined an out of place port we can filter our capture based on the port.</span><span class="sxs-lookup"><span data-stu-id="5c021-179">Now that we have determined an out of place port we can filter our capture based on the port.</span></span>

<span data-ttu-id="5c021-180">The filter in this scenario would be:</span><span class="sxs-lookup"><span data-stu-id="5c021-180">The filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="5c021-181">We enter the filter text from above in the filter textbox and hit enter.</span><span class="sxs-lookup"><span data-stu-id="5c021-181">We enter the filter text from above in the filter textbox and hit enter.</span></span>

![figure 6][6]

<span data-ttu-id="5c021-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span><span class="sxs-lookup"><span data-stu-id="5c021-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span></span> <span data-ttu-id="5c021-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span><span class="sxs-lookup"><span data-stu-id="5c021-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span></span> <span data-ttu-id="5c021-185">With this information we can take the appropriate action.</span><span class="sxs-lookup"><span data-stu-id="5c021-185">With this information we can take the appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c021-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c021-186">Next steps</span></span>

<span data-ttu-id="5c021-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5c021-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-deep-packet-inspection/figure8.png





















