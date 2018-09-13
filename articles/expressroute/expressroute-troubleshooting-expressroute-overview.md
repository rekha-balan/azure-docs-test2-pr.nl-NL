---
title: 'Verifying Connectivity: Azure ExpressRoute Troubleshooting Guide| Microsoft Docs'
description: This page provides instructions on troubleshooting and validating end to end connectivity of an ExpressRoute circuit.
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: ''
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 1/5/2017
ms.author: rambala
ms.openlocfilehash: 7f709ad328c1dfb4ed1cdad49d7e1ec705aa10bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662850"
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="349f9-103">Verifying ExpressRoute connectivity</span><span class="sxs-lookup"><span data-stu-id="349f9-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="349f9-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a dedicated private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span><span class="sxs-lookup"><span data-stu-id="349f9-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a dedicated private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="349f9-105">Customer Network</span><span class="sxs-lookup"><span data-stu-id="349f9-105">Customer Network</span></span>
-   <span data-ttu-id="349f9-106">Provider Network</span><span class="sxs-lookup"><span data-stu-id="349f9-106">Provider Network</span></span>
-   <span data-ttu-id="349f9-107">Microsoft Datacenter</span><span class="sxs-lookup"><span data-stu-id="349f9-107">Microsoft Datacenter</span></span>

<span data-ttu-id="349f9-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="349f9-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="349f9-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="349f9-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="349f9-110">This document is intended to help diagnosing and fixing simple issues.</span><span class="sxs-lookup"><span data-stu-id="349f9-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="349f9-111">It is not intended to be a replacement for Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="349f9-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="349f9-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span><span class="sxs-lookup"><span data-stu-id="349f9-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="349f9-113">Overview</span><span class="sxs-lookup"><span data-stu-id="349f9-113">Overview</span></span>
<span data-ttu-id="349f9-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="349f9-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="349f9-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="349f9-115">[![1]][1]</span></span>

