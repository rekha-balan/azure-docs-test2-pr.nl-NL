---
title: Manage packet captures with Azure Network Watcher - PowerShell | Microsoft Docs
description: This page explains how to manage the packet capture feature of Network Watcher using PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: ec82b8cc381bc5a30763b9f5d1766ac15d5f1734
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551450"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="55667-103">Manage packet captures with Azure Network Watcher using PowerShell</span><span class="sxs-lookup"><span data-stu-id="55667-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI](network-watcher-packet-capture-manage-cli.md)
> - [REST API](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="55667-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55667-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="55667-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="55667-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="55667-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span><span class="sxs-lookup"><span data-stu-id="55667-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="55667-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="55667-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="55667-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="55667-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="55667-113">This article takes you through the different management tasks that are currently available for packet capture.</span><span class="sxs-lookup"><span data-stu-id="55667-113">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="55667-114">**Start a packet capture**</span><span class="sxs-lookup"><span data-stu-id="55667-114">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="55667-115">**Stop a packet capture**</span><span class="sxs-lookup"><span data-stu-id="55667-115">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="55667-116">**Delete a packet capture**</span><span class="sxs-lookup"><span data-stu-id="55667-116">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="55667-117">**Download a packet capture**</span><span class="sxs-lookup"><span data-stu-id="55667-117">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="55667-118">Before you begin</span><span class="sxs-lookup"><span data-stu-id="55667-118">Before you begin</span></span>

<span data-ttu-id="55667-119">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="55667-119">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="55667-120">An instance of Network Watcher in the region you want to create a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-120">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="55667-121">A virtual machine with the packet capture extension enabled.</span><span class="sxs-lookup"><span data-stu-id="55667-121">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a><span data-ttu-id="55667-124">Install VM extension</span><span class="sxs-lookup"><span data-stu-id="55667-124">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="55667-125">Step 1</span><span class="sxs-lookup"><span data-stu-id="55667-125">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="55667-126">Step 2</span><span class="sxs-lookup"><span data-stu-id="55667-126">Step 2</span></span>

<span data-ttu-id="55667-127">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55667-127">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="55667-128">This cmdlet installs the packet capture agent on the guest virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55667-128">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.

<span data-ttu-id="55667-130">For Windows virtual machines:</span><span class="sxs-lookup"><span data-stu-id="55667-130">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="55667-131">For Linux virtual machines:</span><span class="sxs-lookup"><span data-stu-id="55667-131">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="55667-132">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55667-132">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="55667-133">Step 3</span><span class="sxs-lookup"><span data-stu-id="55667-133">Step 3</span></span>

<span data-ttu-id="55667-134">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span><span class="sxs-lookup"><span data-stu-id="55667-134">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="55667-135">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="55667-135">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="55667-136">Start a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-136">Start a packet capture</span></span>

<span data-ttu-id="55667-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="55667-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="55667-138">Step 1</span><span class="sxs-lookup"><span data-stu-id="55667-138">Step 1</span></span>

<span data-ttu-id="55667-139">The next step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="55667-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="55667-140">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span><span class="sxs-lookup"><span data-stu-id="55667-140">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="55667-141">Step 2</span><span class="sxs-lookup"><span data-stu-id="55667-141">Step 2</span></span>

<span data-ttu-id="55667-142">Retrieve a storage account.</span><span class="sxs-lookup"><span data-stu-id="55667-142">Retrieve a storage account.</span></span> <span data-ttu-id="55667-143">This storage account is used to store the packet capture file.</span><span class="sxs-lookup"><span data-stu-id="55667-143">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="55667-144">Step 3</span><span class="sxs-lookup"><span data-stu-id="55667-144">Step 3</span></span>

<span data-ttu-id="55667-145">Filters can be used to limit the data that is stored by the packet capture.</span><span class="sxs-lookup"><span data-stu-id="55667-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="55667-146">The following example sets up two filters.</span><span class="sxs-lookup"><span data-stu-id="55667-146">The following example sets up two filters.</span></span>  <span data-ttu-id="55667-147">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span><span class="sxs-lookup"><span data-stu-id="55667-147">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="55667-148">The second filter collects only UDP traffic.</span><span class="sxs-lookup"><span data-stu-id="55667-148">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Multiple filters can be defined for a packet capture.

### <a name="step-4"></a><span data-ttu-id="55667-150">Step 4</span><span class="sxs-lookup"><span data-stu-id="55667-150">Step 4</span></span>

<span data-ttu-id="55667-151">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="55667-151">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="55667-152">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55667-152">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="55667-153">Get a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-153">Get a packet capture</span></span>

<span data-ttu-id="55667-154">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span><span class="sxs-lookup"><span data-stu-id="55667-154">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="55667-155">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55667-155">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="55667-156">The following example is after the capture is complete.</span><span class="sxs-lookup"><span data-stu-id="55667-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="55667-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="55667-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="55667-158">This value shows that the packet capture was successful and ran its time.</span><span class="sxs-lookup"><span data-stu-id="55667-158">This value shows that the packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="55667-159">Stop a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-159">Stop a packet capture</span></span>

<span data-ttu-id="55667-160">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span><span class="sxs-lookup"><span data-stu-id="55667-160">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.

## <a name="delete-a-packet-capture"></a><span data-ttu-id="55667-162">Delete a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-162">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Deleting a packet capture does not delete the file in the storage account.

## <a name="download-a-packet-capture"></a><span data-ttu-id="55667-164">Download a packet capture</span><span class="sxs-lookup"><span data-stu-id="55667-164">Download a packet capture</span></span>

<span data-ttu-id="55667-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span><span class="sxs-lookup"><span data-stu-id="55667-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="55667-166">The storage location of the packet capture is defined at creation of the session.</span><span class="sxs-lookup"><span data-stu-id="55667-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="55667-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="55667-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="55667-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="55667-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="55667-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="55667-169">Next steps</span></span>

<span data-ttu-id="55667-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="55667-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="55667-171">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="55667-171">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














