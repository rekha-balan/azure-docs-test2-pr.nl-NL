---
title: Troubleshoot connections with Azure Network Watcher - PowerShell | Microsoft Docs
description: Learn how to use the connection troubleshoot capability of Azure Network Watcher using PowerShell.
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: jdial
ms.openlocfilehash: 7e8c04fd2284a3a00d4847f39fd34982a543cc29
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856408"
---
# <a name="troubleshoot-connections-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="7db49-103">Troubleshoot connections with Azure Network Watcher using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7db49-103">Troubleshoot connections with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

<span data-ttu-id="7db49-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span><span class="sxs-lookup"><span data-stu-id="7db49-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7db49-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="7db49-109">Before you begin</span></span>

* <span data-ttu-id="7db49-110">An instance of Network Watcher in the region you want to troubleshoot a connection.</span><span class="sxs-lookup"><span data-stu-id="7db49-110">An instance of Network Watcher in the region you want to troubleshoot a connection.</span></span>
* <span data-ttu-id="7db49-111">Virtual machines to troubleshoot connections with.</span><span class="sxs-lookup"><span data-stu-id="7db49-111">Virtual machines to troubleshoot connections with.</span></span>

> [!IMPORTANT]
> Connection troubleshoot requires that the VM you troubleshoot from has the `AzureNetworkWatcherExtension` VM extension installed. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json). The extension is not required on the destination endpoint.

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="7db49-115">Check connectivity to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="7db49-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="7db49-116">This example checks a connection to a destination virtual machine over port 80.</span><span class="sxs-lookup"><span data-stu-id="7db49-116">This example checks a connection to a destination virtual machine over port 80.</span></span> <span data-ttu-id="7db49-117">This example requires that you have Network Watcher enabled in the region containing the source VM.</span><span class="sxs-lookup"><span data-stu-id="7db49-117">This example requires that you have Network Watcher enabled in the region containing the source VM.</span></span>  

### <a name="example"></a><span data-ttu-id="7db49-118">Example</span><span class="sxs-lookup"><span data-stu-id="7db49-118">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $VM1.Location} 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="7db49-119">Response</span><span class="sxs-lookup"><span data-stu-id="7db49-119">Response</span></span>

<span data-ttu-id="7db49-120">The following response is from the previous example.</span><span class="sxs-lookup"><span data-stu-id="7db49-120">The following response is from the previous example.</span></span>  <span data-ttu-id="7db49-121">In this response, the `ConnectionStatus` is **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="7db49-121">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="7db49-122">You can see that all the probes sent failed.</span><span class="sxs-lookup"><span data-stu-id="7db49-122">You can see that all the probes sent failed.</span></span> <span data-ttu-id="7db49-123">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="7db49-123">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="7db49-124">This information can be used to research connection issues.</span><span class="sxs-lookup"><span data-stu-id="7db49-124">This information can be used to research connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="7db49-125">Validate routing issues</span><span class="sxs-lookup"><span data-stu-id="7db49-125">Validate routing issues</span></span>

<span data-ttu-id="7db49-126">This example checks connectivity between a virtual machine and a remote endpoint.</span><span class="sxs-lookup"><span data-stu-id="7db49-126">This example checks connectivity between a virtual machine and a remote endpoint.</span></span> <span data-ttu-id="7db49-127">This example requires that you have Network Watcher enabled in the region containing the source VM.</span><span class="sxs-lookup"><span data-stu-id="7db49-127">This example requires that you have Network Watcher enabled in the region containing the source VM.</span></span>  

### <a name="example"></a><span data-ttu-id="7db49-128">Example</span><span class="sxs-lookup"><span data-stu-id="7db49-128">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName
$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $VM1.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="7db49-129">Response</span><span class="sxs-lookup"><span data-stu-id="7db49-129">Response</span></span>

<span data-ttu-id="7db49-130">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="7db49-130">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="7db49-131">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="7db49-131">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="7db49-132">Check website latency</span><span class="sxs-lookup"><span data-stu-id="7db49-132">Check website latency</span></span>

<span data-ttu-id="7db49-133">The following example checks connectivity to a website.</span><span class="sxs-lookup"><span data-stu-id="7db49-133">The following example checks connectivity to a website.</span></span> <span data-ttu-id="7db49-134">This example requires that you have Network Watcher enabled in the region containing the source VM.</span><span class="sxs-lookup"><span data-stu-id="7db49-134">This example requires that you have Network Watcher enabled in the region containing the source VM.</span></span>  

### <a name="example"></a><span data-ttu-id="7db49-135">Example</span><span class="sxs-lookup"><span data-stu-id="7db49-135">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName
$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $VM1.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName


Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="7db49-136">Response</span><span class="sxs-lookup"><span data-stu-id="7db49-136">Response</span></span>

<span data-ttu-id="7db49-137">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="7db49-137">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="7db49-138">When a connection is successful, latency values are provided.</span><span class="sxs-lookup"><span data-stu-id="7db49-138">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="7db49-139">Check connectivity to a storage endpoint</span><span class="sxs-lookup"><span data-stu-id="7db49-139">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="7db49-140">The following example checks connectivity from a virtual machine to a blog storage account.</span><span class="sxs-lookup"><span data-stu-id="7db49-140">The following example checks connectivity from a virtual machine to a blog storage account.</span></span> <span data-ttu-id="7db49-141">This example requires that you have Network Watcher enabled in the region containing the source VM.</span><span class="sxs-lookup"><span data-stu-id="7db49-141">This example requires that you have Network Watcher enabled in the region containing the source VM.</span></span>  

### <a name="example"></a><span data-ttu-id="7db49-142">Example</span><span class="sxs-lookup"><span data-stu-id="7db49-142">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $VM1.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="7db49-143">Response</span><span class="sxs-lookup"><span data-stu-id="7db49-143">Response</span></span>

<span data-ttu-id="7db49-144">The following json is the example response from running the previous cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7db49-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="7db49-145">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="7db49-145">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="7db49-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span><span class="sxs-lookup"><span data-stu-id="7db49-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="7db49-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="7db49-147">Next steps</span></span>

<span data-ttu-id="7db49-148">Determine whether certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md).</span><span class="sxs-lookup"><span data-stu-id="7db49-148">Determine whether certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md).</span></span>

<span data-ttu-id="7db49-149">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/manage-network-security-group.md) to track down the network security group and security rules that are defined.</span><span class="sxs-lookup"><span data-stu-id="7db49-149">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/manage-network-security-group.md) to track down the network security group and security rules that are defined.</span></span>