---
title: Azure Virtual Network peering - PowerShell | Microsoft Docs
description: Learn how to create a virtual network peering using Azure PowerShell.
services: virtual-network
documentationcenter: ''
author: NarayanAnnamalai
manager: jefco
editor: ''
tags: azure-resource-manager
ms.assetid: dac579bd-7545-461a-bdac-301c87434c84
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: narayan; annahar
ms.openlocfilehash: b0375a99f5ea3d6af2d3ead382f9a43f1fd285f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555492"
---
# <a name="create-a-virtual-network-peering-using-azure-powershell"></a><span data-ttu-id="1de9c-103">Create a virtual network peering using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1de9c-103">Create a virtual network peering using Azure PowerShell</span></span>
[!INCLUDE [virtual-networks-create-vnet-selectors-arm-include](../../includes/virtual-networks-create-vnetpeering-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnetpeering-intro-include.md)]

[!INCLUDE [virtual-networks-create-vnet-scenario-basic-include](../../includes/virtual-networks-create-vnetpeering-scenario-basic-include.md)]

<span data-ttu-id="1de9c-104">To create a VNet peering by using PowerShell, please follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="1de9c-104">To create a VNet peering by using PowerShell, please follow the steps below:</span></span>

1. <span data-ttu-id="1de9c-105">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="1de9c-105">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1de9c-106">The PowerShell cmdlet for managing VNet peering is shipped with [Azure PowerShell 1.6.](http://www.powershellgallery.com/packages/Azure/1.6.0)</span><span class="sxs-lookup"><span data-stu-id="1de9c-106">The PowerShell cmdlet for managing VNet peering is shipped with [Azure PowerShell 1.6.](http://www.powershellgallery.com/packages/Azure/1.6.0)</span></span>
    >

2. <span data-ttu-id="1de9c-107">Read virtual network objects:</span><span class="sxs-lookup"><span data-stu-id="1de9c-107">Read virtual network objects:</span></span>

    ```powershell
    $vnet1 = Get-AzureRmVirtualNetwork -ResourceGroupName vnet101 -Name vnet1
    $vnet2 = Get-AzureRmVirtualNetwork -ResourceGroupName vnet101 -Name vnet2
    ```

3. <span data-ttu-id="1de9c-108">To establish VNet peering, you need to create two links, one for each direction.</span><span class="sxs-lookup"><span data-stu-id="1de9c-108">To establish VNet peering, you need to create two links, one for each direction.</span></span> <span data-ttu-id="1de9c-109">The following step will create a VNet peering link for VNet1 to VNet2 first:</span><span class="sxs-lookup"><span data-stu-id="1de9c-109">The following step will create a VNet peering link for VNet1 to VNet2 first:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet2 -VirtualNetwork $vnet1 -RemoteVirtualNetworkId $vnet2.Id
    ```

    <span data-ttu-id="1de9c-110">Returned output:</span><span class="sxs-lookup"><span data-stu-id="1de9c-110">Returned output:</span></span>
        
        Name            : LinkToVNet2
        Id: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet1/virtualNetworkPeerings/LinkToVNet2
        Etag            : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName    : vnet101
        VirtualNetworkName    : vnet1
        PeeringState        : Initiated
        ProvisioningState    : Succeeded
        RemoteVirtualNetwork    : {
        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet2"
                                        }
        AllowVirtualNetworkAccess    : True
        AllowForwardedTraffic    : False
        AllowGatewayTransit    : False
            UseRemoteGateways    : False
            RemoteGateways        : null
            RemoteVirtualNetworkAddressSpace : null

4. <span data-ttu-id="1de9c-111">This step will create a VNet peering link for VNet2 to VNet1:</span><span class="sxs-lookup"><span data-stu-id="1de9c-111">This step will create a VNet peering link for VNet2 to VNet1:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet1 -VirtualNetwork $vnet2 -RemoteVirtualNetworkId $vnet1.Id
    ```

    <span data-ttu-id="1de9c-112">Returned output:</span><span class="sxs-lookup"><span data-stu-id="1de9c-112">Returned output:</span></span>

        Name            : LinkToVNet1
        Id                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet2/virtualNetworkPeerings/LinkToVNet1
        Etag            : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName    : vnet101
        VirtualNetworkName    : vnet2
        PeeringState        : Connected
        ProvisioningState    : Succeeded
        RemoteVirtualNetwork    : {
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet1"
                                        }
        AllowVirtualNetworkAccess    : True
        AllowForwardedTraffic    : False
        AllowGatewayTransit    : False
        UseRemoteGateways    : False
        RemoteGateways        : null
        RemoteVirtualNetworkAddressSpace : null
