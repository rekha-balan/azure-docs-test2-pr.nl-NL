---
title: Troubleshoot connections with Azure Network Watcher - Azure CLI 2.0 | Microsoft Docs
description: Learn how to use the connection troubleshoot capability of Azure Network Watcher using the Azure CLI 2.0.
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
ms.openlocfilehash: 1ce5856a5ee2c37d96483df82836d2e8b2a61d4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870650"
---
# <a name="troubleshoot-connections-with-azure-network-watcher-using-the-azure-cli-20"></a><span data-ttu-id="320db-103">Troubleshoot connections with Azure Network Watcher using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="320db-103">Troubleshoot connections with Azure Network Watcher using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

<span data-ttu-id="320db-107">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span><span class="sxs-lookup"><span data-stu-id="320db-107">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="320db-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="320db-108">Before you begin</span></span>

<span data-ttu-id="320db-109">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="320db-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="320db-110">An instance of Network Watcher in the region you want to troubleshoot a connection.</span><span class="sxs-lookup"><span data-stu-id="320db-110">An instance of Network Watcher in the region you want to troubleshoot a connection.</span></span>
* <span data-ttu-id="320db-111">Virtual machines to troubleshoot connections with.</span><span class="sxs-lookup"><span data-stu-id="320db-111">Virtual machines to troubleshoot connections with.</span></span>

> [!IMPORTANT]
> Connection troubleshoot requires that the VM you troubleshoot from has the `AzureNetworkWatcherExtension` VM extension installed. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json). The extension is not required on the destination endpoint.

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="320db-115">Check connectivity to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="320db-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="320db-116">This example checks connectivity to a destination virtual machine over port 80.</span><span class="sxs-lookup"><span data-stu-id="320db-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="320db-117">Example</span><span class="sxs-lookup"><span data-stu-id="320db-117">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="320db-118">Response</span><span class="sxs-lookup"><span data-stu-id="320db-118">Response</span></span>

<span data-ttu-id="320db-119">The following response is from the previous example.</span><span class="sxs-lookup"><span data-stu-id="320db-119">The following response is from the previous example.</span></span>  <span data-ttu-id="320db-120">In this response, the `ConnectionStatus` is **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="320db-120">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="320db-121">You can see that all the probes sent failed.</span><span class="sxs-lookup"><span data-stu-id="320db-121">You can see that all the probes sent failed.</span></span> <span data-ttu-id="320db-122">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="320db-122">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="320db-123">This information can be used to research connection issues.</span><span class="sxs-lookup"><span data-stu-id="320db-123">This information can be used to research connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="320db-124">Validate routing issues</span><span class="sxs-lookup"><span data-stu-id="320db-124">Validate routing issues</span></span>

<span data-ttu-id="320db-125">This example checks connectivity between a virtual machine and a remote endpoint.</span><span class="sxs-lookup"><span data-stu-id="320db-125">This example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="320db-126">Example</span><span class="sxs-lookup"><span data-stu-id="320db-126">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="320db-127">Response</span><span class="sxs-lookup"><span data-stu-id="320db-127">Response</span></span>

<span data-ttu-id="320db-128">In the following example, the `connectionStatus` is shown as **Unreachable**.</span><span class="sxs-lookup"><span data-stu-id="320db-128">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="320db-129">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="320db-129">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="320db-130">Check website latency</span><span class="sxs-lookup"><span data-stu-id="320db-130">Check website latency</span></span>

<span data-ttu-id="320db-131">The following example checks the connectivity to a website.</span><span class="sxs-lookup"><span data-stu-id="320db-131">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="320db-132">Example</span><span class="sxs-lookup"><span data-stu-id="320db-132">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="320db-133">Response</span><span class="sxs-lookup"><span data-stu-id="320db-133">Response</span></span>

<span data-ttu-id="320db-134">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="320db-134">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="320db-135">When a connection is successful, latency values are provided.</span><span class="sxs-lookup"><span data-stu-id="320db-135">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="320db-136">Check connectivity to a storage endpoint</span><span class="sxs-lookup"><span data-stu-id="320db-136">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="320db-137">The following example checks the connectivity from a virtual machine to a blog storage account.</span><span class="sxs-lookup"><span data-stu-id="320db-137">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="320db-138">Example</span><span class="sxs-lookup"><span data-stu-id="320db-138">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="320db-139">Response</span><span class="sxs-lookup"><span data-stu-id="320db-139">Response</span></span>

<span data-ttu-id="320db-140">The following json is the example response from running the previous cmdlet.</span><span class="sxs-lookup"><span data-stu-id="320db-140">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="320db-141">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span><span class="sxs-lookup"><span data-stu-id="320db-141">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="320db-142">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span><span class="sxs-lookup"><span data-stu-id="320db-142">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="320db-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="320db-143">Next steps</span></span>

<span data-ttu-id="320db-144">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="320db-144">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="320db-145">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span><span class="sxs-lookup"><span data-stu-id="320db-145">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span></span>
