---
title: Control routing and virtual appliances using the Azure CLI 1.0 | Microsoft Docs
description: Learn how to control routing and virtual appliances using the Azure CLI 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563412"
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="62eb6-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="62eb6-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Template](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Classic)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Classic)](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="62eb6-109">Create custom routing and virtual appliances using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="62eb6-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="62eb6-110">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="62eb6-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="62eb6-111">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="62eb6-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="62eb6-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="62eb6-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="62eb6-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="62eb6-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="62eb6-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="62eb6-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="62eb6-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="62eb6-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="62eb6-116">Create the UDR for the front-end subnet</span><span class="sxs-lookup"><span data-stu-id="62eb6-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="62eb6-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="62eb6-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="62eb6-118">Run the following command to create a route table for the front-end subnet:</span><span class="sxs-lookup"><span data-stu-id="62eb6-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="62eb6-119">Output:</span><span class="sxs-lookup"><span data-stu-id="62eb6-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="62eb6-120">Parameters:</span><span class="sxs-lookup"><span data-stu-id="62eb6-120">Parameters:</span></span>
   
   * <span data-ttu-id="62eb6-121">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="62eb6-122">Name of the resource group where the UDR will be created.</span><span class="sxs-lookup"><span data-stu-id="62eb6-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="62eb6-123">For our scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="62eb6-124">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-124">**-l (or --location)**.</span></span> <span data-ttu-id="62eb6-125">Azure region where the new UDR will be created.</span><span class="sxs-lookup"><span data-stu-id="62eb6-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="62eb6-126">For our scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="62eb6-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-127">**-n (or --name)**.</span></span> <span data-ttu-id="62eb6-128">Name for the new UDR.</span><span class="sxs-lookup"><span data-stu-id="62eb6-128">Name for the new UDR.</span></span> <span data-ttu-id="62eb6-129">For our scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="62eb6-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="62eb6-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="62eb6-131">Output:</span><span class="sxs-lookup"><span data-stu-id="62eb6-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="62eb6-132">Parameters:</span><span class="sxs-lookup"><span data-stu-id="62eb6-132">Parameters:</span></span>
   
   * <span data-ttu-id="62eb6-133">**-r (or --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="62eb6-134">Name of the route table where the route will be added.</span><span class="sxs-lookup"><span data-stu-id="62eb6-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="62eb6-135">For our scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="62eb6-136">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="62eb6-137">Address prefix for the subnet where packets are destined to.</span><span class="sxs-lookup"><span data-stu-id="62eb6-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="62eb6-138">For our scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="62eb6-139">**-y (or --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="62eb6-140">Type of object traffic will be sent to.</span><span class="sxs-lookup"><span data-stu-id="62eb6-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="62eb6-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="62eb6-142">**-p (or --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="62eb6-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="62eb6-143">IP address for next hop.</span><span class="sxs-lookup"><span data-stu-id="62eb6-143">IP address for next hop.</span></span> <span data-ttu-id="62eb6-144">For our scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="62eb6-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="62eb6-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="62eb6-146">Output:</span><span class="sxs-lookup"><span data-stu-id="62eb6-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="62eb6-147">Parameters:</span><span class="sxs-lookup"><span data-stu-id="62eb6-147">Parameters:</span></span>
   
   * <span data-ttu-id="62eb6-148">**-e (or --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="62eb6-149">Name of the VNet where the subnet is located.</span><span class="sxs-lookup"><span data-stu-id="62eb6-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="62eb6-150">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="62eb6-151">Create the UDR for the back-end subnet</span><span class="sxs-lookup"><span data-stu-id="62eb6-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="62eb6-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="62eb6-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="62eb6-153">Run the following command to create a route table for the back-end subnet:</span><span class="sxs-lookup"><span data-stu-id="62eb6-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="62eb6-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="62eb6-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="62eb6-155">Run the following command to associate the route table with the **BackEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="62eb6-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="62eb6-156">Enable IP forwarding on FW1</span><span class="sxs-lookup"><span data-stu-id="62eb6-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="62eb6-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="62eb6-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="62eb6-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="62eb6-159">It should be set to *false*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="62eb6-160">Output:</span><span class="sxs-lookup"><span data-stu-id="62eb6-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="62eb6-161">Run the following command to enable IP forwarding:</span><span class="sxs-lookup"><span data-stu-id="62eb6-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="62eb6-162">Output:</span><span class="sxs-lookup"><span data-stu-id="62eb6-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="62eb6-163">Parameters:</span><span class="sxs-lookup"><span data-stu-id="62eb6-163">Parameters:</span></span>
   
   * <span data-ttu-id="62eb6-164">**-f (or --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="62eb6-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="62eb6-165">*true* or *false*.</span><span class="sxs-lookup"><span data-stu-id="62eb6-165">*true* or *false*.</span></span>

