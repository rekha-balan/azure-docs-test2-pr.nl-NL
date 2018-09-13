---
title: View Azure Network Watcher topology - Azure CLI | Microsoft Docs
description: This article will describe how to use Azure CLI to query your network topology.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 20e435091a228fd28152ec32d8f38303da606bf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564387"
---
# <a name="view-network-watcher-topology-with-azure-cli"></a><span data-ttu-id="a7367-103">View Network Watcher topology with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7367-103">View Network Watcher topology with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

<span data-ttu-id="a7367-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span><span class="sxs-lookup"><span data-stu-id="a7367-107">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="a7367-108">In the portal, this visualization is presented to you automatically.</span><span class="sxs-lookup"><span data-stu-id="a7367-108">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="a7367-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a7367-109">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="a7367-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span><span class="sxs-lookup"><span data-stu-id="a7367-110">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="a7367-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="a7367-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="a7367-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="a7367-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

<span data-ttu-id="a7367-113">The interconnection is modeled under two relationships.</span><span class="sxs-lookup"><span data-stu-id="a7367-113">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="a7367-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span><span class="sxs-lookup"><span data-stu-id="a7367-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="a7367-115">**Associated** - Example: NIC is associated with a VM</span><span class="sxs-lookup"><span data-stu-id="a7367-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="a7367-116">The following list is properties that are returned when querying the Topology REST API.</span><span class="sxs-lookup"><span data-stu-id="a7367-116">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="a7367-117">**name** - The name of the resource</span><span class="sxs-lookup"><span data-stu-id="a7367-117">**name** - The name of the resource</span></span>
* <span data-ttu-id="a7367-118">**id** - The uri of the resource.</span><span class="sxs-lookup"><span data-stu-id="a7367-118">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="a7367-119">**location** - The location where the resource exists.</span><span class="sxs-lookup"><span data-stu-id="a7367-119">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="a7367-120">**associations** - A list of associations to the referenced object.</span><span class="sxs-lookup"><span data-stu-id="a7367-120">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="a7367-121">**name** - The name of the referenced resource.</span><span class="sxs-lookup"><span data-stu-id="a7367-121">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="a7367-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span><span class="sxs-lookup"><span data-stu-id="a7367-122">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="a7367-123">**associationType** - This value references the relationship between the child object and the parent.</span><span class="sxs-lookup"><span data-stu-id="a7367-123">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="a7367-124">Valid values are **Contains** or **Associated**.</span><span class="sxs-lookup"><span data-stu-id="a7367-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7367-125">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a7367-125">Before you begin</span></span>

<span data-ttu-id="a7367-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span><span class="sxs-lookup"><span data-stu-id="a7367-126">In this scenario, you use the `network watcher topology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="a7367-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a7367-127">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="a7367-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a7367-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a7367-129">Scenario</span><span class="sxs-lookup"><span data-stu-id="a7367-129">Scenario</span></span>

<span data-ttu-id="a7367-130">The scenario covered in this article retrieves the topology response for a given resource group.</span><span class="sxs-lookup"><span data-stu-id="a7367-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="a7367-131">Retrieve topology</span><span class="sxs-lookup"><span data-stu-id="a7367-131">Retrieve topology</span></span>

<span data-ttu-id="a7367-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span><span class="sxs-lookup"><span data-stu-id="a7367-132">The `network watcher topology` cmdlet retrieves the topology for a given resource group.</span></span> <span data-ttu-id="a7367-133">Add the argument "--json" to view the oput in json format</span><span class="sxs-lookup"><span data-stu-id="a7367-133">Add the argument "--json" to view the oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="a7367-134">Results</span><span class="sxs-lookup"><span data-stu-id="a7367-134">Results</span></span>

<span data-ttu-id="a7367-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a7367-135">The results returned have a property name "Resources", which contains the json response body for the `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="a7367-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span><span class="sxs-lookup"><span data-stu-id="a7367-136">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="a7367-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7367-137">Next steps</span></span>

<span data-ttu-id="a7367-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a7367-138">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
