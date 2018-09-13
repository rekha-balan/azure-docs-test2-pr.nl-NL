---
title: Introduction to Packet capture in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher packet capture capability
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1565f731074be416956063ac89cbc0e179e608df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563045"
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="90ae6-103">Introduction to variable packet capture in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="90ae6-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="90ae6-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90ae6-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="90ae6-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span><span class="sxs-lookup"><span data-stu-id="90ae6-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="90ae6-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="90ae6-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="90ae6-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="90ae6-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="90ae6-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="90ae6-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="90ae6-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="90ae6-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="90ae6-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span><span class="sxs-lookup"><span data-stu-id="90ae6-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="90ae6-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="90ae6-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="90ae6-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span><span class="sxs-lookup"><span data-stu-id="90ae6-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="90ae6-113">The captured data is stored in the local disk or a storage blob.</span><span class="sxs-lookup"><span data-stu-id="90ae6-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="90ae6-114">There is a limit of 10 packet capture sessions per region per subscription.</span><span class="sxs-lookup"><span data-stu-id="90ae6-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="90ae6-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span><span class="sxs-lookup"><span data-stu-id="90ae6-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90ae6-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="90ae6-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="90ae6-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="90ae6-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="90ae6-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span><span class="sxs-lookup"><span data-stu-id="90ae6-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="90ae6-119">**Capture configuration**</span><span class="sxs-lookup"><span data-stu-id="90ae6-119">**Capture configuration**</span></span>

|<span data-ttu-id="90ae6-120">Property</span><span class="sxs-lookup"><span data-stu-id="90ae6-120">Property</span></span>|<span data-ttu-id="90ae6-121">Description</span><span class="sxs-lookup"><span data-stu-id="90ae6-121">Description</span></span>|
|---|---|
|<span data-ttu-id="90ae6-122">**Maximum bytes per packet (bytes)**</span><span class="sxs-lookup"><span data-stu-id="90ae6-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="90ae6-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span><span class="sxs-lookup"><span data-stu-id="90ae6-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="90ae6-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span><span class="sxs-lookup"><span data-stu-id="90ae6-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="90ae6-125">If you need only the IPv4 header – indicate 60 here</span><span class="sxs-lookup"><span data-stu-id="90ae6-125">If you need only the IPv4 header – indicate 60 here</span></span> |
|<span data-ttu-id="90ae6-126">**Maximum bytes per session (bytes)**</span><span class="sxs-lookup"><span data-stu-id="90ae6-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="90ae6-127">Total number of bytes in that are captured, once the value is reached the session ends.</span><span class="sxs-lookup"><span data-stu-id="90ae6-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="90ae6-128">**Time limit (seconds)**</span><span class="sxs-lookup"><span data-stu-id="90ae6-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="90ae6-129">Sets a time constraint on the packet capture session.</span><span class="sxs-lookup"><span data-stu-id="90ae6-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="90ae6-130">The default value is 18000 seconds or 5 hours.</span><span class="sxs-lookup"><span data-stu-id="90ae6-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="90ae6-131">**Filtering (optional)**</span><span class="sxs-lookup"><span data-stu-id="90ae6-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="90ae6-132">Property</span><span class="sxs-lookup"><span data-stu-id="90ae6-132">Property</span></span>|<span data-ttu-id="90ae6-133">Description</span><span class="sxs-lookup"><span data-stu-id="90ae6-133">Description</span></span>|
|---|---|
|<span data-ttu-id="90ae6-134">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="90ae6-134">**Protocol**</span></span> | <span data-ttu-id="90ae6-135">The protocol to filter for the packet capture.</span><span class="sxs-lookup"><span data-stu-id="90ae6-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="90ae6-136">The available values are TCP, UDP, and All.</span><span class="sxs-lookup"><span data-stu-id="90ae6-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="90ae6-137">**Local IP address**</span><span class="sxs-lookup"><span data-stu-id="90ae6-137">**Local IP address**</span></span> | <span data-ttu-id="90ae6-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="90ae6-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="90ae6-139">**Local port**</span><span class="sxs-lookup"><span data-stu-id="90ae6-139">**Local port**</span></span> | <span data-ttu-id="90ae6-140">This value filters the packet capture to packets where the local port matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="90ae6-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="90ae6-141">**Remote IP address**</span><span class="sxs-lookup"><span data-stu-id="90ae6-141">**Remote IP address**</span></span> | <span data-ttu-id="90ae6-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="90ae6-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="90ae6-143">**Remote port**</span><span class="sxs-lookup"><span data-stu-id="90ae6-143">**Remote port**</span></span> | <span data-ttu-id="90ae6-144">This value filters the packet capture to packets where the remote port matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="90ae6-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="90ae6-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="90ae6-145">Next steps</span></span>

<span data-ttu-id="90ae6-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="90ae6-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="90ae6-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="90ae6-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-overview/figure1.png














