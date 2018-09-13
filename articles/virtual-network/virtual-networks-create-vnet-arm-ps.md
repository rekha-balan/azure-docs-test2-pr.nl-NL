---
title: Create a virtual network - Azure PowerShell | Microsoft Docs
description: Learn how to create a virtual network using PowerShell.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d6ea6100045bf89c19190272605fe6635a268bae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556062"
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="e1c7a-103">Create a virtual network using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c7a-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="e1c7a-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e1c7a-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="e1c7a-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="e1c7a-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e1c7a-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Template](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Classic)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Classic)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Classic)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="e1c7a-116">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="e1c7a-116">Create a virtual network</span></span>

<span data-ttu-id="e1c7a-117">To create a virtual network using PowerShell, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="e1c7a-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span></span>

2. <span data-ttu-id="e1c7a-119">If necessary, create a new resource group, as shown below.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="e1c7a-120">For this scenario, create a resource group named *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="e1c7a-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1c7a-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="e1c7a-122">Expected output:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="e1c7a-123">Create a new VNet named *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="e1c7a-124">Expected output:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="e1c7a-125">Store the virtual network object in a variable:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.
   > 

5. <span data-ttu-id="e1c7a-127">Add a subnet to the new VNet variable:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="e1c7a-128">Expected output:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="e1c7a-129">Repeat step 5 above for each subnet you want to create.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="e1c7a-130">The following command creates the *BackEnd* subnet for the scenario:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="e1c7a-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="e1c7a-132">To save the changes to Azure, run the following command:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="e1c7a-133">Expected output:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="e1c7a-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1c7a-134">Next steps</span></span>

<span data-ttu-id="e1c7a-135">Learn how to connect:</span><span class="sxs-lookup"><span data-stu-id="e1c7a-135">Learn how to connect:</span></span>

- <span data-ttu-id="e1c7a-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="e1c7a-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="e1c7a-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="e1c7a-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="e1c7a-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span><span class="sxs-lookup"><span data-stu-id="e1c7a-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