<span data-ttu-id="349f9-116">In the preceding diagram, the numbers indicate key network points.</span><span class="sxs-lookup"><span data-stu-id="349f9-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="349f9-117">The network points are referenced often through this article by their associated number.</span><span class="sxs-lookup"><span data-stu-id="349f9-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="349f9-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span><span class="sxs-lookup"><span data-stu-id="349f9-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="349f9-119">The key network points illustrated are as follows:</span><span class="sxs-lookup"><span data-stu-id="349f9-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="349f9-120">Customer compute device (for example, a server or PC)</span><span class="sxs-lookup"><span data-stu-id="349f9-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="349f9-121">CEs: Customer edge routers</span><span class="sxs-lookup"><span data-stu-id="349f9-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="349f9-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers</span><span class="sxs-lookup"><span data-stu-id="349f9-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers</span></span>
4.  <span data-ttu-id="349f9-123">PEs (MSEE facing: Provider edge routers/switches that are facing MSEEs</span><span class="sxs-lookup"><span data-stu-id="349f9-123">PEs (MSEE facing: Provider edge routers/switches that are facing MSEEs</span></span>
5.  <span data-ttu-id="349f9-124">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span><span class="sxs-lookup"><span data-stu-id="349f9-124">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="349f9-125">Virtual Network (VNet) Gateway</span><span class="sxs-lookup"><span data-stu-id="349f9-125">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="349f9-126">Compute device on the Azure VNet</span><span class="sxs-lookup"><span data-stu-id="349f9-126">Compute device on the Azure VNet</span></span>

<span data-ttu-id="349f9-127">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="349f9-127">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="349f9-128">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span><span class="sxs-lookup"><span data-stu-id="349f9-128">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="349f9-129">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="349f9-129">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="349f9-130">Routes would then propagate back to the customer network via the IPVPN service provider network.</span><span class="sxs-lookup"><span data-stu-id="349f9-130">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="349f9-131">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and MSEE-PRs (4).</span><span class="sxs-lookup"><span data-stu-id="349f9-131">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and MSEE-PRs (4).</span></span> <span data-ttu-id="349f9-132">A redundant pair of network paths is also encouraged between customer network and MSEE-PRs.</span><span class="sxs-lookup"><span data-stu-id="349f9-132">A redundant pair of network paths is also encouraged between customer network and MSEE-PRs.</span></span> <span data-ttu-id="349f9-133">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span><span class="sxs-lookup"><span data-stu-id="349f9-133">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="349f9-134">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span><span class="sxs-lookup"><span data-stu-id="349f9-134">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="349f9-135">Validate circuit provisioning and state (5)</span><span class="sxs-lookup"><span data-stu-id="349f9-135">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="349f9-136">Validate at least one ExpressRoute peering is configured (5)</span><span class="sxs-lookup"><span data-stu-id="349f9-136">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="349f9-137">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span><span class="sxs-lookup"><span data-stu-id="349f9-137">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="349f9-138">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span><span class="sxs-lookup"><span data-stu-id="349f9-138">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="349f9-139">Check the Traffic Statistics (Traffic passing through 5)</span><span class="sxs-lookup"><span data-stu-id="349f9-139">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="349f9-140">More validations and checks will be added in the future, check back monthly!</span><span class="sxs-lookup"><span data-stu-id="349f9-140">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="349f9-141">Validate circuit provisioning and state</span><span class="sxs-lookup"><span data-stu-id="349f9-141">Validate circuit provisioning and state</span></span>
<span data-ttu-id="349f9-142">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span><span class="sxs-lookup"><span data-stu-id="349f9-142">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="349f9-143">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between MSEE-PRs (4) and MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="349f9-143">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="349f9-144">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="349f9-144">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="349f9-145">A service key uniquely identifies an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="349f9-145">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="349f9-146">This key is required for most of the powershell commands mentioned in this document.</span><span class="sxs-lookup"><span data-stu-id="349f9-146">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="349f9-147">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span><span class="sxs-lookup"><span data-stu-id="349f9-147">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="349f9-148">Verification via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="349f9-148">Verification via the Azure portal</span></span>
<span data-ttu-id="349f9-149">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="349f9-149">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="349f9-150">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span><span class="sxs-lookup"><span data-stu-id="349f9-150">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="349f9-151">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="349f9-151">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="349f9-152">![4][4]</span><span class="sxs-lookup"><span data-stu-id="349f9-152">![4][4]</span></span>    

<span data-ttu-id="349f9-153">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="349f9-153">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="349f9-154">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span><span class="sxs-lookup"><span data-stu-id="349f9-154">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="349f9-155">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="349f9-155">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="349f9-156">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="349f9-156">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="349f9-157">If the *Provider status* is not provisioned, contact your service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-157">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="349f9-158">Verification via PowerShell</span><span class="sxs-lookup"><span data-stu-id="349f9-158">Verification via PowerShell</span></span>
<span data-ttu-id="349f9-159">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-159">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="349f9-160">You can get your resource group name through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="349f9-160">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="349f9-161">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span><span class="sxs-lookup"><span data-stu-id="349f9-161">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="349f9-162">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-162">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="349f9-163">A sample response is:</span><span class="sxs-lookup"><span data-stu-id="349f9-163">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="349f9-164">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span><span class="sxs-lookup"><span data-stu-id="349f9-164">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="349f9-165">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="349f9-165">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="349f9-166">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-166">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="349f9-167">Verification via PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="349f9-167">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="349f9-168">To list all the ExpressRoute circuits under a subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-168">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="349f9-169">To select a particular ExpressRoute circuit, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-169">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="349f9-170">A sample response is:</span><span class="sxs-lookup"><span data-stu-id="349f9-170">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="349f9-171">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span><span class="sxs-lookup"><span data-stu-id="349f9-171">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="349f9-172">If the *Status* is not enabled, contact [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="349f9-172">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="349f9-173">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-173">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="349f9-174">Validate Peering Configuration</span><span class="sxs-lookup"><span data-stu-id="349f9-174">Validate Peering Configuration</span></span>
<span data-ttu-id="349f9-175">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="349f9-175">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="349f9-176">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and CRM Online).</span><span class="sxs-lookup"><span data-stu-id="349f9-176">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and CRM Online).</span></span> <span data-ttu-id="349f9-177">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="349f9-177">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="349f9-178">Verification via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="349f9-178">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="349f9-179">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-179">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="349f9-180">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span><span class="sxs-lookup"><span data-stu-id="349f9-180">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="349f9-181">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span><span class="sxs-lookup"><span data-stu-id="349f9-181">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="349f9-182">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span><span class="sxs-lookup"><span data-stu-id="349f9-182">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="349f9-183">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span><span class="sxs-lookup"><span data-stu-id="349f9-183">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="349f9-184">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="349f9-184">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="349f9-185">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span><span class="sxs-lookup"><span data-stu-id="349f9-185">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="349f9-186">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="349f9-186">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="349f9-187">![5][5]</span><span class="sxs-lookup"><span data-stu-id="349f9-187">![5][5]</span></span>

