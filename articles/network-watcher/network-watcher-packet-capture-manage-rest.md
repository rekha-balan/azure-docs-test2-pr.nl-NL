---
title: Manage packet captures with Azure Network Watcher - REST API | Microsoft Docs
description: This page explains how to manage the packet capture feature of Network Watcher using Azure REST API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 633923190e8b6abf0f108d7823d9372a457981c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662891"
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="68c45-103">Manage packet captures with Azure Network Watcher using Azure REST API</span><span class="sxs-lookup"><span data-stu-id="68c45-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI](network-watcher-packet-capture-manage-cli.md)
> - [REST API](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="68c45-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68c45-108">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="68c45-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span><span class="sxs-lookup"><span data-stu-id="68c45-109">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="68c45-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span><span class="sxs-lookup"><span data-stu-id="68c45-110">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="68c45-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="68c45-111">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="68c45-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span><span class="sxs-lookup"><span data-stu-id="68c45-112">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="68c45-113">This article takes you through the different management tasks that are currently available for packet capture.</span><span class="sxs-lookup"><span data-stu-id="68c45-113">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="68c45-114">**Get a packet capture**</span><span class="sxs-lookup"><span data-stu-id="68c45-114">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="68c45-115">**List all packet captures**</span><span class="sxs-lookup"><span data-stu-id="68c45-115">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="68c45-116">**Query the status of a packet capture**</span><span class="sxs-lookup"><span data-stu-id="68c45-116">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="68c45-117">**Start a packet capture**</span><span class="sxs-lookup"><span data-stu-id="68c45-117">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="68c45-118">**Stop a packet capture**</span><span class="sxs-lookup"><span data-stu-id="68c45-118">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="68c45-119">**Delete a packet capture**</span><span class="sxs-lookup"><span data-stu-id="68c45-119">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="68c45-120">Before you begin</span><span class="sxs-lookup"><span data-stu-id="68c45-120">Before you begin</span></span>

<span data-ttu-id="68c45-121">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span><span class="sxs-lookup"><span data-stu-id="68c45-121">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="68c45-122">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68c45-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="68c45-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="68c45-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="68c45-124">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="68c45-124">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="log-in-with-armclient"></a><span data-ttu-id="68c45-127">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="68c45-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="68c45-128">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="68c45-128">Retrieve a virtual machine</span></span>

<span data-ttu-id="68c45-129">Run the following script to return a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68c45-129">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="68c45-130">This information is needed for starting a packet capture.</span><span class="sxs-lookup"><span data-stu-id="68c45-130">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="68c45-131">The following code needs variables:</span><span class="sxs-lookup"><span data-stu-id="68c45-131">The following code needs variables:</span></span>

- <span data-ttu-id="68c45-132">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68c45-132">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="68c45-133">**resourceGroupName** - The name of a resource group that contains virtual machines.</span><span class="sxs-lookup"><span data-stu-id="68c45-133">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="68c45-134">From the following output, the id of the virtual machine is used in the next example.</span><span class="sxs-lookup"><span data-stu-id="68c45-134">From the following output, the id of the virtual machine is used in the next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="68c45-135">Get a packet capture</span><span class="sxs-lookup"><span data-stu-id="68c45-135">Get a packet capture</span></span>

<span data-ttu-id="68c45-136">The following example gets the status of a single packet capture</span><span class="sxs-lookup"><span data-stu-id="68c45-136">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="68c45-137">The following responses are examples of a typical response returned when querying the status of a packet capture.</span><span class="sxs-lookup"><span data-stu-id="68c45-137">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="68c45-138">List all packet captures</span><span class="sxs-lookup"><span data-stu-id="68c45-138">List all packet captures</span></span>

<span data-ttu-id="68c45-139">The following example gets all packet capture sessions in a region.</span><span class="sxs-lookup"><span data-stu-id="68c45-139">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="68c45-140">The following response is an example of a typical response returned when getting all packet captures</span><span class="sxs-lookup"><span data-stu-id="68c45-140">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="68c45-141">Query packet capture status</span><span class="sxs-lookup"><span data-stu-id="68c45-141">Query packet capture status</span></span>

<span data-ttu-id="68c45-142">The following example gets all packet capture sessions in a region.</span><span class="sxs-lookup"><span data-stu-id="68c45-142">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="68c45-143">The following response is an example of a typical response returned when querying the status of a packet capture.</span><span class="sxs-lookup"><span data-stu-id="68c45-143">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="68c45-144">Start packet capture</span><span class="sxs-lookup"><span data-stu-id="68c45-144">Start packet capture</span></span>

<span data-ttu-id="68c45-145">The following example creates a packet capture on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68c45-145">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="68c45-146">The example is parameterized to allow for flexibility in creating an example.</span><span class="sxs-lookup"><span data-stu-id="68c45-146">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="68c45-147">Stop packet capture</span><span class="sxs-lookup"><span data-stu-id="68c45-147">Stop packet capture</span></span>

<span data-ttu-id="68c45-148">The following example stops a packet capture on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68c45-148">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="68c45-149">The example is parameterized to allow for flexibility in creating an example.</span><span class="sxs-lookup"><span data-stu-id="68c45-149">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="68c45-150">Delete packet capture</span><span class="sxs-lookup"><span data-stu-id="68c45-150">Delete packet capture</span></span>

<span data-ttu-id="68c45-151">The following example deletes a packet capture on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="68c45-151">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="68c45-152">The example is parameterized to allow for flexibility in creating an example.</span><span class="sxs-lookup"><span data-stu-id="68c45-152">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> Deleting a packet capture does not delete the file in the storage account

## <a name="next-steps"></a><span data-ttu-id="68c45-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="68c45-154">Next steps</span></span>

<span data-ttu-id="68c45-155">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="68c45-155">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="68c45-156">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="68c45-156">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="68c45-157">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="68c45-157">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="68c45-158">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="68c45-158">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













