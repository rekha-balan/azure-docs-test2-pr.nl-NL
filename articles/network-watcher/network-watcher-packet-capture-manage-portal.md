---
title: Manage packet captures with Azure Network Watcher - Azure portal | Microsoft Docs
description: Learn how to manage the packet capture feature of Network Watcher using the Azure portal.
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/10/2018
ms.author: jdial
ms.openlocfilehash: 827a3c2f831c8e8fb459e494dcad58e3661e78bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818381"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="f0cfb-103">Manage packet captures with Azure Network Watcher using the portal</span><span class="sxs-lookup"><span data-stu-id="f0cfb-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

<span data-ttu-id="f0cfb-104">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-104">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="f0cfb-105">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-105">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="f0cfb-106">Packet capture helps to diagnose network anomalies, both reactively, and proactively.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-106">Packet capture helps to diagnose network anomalies, both reactively, and proactively.</span></span> <span data-ttu-id="f0cfb-107">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communication, and much more.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-107">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communication, and much more.</span></span> <span data-ttu-id="f0cfb-108">Being able to remotely trigger packet captures, eases the burden of running a packet capture manually on a desired virtual machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-108">Being able to remotely trigger packet captures, eases the burden of running a packet capture manually on a desired virtual machine, which saves valuable time.</span></span>

<span data-ttu-id="f0cfb-109">In this article, you learn to start, stop, download, and delete a packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-109">In this article, you learn to start, stop, download, and delete a packet capture.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f0cfb-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f0cfb-110">Before you begin</span></span>

<span data-ttu-id="f0cfb-111">Packet capture requires the following connectivity:</span><span class="sxs-lookup"><span data-stu-id="f0cfb-111">Packet capture requires the following connectivity:</span></span>
* <span data-ttu-id="f0cfb-112">Outbound connectivity to a storage account over port 443.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-112">Outbound connectivity to a storage account over port 443.</span></span>
* <span data-ttu-id="f0cfb-113">Inbound and outbound connectivity to 169.254.169.254</span><span class="sxs-lookup"><span data-stu-id="f0cfb-113">Inbound and outbound connectivity to 169.254.169.254</span></span>
* <span data-ttu-id="f0cfb-114">Inbound and outbound connectivity to 168.63.129.16</span><span class="sxs-lookup"><span data-stu-id="f0cfb-114">Inbound and outbound connectivity to 168.63.129.16</span></span>

<span data-ttu-id="f0cfb-115">If a network security group is associated to the network interface, or subnet that the network interface is in, ensure that rules exist that allow the previous ports.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-115">If a network security group is associated to the network interface, or subnet that the network interface is in, ensure that rules exist that allow the previous ports.</span></span> 

## <a name="start-a-packet-capture"></a><span data-ttu-id="f0cfb-116">Start a packet capture</span><span class="sxs-lookup"><span data-stu-id="f0cfb-116">Start a packet capture</span></span>

