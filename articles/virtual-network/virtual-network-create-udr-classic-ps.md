---
title: Control routing in an Azure Virtual Network - PowerShell - Classic | Microsoft Docs
description: Learn how to control routing in VNets using PowerShell | Classic
services: virtual-network
documentationcenter: na
author: genlin
manager: cshepard
editor: ''
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: genli
ms.openlocfilehash: 930676a396ae316ec761ba5d03ad1a1d0fd7a425
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803145"
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="e9c21-103">Control routing and use virtual appliances (classic) using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9c21-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](tutorial-create-route-table-powershell.md)
> * [Azure CLI](tutorial-create-route-table-cli.md)
> * [PowerShell (Classic)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Classic)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic. Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource. You can view the documentation for different tools by selecting an option at the top of this article. This article covers the classic deployment model.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="e9c21-112">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="e9c21-112">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="e9c21-113">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e9c21-113">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="e9c21-114">Create the UDR for the front end subnet</span><span class="sxs-lookup"><span data-stu-id="e9c21-114">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="e9c21-115">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="e9c21-115">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e9c21-116">Run the following command to create a route table for the front-end subnet:</span><span class="sxs-lookup"><span data-stu-id="e9c21-116">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="e9c21-117">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e9c21-117">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="e9c21-118">Run the following command to associate the route table with the **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="e9c21-118">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="e9c21-119">Create the UDR for the back-end subnet</span><span class="sxs-lookup"><span data-stu-id="e9c21-119">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="e9c21-120">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9c21-120">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="e9c21-121">Run the following command to create a route table for the back-end subnet:</span><span class="sxs-lookup"><span data-stu-id="e9c21-121">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="e9c21-122">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e9c21-122">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="e9c21-123">Run the following command to associate the route table with the **BackEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="e9c21-123">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="e9c21-124">Enable IP forwarding on the FW1 VM</span><span class="sxs-lookup"><span data-stu-id="e9c21-124">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="e9c21-125">To enable IP forwarding in the FW1 VM, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9c21-125">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="e9c21-126">Run the following command to check the status of IP forwarding:</span><span class="sxs-lookup"><span data-stu-id="e9c21-126">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="e9c21-127">Run the following command to enable IP forwarding for the *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="e9c21-127">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
