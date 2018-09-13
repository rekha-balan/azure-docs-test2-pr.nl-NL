---
title: Manage packet captures with Azure Network Watcher - Azure CLI | Microsoft Docs
description: This page explains how to manage the packet capture feature of Network Watcher using the Azure CLI
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 9b40a85cf3c4edd26f2fc15045f3d6862d4ac1ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791510"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-azure-cli"></a><span data-ttu-id="f94d2-103">Manage packet captures with Azure Network Watcher using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f94d2-103">Manage packet captures with Azure Network Watcher using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Azure CLI](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="f94d2-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f94d2-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="f94d2-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="f94d2-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="f94d2-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span><span class="sxs-lookup"><span data-stu-id="f94d2-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="f94d2-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="f94d2-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="f94d2-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="f94d2-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="f94d2-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="f94d2-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="f94d2-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f94d2-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="f94d2-115">This article takes you through the different management tasks that are currently available for packet capture.</span><span class="sxs-lookup"><span data-stu-id="f94d2-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="f94d2-116">**Start a packet capture**</span><span class="sxs-lookup"><span data-stu-id="f94d2-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="f94d2-117">**Stop a packet capture**</span><span class="sxs-lookup"><span data-stu-id="f94d2-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="f94d2-118">**Delete a packet capture**</span><span class="sxs-lookup"><span data-stu-id="f94d2-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="f94d2-119">**Download a packet capture**</span><span class="sxs-lookup"><span data-stu-id="f94d2-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="f94d2-120">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f94d2-120">Before you begin</span></span>

<span data-ttu-id="f94d2-121">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="f94d2-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="f94d2-122">An instance of Network Watcher in the region you want to create a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="f94d2-123">A virtual machine with the packet capture extension enabled.</span><span class="sxs-lookup"><span data-stu-id="f94d2-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> Packet capture requires an agent to be running on the virtual machine. The Agent is installed as an extension. For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a><span data-ttu-id="f94d2-127">Install VM extension</span><span class="sxs-lookup"><span data-stu-id="f94d2-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="f94d2-128">Step 1</span><span class="sxs-lookup"><span data-stu-id="f94d2-128">Step 1</span></span>

<span data-ttu-id="f94d2-129">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f94d2-129">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="f94d2-130">For Windows virtual machines:</span><span class="sxs-lookup"><span data-stu-id="f94d2-130">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="f94d2-131">For Linux virtual machines:</span><span class="sxs-lookup"><span data-stu-id="f94d2-131">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="f94d2-132">Step 2</span><span class="sxs-lookup"><span data-stu-id="f94d2-132">Step 2</span></span>

<span data-ttu-id="f94d2-133">To ensure that the agent is installed, run the `vm extension show` cmdlet and pass it the resource group and virtual machine name.</span><span class="sxs-lookup"><span data-stu-id="f94d2-133">To ensure that the agent is installed, run the `vm extension show` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="f94d2-134">Check the resulting list to ensure the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="f94d2-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show --resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="f94d2-135">The following sample is an example of the response from running `az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="f94d2-135">The following sample is an example of the response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="f94d2-136">Start a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-136">Start a packet capture</span></span>

<span data-ttu-id="f94d2-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f94d2-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="f94d2-138">Step 1</span><span class="sxs-lookup"><span data-stu-id="f94d2-138">Step 1</span></span>

<span data-ttu-id="f94d2-139">The next step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="f94d2-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f94d2-140">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span><span class="sxs-lookup"><span data-stu-id="f94d2-140">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show --resource-group resourceGroup --name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="f94d2-141">Step 2</span><span class="sxs-lookup"><span data-stu-id="f94d2-141">Step 2</span></span>

<span data-ttu-id="f94d2-142">Retrieve a storage account.</span><span class="sxs-lookup"><span data-stu-id="f94d2-142">Retrieve a storage account.</span></span> <span data-ttu-id="f94d2-143">This storage account is used to store the packet capture file.</span><span class="sxs-lookup"><span data-stu-id="f94d2-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="f94d2-144">Step 3</span><span class="sxs-lookup"><span data-stu-id="f94d2-144">Step 3</span></span>

<span data-ttu-id="f94d2-145">Filters can be used to limit the data that is stored by the packet capture.</span><span class="sxs-lookup"><span data-stu-id="f94d2-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="f94d2-146">The following example sets up a packet capture with several  filters.</span><span class="sxs-lookup"><span data-stu-id="f94d2-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="f94d2-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span><span class="sxs-lookup"><span data-stu-id="f94d2-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="f94d2-148">The last filter collects only UDP traffic.</span><span class="sxs-lookup"><span data-stu-id="f94d2-148">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resourceGroupName} --vm {vmName} --name packetCaptureName --storage-account {storageAccountName} --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="f94d2-149">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f94d2-149">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="f94d2-150">Get a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-150">Get a packet capture</span></span>

<span data-ttu-id="f94d2-151">Running the `az network watcher packet-capture show-status` cmdlet, retrieves the status of a currently running, or completed packet capture.</span><span class="sxs-lookup"><span data-stu-id="f94d2-151">Running the `az network watcher packet-capture show-status` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show-status --name packetCaptureName --location {networkWatcherLocation}
```

<span data-ttu-id="f94d2-152">The following example is the output from the `az network watcher packet-capture show-status` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f94d2-152">The following example is the output from the `az network watcher packet-capture show-status` cmdlet.</span></span> <span data-ttu-id="f94d2-153">The following example is when the capture is Stopped, with a StopReason of TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="f94d2-153">The following example is when the capture is Stopped, with a StopReason of TimeExceeded.</span></span> 

```
{
  "additionalProperties": {
    "status": "Succeeded"
  },
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "packetCaptureError": [],
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded"
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="f94d2-154">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-154">Stop a packet capture</span></span>

<span data-ttu-id="f94d2-155">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span><span class="sxs-lookup"><span data-stu-id="f94d2-155">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.

## <a name="delete-a-packet-capture"></a><span data-ttu-id="f94d2-157">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-157">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> Deleting a packet capture does not delete the file in the storage account.

## <a name="download-a-packet-capture"></a><span data-ttu-id="f94d2-159">Download a packet capture</span><span class="sxs-lookup"><span data-stu-id="f94d2-159">Download a packet capture</span></span>

<span data-ttu-id="f94d2-160">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span><span class="sxs-lookup"><span data-stu-id="f94d2-160">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="f94d2-161">The storage location of the packet capture is defined at creation of the session.</span><span class="sxs-lookup"><span data-stu-id="f94d2-161">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="f94d2-162">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="f94d2-162">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="f94d2-163">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="f94d2-163">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="f94d2-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="f94d2-164">Next steps</span></span>

<span data-ttu-id="f94d2-165">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="f94d2-165">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="f94d2-166">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span><span class="sxs-lookup"><span data-stu-id="f94d2-166">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span></span>

<!-- Image references -->
