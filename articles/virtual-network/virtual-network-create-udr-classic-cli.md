---
title: Control routing in an Azure Virtual Network - CLI - Classic | Microsoft Docs
description: Learn how to control routing in VNets using the Azure CLI in the classic deployment model
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: ''
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555624"
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="53a2d-103">Control routing and use virtual appliances (classic) using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53a2d-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Template](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Classic)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Classic)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="53a2d-109">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="53a2d-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="53a2d-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="53a2d-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="53a2d-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="53a2d-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="53a2d-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="53a2d-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="53a2d-113">Create the UDR for the front end subnet</span><span class="sxs-lookup"><span data-stu-id="53a2d-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="53a2d-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="53a2d-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="53a2d-115">Run the following command to switch to classic mode:</span><span class="sxs-lookup"><span data-stu-id="53a2d-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="53a2d-116">Output:</span><span class="sxs-lookup"><span data-stu-id="53a2d-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="53a2d-117">Run the following command to create a route table for the front-end subnet:</span><span class="sxs-lookup"><span data-stu-id="53a2d-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="53a2d-118">Output:</span><span class="sxs-lookup"><span data-stu-id="53a2d-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="53a2d-119">Parameters:</span><span class="sxs-lookup"><span data-stu-id="53a2d-119">Parameters:</span></span>
   
   * <span data-ttu-id="53a2d-120">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-120">**-l (or --location)**.</span></span> <span data-ttu-id="53a2d-121">Azure region where the new NSG will be created.</span><span class="sxs-lookup"><span data-stu-id="53a2d-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="53a2d-122">For our scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="53a2d-123">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-123">**-n (or --name)**.</span></span> <span data-ttu-id="53a2d-124">Name for the new NSG.</span><span class="sxs-lookup"><span data-stu-id="53a2d-124">Name for the new NSG.</span></span> <span data-ttu-id="53a2d-125">For our scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="53a2d-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="53a2d-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="53a2d-127">Output:</span><span class="sxs-lookup"><span data-stu-id="53a2d-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="53a2d-128">Parameters:</span><span class="sxs-lookup"><span data-stu-id="53a2d-128">Parameters:</span></span>
   
   * <span data-ttu-id="53a2d-129">**-r (or --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="53a2d-130">Name of the route table where the route will be added.</span><span class="sxs-lookup"><span data-stu-id="53a2d-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="53a2d-131">For our scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="53a2d-132">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="53a2d-133">Address prefix for the subnet where packets are destined to.</span><span class="sxs-lookup"><span data-stu-id="53a2d-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="53a2d-134">For our scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="53a2d-135">**-t (or --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="53a2d-136">Type of object traffic will be sent to.</span><span class="sxs-lookup"><span data-stu-id="53a2d-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="53a2d-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="53a2d-138">**-p (or --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="53a2d-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="53a2d-139">IP address for next hop.</span><span class="sxs-lookup"><span data-stu-id="53a2d-139">IP address for next hop.</span></span> <span data-ttu-id="53a2d-140">For our scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="53a2d-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="53a2d-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="53a2d-142">Output:</span><span class="sxs-lookup"><span data-stu-id="53a2d-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="53a2d-143">Parameters:</span><span class="sxs-lookup"><span data-stu-id="53a2d-143">Parameters:</span></span>
   
   * <span data-ttu-id="53a2d-144">**-t (or --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="53a2d-145">Name of the VNet where the subnet is located.</span><span class="sxs-lookup"><span data-stu-id="53a2d-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="53a2d-146">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="53a2d-147">**-n (or --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="53a2d-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="53a2d-148">Name of the subnet the route table will be added to.</span><span class="sxs-lookup"><span data-stu-id="53a2d-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="53a2d-149">For our scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="53a2d-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="53a2d-150">Create the UDR for the back-end subnet</span><span class="sxs-lookup"><span data-stu-id="53a2d-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="53a2d-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="53a2d-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="53a2d-152">Run the following command to create a route table for the back-end subnet:</span><span class="sxs-lookup"><span data-stu-id="53a2d-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="53a2d-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="53a2d-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="53a2d-154">Run the following command to associate the route table with the **BackEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="53a2d-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

