---
title: Control routing and virtual appliances using the Azure CLI 2.0 | Microsoft Docs
description: Learn how to control routing and virtual appliances using the Azure CLI 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: fc2f54e5626313b5f82a8e5ce85e6af45a2ec400
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671232"
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="f1c55-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f1c55-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Template](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Classic deployment)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Classic deployment)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f1c55-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="f1c55-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="f1c55-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="f1c55-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="f1c55-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span><span class="sxs-lookup"><span data-stu-id="f1c55-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="f1c55-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span><span class="sxs-lookup"><span data-stu-id="f1c55-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="f1c55-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="f1c55-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="f1c55-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="f1c55-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="f1c55-115">Create the UDR for the front-end subnet</span><span class="sxs-lookup"><span data-stu-id="f1c55-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="f1c55-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="f1c55-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="f1c55-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span><span class="sxs-lookup"><span data-stu-id="f1c55-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="f1c55-118">Output:</span><span class="sxs-lookup"><span data-stu-id="f1c55-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="f1c55-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span><span class="sxs-lookup"><span data-stu-id="f1c55-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="f1c55-120">Output:</span><span class="sxs-lookup"><span data-stu-id="f1c55-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="f1c55-121">Parameters:</span><span class="sxs-lookup"><span data-stu-id="f1c55-121">Parameters:</span></span>

    * <span data-ttu-id="f1c55-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-122">**--route-table-name**.</span></span> <span data-ttu-id="f1c55-123">Name of the route table where the route will be added.</span><span class="sxs-lookup"><span data-stu-id="f1c55-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="f1c55-124">For our scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="f1c55-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-125">**--address-prefix**.</span></span> <span data-ttu-id="f1c55-126">Address prefix for the subnet where packets are destined to.</span><span class="sxs-lookup"><span data-stu-id="f1c55-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="f1c55-127">For our scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="f1c55-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-128">**--next-hop-type**.</span></span> <span data-ttu-id="f1c55-129">Type of object traffic will be sent to.</span><span class="sxs-lookup"><span data-stu-id="f1c55-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="f1c55-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="f1c55-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="f1c55-132">IP address for next hop.</span><span class="sxs-lookup"><span data-stu-id="f1c55-132">IP address for next hop.</span></span> <span data-ttu-id="f1c55-133">For our scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="f1c55-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="f1c55-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="f1c55-135">Output:</span><span class="sxs-lookup"><span data-stu-id="f1c55-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="f1c55-136">Parameters:</span><span class="sxs-lookup"><span data-stu-id="f1c55-136">Parameters:</span></span>
    
    * <span data-ttu-id="f1c55-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-137">**--vnet-name**.</span></span> <span data-ttu-id="f1c55-138">Name of the VNet where the subnet is located.</span><span class="sxs-lookup"><span data-stu-id="f1c55-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="f1c55-139">For our scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="f1c55-140">Create the UDR for the back-end subnet</span><span class="sxs-lookup"><span data-stu-id="f1c55-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="f1c55-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1c55-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="f1c55-142">Run the following command to create a route table for the back-end subnet:</span><span class="sxs-lookup"><span data-stu-id="f1c55-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="f1c55-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f1c55-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="f1c55-144">Run the following command to associate the route table with the **BackEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="f1c55-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="f1c55-145">Enable IP forwarding on FW1</span><span class="sxs-lookup"><span data-stu-id="f1c55-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="f1c55-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1c55-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="f1c55-147">Run the [az network nic show](/cli/az/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span><span class="sxs-lookup"><span data-stu-id="f1c55-147">Run the [az network nic show](/cli/az/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="f1c55-148">It should be set to *false*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="f1c55-149">Output:</span><span class="sxs-lookup"><span data-stu-id="f1c55-149">Output:</span></span>

        false

2. <span data-ttu-id="f1c55-150">Run the following command to enable IP forwarding:</span><span class="sxs-lookup"><span data-stu-id="f1c55-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="f1c55-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span><span class="sxs-lookup"><span data-stu-id="f1c55-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="f1c55-152">Output:</span><span class="sxs-lookup"><span data-stu-id="f1c55-152">Output:</span></span>

        true

    <span data-ttu-id="f1c55-153">Parameters:</span><span class="sxs-lookup"><span data-stu-id="f1c55-153">Parameters:</span></span>

    <span data-ttu-id="f1c55-154">**--ip-forwarding**: *true* or *false*.</span><span class="sxs-lookup"><span data-stu-id="f1c55-154">**--ip-forwarding**: *true* or *false*.</span></span>

