---
title: Manage packet captures with Azure Network Watcher - Azure portal | Microsoft Docs
description: This page explains how to manage the packet capture feature of Network Watcher using Azure portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1092ab89c541e1053d98579be099abae2bb0e1d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548784"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="8e5a9-103">Manage packet captures with Azure Network Watcher using the portal</span><span class="sxs-lookup"><span data-stu-id="8e5a9-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI](network-watcher-packet-capture-manage-cli.md)
> - [REST API](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="8e5a9-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="8e5a9-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="8e5a9-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="8e5a9-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="8e5a9-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="8e5a9-113">This article takes you through the different management tasks that are currently available for packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-113">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="8e5a9-114">**Start a packet capture**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-114">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="8e5a9-115">**Stop a packet capture**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-115">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="8e5a9-116">**Delete a packet capture**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-116">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="8e5a9-117">**Download a packet capture**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-117">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="8e5a9-118">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8e5a9-118">Before you begin</span></span>

<span data-ttu-id="8e5a9-119">This article assumes that you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="8e5a9-119">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="8e5a9-120">An instance of Network Watcher in the region you want to create a packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-120">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="8e5a9-121">A virtual machine with the packet capture extension enabled.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-121">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="8e5a9-124">Packet Capture agent extension through the portal</span><span class="sxs-lookup"><span data-stu-id="8e5a9-124">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="8e5a9-125">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-125">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![agent view][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="8e5a9-127">Packet Capture overview</span><span class="sxs-lookup"><span data-stu-id="8e5a9-127">Packet Capture overview</span></span>

<span data-ttu-id="8e5a9-128">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-128">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="8e5a9-129">The overview page shows a list of all packet captures that exist no matter the state.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-129">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> Packet capture requires connectivity to the storage account over port 443.

![packet capture overview screen][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="8e5a9-132">Start a packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-132">Start a packet capture</span></span>

<span data-ttu-id="8e5a9-133">Click **Add** to create a packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-133">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="8e5a9-134">The properties that can be defined on a packet capture are:</span><span class="sxs-lookup"><span data-stu-id="8e5a9-134">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="8e5a9-135">**Main settings**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-135">**Main settings**</span></span>

- <span data-ttu-id="8e5a9-136">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-136">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="8e5a9-137">**Resource group** - The resource group of the virtual machine that is being targeted.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-137">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="8e5a9-138">**Target virtual machine** - The virtual machine that is running the packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-138">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="8e5a9-139">**Packet capture name** - This value is the name of the packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-139">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="8e5a9-140">**Capture configuration**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-140">**Capture configuration**</span></span>

- <span data-ttu-id="8e5a9-141">**Storage Account** - Determines if packet capture is saved in a storage account.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-141">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="8e5a9-142">**File** - Determines if a packet capture is saved locally on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-142">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="8e5a9-143">**Storage Accounts** - The selected storage account to save the packet capture in.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-143">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="8e5a9-144">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-144">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="8e5a9-145">(Only enabled if **Storage** is selected)</span><span class="sxs-lookup"><span data-stu-id="8e5a9-145">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="8e5a9-146">**Local file path** - The local path on a virtual machine to save the packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-146">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="8e5a9-147">(Only enabled if **File** is selected).</span><span class="sxs-lookup"><span data-stu-id="8e5a9-147">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="8e5a9-148">A Valid path must be supplied</span><span class="sxs-lookup"><span data-stu-id="8e5a9-148">A Valid path must be supplied</span></span>
- <span data-ttu-id="8e5a9-149">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-149">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="8e5a9-150">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-150">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="8e5a9-151">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-151">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="8e5a9-152">Default is 1800 seconds.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-152">Default is 1800 seconds.</span></span>

> [!NOTE]
> Premium storage accounts are currently not supported for storing packet captures.

<span data-ttu-id="8e5a9-154">**Filtering (Optional)**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-154">**Filtering (Optional)**</span></span>

- <span data-ttu-id="8e5a9-155">**Protocol** - The protocol to filter for the packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-155">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="8e5a9-156">The available values are TCP, UDP, and Any.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-156">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="8e5a9-157">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-157">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="8e5a9-158">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-158">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="8e5a9-159">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-159">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="8e5a9-160">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-160">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> Port and IP address values can be a single value, range of values, or a set. (that is, 80-1024 for port) You can define as many filters as you want.

<span data-ttu-id="8e5a9-163">Once the values are filled out, click **OK** to create the packet capture.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-163">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![create a packet capture][2]

<span data-ttu-id="8e5a9-165">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-165">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="8e5a9-166">You can also manually stop the packet captures sessions.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-166">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="8e5a9-167">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-167">Delete a packet capture</span></span>

<span data-ttu-id="8e5a9-168">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-168">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![delete a packet capture][3]

> [!NOTE]
> Deleting a packet capture does not delete the file in the storage account.

<span data-ttu-id="8e5a9-171">You are asked to confirm you want to delete the packet capture, click **Yes**</span><span class="sxs-lookup"><span data-stu-id="8e5a9-171">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![confirmation][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="8e5a9-173">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-173">Stop a packet capture</span></span>

<span data-ttu-id="8e5a9-174">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-174">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="8e5a9-175">Download a packet capture</span><span class="sxs-lookup"><span data-stu-id="8e5a9-175">Download a packet capture</span></span>

<span data-ttu-id="8e5a9-176">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-176">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="8e5a9-177">The storage location of the packet capture is defined at creation of the session.</span><span class="sxs-lookup"><span data-stu-id="8e5a9-177">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="8e5a9-178">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="8e5a9-178">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="8e5a9-179">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="8e5a9-179">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="8e5a9-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e5a9-180">Next steps</span></span>

<span data-ttu-id="8e5a9-181">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="8e5a9-181">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8e5a9-182">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8e5a9-182">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-packet-capture-manage-portal/agent.png


















