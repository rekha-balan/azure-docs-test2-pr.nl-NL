---
title: Troubleshoot connections with Azure Network Watcher - Azure REST API | Microsoft Docs
description: Learn how to use the connection troubleshoot capability of Azure Network Watcher using the Azure REST API.
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
ms.date: 08/02/2017
ms.author: jdial
ms.openlocfilehash: 848db5d0df63707eece4f9f7a2a69135bed2d389
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866939"
---
# <a name="troubleshoot-connections-with-azure-network-watcher-using-the-azure-rest-api"></a><span data-ttu-id="9b4e0-103">Troubleshoot connections with Azure Network Watcher using the Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9b4e0-103">Troubleshoot connections with Azure Network Watcher using the Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

<span data-ttu-id="9b4e0-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b4e0-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9b4e0-109">Before you begin</span></span>

<span data-ttu-id="9b4e0-110">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="9b4e0-111">An instance of Network Watcher in the region you want to troubleshoot a connection.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-111">An instance of Network Watcher in the region you want to troubleshoot a connection.</span></span>
* <span data-ttu-id="9b4e0-112">Virtual machines to troubleshoot connections with.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-112">Virtual machines to troubleshoot connections with.</span></span>

> [!IMPORTANT]
> Connection troubleshoot requires that the VM you troubleshoot from has the `AzureNetworkWatcherExtension` VM extension installed. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json). The extension is not required on the destination endpoint.

## <a name="log-in-with-armclient"></a><span data-ttu-id="9b4e0-116">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="9b4e0-116">Log in with ARMClient</span></span>

<span data-ttu-id="9b4e0-117">Log in to armclient with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-117">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="9b4e0-118">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="9b4e0-118">Retrieve a virtual machine</span></span>

<span data-ttu-id="9b4e0-119">Run the following script to return a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-119">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="9b4e0-120">This information is needed for running connectivity.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-120">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="9b4e0-121">The following code needs values for the following variables:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-121">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="9b4e0-122">**subscriptionId** - The subscription ID to use.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-122">**subscriptionId** - The subscription ID to use.</span></span>
- <span data-ttu-id="9b4e0-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="9b4e0-124">From the following output, the ID of the virtual machine is used in the following example:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-124">From the following output, the ID of the virtual machine is used in the following example:</span></span>

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="9b4e0-125">Check connectivity to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="9b4e0-125">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="9b4e0-126">This example checks connectivity to a destination virtual machine over port 80.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-126">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="9b4e0-127">Example</span><span class="sxs-lookup"><span data-stu-id="9b4e0-127">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9b4e0-128">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-128">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9b4e0-129">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="9b4e0-129">**Important Values**</span></span>

* <span data-ttu-id="9b4e0-130">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="9b4e0-130">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="9b4e0-131">Response</span><span class="sxs-lookup"><span data-stu-id="9b4e0-131">Response</span></span>

<span data-ttu-id="9b4e0-132">The following response is from the previous example.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-132">The following response is from the previous example.</span></span>  <span data-ttu-id="9b4e0-133">In this response, the `ConnectionStatus` is **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-133">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="9b4e0-134">You can see that all the probes sent failed.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-134">You can see that all the probes sent failed.</span></span> <span data-ttu-id="9b4e0-135">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-135">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="9b4e0-136">This information can be used to research connection issues.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-136">This information can be used to research connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="9b4e0-137">Validate routing issues</span><span class="sxs-lookup"><span data-stu-id="9b4e0-137">Validate routing issues</span></span>

<span data-ttu-id="9b4e0-138">The example checks connectivity between a virtual machine and a remote endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-138">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="9b4e0-139">Example</span><span class="sxs-lookup"><span data-stu-id="9b4e0-139">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9b4e0-140">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-140">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9b4e0-141">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="9b4e0-141">**Important Values**</span></span>

* <span data-ttu-id="9b4e0-142">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="9b4e0-142">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="9b4e0-143">Response</span><span class="sxs-lookup"><span data-stu-id="9b4e0-143">Response</span></span>

<span data-ttu-id="9b4e0-144">In the following example, the `connectionStatus` is shown as **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-144">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="9b4e0-145">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-145">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="9b4e0-146">Check website latency</span><span class="sxs-lookup"><span data-stu-id="9b4e0-146">Check website latency</span></span>

<span data-ttu-id="9b4e0-147">The following example checks the connectivity to a website.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-147">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="9b4e0-148">Example</span><span class="sxs-lookup"><span data-stu-id="9b4e0-148">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9b4e0-149">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-149">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9b4e0-150">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="9b4e0-150">**Important Values**</span></span>

* <span data-ttu-id="9b4e0-151">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="9b4e0-151">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="9b4e0-152">Response</span><span class="sxs-lookup"><span data-stu-id="9b4e0-152">Response</span></span>

<span data-ttu-id="9b4e0-153">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-153">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="9b4e0-154">When a connection is successful, latency values are provided.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-154">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="9b4e0-155">Check connectivity to a storage endpoint</span><span class="sxs-lookup"><span data-stu-id="9b4e0-155">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="9b4e0-156">The following example checks the connectivity from a virtual machine to a blog storage account.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-156">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="9b4e0-157">Example</span><span class="sxs-lookup"><span data-stu-id="9b4e0-157">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="9b4e0-158">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-158">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="9b4e0-159">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="9b4e0-159">**Important Values**</span></span>

* <span data-ttu-id="9b4e0-160">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="9b4e0-160">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="9b4e0-161">Response</span><span class="sxs-lookup"><span data-stu-id="9b4e0-161">Response</span></span>

<span data-ttu-id="9b4e0-162">The following example is the response from running the previous API call.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-162">The following example is the response from running the previous API call.</span></span> <span data-ttu-id="9b4e0-163">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-163">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="9b4e0-164">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-164">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="9b4e0-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b4e0-165">Next steps</span></span>

<span data-ttu-id="9b4e0-166">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="9b4e0-166">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span></span>

<span data-ttu-id="9b4e0-167">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md).</span><span class="sxs-lookup"><span data-stu-id="9b4e0-167">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md).</span></span>