5. <span data-ttu-id="1de9c-113">Once the VNet peering link is created, enter the following command to view the link state:</span><span class="sxs-lookup"><span data-stu-id="1de9c-113">Once the VNet peering link is created, enter the following command to view the link state:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering -VirtualNetworkName vnet1 -ResourceGroupName vnet101 -Name linktovnet2
    ```

    <span data-ttu-id="1de9c-114">Returned output:</span><span class="sxs-lookup"><span data-stu-id="1de9c-114">Returned output:</span></span>
   
        Name            : LinkToVNet2
        Id                : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet1/virtualNetworkPeerings/LinkToVNet2
        Etag            : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName    : vnet101
        VirtualNetworkName    : vnet1
        PeeringState        : Connected
        ProvisioningState    : Succeeded
        RemoteVirtualNetwork    : {
                                             "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet2"
                                        }
        AllowVirtualNetworkAccess    : True
        AllowForwardedTraffic            : False
        AllowGatewayTransit              : False
        UseRemoteGateways                : False
        RemoteGateways                   : null
        RemoteVirtualNetworkAddressSpace : null
   
    <span data-ttu-id="1de9c-115">There are a few configurable properties for VNet peering:</span><span class="sxs-lookup"><span data-stu-id="1de9c-115">There are a few configurable properties for VNet peering:</span></span>
   
   | <span data-ttu-id="1de9c-116">Option</span><span class="sxs-lookup"><span data-stu-id="1de9c-116">Option</span></span> | <span data-ttu-id="1de9c-117">Description</span><span class="sxs-lookup"><span data-stu-id="1de9c-117">Description</span></span> | <span data-ttu-id="1de9c-118">Default</span><span class="sxs-lookup"><span data-stu-id="1de9c-118">Default</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="1de9c-119">AllowVirtualNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="1de9c-119">AllowVirtualNetworkAccess</span></span> |<span data-ttu-id="1de9c-120">Whether address space of Peer VNet to be included as part of the Virtual_network Tag</span><span class="sxs-lookup"><span data-stu-id="1de9c-120">Whether address space of Peer VNet to be included as part of the Virtual_network Tag</span></span> |<span data-ttu-id="1de9c-121">Yes</span><span class="sxs-lookup"><span data-stu-id="1de9c-121">Yes</span></span> |
   | <span data-ttu-id="1de9c-122">AllowForwardedTraffic</span><span class="sxs-lookup"><span data-stu-id="1de9c-122">AllowForwardedTraffic</span></span> |<span data-ttu-id="1de9c-123">Whether traffic not originating from a peered VNet is accepted or dropped</span><span class="sxs-lookup"><span data-stu-id="1de9c-123">Whether traffic not originating from a peered VNet is accepted or dropped</span></span> |<span data-ttu-id="1de9c-124">No</span><span class="sxs-lookup"><span data-stu-id="1de9c-124">No</span></span> |
   | <span data-ttu-id="1de9c-125">AllowGatewayTransit</span><span class="sxs-lookup"><span data-stu-id="1de9c-125">AllowGatewayTransit</span></span> |<span data-ttu-id="1de9c-126">Allows the peer VNet to use your VNet gateway</span><span class="sxs-lookup"><span data-stu-id="1de9c-126">Allows the peer VNet to use your VNet gateway</span></span> |<span data-ttu-id="1de9c-127">No</span><span class="sxs-lookup"><span data-stu-id="1de9c-127">No</span></span> |
   | <span data-ttu-id="1de9c-128">UseRemoteGateways</span><span class="sxs-lookup"><span data-stu-id="1de9c-128">UseRemoteGateways</span></span> |<span data-ttu-id="1de9c-129">Use your peer’s VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="1de9c-129">Use your peer’s VNet gateway.</span></span> <span data-ttu-id="1de9c-130">The peer VNet must have a gateway configured and AllowGatewayTransit selected.</span><span class="sxs-lookup"><span data-stu-id="1de9c-130">The peer VNet must have a gateway configured and AllowGatewayTransit selected.</span></span> <span data-ttu-id="1de9c-131">You cannot use this option if you have a gateway configured</span><span class="sxs-lookup"><span data-stu-id="1de9c-131">You cannot use this option if you have a gateway configured</span></span> |<span data-ttu-id="1de9c-132">No</span><span class="sxs-lookup"><span data-stu-id="1de9c-132">No</span></span> |

    <span data-ttu-id="1de9c-133">Each link in a VNet peering has the previous set of properties.</span><span class="sxs-lookup"><span data-stu-id="1de9c-133">Each link in a VNet peering has the previous set of properties.</span></span> <span data-ttu-id="1de9c-134">For example, you can set `AllowVirtualNetworkAccess` to *True* for VNet peering link VNet1 to VNet2 and set it to *False* for the VNet peering link in the other direction.</span><span class="sxs-lookup"><span data-stu-id="1de9c-134">For example, you can set `AllowVirtualNetworkAccess` to *True* for VNet peering link VNet1 to VNet2 and set it to *False* for the VNet peering link in the other direction.</span></span>

    ```powershell
    $LinktoVNet2 = Get-AzureRmVirtualNetworkPeering -VirtualNetworkName vnet1 `
    -ResourceGroupName vnet101 -Name LinkToVNet2

    $LinktoVNet2.AllowForwardedTraffic = $true
    Set-AzureRmVirtualNetworkPeering -VirtualNetworkPeering $LinktoVNet2
    ```

    <span data-ttu-id="1de9c-135">You can run `Get-AzureRmVirtualNetworkPeering` to double check the property value after the change.</span><span class="sxs-lookup"><span data-stu-id="1de9c-135">You can run `Get-AzureRmVirtualNetworkPeering` to double check the property value after the change.</span></span> <span data-ttu-id="1de9c-136">From the output, you can see `AllowForwardedTraffic` changes set to *True* after running the previous cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1de9c-136">From the output, you can see `AllowForwardedTraffic` changes set to *True* after running the previous cmdlets.</span></span>

        Name            : LinkToVNet2
        Id            : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet1/virtualNetworkPeerings/LinkToVNet2
        Etag            : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        ResourceGroupName    : vnet101
        VirtualNetworkName    : vnet1
        PeeringState        : Connected
        ProvisioningState    : Succeeded
        RemoteVirtualNetwork    : {
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/vnet101/providers/Microsoft.Network/virtualNetworks/vnet2"
                                        }
        AllowVirtualNetworkAccess    : True
        AllowForwardedTraffic        : True
        AllowGatewayTransit        : False
        UseRemoteGateways        : False
        RemoteGateways        : null
        RemoteVirtualNetworkAddressSpace : null

    <span data-ttu-id="1de9c-137">After peering is established, VMs should be able to communicate with each other across both VNets.</span><span class="sxs-lookup"><span data-stu-id="1de9c-137">After peering is established, VMs should be able to communicate with each other across both VNets.</span></span> <span data-ttu-id="1de9c-138">By default, `AllowVirtualNetworkAccess` is *True* and VNet peering will provision the proper ACLs to allow the communication between VNets.</span><span class="sxs-lookup"><span data-stu-id="1de9c-138">By default, `AllowVirtualNetworkAccess` is *True* and VNet peering will provision the proper ACLs to allow the communication between VNets.</span></span> <span data-ttu-id="1de9c-139">You can still apply network security group (NSG) rules to block connectivity between specific subnets or virtual machines to gain fine grain control of access between two VNets.</span><span class="sxs-lookup"><span data-stu-id="1de9c-139">You can still apply network security group (NSG) rules to block connectivity between specific subnets or virtual machines to gain fine grain control of access between two VNets.</span></span> <span data-ttu-id="1de9c-140">Read the [network security group](virtual-networks-create-nsg-arm-ps.md) article to learn more about NSGs.</span><span class="sxs-lookup"><span data-stu-id="1de9c-140">Read the [network security group](virtual-networks-create-nsg-arm-ps.md) article to learn more about NSGs.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-crosssub-include](../../includes/virtual-networks-create-vnetpeering-scenario-crosssub-include.md)]

