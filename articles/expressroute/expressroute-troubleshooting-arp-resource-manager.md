---
title: 'Getting ARP tables: Resource Manager: Azure ExpressRoute Troubleshooting | Microsoft Docs'
description: This page provides instructions on getting the ARP tables for an ExpressRoute circuit
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660970"
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="26209-103">Getting ARP tables in the Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="26209-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classic](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="26209-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="26209-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> This document is intended to help you diagnose and fix simple issues. It is not intended to be a replacement for Microsoft support. You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="26209-110">Address Resolution Protocol (ARP) and ARP tables</span><span class="sxs-lookup"><span data-stu-id="26209-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="26209-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="26209-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="26209-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span><span class="sxs-lookup"><span data-stu-id="26209-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="26209-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span><span class="sxs-lookup"><span data-stu-id="26209-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="26209-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span><span class="sxs-lookup"><span data-stu-id="26209-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="26209-115">Mapping of on-premises router interface ip address to the MAC address</span><span class="sxs-lookup"><span data-stu-id="26209-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="26209-116">Mapping of ExpressRoute router interface ip address to the MAC address</span><span class="sxs-lookup"><span data-stu-id="26209-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="26209-117">Age of the mapping</span><span class="sxs-lookup"><span data-stu-id="26209-117">Age of the mapping</span></span>

<span data-ttu-id="26209-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="26209-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="26209-119">Example ARP table:</span><span class="sxs-lookup"><span data-stu-id="26209-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="26209-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span><span class="sxs-lookup"><span data-stu-id="26209-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="26209-121">Prerequisites for learning ARP tables</span><span class="sxs-lookup"><span data-stu-id="26209-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="26209-122">Ensure that you have the following before you progress further</span><span class="sxs-lookup"><span data-stu-id="26209-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="26209-123">A Valid ExpressRoute circuit configured with at least one peering.</span><span class="sxs-lookup"><span data-stu-id="26209-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="26209-124">The circuit must be fully configured by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="26209-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="26209-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span><span class="sxs-lookup"><span data-stu-id="26209-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="26209-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span><span class="sxs-lookup"><span data-stu-id="26209-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="26209-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span><span class="sxs-lookup"><span data-stu-id="26209-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="26209-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="26209-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="26209-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span><span class="sxs-lookup"><span data-stu-id="26209-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="26209-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span><span class="sxs-lookup"><span data-stu-id="26209-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="26209-131">Getting the ARP tables for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="26209-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="26209-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26209-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="26209-133">You or your connectivity provider must have configured the peering before progressing further.</span><span class="sxs-lookup"><span data-stu-id="26209-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="26209-134">Each circuit has two paths (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="26209-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="26209-135">You can check the ARP table for each path independently.</span><span class="sxs-lookup"><span data-stu-id="26209-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="26209-136">ARP tables for Azure private peering</span><span class="sxs-lookup"><span data-stu-id="26209-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="26209-137">The following cmdlet provides the ARP tables for Azure private peering</span><span class="sxs-lookup"><span data-stu-id="26209-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="26209-138">Sample output is shown below for one of the paths</span><span class="sxs-lookup"><span data-stu-id="26209-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="26209-139">ARP tables for Azure public peering</span><span class="sxs-lookup"><span data-stu-id="26209-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="26209-140">The following cmdlet provides the ARP tables for Azure public peering</span><span class="sxs-lookup"><span data-stu-id="26209-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="26209-141">Sample output is shown below for one of the paths</span><span class="sxs-lookup"><span data-stu-id="26209-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="26209-142">ARP tables for Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="26209-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="26209-143">The following cmdlet provides the ARP tables for Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="26209-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="26209-144">Sample output is shown below for one of the paths</span><span class="sxs-lookup"><span data-stu-id="26209-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="26209-145">How to use this information</span><span class="sxs-lookup"><span data-stu-id="26209-145">How to use this information</span></span>
<span data-ttu-id="26209-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span><span class="sxs-lookup"><span data-stu-id="26209-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="26209-147">This section provides an overview of how ARP tables will look under different scenarios.</span><span class="sxs-lookup"><span data-stu-id="26209-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="26209-148">ARP table when a circuit is in operational state (expected state)</span><span class="sxs-lookup"><span data-stu-id="26209-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="26209-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="26209-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="26209-150">The last octet of the on-premises ip address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="26209-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="26209-151">The last octet of the Microsoft ip address will always be an even number.</span><span class="sxs-lookup"><span data-stu-id="26209-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="26209-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span><span class="sxs-lookup"><span data-stu-id="26209-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="26209-153">ARP table when on-premises / connectivity provider side has problems</span><span class="sxs-lookup"><span data-stu-id="26209-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="26209-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span><span class="sxs-lookup"><span data-stu-id="26209-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="26209-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="26209-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="26209-156">or</span><span class="sxs-lookup"><span data-stu-id="26209-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Open a support request with your connectivity provider to debug such issues. If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:
> 
> 1. If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR. Azure always uses the second IP address for MSEEs.
> 2. Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="26209-162">ARP table when Microsoft side has problems</span><span class="sxs-lookup"><span data-stu-id="26209-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="26209-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="26209-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="26209-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="26209-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="26209-165">Specify that you have an issue with layer 2 connectivity.</span><span class="sxs-lookup"><span data-stu-id="26209-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="26209-166">Next Steps</span><span class="sxs-lookup"><span data-stu-id="26209-166">Next Steps</span></span>
* <span data-ttu-id="26209-167">Validate Layer 3 configurations for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="26209-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="26209-168">Get route summary to determine the state of BGP sessions</span><span class="sxs-lookup"><span data-stu-id="26209-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="26209-169">Get route table to determine which prefixes are advertised across ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26209-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="26209-170">Validate data transfer by reviewing bytes in / out</span><span class="sxs-lookup"><span data-stu-id="26209-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="26209-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span><span class="sxs-lookup"><span data-stu-id="26209-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

