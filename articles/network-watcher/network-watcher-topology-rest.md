---
title: View Azure Network Watcher topology - REST API | Microsoft Docs
description: This article will describe how to use REST API to query your network topology.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4fa34050a8039cebebe30842469c596c83744313
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549097"
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="60bfb-103">View Network Watcher topology with REST API</span><span class="sxs-lookup"><span data-stu-id="60bfb-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

<span data-ttu-id="60bfb-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span><span class="sxs-lookup"><span data-stu-id="60bfb-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="60bfb-108">In the portal, this visualization is presented to you automatically.</span><span class="sxs-lookup"><span data-stu-id="60bfb-108">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="60bfb-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60bfb-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="60bfb-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span><span class="sxs-lookup"><span data-stu-id="60bfb-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="60bfb-111">The interconnection is modeled under two relationships.</span><span class="sxs-lookup"><span data-stu-id="60bfb-111">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="60bfb-112">**Containment** - Example: VNet contains a Subnet contains a NIC</span><span class="sxs-lookup"><span data-stu-id="60bfb-112">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="60bfb-113">**Associated** - Example: NIC is associated with a VM</span><span class="sxs-lookup"><span data-stu-id="60bfb-113">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="60bfb-114">The following list is properties that are returned when querying the Topology REST API.</span><span class="sxs-lookup"><span data-stu-id="60bfb-114">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="60bfb-115">**name** - The name of the resource</span><span class="sxs-lookup"><span data-stu-id="60bfb-115">**name** - The name of the resource</span></span>
* <span data-ttu-id="60bfb-116">**id** - The uri of the resource.</span><span class="sxs-lookup"><span data-stu-id="60bfb-116">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="60bfb-117">**location** - The location where the resource exists.</span><span class="sxs-lookup"><span data-stu-id="60bfb-117">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="60bfb-118">**associations** - A list of associations to the referenced object.</span><span class="sxs-lookup"><span data-stu-id="60bfb-118">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="60bfb-119">**name** - The name of the referenced resource.</span><span class="sxs-lookup"><span data-stu-id="60bfb-119">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="60bfb-120">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span><span class="sxs-lookup"><span data-stu-id="60bfb-120">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="60bfb-121">**associationType** - This value references the relationship between the child object and the parent.</span><span class="sxs-lookup"><span data-stu-id="60bfb-121">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="60bfb-122">Valid values are **Contains** or **Associated**.</span><span class="sxs-lookup"><span data-stu-id="60bfb-122">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="60bfb-123">Before you begin</span><span class="sxs-lookup"><span data-stu-id="60bfb-123">Before you begin</span></span>

<span data-ttu-id="60bfb-124">In this scenario, you retrieve the topology information.</span><span class="sxs-lookup"><span data-stu-id="60bfb-124">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="60bfb-125">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60bfb-125">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="60bfb-126">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="60bfb-126">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="60bfb-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="60bfb-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="60bfb-128">Scenario</span><span class="sxs-lookup"><span data-stu-id="60bfb-128">Scenario</span></span>

<span data-ttu-id="60bfb-129">The scenario covered in this article retrieves the topology response for a given resource group.</span><span class="sxs-lookup"><span data-stu-id="60bfb-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="60bfb-130">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="60bfb-130">Log in with ARMClient</span></span>

<span data-ttu-id="60bfb-131">Log in to armclient with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="60bfb-131">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="60bfb-132">Retrieve topology</span><span class="sxs-lookup"><span data-stu-id="60bfb-132">Retrieve topology</span></span>

<span data-ttu-id="60bfb-133">The following example requests the topology from the REST API.</span><span class="sxs-lookup"><span data-stu-id="60bfb-133">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="60bfb-134">The example is parameterized to allow for flexibility in creating an example.</span><span class="sxs-lookup"><span data-stu-id="60bfb-134">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="60bfb-135">Replace all values with \< \> surrounding them.</span><span class="sxs-lookup"><span data-stu-id="60bfb-135">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="60bfb-136">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span><span class="sxs-lookup"><span data-stu-id="60bfb-136">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="60bfb-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="60bfb-137">Next steps</span></span>

<span data-ttu-id="60bfb-138">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="60bfb-138">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