<span data-ttu-id="1de9c-141">To create VNet peering across subscriptions using PowerShell, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="1de9c-141">To create VNet peering across subscriptions using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="1de9c-142">Sign in to Azure with privileged User-A's account for Subscription-A and run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1de9c-142">Sign in to Azure with privileged User-A's account for Subscription-A and run the following cmdlet:</span></span>

    ```powershell
    New-AzureRmRoleAssignment -SignInName <UserB ID> -RoleDefinitionName "Network Contributor" -Scope /subscriptions/<Subscription-A-ID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/VirtualNetworks/VNet5
    ```

    <span data-ttu-id="1de9c-143">This is not a requirement.</span><span class="sxs-lookup"><span data-stu-id="1de9c-143">This is not a requirement.</span></span> <span data-ttu-id="1de9c-144">Peering can be established even if users individually raise peering requests for their respective VNets, as long as the requests match.</span><span class="sxs-lookup"><span data-stu-id="1de9c-144">Peering can be established even if users individually raise peering requests for their respective VNets, as long as the requests match.</span></span> <span data-ttu-id="1de9c-145">Adding a privileged user of the other VNet as a user in the local VNet makes it easier to do the setup.</span><span class="sxs-lookup"><span data-stu-id="1de9c-145">Adding a privileged user of the other VNet as a user in the local VNet makes it easier to do the setup.</span></span>
