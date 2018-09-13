---
title: Find Next Hop with Azure Network Watcher Next Hop - REST | Microsoft Docs
description: This article will describe how you can find what the next hop type is and ip address using Next Hop using the Azure REST API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7653f5d264497028a72124083accbc6d20826842
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549080"
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="9f233-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9f233-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="9f233-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f233-108">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="9f233-109">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span><span class="sxs-lookup"><span data-stu-id="9f233-109">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f233-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9f233-110">Before you begin</span></span>

<span data-ttu-id="9f233-111">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f233-111">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="9f233-112">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="9f233-112">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="9f233-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="9f233-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="9f233-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="9f233-114">Scenario</span></span>

<span data-ttu-id="9f233-115">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span><span class="sxs-lookup"><span data-stu-id="9f233-115">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="9f233-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f233-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="9f233-117">In this scenario, you will:</span><span class="sxs-lookup"><span data-stu-id="9f233-117">In this scenario, you will:</span></span>

* <span data-ttu-id="9f233-118">Retrieve the next hop for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f233-118">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="9f233-119">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="9f233-119">Log in with ARMClient</span></span>

<span data-ttu-id="9f233-120">Log in to armclient with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="9f233-120">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="9f233-121">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="9f233-121">Retrieve a virtual machine</span></span>

<span data-ttu-id="9f233-122">Run the following script to return a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9f233-122">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="9f233-123">This information is needed for running next hop.</span><span class="sxs-lookup"><span data-stu-id="9f233-123">This information is needed for running next hop.</span></span>

<span data-ttu-id="9f233-124">The following code needs values for the following variables:</span><span class="sxs-lookup"><span data-stu-id="9f233-124">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="9f233-125">**subscriptionId** - The subscription Id to use.</span><span class="sxs-lookup"><span data-stu-id="9f233-125">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="9f233-126">**resourceGroupName** - The name of a resource group that contains virtual machines.</span><span class="sxs-lookup"><span data-stu-id="9f233-126">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="9f233-127">From the following output, the id of the virtual machine is used in the following example:</span><span class="sxs-lookup"><span data-stu-id="9f233-127">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="9f233-128">Get Next Hop</span><span class="sxs-lookup"><span data-stu-id="9f233-128">Get Next Hop</span></span>

<span data-ttu-id="9f233-129">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span><span class="sxs-lookup"><span data-stu-id="9f233-129">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="9f233-130">The following values must be replaced for the code example to work.</span><span class="sxs-lookup"><span data-stu-id="9f233-130">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Next hop requires that the VM resource is allocated to run.

## <a name="results"></a><span data-ttu-id="9f233-133">Results</span><span class="sxs-lookup"><span data-stu-id="9f233-133">Results</span></span>

<span data-ttu-id="9f233-134">The following snippet is an example of the output received.</span><span class="sxs-lookup"><span data-stu-id="9f233-134">The following snippet is an example of the output received.</span></span> <span data-ttu-id="9f233-135">The results contain the following values:</span><span class="sxs-lookup"><span data-stu-id="9f233-135">The results contain the following values:</span></span>

* <span data-ttu-id="9f233-136">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span><span class="sxs-lookup"><span data-stu-id="9f233-136">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="9f233-137">**nextHopIpAddress** - The IP address of the next hop.</span><span class="sxs-lookup"><span data-stu-id="9f233-137">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="9f233-138">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span><span class="sxs-lookup"><span data-stu-id="9f233-138">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="9f233-139">The following are the results in json format.</span><span class="sxs-lookup"><span data-stu-id="9f233-139">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="9f233-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f233-140">Next steps</span></span>

<span data-ttu-id="9f233-141">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9f233-141">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