<span data-ttu-id="349f9-188">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span><span class="sxs-lookup"><span data-stu-id="349f9-188">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="349f9-189">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span><span class="sxs-lookup"><span data-stu-id="349f9-189">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="349f9-190">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span><span class="sxs-lookup"><span data-stu-id="349f9-190">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span></span> 

>[!NOTE]
><span data-ttu-id="349f9-191">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on MSEE-PRs.</span><span class="sxs-lookup"><span data-stu-id="349f9-191">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on MSEE-PRs.</span></span> <span data-ttu-id="349f9-192">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="349f9-192">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="349f9-193">Verification via PowerShell</span><span class="sxs-lookup"><span data-stu-id="349f9-193">Verification via PowerShell</span></span>
<span data-ttu-id="349f9-194">To get the Azure private peering configuration details, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="349f9-194">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="349f9-195">A sample response, for a successfully configured private peering, is:</span><span class="sxs-lookup"><span data-stu-id="349f9-195">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="349f9-196">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span><span class="sxs-lookup"><span data-stu-id="349f9-196">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="349f9-197">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span><span class="sxs-lookup"><span data-stu-id="349f9-197">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span></span>

<span data-ttu-id="349f9-198">To get the Azure public peering configuration details, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="349f9-198">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="349f9-199">To get the Microsoft peering configuration details, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="349f9-199">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="349f9-200">If a peering is not configured, there would be an error message.</span><span class="sxs-lookup"><span data-stu-id="349f9-200">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="349f9-201">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span><span class="sxs-lookup"><span data-stu-id="349f9-201">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand

>[!IMPORTANT]
><span data-ttu-id="349f9-202">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span><span class="sxs-lookup"><span data-stu-id="349f9-202">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="349f9-203">Resetting the provider side peering settings requires the support of the service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-203">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="349f9-204">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span><span class="sxs-lookup"><span data-stu-id="349f9-204">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="349f9-205">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-205">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-206">Also check if the correct *VlandId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-206">Also check if the correct *VlandId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-207">If MD5 hashing is chosen, the shared key should be same on MSEE and MSEE-PR pair.</span><span class="sxs-lookup"><span data-stu-id="349f9-207">If MD5 hashing is chosen, the shared key should be same on MSEE and MSEE-PR pair.</span></span> <span data-ttu-id="349f9-208">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="349f9-208">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="349f9-209">Verification via PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="349f9-209">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="349f9-210">To get the Azure private peering configuration details, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-210">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="349f9-211">A sample response, for a successfully configured private peering is:</span><span class="sxs-lookup"><span data-stu-id="349f9-211">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="349f9-212">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span><span class="sxs-lookup"><span data-stu-id="349f9-212">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="349f9-213">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span><span class="sxs-lookup"><span data-stu-id="349f9-213">The /30 subnets are used for the interface IP address of the MSEEs and MSEE-PRs.</span></span>