2. <span data-ttu-id="1de9c-146">Sign in to Azure with privileged User-B's account for Subscription-B and run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1de9c-146">Sign in to Azure with privileged User-B's account for Subscription-B and run the following cmdlet:</span></span>

    ```powershell
    New-AzureRmRoleAssignment -SignInName <UserA ID> -RoleDefinitionName "Network Contributor" -Scope /subscriptions/<Subscription-B-ID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/VirtualNetworks/VNet3
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1de9c-147">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span><span class="sxs-lookup"><span data-stu-id="1de9c-147">If the peering you're creating is between two VNets created through the Azure Resource Manager deployment model, continue with the remaining steps in this section.</span></span> <span data-ttu-id="1de9c-148">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1de9c-148">If the two VNets were created through different deployment models, skip the remaining steps of this section and complete the steps in the [Peering virtual networks created through different deployment models](#x-model) section of this article.</span></span>

3. <span data-ttu-id="1de9c-149">In User-A’s login session, run the following command:</span><span class="sxs-lookup"><span data-stu-id="1de9c-149">In User-A’s login session, run the following command:</span></span>

    ```powershell
    $vnet3 = Get-AzureRmVirtualNetwork -ResourceGroupName hr-vnets -Name vnet3

    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet5 -VirtualNetwork $vnet3 -RemoteVirtualNetworkId "/subscriptions/<Subscription-B-Id>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/VNet5" -BlockVirtualNetworkAccess
    ```

4. <span data-ttu-id="1de9c-150">In User-B’s login session, run the cmdlet below:</span><span class="sxs-lookup"><span data-stu-id="1de9c-150">In User-B’s login session, run the cmdlet below:</span></span>

    ```powershell
    $vnet5 = Get-AzureRmVirtualNetwork -ResourceGroupName vendor-vnets -Name vnet5

    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet3 -VirtualNetwork $vnet5 -RemoteVirtualNetworkId "/subscriptions/<Subscriptoin-A-Id>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/VNet3" -BlockVirtualNetworkAccess
    ```

5. <span data-ttu-id="1de9c-151">After peering is established, any VM in VNet3 should be able to communicate with any VM in VNet5.</span><span class="sxs-lookup"><span data-stu-id="1de9c-151">After peering is established, any VM in VNet3 should be able to communicate with any VM in VNet5.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-transit-include](../../includes/virtual-networks-create-vnetpeering-scenario-transit-include.md)]

1. <span data-ttu-id="1de9c-152">In this scenario, run the following PowerShell cmdlets to establish the VNet peering.</span><span class="sxs-lookup"><span data-stu-id="1de9c-152">In this scenario, run the following PowerShell cmdlets to establish the VNet peering.</span></span> <span data-ttu-id="1de9c-153">You need to set the `AllowForwardedTraffic` property to *True* and link VNET1 to HubVNet, which allows the inbound traffic from outside of the peering VNet address space.</span><span class="sxs-lookup"><span data-stu-id="1de9c-153">You need to set the `AllowForwardedTraffic` property to *True* and link VNET1 to HubVNet, which allows the inbound traffic from outside of the peering VNet address space.</span></span>

    ```powershell
    $hubVNet = Get-AzureRmVirtualNetwork -ResourceGroupName vnet101 -Name HubVNet
    $vnet1 = Get-AzureRmVirtualNetwork -ResourceGroupName vnet101 -Name vnet1

    Add-AzureRmVirtualNetworkPeering -Name LinkToHub -VirtualNetwork $vnet1 -RemoteVirtualNetworkId $HubVNet.Id -AllowForwardedTraffic

    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet1 -VirtualNetwork $HubVNet -RemoteVirtualNetworkId $vnet1.Id
    ```

2. <span data-ttu-id="1de9c-154">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) and define a user-defined route (UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span><span class="sxs-lookup"><span data-stu-id="1de9c-154">After peering is established, you can refer to this [article](virtual-network-create-udr-arm-ps.md) and define a user-defined route (UDR) to redirect VNet1 traffic through a virtual appliance to use its capabilities.</span></span> <span data-ttu-id="1de9c-155">When you specify the next hop address in the route, you can set it to the IP address of the virtual appliance in the peer VNet HubVNet.</span><span class="sxs-lookup"><span data-stu-id="1de9c-155">When you specify the next hop address in the route, you can set it to the IP address of the virtual appliance in the peer VNet HubVNet.</span></span> <span data-ttu-id="1de9c-156">The following is a sample:</span><span class="sxs-lookup"><span data-stu-id="1de9c-156">The following is a sample:</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name TestNVA -AddressPrefix 10.3.0.0/16 -NextHopType VirtualAppliance -NextHopIpAddress 192.0.1.5

    $routeTable = New-AzureRmRouteTable -ResourceGroupName VNet101 -Location brazilsouth -Name TestRT -Route $route

    $vnet1 = Get-AzureRmVirtualNetwork -ResourceGroupName VNet101 -Name VNet1

    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet1 -Name subnet-1 -AddressPrefix 10.1.1.0/24 -RouteTable $routeTable

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet1
    ```

