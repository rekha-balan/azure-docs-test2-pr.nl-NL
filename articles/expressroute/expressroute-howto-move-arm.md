---
title: 'Move ExpressRoute circuits from classic to Resource Manager: PowerShell: Azure | Microsoft Docs'
description: This page describes how to move a classic circuit to the Resource Manager deployment model using PowerShell.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 73f42b25d667f07205e7e67556c367f1a0e6e215
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550720"
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="44533-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span><span class="sxs-lookup"><span data-stu-id="44533-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="44533-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="44533-105">The following sections will walk you through the steps to move your circuit by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44533-105">The following sections will walk you through the steps to move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="44533-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="44533-106">Before you begin</span></span>
* <span data-ttu-id="44533-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span><span class="sxs-lookup"><span data-stu-id="44533-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="44533-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="44533-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="44533-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="44533-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="44533-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="44533-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="44533-111">Make sure that you fully understand the limits and limitations.</span><span class="sxs-lookup"><span data-stu-id="44533-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="44533-112">Verify that the circuit is fully operational in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="44533-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="44533-114">Move an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="44533-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="44533-115">Step 1: Gather circuit details from the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="44533-115">Step 1: Gather circuit details from the classic deployment model</span></span>
<span data-ttu-id="44533-116">Sign in to the Azure classic environment and gather the service key.</span><span class="sxs-lookup"><span data-stu-id="44533-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="44533-117">Sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="44533-117">Sign in to your Azure account.</span></span>

        Add-AzureAccount

2. <span data-ttu-id="44533-118">Select the appropriate Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="44533-118">Select the appropriate Azure subscription.</span></span>

        Select-AzureSubscription "<Enter Subscription Name here>"

3. <span data-ttu-id="44533-119">Import the PowerShell modules for Azure and ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44533-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

4. <span data-ttu-id="44533-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="44533-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="44533-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

        Get-AzureDedicatedCircuit

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="44533-122">Step 2: Sign in and create a resource group</span><span class="sxs-lookup"><span data-stu-id="44533-122">Step 2: Sign in and create a resource group</span></span>
<span data-ttu-id="44533-123">Sign in to the Resource Manager environment and create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="44533-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="44533-124">Sign in to your Azure Resource Manager environment.</span><span class="sxs-lookup"><span data-stu-id="44533-124">Sign in to your Azure Resource Manager environment.</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="44533-125">Select the appropriate Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="44533-125">Select the appropriate Azure subscription.</span></span>

        Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription

3. <span data-ttu-id="44533-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span><span class="sxs-lookup"><span data-stu-id="44533-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

        New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="44533-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="44533-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>
<span data-ttu-id="44533-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="44533-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="44533-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="44533-130">To move your circuit, modify and run the following snippet:</span><span class="sxs-lookup"><span data-stu-id="44533-130">To move your circuit, modify and run the following snippet:</span></span>

    Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"

> [!NOTE]
> <span data-ttu-id="44533-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span><span class="sxs-lookup"><span data-stu-id="44533-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="44533-132">The circuit will essentially be renamed.</span><span class="sxs-lookup"><span data-stu-id="44533-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="44533-133">Modify circuit access</span><span class="sxs-lookup"><span data-stu-id="44533-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="44533-134">To enable ExpressRoute circuit access for both deployment models</span><span class="sxs-lookup"><span data-stu-id="44533-134">To enable ExpressRoute circuit access for both deployment models</span></span>
<span data-ttu-id="44533-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span><span class="sxs-lookup"><span data-stu-id="44533-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="44533-136">Run the following cmdlets to enable access to both deployment models:</span><span class="sxs-lookup"><span data-stu-id="44533-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="44533-137">Get the circuit details.</span><span class="sxs-lookup"><span data-stu-id="44533-137">Get the circuit details.</span></span>

        $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"

2. <span data-ttu-id="44533-138">Set "Allow Classic Operations" to TRUE.</span><span class="sxs-lookup"><span data-stu-id="44533-138">Set "Allow Classic Operations" to TRUE.</span></span>

        $ckt.AllowClassicOperations = $true

3. <span data-ttu-id="44533-139">Update the circuit.</span><span class="sxs-lookup"><span data-stu-id="44533-139">Update the circuit.</span></span> <span data-ttu-id="44533-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

        Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

4. <span data-ttu-id="44533-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="44533-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="44533-142">You must be able to see the service key listed.</span><span class="sxs-lookup"><span data-stu-id="44533-142">You must be able to see the service key listed.</span></span> 

        get-azurededicatedcircuit

5. <span data-ttu-id="44533-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span><span class="sxs-lookup"><span data-stu-id="44533-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="44533-144">The following articles will walk you through how to manage links to the ExpressRoute circuit:</span><span class="sxs-lookup"><span data-stu-id="44533-144">The following articles will walk you through how to manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="44533-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="44533-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="44533-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="44533-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="44533-147">To disable ExpressRoute circuit access to the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="44533-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>
<span data-ttu-id="44533-148">Run the following cmdlets to disable access to the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="44533-149">Get details of the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="44533-149">Get details of the ExpressRoute circuit.</span></span>

        $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"

2. <span data-ttu-id="44533-150">Set "Allow Classic Operations" to FALSE.</span><span class="sxs-lookup"><span data-stu-id="44533-150">Set "Allow Classic Operations" to FALSE.</span></span>

        $ckt.AllowClassicOperations = $false

3. <span data-ttu-id="44533-151">Update the circuit.</span><span class="sxs-lookup"><span data-stu-id="44533-151">Update the circuit.</span></span> <span data-ttu-id="44533-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="44533-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

        Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

## <a name="next-steps"></a><span data-ttu-id="44533-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="44533-153">Next steps</span></span>

* [<span data-ttu-id="44533-154">Create and modify routing for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="44533-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="44533-155">Link your virtual network to your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="44533-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

