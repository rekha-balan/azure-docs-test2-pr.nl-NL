---
title: Workflows for configuring an ExpressRoute circuit | Microsoft Docs
description: This page walks you through the workflows for configuring ExpressRoute circuit and peerings
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: ''
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 56a08ef89c2dd48771ce628099fd138351fa92cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553474"
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="56ff4-103">ExpressRoute workflows for circuit provisioning and circuit states</span><span class="sxs-lookup"><span data-stu-id="56ff4-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="56ff4-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span><span class="sxs-lookup"><span data-stu-id="56ff4-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="56ff4-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span><span class="sxs-lookup"><span data-stu-id="56ff4-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="56ff4-106">Use PowerShell to configure an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="56ff4-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span><span class="sxs-lookup"><span data-stu-id="56ff4-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="56ff4-108">Order connectivity from the service provider.</span><span class="sxs-lookup"><span data-stu-id="56ff4-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="56ff4-109">This process varies.</span><span class="sxs-lookup"><span data-stu-id="56ff4-109">This process varies.</span></span> <span data-ttu-id="56ff4-110">Contact your connectivity provider for more details about how to order connectivity.</span><span class="sxs-lookup"><span data-stu-id="56ff4-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="56ff4-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56ff4-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="56ff4-112">Configure routing domains.</span><span class="sxs-lookup"><span data-stu-id="56ff4-112">Configure routing domains.</span></span> <span data-ttu-id="56ff4-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="56ff4-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span><span class="sxs-lookup"><span data-stu-id="56ff4-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="56ff4-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span><span class="sxs-lookup"><span data-stu-id="56ff4-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="56ff4-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="56ff4-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="56ff4-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span><span class="sxs-lookup"><span data-stu-id="56ff4-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="56ff4-118">Enable Microsoft peering - You must enable this to access Office 365 and CRM online services.</span><span class="sxs-lookup"><span data-stu-id="56ff4-118">Enable Microsoft peering - You must enable this to access Office 365 and CRM online services.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="56ff4-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span><span class="sxs-lookup"><span data-stu-id="56ff4-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="56ff4-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span><span class="sxs-lookup"><span data-stu-id="56ff4-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="56ff4-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="56ff4-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="56ff4-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="56ff4-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="56ff4-124">ExpressRoute circuit provisioning states</span><span class="sxs-lookup"><span data-stu-id="56ff4-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="56ff4-125">Each ExpressRoute circuit has two states:</span><span class="sxs-lookup"><span data-stu-id="56ff4-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="56ff4-126">Service provider provisioning state</span><span class="sxs-lookup"><span data-stu-id="56ff4-126">Service provider provisioning state</span></span>
* <span data-ttu-id="56ff4-127">Status</span><span class="sxs-lookup"><span data-stu-id="56ff4-127">Status</span></span>

<span data-ttu-id="56ff4-128">Status represents Microsoft's provisioning state.</span><span class="sxs-lookup"><span data-stu-id="56ff4-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="56ff4-129">This property is set to Enabled when you create an Expressroute circuit</span><span class="sxs-lookup"><span data-stu-id="56ff4-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="56ff4-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span><span class="sxs-lookup"><span data-stu-id="56ff4-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="56ff4-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="56ff4-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="56ff4-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span><span class="sxs-lookup"><span data-stu-id="56ff4-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="56ff4-133">Possible states of an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="56ff4-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="56ff4-134">This section lists out the possible states for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="56ff4-135">**At creation time**</span><span class="sxs-lookup"><span data-stu-id="56ff4-135">**At creation time**</span></span>

<span data-ttu-id="56ff4-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="56ff4-137">**When connectivity provider is in the process of provisioning the circuit**</span><span class="sxs-lookup"><span data-stu-id="56ff4-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="56ff4-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="56ff4-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="56ff4-139">**When connectivity provider has completed the provisioning process**</span><span class="sxs-lookup"><span data-stu-id="56ff4-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="56ff4-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="56ff4-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="56ff4-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span><span class="sxs-lookup"><span data-stu-id="56ff4-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="56ff4-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span><span class="sxs-lookup"><span data-stu-id="56ff4-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="56ff4-143">**When connectivity provider is deprovisioning the circuit**</span><span class="sxs-lookup"><span data-stu-id="56ff4-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="56ff4-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span><span class="sxs-lookup"><span data-stu-id="56ff4-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="56ff4-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="56ff4-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span><span class="sxs-lookup"><span data-stu-id="56ff4-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="56ff4-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="56ff4-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="56ff4-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="56ff4-149">Routing session configuration state</span><span class="sxs-lookup"><span data-stu-id="56ff4-149">Routing session configuration state</span></span>
<span data-ttu-id="56ff4-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="56ff4-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="56ff4-151">The state must be enabled for you to be able to use the peering.</span><span class="sxs-lookup"><span data-stu-id="56ff4-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="56ff4-152">It is important to check the BGP session state especially for Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="56ff4-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="56ff4-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span><span class="sxs-lookup"><span data-stu-id="56ff4-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="56ff4-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span><span class="sxs-lookup"><span data-stu-id="56ff4-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="56ff4-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span><span class="sxs-lookup"><span data-stu-id="56ff4-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="56ff4-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span><span class="sxs-lookup"><span data-stu-id="56ff4-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="56ff4-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="56ff4-157">Next steps</span></span>
* <span data-ttu-id="56ff4-158">Configure your ExpressRoute connection.</span><span class="sxs-lookup"><span data-stu-id="56ff4-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="56ff4-159">Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="56ff4-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="56ff4-160">Configure routing</span><span class="sxs-lookup"><span data-stu-id="56ff4-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="56ff4-161">Link a VNet to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="56ff4-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)



