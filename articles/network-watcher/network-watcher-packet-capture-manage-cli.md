---
title: Manage packet captures with Azure Network Watcher - Azure CLI | Microsoft Docs
description: This page explains how to manage the packet capture feature of Network Watcher using Azure CLI
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 89e58686dcefb784a865f7842e78ef4d00f5783c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549094"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli"></a><span data-ttu-id="318fd-103">Manage packet captures with Azure Network Watcher using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="318fd-103">Manage packet captures with Azure Network Watcher using Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="318fd-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="318fd-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="318fd-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="318fd-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="318fd-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span><span class="sxs-lookup"><span data-stu-id="318fd-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="318fd-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="318fd-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="318fd-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="318fd-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="318fd-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="318fd-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="318fd-114">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="318fd-114">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="318fd-115">This article takes you through the different management tasks that are currently available for packet capture.</span><span class="sxs-lookup"><span data-stu-id="318fd-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="318fd-116">**Start a packet capture**</span><span class="sxs-lookup"><span data-stu-id="318fd-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="318fd-117">**Stop a packet capture**</span><span class="sxs-lookup"><span data-stu-id="318fd-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="318fd-118">**Delete a packet capture**</span><span class="sxs-lookup"><span data-stu-id="318fd-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="318fd-119">**Download a packet capture**</span><span class="sxs-lookup"><span data-stu-id="318fd-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="318fd-120">Before you begin</span><span class="sxs-lookup"><span data-stu-id="318fd-120">Before you begin</span></span>

<span data-ttu-id="318fd-121">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="318fd-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="318fd-122">An instance of Network Watcher in the region you want to create a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="318fd-123">A virtual machine with the packet capture extension enabled.</span><span class="sxs-lookup"><span data-stu-id="318fd-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> Packet capture requires an agent to be running on the virtual machine. The Agent is installed as an extension. For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a><span data-ttu-id="318fd-127">Install VM extension</span><span class="sxs-lookup"><span data-stu-id="318fd-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="318fd-128">Step 1</span><span class="sxs-lookup"><span data-stu-id="318fd-128">Step 1</span></span>

<span data-ttu-id="318fd-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span><span class="sxs-lookup"><span data-stu-id="318fd-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="318fd-130">For Windows virtual machines:</span><span class="sxs-lookup"><span data-stu-id="318fd-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="318fd-131">For Linux virtual machines:</span><span class="sxs-lookup"><span data-stu-id="318fd-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="318fd-132">Step 2</span><span class="sxs-lookup"><span data-stu-id="318fd-132">Step 2</span></span>

<span data-ttu-id="318fd-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span><span class="sxs-lookup"><span data-stu-id="318fd-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="318fd-134">Check the resulting list to ensure the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="318fd-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="318fd-135">The following sample is an example of the response from running `azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="318fd-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                     Version  State
data:    ------------------------------  -----------------------  -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentTest  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="318fd-136">Start a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-136">Start a packet capture</span></span>

<span data-ttu-id="318fd-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="318fd-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="318fd-138">Step 1</span><span class="sxs-lookup"><span data-stu-id="318fd-138">Step 1</span></span>

<span data-ttu-id="318fd-139">The next step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="318fd-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="318fd-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span><span class="sxs-lookup"><span data-stu-id="318fd-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="318fd-141">Step 2</span><span class="sxs-lookup"><span data-stu-id="318fd-141">Step 2</span></span>

<span data-ttu-id="318fd-142">Retrieve a storage account.</span><span class="sxs-lookup"><span data-stu-id="318fd-142">Retrieve a storage account.</span></span> <span data-ttu-id="318fd-143">This storage account is used to store the packet capture file.</span><span class="sxs-lookup"><span data-stu-id="318fd-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="318fd-144">Step 3</span><span class="sxs-lookup"><span data-stu-id="318fd-144">Step 3</span></span>

<span data-ttu-id="318fd-145">Filters can be used to limit the data that is stored by the packet capture.</span><span class="sxs-lookup"><span data-stu-id="318fd-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="318fd-146">The following example sets up a packet capture with several  filters.</span><span class="sxs-lookup"><span data-stu-id="318fd-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="318fd-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span><span class="sxs-lookup"><span data-stu-id="318fd-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="318fd-148">The last filter collects only UDP traffic.</span><span class="sxs-lookup"><span data-stu-id="318fd-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="318fd-149">Multiple filters can be defined for a packet capture.</span><span class="sxs-lookup"><span data-stu-id="318fd-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="318fd-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span><span class="sxs-lookup"><span data-stu-id="318fd-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="318fd-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span><span class="sxs-lookup"><span data-stu-id="318fd-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="318fd-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="318fd-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="318fd-153">Get a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-153">Get a packet capture</span></span>

<span data-ttu-id="318fd-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span><span class="sxs-lookup"><span data-stu-id="318fd-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="318fd-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="318fd-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="318fd-156">The following example is after the capture is complete.</span><span class="sxs-lookup"><span data-stu-id="318fd-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="318fd-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="318fd-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="318fd-158">This value shows that the packet capture was successful and ran its time.</span><span class="sxs-lookup"><span data-stu-id="318fd-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="318fd-159">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-159">Stop a packet capture</span></span>

<span data-ttu-id="318fd-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span><span class="sxs-lookup"><span data-stu-id="318fd-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.

## <a name="delete-a-packet-capture"></a><span data-ttu-id="318fd-162">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Deleting a packet capture does not delete the file in the storage account.

## <a name="download-a-packet-capture"></a><span data-ttu-id="318fd-164">Download a packet capture</span><span class="sxs-lookup"><span data-stu-id="318fd-164">Download a packet capture</span></span>

<span data-ttu-id="318fd-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span><span class="sxs-lookup"><span data-stu-id="318fd-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="318fd-166">The storage location of the packet capture is defined at creation of the session.</span><span class="sxs-lookup"><span data-stu-id="318fd-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="318fd-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="318fd-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="318fd-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="318fd-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="318fd-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="318fd-169">Next steps</span></span>

<span data-ttu-id="318fd-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="318fd-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="318fd-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="318fd-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
