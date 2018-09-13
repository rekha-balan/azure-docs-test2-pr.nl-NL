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
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a>Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell

To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model. The following sections will walk you through the steps to move your circuit by using PowerShell.

## <a name="before-you-begin"></a>Before you begin
* Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0). For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.
* Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md). Make sure that you fully understand the limits and limitations.
* Verify that the circuit is fully operational in the classic deployment model.
* Ensure that you have a resource group that was created in the Resource Manager deployment model.

## <a name="move-an-expressroute-circuit"></a>Move an ExpressRoute circuit

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a>Step 1: Gather circuit details from the classic deployment model
Sign in to the Azure classic environment and gather the service key.

1. Sign in to your Azure account.

        Add-AzureAccount

2. Select the appropriate Azure subscription.

        Select-AzureSubscription "<Enter Subscription Name here>"

3. Import the PowerShell modules for Azure and ExpressRoute.

        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

4. Use the cmdlet below to get the service keys for all of your ExpressRoute circuits. After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.

        Get-AzureDedicatedCircuit

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Step 2: Sign in and create a resource group
Sign in to the Resource Manager environment and create a new resource group.

1. Sign in to your Azure Resource Manager environment.

        Login-AzureRmAccount

2. Select the appropriate Azure subscription.

        Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription

3. Modify the snippet below to create a new resource group if you don't already have a resource group.

        New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a>Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model
You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model. Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).

To move your circuit, modify and run the following snippet:

    Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"

> [!NOTE]
> After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource. The circuit will essentially be renamed.
> 

## <a name="modify-circuit-access"></a>Modify circuit access

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a>To enable ExpressRoute circuit access for both deployment models
After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models. Run the following cmdlets to enable access to both deployment models:

1. Get the circuit details.

        $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"

2. Set "Allow Classic Operations" to TRUE.

        $ckt.AllowClassicOperations = $true

3. Update the circuit. After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.

        Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

4. Run the following cmdlet to get the details of the ExpressRoute circuit. You must be able to see the service key listed. 

        get-azurededicatedcircuit

5. You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets. The following articles will walk you through how to manage links to the ExpressRoute circuit:

    * [Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model](expressroute-howto-linkvnet-arm.md)
    * [Link your virtual network to your ExpressRoute circuit in the classic deployment model](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a>To disable ExpressRoute circuit access to the classic deployment model
Run the following cmdlets to disable access to the classic deployment model.

1. Get details of the ExpressRoute circuit.

        $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"

2. Set "Allow Classic Operations" to FALSE.

        $ckt.AllowClassicOperations = $false

3. Update the circuit. After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.

        Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

## <a name="next-steps"></a>Next steps

* [Create and modify routing for your ExpressRoute circuit](expressroute-howto-routing-arm.md)
* [Link your virtual network to your ExpressRoute circuit](expressroute-howto-linkvnet-arm.md)