<span data-ttu-id="349f9-214">To get the Azure public peering configuration details, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="349f9-214">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="349f9-215">To get the Microsoft peering configuration details, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="349f9-215">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="349f9-216">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span><span class="sxs-lookup"><span data-stu-id="349f9-216">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="349f9-217">Resetting the provider side peering settings requires the support of the service provider.</span><span class="sxs-lookup"><span data-stu-id="349f9-217">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="349f9-218">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span><span class="sxs-lookup"><span data-stu-id="349f9-218">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="349f9-219">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-219">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-220">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-220">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-221">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="349f9-221">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="349f9-222">Validate ARP between Microsoft and the service provider</span><span class="sxs-lookup"><span data-stu-id="349f9-222">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="349f9-223">This section uses PowerShell (Classic) commands.</span><span class="sxs-lookup"><span data-stu-id="349f9-223">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="349f9-224">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="349f9-224">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="349f9-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span><span class="sxs-lookup"><span data-stu-id="349f9-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="349f9-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="349f9-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="349f9-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="349f9-228">An example response for the command, in the successful scenario:</span><span class="sxs-lookup"><span data-stu-id="349f9-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="349f9-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span><span class="sxs-lookup"><span data-stu-id="349f9-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="349f9-230">The following example shows the response of the command for a peering does not exist.</span><span class="sxs-lookup"><span data-stu-id="349f9-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="349f9-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span><span class="sxs-lookup"><span data-stu-id="349f9-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="349f9-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="349f9-233">Azure always uses the second IP address for MSEEs.</span><span class="sxs-lookup"><span data-stu-id="349f9-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="349f9-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span><span class="sxs-lookup"><span data-stu-id="349f9-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

##<a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="349f9-235">Validate BGP and routes on the MSEE</span><span class="sxs-lookup"><span data-stu-id="349f9-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="349f9-236">This section uses PowerShell (Classic) commands.</span><span class="sxs-lookup"><span data-stu-id="349f9-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="349f9-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="349f9-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="349f9-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span><span class="sxs-lookup"><span data-stu-id="349f9-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="349f9-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="349f9-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="349f9-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="349f9-241">An example response is:</span><span class="sxs-lookup"><span data-stu-id="349f9-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="349f9-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span><span class="sxs-lookup"><span data-stu-id="349f9-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="349f9-243">It also indicates number of route prefixes advertised by the peering router.</span><span class="sxs-lookup"><span data-stu-id="349f9-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="349f9-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="349f9-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked MSEE-PR.</span></span> <span data-ttu-id="349f9-246">If MD5 hashing is chosen, the shared key should be same on MSEE and MSEE-PR pair.</span><span class="sxs-lookup"><span data-stu-id="349f9-246">If MD5 hashing is chosen, the shared key should be same on MSEE and MSEE-PR pair.</span></span> <span data-ttu-id="349f9-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="349f9-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="349f9-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span><span class="sxs-lookup"><span data-stu-id="349f9-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="349f9-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span><span class="sxs-lookup"><span data-stu-id="349f9-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="349f9-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="349f9-251">An example successful outcome for the command is:</span><span class="sxs-lookup"><span data-stu-id="349f9-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="349f9-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span><span class="sxs-lookup"><span data-stu-id="349f9-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="349f9-253">The following example shows the response of the command for a peering does not exist:</span><span class="sxs-lookup"><span data-stu-id="349f9-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="349f9-254">Check the Traffic Statistics</span><span class="sxs-lookup"><span data-stu-id="349f9-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="349f9-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span><span class="sxs-lookup"><span data-stu-id="349f9-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="349f9-256">A sample output of the command is:</span><span class="sxs-lookup"><span data-stu-id="349f9-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="349f9-257">A sample output of the command for a non-existent peering is:</span><span class="sxs-lookup"><span data-stu-id="349f9-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="349f9-258">Next Steps</span><span class="sxs-lookup"><span data-stu-id="349f9-258">Next Steps</span></span>
<span data-ttu-id="349f9-259">For more information or help, check out the following links:</span><span class="sxs-lookup"><span data-stu-id="349f9-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="349f9-260">[Microsoft Support][Support]</span><span class="sxs-lookup"><span data-stu-id="349f9-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="349f9-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="349f9-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="349f9-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="349f9-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com











