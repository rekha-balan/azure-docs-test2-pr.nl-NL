---
title: 'Getting ARP tables: Classic: Azure ExpressRoute Troubleshooting | Microsoft Docs'
description: This page provides instructions for getting the ARP tables for an ExpressRoute circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555853"
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="92769-103">Getting ARP tables in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="92769-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Classic](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="92769-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="92769-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> This document is intended to help you diagnose and fix simple issues. It is not intended to be a replacement for Microsoft support. If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="92769-110">Address Resolution Protocol (ARP) and ARP tables</span><span class="sxs-lookup"><span data-stu-id="92769-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="92769-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="92769-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="92769-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span><span class="sxs-lookup"><span data-stu-id="92769-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="92769-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span><span class="sxs-lookup"><span data-stu-id="92769-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="92769-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span><span class="sxs-lookup"><span data-stu-id="92769-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="92769-115">Mapping of an on-premises router interface IP address to a MAC address</span><span class="sxs-lookup"><span data-stu-id="92769-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="92769-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span><span class="sxs-lookup"><span data-stu-id="92769-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="92769-117">The age of the mapping</span><span class="sxs-lookup"><span data-stu-id="92769-117">The age of the mapping</span></span>

<span data-ttu-id="92769-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="92769-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="92769-119">Following is an example of an ARP table:</span><span class="sxs-lookup"><span data-stu-id="92769-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="92769-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span><span class="sxs-lookup"><span data-stu-id="92769-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="92769-121">Prerequisites for using ARP tables</span><span class="sxs-lookup"><span data-stu-id="92769-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="92769-122">Ensure that you have the following before you continue:</span><span class="sxs-lookup"><span data-stu-id="92769-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="92769-123">A valid ExpressRoute circuit that's configured with at least one peering.</span><span class="sxs-lookup"><span data-stu-id="92769-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="92769-124">The circuit must be fully configured by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="92769-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="92769-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span><span class="sxs-lookup"><span data-stu-id="92769-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="92769-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span><span class="sxs-lookup"><span data-stu-id="92769-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="92769-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span><span class="sxs-lookup"><span data-stu-id="92769-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="92769-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="92769-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="92769-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span><span class="sxs-lookup"><span data-stu-id="92769-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="92769-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span><span class="sxs-lookup"><span data-stu-id="92769-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="92769-131">ARP tables for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="92769-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="92769-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92769-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="92769-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span><span class="sxs-lookup"><span data-stu-id="92769-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="92769-134">Each circuit has two paths (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="92769-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="92769-135">You can check the ARP table for each path independently.</span><span class="sxs-lookup"><span data-stu-id="92769-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="92769-136">ARP tables for Azure private peering</span><span class="sxs-lookup"><span data-stu-id="92769-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="92769-137">The following cmdlet provides the ARP tables for Azure private peering:</span><span class="sxs-lookup"><span data-stu-id="92769-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="92769-138">Following is sample output for one of the paths:</span><span class="sxs-lookup"><span data-stu-id="92769-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="92769-139">ARP tables for Azure public peering:</span><span class="sxs-lookup"><span data-stu-id="92769-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="92769-140">The following cmdlet provides the ARP tables for Azure public peering:</span><span class="sxs-lookup"><span data-stu-id="92769-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="92769-141">Following is sample output for one of the paths:</span><span class="sxs-lookup"><span data-stu-id="92769-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="92769-142">Following is sample output for one of the paths:</span><span class="sxs-lookup"><span data-stu-id="92769-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="92769-143">ARP tables for Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="92769-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="92769-144">The following cmdlet provides the ARP tables for Microsoft peering:</span><span class="sxs-lookup"><span data-stu-id="92769-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="92769-145">Sample output is shown below for one of the paths:</span><span class="sxs-lookup"><span data-stu-id="92769-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="92769-146">How to use this information</span><span class="sxs-lookup"><span data-stu-id="92769-146">How to use this information</span></span>
<span data-ttu-id="92769-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span><span class="sxs-lookup"><span data-stu-id="92769-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="92769-148">This section provides an overview of how ARP tables look in different scenarios.</span><span class="sxs-lookup"><span data-stu-id="92769-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="92769-149">ARP table when a circuit is in an operational (expected) state</span><span class="sxs-lookup"><span data-stu-id="92769-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="92769-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="92769-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="92769-151">The last octet of the on-premises IP address is always an odd number.</span><span class="sxs-lookup"><span data-stu-id="92769-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="92769-152">The last octet of the Microsoft IP address is always an even number.</span><span class="sxs-lookup"><span data-stu-id="92769-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="92769-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span><span class="sxs-lookup"><span data-stu-id="92769-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="92769-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span><span class="sxs-lookup"><span data-stu-id="92769-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="92769-155">Only one entry appears in the ARP table.</span><span class="sxs-lookup"><span data-stu-id="92769-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="92769-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="92769-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> If you experience an issue like this, open a support request with your connectivity provider to resolve it.
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="92769-158">ARP table when the Microsoft side has problems</span><span class="sxs-lookup"><span data-stu-id="92769-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="92769-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="92769-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="92769-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="92769-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="92769-161">Specify that you have an issue with Layer 2 connectivity.</span><span class="sxs-lookup"><span data-stu-id="92769-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92769-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="92769-162">Next steps</span></span>
* <span data-ttu-id="92769-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span><span class="sxs-lookup"><span data-stu-id="92769-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="92769-164">Get a route summary to determine the state of BGP sessions.</span><span class="sxs-lookup"><span data-stu-id="92769-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="92769-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="92769-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="92769-166">Validate data transfer by reviewing bytes in and out.</span><span class="sxs-lookup"><span data-stu-id="92769-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="92769-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span><span class="sxs-lookup"><span data-stu-id="92769-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

