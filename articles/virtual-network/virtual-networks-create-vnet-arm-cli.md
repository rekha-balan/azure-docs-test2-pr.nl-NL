---
title: Create a virtual network - Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a virtual network using the Azure CLI 2.0.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554487"
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="ac481-103">Create a virtual network using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ac481-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="ac481-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="ac481-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ac481-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="ac481-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="ac481-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="ac481-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ac481-107">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="ac481-107">CLI versions to complete the task</span></span>
<span data-ttu-id="ac481-108">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="ac481-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ac481-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span><span class="sxs-lookup"><span data-stu-id="ac481-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="ac481-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span><span class="sxs-lookup"><span data-stu-id="ac481-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="ac481-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="ac481-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Template](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Classic)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Classic)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Classic)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="ac481-119">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="ac481-119">Create a virtual network</span></span>

<span data-ttu-id="ac481-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="ac481-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="ac481-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ac481-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="ac481-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span><span class="sxs-lookup"><span data-stu-id="ac481-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="ac481-123">Create a VNet and a subnet:</span><span class="sxs-lookup"><span data-stu-id="ac481-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="ac481-124">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ac481-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="ac481-125">Parameters used:</span><span class="sxs-lookup"><span data-stu-id="ac481-125">Parameters used:</span></span>

    - <span data-ttu-id="ac481-126">`--name TestVNet`: Name of the VNet to be created.</span><span class="sxs-lookup"><span data-stu-id="ac481-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="ac481-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span><span class="sxs-lookup"><span data-stu-id="ac481-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="ac481-128">`--location centralus`: The location into which to deploy.</span><span class="sxs-lookup"><span data-stu-id="ac481-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="ac481-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span><span class="sxs-lookup"><span data-stu-id="ac481-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="ac481-130">`--subnet-name FrontEnd`: The name of the subnet.</span><span class="sxs-lookup"><span data-stu-id="ac481-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="ac481-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span><span class="sxs-lookup"><span data-stu-id="ac481-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="ac481-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="ac481-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="ac481-133">Which produces the following output:</span><span class="sxs-lookup"><span data-stu-id="ac481-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="ac481-134">Create a subnet:</span><span class="sxs-lookup"><span data-stu-id="ac481-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="ac481-135">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ac481-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="ac481-136">Parameters used:</span><span class="sxs-lookup"><span data-stu-id="ac481-136">Parameters used:</span></span>

    - <span data-ttu-id="ac481-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span><span class="sxs-lookup"><span data-stu-id="ac481-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="ac481-138">`--name BackEnd`: Name of the new subnet.</span><span class="sxs-lookup"><span data-stu-id="ac481-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="ac481-139">`--resource-group TestRG`: The resource group.</span><span class="sxs-lookup"><span data-stu-id="ac481-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="ac481-140">`--vnet-name TestVNet`: The name of the owning VNet.</span><span class="sxs-lookup"><span data-stu-id="ac481-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="ac481-141">Query the properties of the new VNet:</span><span class="sxs-lookup"><span data-stu-id="ac481-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="ac481-142">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ac481-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="ac481-143">Query the properties of the subnets:</span><span class="sxs-lookup"><span data-stu-id="ac481-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="ac481-144">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ac481-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="ac481-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac481-145">Next steps</span></span>

<span data-ttu-id="ac481-146">Learn how to connect:</span><span class="sxs-lookup"><span data-stu-id="ac481-146">Learn how to connect:</span></span>

- <span data-ttu-id="ac481-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span><span class="sxs-lookup"><span data-stu-id="ac481-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="ac481-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span><span class="sxs-lookup"><span data-stu-id="ac481-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="ac481-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="ac481-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="ac481-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="ac481-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="ac481-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ac481-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>