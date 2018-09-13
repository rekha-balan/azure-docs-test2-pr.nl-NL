---
title: 'Migrate ExpressRoute associated virtual networks from classic to Resource Manager: Azure: PowerShell | Microsoft Docs'
description: This page describes how to migrate associated virtual networks to Resource Manager after moving your circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 5cebc3c5f2bcfb89f939b98391ffd072263c3e08
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548857"
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-to-resource-manager"></a><span data-ttu-id="957a1-103">Migrate ExpressRoute associated virtual networks from classic to Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-103">Migrate ExpressRoute associated virtual networks from classic to Resource Manager</span></span>

<span data-ttu-id="957a1-104">This article explains how to migrate Azure ExpressRoute associated virtual networks from the classic deployment model to the Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="957a1-104">This article explains how to migrate Azure ExpressRoute associated virtual networks from the classic deployment model to the Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="957a1-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="957a1-105">Before you begin</span></span>
* <span data-ttu-id="957a1-106">Verify that you have the latest version of the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="957a1-106">Verify that you have the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="957a1-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="957a1-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="957a1-108">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="957a1-108">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="957a1-109">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="957a1-109">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="957a1-110">Make sure that you fully understand the limits and limitations.</span><span class="sxs-lookup"><span data-stu-id="957a1-110">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="957a1-111">Verify that the circuit is fully operational in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="957a1-111">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="957a1-112">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="957a1-112">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="957a1-113">Review the following resource-migration documentation:</span><span class="sxs-lookup"><span data-stu-id="957a1-113">Review the following resource-migration documentation:</span></span>

    * [<span data-ttu-id="957a1-114">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-114">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="957a1-115">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-115">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [<span data-ttu-id="957a1-116">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-116">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="957a1-117">Review most common migration errors and mitigations</span><span class="sxs-lookup"><span data-stu-id="957a1-117">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a><span data-ttu-id="957a1-118">Supported and unsupported scenarios</span><span class="sxs-lookup"><span data-stu-id="957a1-118">Supported and unsupported scenarios</span></span>

* <span data-ttu-id="957a1-119">An ExpressRoute circuit can be moved from the classic to the Resource Manager environment without any downtime.</span><span class="sxs-lookup"><span data-stu-id="957a1-119">An ExpressRoute circuit can be moved from the classic to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="957a1-120">You can move any ExpressRoute circuit from the classic to the Resource Manager environment with no downtime.</span><span class="sxs-lookup"><span data-stu-id="957a1-120">You can move any ExpressRoute circuit from the classic to the Resource Manager environment with no downtime.</span></span> <span data-ttu-id="957a1-121">Follow the instructions in [moving ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="957a1-121">Follow the instructions in [moving ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span></span> <span data-ttu-id="957a1-122">This is a prerequisite to move resources connected to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="957a1-122">This is a prerequisite to move resources connected to the virtual network.</span></span>
* <span data-ttu-id="957a1-123">Virtual networks, gateways, and associated deployments within the virtual network that are attached to an ExpressRoute circuit in the same subscription can be migrated to the Resource Manager environment without any downtime.</span><span class="sxs-lookup"><span data-stu-id="957a1-123">Virtual networks, gateways, and associated deployments within the virtual network that are attached to an ExpressRoute circuit in the same subscription can be migrated to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="957a1-124">You can follow the steps described later to migrate resources such as virtual networks, gateways, and virtual machines deployed within the virtual network.</span><span class="sxs-lookup"><span data-stu-id="957a1-124">You can follow the steps described later to migrate resources such as virtual networks, gateways, and virtual machines deployed within the virtual network.</span></span> <span data-ttu-id="957a1-125">You must ensure that the virtual networks are configured correctly before they are migrated.</span><span class="sxs-lookup"><span data-stu-id="957a1-125">You must ensure that the virtual networks are configured correctly before they are migrated.</span></span> 
* <span data-ttu-id="957a1-126">Virtual networks, gateways, and associated deployments within the virtual network that are not in the same subscription as the ExpressRoute circuit require some downtime to complete the migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-126">Virtual networks, gateways, and associated deployments within the virtual network that are not in the same subscription as the ExpressRoute circuit require some downtime to complete the migration.</span></span> <span data-ttu-id="957a1-127">The last section of the document describes the steps to be followed to migrate resources.</span><span class="sxs-lookup"><span data-stu-id="957a1-127">The last section of the document describes the steps to be followed to migrate resources.</span></span>

## <a name="move-an-expressroute-circuit-from-classic-to-resource-manager"></a><span data-ttu-id="957a1-128">Move an ExpressRoute circuit from classic to Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-128">Move an ExpressRoute circuit from classic to Resource Manager</span></span>
<span data-ttu-id="957a1-129">You must move an ExpressRoute circuit from the classic to the Resource Manager environment before you try to migrate resources that are attached to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="957a1-129">You must move an ExpressRoute circuit from the classic to the Resource Manager environment before you try to migrate resources that are attached to the ExpressRoute circuit.</span></span> <span data-ttu-id="957a1-130">To accomplish this task, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="957a1-130">To accomplish this task, see the following articles:</span></span>

* <span data-ttu-id="957a1-131">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="957a1-131">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span>
* <span data-ttu-id="957a1-132">[Move a circuit from classic to Resource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="957a1-132">[Move a circuit from classic to Resource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span></span>
* <span data-ttu-id="957a1-133">Use the Azure Service Management portal.</span><span class="sxs-lookup"><span data-stu-id="957a1-133">Use the Azure Service Management portal.</span></span> <span data-ttu-id="957a1-134">You can follow the workflow to [create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select the import option.</span><span class="sxs-lookup"><span data-stu-id="957a1-134">You can follow the workflow to [create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select the import option.</span></span> 

<span data-ttu-id="957a1-135">This operation does not involve downtime.</span><span class="sxs-lookup"><span data-stu-id="957a1-135">This operation does not involve downtime.</span></span> <span data-ttu-id="957a1-136">You can continue to transfer data between your premises and Microsoft while the migration is in progress.</span><span class="sxs-lookup"><span data-stu-id="957a1-136">You can continue to transfer data between your premises and Microsoft while the migration is in progress.</span></span>

## <a name="prepare-your-virtual-network-for-migration"></a><span data-ttu-id="957a1-137">Prepare your virtual network for migration</span><span class="sxs-lookup"><span data-stu-id="957a1-137">Prepare your virtual network for migration</span></span>
<span data-ttu-id="957a1-138">You must ensure that the network of your virtual network to be migrated does not have unnecessary artifacts.</span><span class="sxs-lookup"><span data-stu-id="957a1-138">You must ensure that the network of your virtual network to be migrated does not have unnecessary artifacts.</span></span> <span data-ttu-id="957a1-139">To download your virtual network configuration and update it as needed, run the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="957a1-139">To download your virtual network configuration and update it as needed, run the following PowerShell cmdlet:</span></span>

```powershell
Add-AzureAccount
Select-AzureSubscription -SubscriptionName <VNET Subscription>
Get-AzureVNetConfig -ExportToFile C:\virtualnetworkconfig.xml
```
      
<span data-ttu-id="957a1-140">You must ensure that all references to <ConnectionsToLocalNetwork> are removed from the virtual networks to be migrated.</span><span class="sxs-lookup"><span data-stu-id="957a1-140">You must ensure that all references to <ConnectionsToLocalNetwork> are removed from the virtual networks to be migrated.</span></span> <span data-ttu-id="957a1-141">A sample network configuration is shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-141">A sample network configuration is shown in the following snippet:</span></span>

```
    <VirtualNetworkSite name="MyVNet" Location="East US">
        <AddressSpace>
            <AddressPrefix>10.0.0.0/8</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="Subnet-1">
                <AddressPrefix>10.0.0.0/11</AddressPrefix>
            </Subnet>
            <Subnet name="GatewaySubnet">
                <AddressPrefix>10.32.0.0/28</AddressPrefix>
            </Subnet>
        </Subnets>
        <Gateway>
            <ConnectionsToLocalNetwork>
            </ConnectionsToLocalNetwork>
        </Gateway>
    </VirtualNetworkSite>
```
 
<span data-ttu-id="957a1-142">If <ConnectionsToLocalNetwork> is not empty, delete the references under it and resubmit your network configuration.</span><span class="sxs-lookup"><span data-stu-id="957a1-142">If <ConnectionsToLocalNetwork> is not empty, delete the references under it and resubmit your network configuration.</span></span> <span data-ttu-id="957a1-143">You can do so by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="957a1-143">You can do so by running the following PowerShell cmdlet:</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath c:\virtualnetworkconfig.xml
```

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a><span data-ttu-id="957a1-144">Migrate virtual networks, gateways, and associated deployments</span><span class="sxs-lookup"><span data-stu-id="957a1-144">Migrate virtual networks, gateways, and associated deployments</span></span>

<span data-ttu-id="957a1-145">The steps you follow to migrate depend on whether your resources are in the same subscription, different subscriptions, or both.</span><span class="sxs-lookup"><span data-stu-id="957a1-145">The steps you follow to migrate depend on whether your resources are in the same subscription, different subscriptions, or both.</span></span>

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-the-same-subscription-as-the-expressroute-circuit"></a><span data-ttu-id="957a1-146">Migrate virtual networks, gateways, and associated deployments in the same subscription as the ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="957a1-146">Migrate virtual networks, gateways, and associated deployments in the same subscription as the ExpressRoute circuit</span></span>
<span data-ttu-id="957a1-147">This section describes the steps to be followed to migrate a virtual network, gateway, and associated deployments in the same subscription as the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="957a1-147">This section describes the steps to be followed to migrate a virtual network, gateway, and associated deployments in the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="957a1-148">No downtime is associated with this migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-148">No downtime is associated with this migration.</span></span> <span data-ttu-id="957a1-149">You can continue to use all resources through the migration process.</span><span class="sxs-lookup"><span data-stu-id="957a1-149">You can continue to use all resources through the migration process.</span></span> <span data-ttu-id="957a1-150">The management plane is locked while the migration is in progress.</span><span class="sxs-lookup"><span data-stu-id="957a1-150">The management plane is locked while the migration is in progress.</span></span> 

1. <span data-ttu-id="957a1-151">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span><span class="sxs-lookup"><span data-stu-id="957a1-151">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span></span>
2. <span data-ttu-id="957a1-152">Ensure that the virtual network has been prepared appropriately for the migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-152">Ensure that the virtual network has been prepared appropriately for the migration.</span></span>
3. <span data-ttu-id="957a1-153">Register your subscription for resource migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-153">Register your subscription for resource migration.</span></span> <span data-ttu-id="957a1-154">To register your subscription for resource migration, use the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-154">To register your subscription for resource migration, use the following PowerShell snippet:</span></span>

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. <span data-ttu-id="957a1-155">Validate, prepare, and migrate.</span><span class="sxs-lookup"><span data-stu-id="957a1-155">Validate, prepare, and migrate.</span></span> <span data-ttu-id="957a1-156">To move the virtual network, use the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-156">To move the virtual network, use the following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  <span data-ttu-id="957a1-157">You can also abort migration by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="957a1-157">You can also abort migration by running the following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-a-different-subscription-from-that-of-the-expressroute-circuit"></a><span data-ttu-id="957a1-158">Migrate virtual networks, gateways, and associated deployments in a different subscription from that of the ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="957a1-158">Migrate virtual networks, gateways, and associated deployments in a different subscription from that of the ExpressRoute circuit</span></span>

1. <span data-ttu-id="957a1-159">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span><span class="sxs-lookup"><span data-stu-id="957a1-159">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span></span>
2. <span data-ttu-id="957a1-160">Ensure that the virtual network has been prepared appropriately for the migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-160">Ensure that the virtual network has been prepared appropriately for the migration.</span></span>
3. <span data-ttu-id="957a1-161">Ensure that the ExpressRoute circuit can operate in both the classic and the Resource Manager environment.</span><span class="sxs-lookup"><span data-stu-id="957a1-161">Ensure that the ExpressRoute circuit can operate in both the classic and the Resource Manager environment.</span></span> <span data-ttu-id="957a1-162">To allow the circuit to be used in both classic and Resource Manager environments, use the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="957a1-162">To allow the circuit to be used in both classic and Resource Manager environments, use the following PowerShell script:</span></span>

  ```powershell
  Login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName <My subscription>
  $circuit = Get-AzureRmExpressRouteCircuit -Name <CircuitName> -ResourceGroupName <ResourceGroup Name> 
  $circuit.AllowClassicOperations = $true
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
  ```
4. <span data-ttu-id="957a1-163">Create authorizations in the Resource Manager environment.</span><span class="sxs-lookup"><span data-stu-id="957a1-163">Create authorizations in the Resource Manager environment.</span></span> <span data-ttu-id="957a1-164">To learn how to create authorizations, see [how to link virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="957a1-164">To learn how to create authorizations, see [how to link virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md).</span></span> <span data-ttu-id="957a1-165">To create an authorization, use the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-165">To create an authorization, use the following PowerShell snippet:</span></span>

  ```powershell
  circuit = Get-AzureRmExpressRouteCircuit -Name <CircuitName> -ResourceGroupName <ResourceGroup Name> 
  Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "AuthorizationForMigration"
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
  $circuit = Get-AzureRmExpressRouteCircuit -Name MigrateCircuit -ResourceGroupName MigrateRGWest

  $id = $circuit.id 
  $auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "AuthorizationForMigration"

  $key=$auth1.AuthorizationKey 
 ```

    <span data-ttu-id="957a1-166">Note the circuit ID and authorization key.</span><span class="sxs-lookup"><span data-stu-id="957a1-166">Note the circuit ID and authorization key.</span></span> <span data-ttu-id="957a1-167">These elements are used to connect the circuit to the virtual network after the migration is complete.</span><span class="sxs-lookup"><span data-stu-id="957a1-167">These elements are used to connect the circuit to the virtual network after the migration is complete.</span></span>
  
5. <span data-ttu-id="957a1-168">Delete the dedicated circuit link that's associated with the virtual network.</span><span class="sxs-lookup"><span data-stu-id="957a1-168">Delete the dedicated circuit link that's associated with the virtual network.</span></span> <span data-ttu-id="957a1-169">To remove the circuit link in the classic environment, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="957a1-169">To remove the circuit link in the classic environment, use the following cmdlet:</span></span>

  ```powershell
  $skey = Get-AzureDedicatedCircuit | select ServiceKey
  Remove-AzureDedicatedCircuitLink -ServiceKey $skey -VNetName $vnetName
  ```  

6. <span data-ttu-id="957a1-170">Register your subscription for resource migration.</span><span class="sxs-lookup"><span data-stu-id="957a1-170">Register your subscription for resource migration.</span></span> <span data-ttu-id="957a1-171">To register your subscription for resource migration, use the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-171">To register your subscription for resource migration, use the following PowerShell snippet:</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
7. <span data-ttu-id="957a1-172">Validate, prepare, and migrate.</span><span class="sxs-lookup"><span data-stu-id="957a1-172">Validate, prepare, and migrate.</span></span> <span data-ttu-id="957a1-173">To move the virtual network, use the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="957a1-173">To move the virtual network, use the following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

    <span data-ttu-id="957a1-174">You can also abort migration by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="957a1-174">You can also abort migration by running the following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```
8. <span data-ttu-id="957a1-175">Connect the virtual network back to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="957a1-175">Connect the virtual network back to the ExpressRoute circuit.</span></span> <span data-ttu-id="957a1-176">The following PowerShell snippet is run in the context of the subscription in which the virtual network is created.</span><span class="sxs-lookup"><span data-stu-id="957a1-176">The following PowerShell snippet is run in the context of the subscription in which the virtual network is created.</span></span> <span data-ttu-id="957a1-177">You must not run this snippet in the subscription where the circuit is created.</span><span class="sxs-lookup"><span data-stu-id="957a1-177">You must not run this snippet in the subscription where the circuit is created.</span></span> <span data-ttu-id="957a1-178">Use the circuit ID as PeerID and authorization key noted in step 4.</span><span class="sxs-lookup"><span data-stu-id="957a1-178">Use the circuit ID as PeerID and authorization key noted in step 4.</span></span>

  ```powershell
  Select-AzureRMSubscription –SubscriptionName <customer subscription>  
  $gw = Get-AzureRmVirtualNetworkGateway -Name $vnetName-Default-Gateway -ResourceGroupName ($vnetName + "-Migrated")
  $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroup  ($vnetName + "-Migrated")  

  New-AzureRmVirtualNetworkGatewayConnection -Name  ($vnetName + "-GwConn") -ResourceGroupName ($vnetName + "-Migrated")  -Location $vnet.Location -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey $key
  ```

## <a name="next-steps"></a><span data-ttu-id="957a1-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="957a1-179">Next steps</span></span>
* [<span data-ttu-id="957a1-180">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-180">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="957a1-181">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-181">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [<span data-ttu-id="957a1-182">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="957a1-182">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="957a1-183">Review most common migration errors and mitigations</span><span class="sxs-lookup"><span data-stu-id="957a1-183">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