1. <span data-ttu-id="f0cfb-117">In your browser, navigate to the [Azure portal](https://portal.azure.com) and select **All services**, and then select **Network Watcher** in the **Networking section**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-117">In your browser, navigate to the [Azure portal](https://portal.azure.com) and select **All services**, and then select **Network Watcher** in the **Networking section**.</span></span>
2. <span data-ttu-id="f0cfb-118">Select **Packet capture** under **Network diagnostic tools**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-118">Select **Packet capture** under **Network diagnostic tools**.</span></span> <span data-ttu-id="f0cfb-119">Any existing packet captures are listed, regardless of their status.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-119">Any existing packet captures are listed, regardless of their status.</span></span>
3. <span data-ttu-id="f0cfb-120">Select **Add** to create a packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-120">Select **Add** to create a packet capture.</span></span> <span data-ttu-id="f0cfb-121">You can select values for the following properties:</span><span class="sxs-lookup"><span data-stu-id="f0cfb-121">You can select values for the following properties:</span></span>
   - <span data-ttu-id="f0cfb-122">**Subscription**: The subscription that the virtual machine you want to create the packet capture for is in.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-122">**Subscription**: The subscription that the virtual machine you want to create the packet capture for is in.</span></span>
   - <span data-ttu-id="f0cfb-123">**Resource group**: The resource group of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-123">**Resource group**: The resource group of the virtual machine.</span></span>
   - <span data-ttu-id="f0cfb-124">**Target virtual machine**: The virtual machine that you want to create the packet capture for.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-124">**Target virtual machine**: The virtual machine that you want to create the packet capture for.</span></span>
   - <span data-ttu-id="f0cfb-125">**Packet capture name**: A name for the packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-125">**Packet capture name**: A name for the packet capture.</span></span>
   - <span data-ttu-id="f0cfb-126">**Storage account or file**: Select **Storage account**, **File**, or both.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-126">**Storage account or file**: Select **Storage account**, **File**, or both.</span></span> <span data-ttu-id="f0cfb-127">If you select **File**, the capture is written to a path within the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-127">If you select **File**, the capture is written to a path within the virtual machine.</span></span>
   - <span data-ttu-id="f0cfb-128">**Local file path**: The local path on the virtual machine where the packet capture will be saved (valid only when *File* is selected).</span><span class="sxs-lookup"><span data-stu-id="f0cfb-128">**Local file path**: The local path on the virtual machine where the packet capture will be saved (valid only when *File* is selected).</span></span> <span data-ttu-id="f0cfb-129">The path must be a valid path.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-129">The path must be a valid path.</span></span> <span data-ttu-id="f0cfb-130">If you are using a Linux virtual machine, the path must start with */var/captures*.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-130">If you are using a Linux virtual machine, the path must start with */var/captures*.</span></span>
   - <span data-ttu-id="f0cfb-131">**Storage accounts**: Select an existing storage account, if you selected *Storage account*.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-131">**Storage accounts**: Select an existing storage account, if you selected *Storage account*.</span></span> <span data-ttu-id="f0cfb-132">This option is only available if you selected **Storage**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-132">This option is only available if you selected **Storage**.</span></span>
   
     > [!NOTE]
     > <span data-ttu-id="f0cfb-133">Premium storage accounts are currently not supported for storing packet captures.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-133">Premium storage accounts are currently not supported for storing packet captures.</span></span>

   - <span data-ttu-id="f0cfb-134">**Maximum bytes per packet**: The number of bytes from each packet that are captured.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-134">**Maximum bytes per packet**: The number of bytes from each packet that are captured.</span></span> <span data-ttu-id="f0cfb-135">If left blank, all bytes are captured.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-135">If left blank, all bytes are captured.</span></span>
   - <span data-ttu-id="f0cfb-136">**Maximum bytes per session**: The total number of bytes that are captured.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-136">**Maximum bytes per session**: The total number of bytes that are captured.</span></span> <span data-ttu-id="f0cfb-137">Once the value is reached the packet capture stops.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-137">Once the value is reached the packet capture stops.</span></span>
   - <span data-ttu-id="f0cfb-138">**Time limit (seconds)**: The time limit before the packet capture is stopped.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-138">**Time limit (seconds)**: The time limit before the packet capture is stopped.</span></span> <span data-ttu-id="f0cfb-139">The default is 18,000 seconds.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-139">The default is 18,000 seconds.</span></span>
   - <span data-ttu-id="f0cfb-140">Filtering (Optional).</span><span class="sxs-lookup"><span data-stu-id="f0cfb-140">Filtering (Optional).</span></span> <span data-ttu-id="f0cfb-141">Select **+ Add filter**</span><span class="sxs-lookup"><span data-stu-id="f0cfb-141">Select **+ Add filter**</span></span>
     - <span data-ttu-id="f0cfb-142">**Protocol**: The protocol to filter for the packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-142">**Protocol**: The protocol to filter for the packet capture.</span></span> <span data-ttu-id="f0cfb-143">The available values are TCP, UDP, and Any.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-143">The available values are TCP, UDP, and Any.</span></span>
     - <span data-ttu-id="f0cfb-144">**Local IP address**: Filters the packet capture for packets where the local IP address matches this value.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-144">**Local IP address**: Filters the packet capture for packets where the local IP address matches this value.</span></span>
     - <span data-ttu-id="f0cfb-145">**Local port**: Filters the packet capture for packets where the local port matches this value.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-145">**Local port**: Filters the packet capture for packets where the local port matches this value.</span></span>
     - <span data-ttu-id="f0cfb-146">**Remote IP address**: Filters the packet capture for packets where the remote IP address matches this value.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-146">**Remote IP address**: Filters the packet capture for packets where the remote IP address matches this value.</span></span>
     - <span data-ttu-id="f0cfb-147">**Remote port**: Filters the packet capture for packets where the remote port matches this value.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-147">**Remote port**: Filters the packet capture for packets where the remote port matches this value.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f0cfb-148">Port and IP address values can be a single value, range of values, or a range, such as 80-1024, for port.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-148">Port and IP address values can be a single value, range of values, or a range, such as 80-1024, for port.</span></span> <span data-ttu-id="f0cfb-149">You can define as many filters as you need.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-149">You can define as many filters as you need.</span></span>

4. <span data-ttu-id="f0cfb-150">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-150">Select **OK**.</span></span>

<span data-ttu-id="f0cfb-151">After the time limit set on the packet capture has expired, the packet capture is stopped, and can be reviewed.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-151">After the time limit set on the packet capture has expired, the packet capture is stopped, and can be reviewed.</span></span> <span data-ttu-id="f0cfb-152">You can also manually stop a packet capture session.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-152">You can also manually stop a packet capture session.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cfb-153">The portal automatically:</span><span class="sxs-lookup"><span data-stu-id="f0cfb-153">The portal automatically:</span></span>
>  * <span data-ttu-id="f0cfb-154">Creates a  network watcher in the same region as the region the virtual machine you selected exists in, if the region doesn't already have a network watcher.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-154">Creates a  network watcher in the same region as the region the virtual machine you selected exists in, if the region doesn't already have a network watcher.</span></span>
>  * <span data-ttu-id="f0cfb-155">Adds the *AzureNetworkWatcherExtension* [Linux](../virtual-machines/linux/extensions-nwa.md) or [Windows](../virtual-machines/windows/extensions-nwa.md) virtual machine extension to the virtual machine, if it's not already installed.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-155">Adds the *AzureNetworkWatcherExtension* [Linux](../virtual-machines/linux/extensions-nwa.md) or [Windows](../virtual-machines/windows/extensions-nwa.md) virtual machine extension to the virtual machine, if it's not already installed.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="f0cfb-156">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="f0cfb-156">Delete a packet capture</span></span>

1. <span data-ttu-id="f0cfb-157">In the packet capture view, select **...** on the right-side of the packet capture, or right-click an existing packet capture, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-157">In the packet capture view, select **...** on the right-side of the packet capture, or right-click an existing packet capture, and select **Delete**.</span></span>
2. <span data-ttu-id="f0cfb-158">You are asked to confirm you want to delete the packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-158">You are asked to confirm you want to delete the packet capture.</span></span> <span data-ttu-id="f0cfb-159">Select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-159">Select **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cfb-160">Deleting a packet capture does not delete the capture file in the storage account or on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-160">Deleting a packet capture does not delete the capture file in the storage account or on the virtual machine.</span></span>

## <a name="stop-a-packet-capture"></a><span data-ttu-id="f0cfb-161">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="f0cfb-161">Stop a packet capture</span></span>

<span data-ttu-id="f0cfb-162">In the packet capture view, select **...** on the right-side of the packet capture, or right-click an existing packet capture, and select **Stop**.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-162">In the packet capture view, select **...** on the right-side of the packet capture, or right-click an existing packet capture, and select **Stop**.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="f0cfb-163">Download a packet capture</span><span class="sxs-lookup"><span data-stu-id="f0cfb-163">Download a packet capture</span></span>

<span data-ttu-id="f0cfb-164">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-164">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the virtual machine.</span></span> <span data-ttu-id="f0cfb-165">The storage location of the packet capture is defined during creation of the packet capture.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-165">The storage location of the packet capture is defined during creation of the packet capture.</span></span> <span data-ttu-id="f0cfb-166">A convenient tool to access capture files saved to a storage account is Microsoft Azure Storage Explorer, which you can [download](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f0cfb-166">A convenient tool to access capture files saved to a storage account is Microsoft Azure Storage Explorer, which you can [download](http://storageexplorer.com/).</span></span>

<span data-ttu-id="f0cfb-167">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="f0cfb-167">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

<span data-ttu-id="f0cfb-168">If you selected **File** when you created the capture, you can view or download the file from the path you configured on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f0cfb-168">If you selected **File** when you created the capture, you can view or download the file from the path you configured on the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0cfb-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0cfb-169">Next steps</span></span>

- <span data-ttu-id="f0cfb-170">To learn how to automate packet captures with virtual machine alerts, see [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="f0cfb-170">To learn how to automate packet captures with virtual machine alerts, see [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span></span>
- <span data-ttu-id="f0cfb-171">To determine whether specific traffic is allowed in or out of a virtual machine, see [Diagnose a virtual machine network traffic filter problem](diagnose-vm-network-traffic-filtering-problem.md).</span><span class="sxs-lookup"><span data-stu-id="f0cfb-171">To determine whether specific traffic is allowed in or out of a virtual machine, see [Diagnose a virtual machine network traffic filter problem](diagnose-vm-network-traffic-filtering-problem.md).</span></span>