[!INCLUDE [virtual-networks-create-vnet-scenario-asmtoarm-include](../../includes/virtual-networks-create-vnetpeering-scenario-asmtoarm-include.md)]

1. <span data-ttu-id="1de9c-157">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 2.</span><span class="sxs-lookup"><span data-stu-id="1de9c-157">If you are creating a peering between VNets deployed through different deployment models in the *same* subscription, skip to step 2.</span></span> <span data-ttu-id="1de9c-158">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span><span class="sxs-lookup"><span data-stu-id="1de9c-158">The ability to create a VNet peering between VNets deployed through different deployment models in *different* subscriptions is in **preview** release.</span></span> <span data-ttu-id="1de9c-159">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span><span class="sxs-lookup"><span data-stu-id="1de9c-159">Capabilities in preview release do not have the same level of reliability and service level agreement as general release capabilities.</span></span> <span data-ttu-id="1de9c-160">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1de9c-160">If you are creating a peering between VNets deployed through different deployment models in different subscriptions you must first complete the following tasks:</span></span>
    - <span data-ttu-id="1de9c-161">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network` and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network`</span><span class="sxs-lookup"><span data-stu-id="1de9c-161">Register the preview capability in your Azure subscription by entering the following commands from PowerShell: `Register-AzureRmProviderFeature -FeatureName AllowClassicCrossSubscriptionPeering -ProviderNamespace Microsoft.Network` and `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network`</span></span>
    - <span data-ttu-id="1de9c-162">Complete steps 1-2 in the [Peering across subscriptions](#x-sub) section of this article.</span><span class="sxs-lookup"><span data-stu-id="1de9c-162">Complete steps 1-2 in the [Peering across subscriptions](#x-sub) section of this article.</span></span>
2. <span data-ttu-id="1de9c-163">Read the virtual network object for **VNET1**, the Azure Resource Manager virtual network, by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="1de9c-163">Read the virtual network object for **VNET1**, the Azure Resource Manager virtual network, by entering the following command:</span></span>

    ```powershell
    $vnet1 = Get-AzureRmVirtualNetwork -ResourceGroupName vnet101 -Name vnet1
    ```

3. <span data-ttu-id="1de9c-164">To establish VNet peering in this scenario, only one link is needed, specifically a link from **VNET1** to **VNET2**.</span><span class="sxs-lookup"><span data-stu-id="1de9c-164">To establish VNet peering in this scenario, only one link is needed, specifically a link from **VNET1** to **VNET2**.</span></span> <span data-ttu-id="1de9c-165">This step requires knowing your classic VNet's resource ID.</span><span class="sxs-lookup"><span data-stu-id="1de9c-165">This step requires knowing your classic VNet's resource ID.</span></span> <span data-ttu-id="1de9c-166">The resource group ID format looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="1de9c-166">The resource group ID format looks like the following example:</span></span>

        subscriptions/{SubscriptionID}/resourceGroups/{ResourceGroupName}/providers/Microsoft.ClassicNetwork/virtualNetworks/{VirtualNetworkName}

    <span data-ttu-id="1de9c-167">Be sure to replace SubscriptionID, ResourceGroupName, and VirtualNetworkName with the appropriate names.</span><span class="sxs-lookup"><span data-stu-id="1de9c-167">Be sure to replace SubscriptionID, ResourceGroupName, and VirtualNetworkName with the appropriate names.</span></span>

    <span data-ttu-id="1de9c-168">This can be accomplished by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="1de9c-168">This can be accomplished by entering the following command:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering -Name LinkToVNet2 -VirtualNetwork $vnet1 -RemoteVirtualNetworkId /subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx/resourceGroups/MyResourceGroup/providers/Microsoft.ClassicNetwork/virtualNetworks/VNET2
    ```

4. <span data-ttu-id="1de9c-169">Once the VNet peering link is created, you can see the link state, as shown in the following output:</span><span class="sxs-lookup"><span data-stu-id="1de9c-169">Once the VNet peering link is created, you can see the link state, as shown in the following output:</span></span>
   
        Name                             : LinkToVNet2
        Id                               : /subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx/resourceGroups/MyResourceGroup/providers/Microsoft.Network/virtualNetworks/VNET1/virtualNetworkPeerings/LinkToVNet2
        Etag                             : W/"acecbd0f-766c-46be-aa7e-d03e41c46b16"
        ResourceGroupName                : MyResourceGroup
        VirtualNetworkName               : VNET1
        PeeringState                     : Connected
        ProvisioningState                : Succeeded
        RemoteVirtualNetwork             : {
                                         "Id": "/subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx/resourceGroups/MyResourceGroup/providers/Microsoft.ClassicNetwork/virtualNetworks/VNET2"
                                       }
        AllowVirtualNetworkAccess        : True
        AllowForwardedTraffic            : False
        AllowGatewayTransit              : False
        UseRemoteGateways                : False
        RemoteGateways                   : null
        RemoteVirtualNetworkAddressSpace : null

## <a name="remove-a-vnet-peering"></a><span data-ttu-id="1de9c-170">Remove a VNet peering</span><span class="sxs-lookup"><span data-stu-id="1de9c-170">Remove a VNet peering</span></span>
1. <span data-ttu-id="1de9c-171">In order to remove a VNet peering, you need to run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1de9c-171">In order to remove a VNet peering, you need to run the following cmdlet:</span></span>

    ```powershell
    Remove-AzureRmVirtualNetworkPeering
    ```

    <span data-ttu-id="1de9c-172">To remove both links, enter the following commands:</span><span class="sxs-lookup"><span data-stu-id="1de9c-172">To remove both links, enter the following commands:</span></span>

    ```powershell
    Remove-AzureRmVirtualNetworkPeering -ResourceGroupName vnet101 -VirtualNetworkName vnet1 -Name linktovnet2
    Remove-AzureRmVirtualNetworkPeering -ResourceGroupName vnet101 -VirtualNetworkName vnet1 -Name linktovnet2
    ```

2. <span data-ttu-id="1de9c-173">Once you remove one link in a VNET peering, the  peer link state will go to *Disconnected*.</span><span class="sxs-lookup"><span data-stu-id="1de9c-173">Once you remove one link in a VNET peering, the  peer link state will go to *Disconnected*.</span></span> <span data-ttu-id="1de9c-174">In this state, you cannot re-create the link until the peer link state changes to *Initiated*.</span><span class="sxs-lookup"><span data-stu-id="1de9c-174">In this state, you cannot re-create the link until the peer link state changes to *Initiated*.</span></span> <span data-ttu-id="1de9c-175">We recommend you remove both links before you re-create the VNet peering.</span><span class="sxs-lookup"><span data-stu-id="1de9c-175">We recommend you remove both links before you re-create the VNet peering.</span></span>

