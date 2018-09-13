---
title: View Azure Network Watcher topology - PowerShell | Microsoft Docs
description: This article will describe how to use PowerShell to query your network topology.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6b370e26401aa2f6f1aa34a98b11d349908361be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553335"
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="3d30c-103">View Network Watcher topology with PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d30c-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

<span data-ttu-id="3d30c-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span><span class="sxs-lookup"><span data-stu-id="3d30c-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="3d30c-108">In the portal, this visualization is presented to you automatically.</span><span class="sxs-lookup"><span data-stu-id="3d30c-108">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="3d30c-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d30c-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="3d30c-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span><span class="sxs-lookup"><span data-stu-id="3d30c-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="3d30c-111">The interconnection is modeled under two relationships.</span><span class="sxs-lookup"><span data-stu-id="3d30c-111">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="3d30c-112">**Containment** - Example: VNet contains a Subnet contains a NIC</span><span class="sxs-lookup"><span data-stu-id="3d30c-112">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="3d30c-113">**Associated** - Example: NIC is associated with a VM</span><span class="sxs-lookup"><span data-stu-id="3d30c-113">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="3d30c-114">The following list is properties that are returned when querying the Topology REST API.</span><span class="sxs-lookup"><span data-stu-id="3d30c-114">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="3d30c-115">**name** - The name of the resource</span><span class="sxs-lookup"><span data-stu-id="3d30c-115">**name** - The name of the resource</span></span>
* <span data-ttu-id="3d30c-116">**id** - The uri of the resource.</span><span class="sxs-lookup"><span data-stu-id="3d30c-116">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="3d30c-117">**location** - The location where the resource exists.</span><span class="sxs-lookup"><span data-stu-id="3d30c-117">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="3d30c-118">**associations** - A list of associations to the referenced object.</span><span class="sxs-lookup"><span data-stu-id="3d30c-118">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="3d30c-119">**name** - The name of the referenced resource.</span><span class="sxs-lookup"><span data-stu-id="3d30c-119">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="3d30c-120">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span><span class="sxs-lookup"><span data-stu-id="3d30c-120">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="3d30c-121">**associationType** - This value references the relationship between the child object and the parent.</span><span class="sxs-lookup"><span data-stu-id="3d30c-121">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="3d30c-122">Valid values are **Contains** or **Associated**.</span><span class="sxs-lookup"><span data-stu-id="3d30c-122">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3d30c-123">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3d30c-123">Before you begin</span></span>

<span data-ttu-id="3d30c-124">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span><span class="sxs-lookup"><span data-stu-id="3d30c-124">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="3d30c-125">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3d30c-125">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="3d30c-126">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="3d30c-126">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3d30c-127">Scenario</span><span class="sxs-lookup"><span data-stu-id="3d30c-127">Scenario</span></span>

<span data-ttu-id="3d30c-128">The scenario covered in this article retrieves the topology response for a given resource group.</span><span class="sxs-lookup"><span data-stu-id="3d30c-128">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="3d30c-129">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="3d30c-129">Retrieve Network Watcher</span></span>

<span data-ttu-id="3d30c-130">The first step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="3d30c-130">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="3d30c-131">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d30c-131">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="3d30c-132">Retrieve topology</span><span class="sxs-lookup"><span data-stu-id="3d30c-132">Retrieve topology</span></span>

<span data-ttu-id="3d30c-133">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span><span class="sxs-lookup"><span data-stu-id="3d30c-133">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="3d30c-134">Results</span><span class="sxs-lookup"><span data-stu-id="3d30c-134">Results</span></span>

<span data-ttu-id="3d30c-135">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3d30c-135">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="3d30c-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="3d30c-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="3d30c-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d30c-137">Next steps</span></span>

<span data-ttu-id="3d30c-138">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3d30c-138">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


