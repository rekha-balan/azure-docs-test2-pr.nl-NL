---
title: DMZ Example – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG | Microsoft Docs
description: Build a DMZ with a Firewall, User Defined Routing (UDR), and Network Security Groups (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: ''
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 5294f150e9de91d25aa872329d686d403551d2df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670902"
---
# <a name="example-3--build-a-dmz-to-protect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="c2dab-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span><span class="sxs-lookup"><span data-stu-id="c2dab-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="c2dab-104">[Return to the Security Boundary Best Practices Page][HOME]</span><span class="sxs-lookup"><span data-stu-id="c2dab-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="c2dab-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="c2dab-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="c2dab-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span><span class="sxs-lookup"><span data-stu-id="c2dab-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="c2dab-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span><span class="sxs-lookup"><span data-stu-id="c2dab-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="c2dab-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span><span class="sxs-lookup"><span data-stu-id="c2dab-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="c2dab-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span><span class="sxs-lookup"><span data-stu-id="c2dab-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="c2dab-110">Environment Setup</span><span class="sxs-lookup"><span data-stu-id="c2dab-110">Environment Setup</span></span>
<span data-ttu-id="c2dab-111">In this example there is a subscription that contains the following:</span><span class="sxs-lookup"><span data-stu-id="c2dab-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="c2dab-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="c2dab-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="c2dab-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="c2dab-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="c2dab-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span><span class="sxs-lookup"><span data-stu-id="c2dab-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span></span>
* <span data-ttu-id="c2dab-115">A Windows Server that represents an application web server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="c2dab-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="c2dab-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="c2dab-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="c2dab-117">A Windows server that represents a DNS server (“DNS01”)</span><span class="sxs-lookup"><span data-stu-id="c2dab-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="c2dab-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="c2dab-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span><span class="sxs-lookup"><span data-stu-id="c2dab-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="c2dab-120">To build the environment:</span><span class="sxs-lookup"><span data-stu-id="c2dab-120">To build the environment:</span></span>

1. <span data-ttu-id="c2dab-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span><span class="sxs-lookup"><span data-stu-id="c2dab-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="c2dab-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span><span class="sxs-lookup"><span data-stu-id="c2dab-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="c2dab-123">Execute the script in PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2dab-123">Execute the script in PowerShell</span></span>

<span data-ttu-id="c2dab-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span><span class="sxs-lookup"><span data-stu-id="c2dab-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="c2dab-125">Once the script runs successfully the following post-script steps may be taken:</span><span class="sxs-lookup"><span data-stu-id="c2dab-125">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="c2dab-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span><span class="sxs-lookup"><span data-stu-id="c2dab-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="c2dab-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span><span class="sxs-lookup"><span data-stu-id="c2dab-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="c2dab-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span><span class="sxs-lookup"><span data-stu-id="c2dab-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="c2dab-129">User Defined Routing (UDR)</span><span class="sxs-lookup"><span data-stu-id="c2dab-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="c2dab-130">By default, the following system routes are defined as:</span><span class="sxs-lookup"><span data-stu-id="c2dab-130">By default, the following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="c2dab-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span><span class="sxs-lookup"><span data-stu-id="c2dab-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="c2dab-132">The remaining system routes are static and default as above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-132">The remaining system routes are static and default as above.</span></span>

<span data-ttu-id="c2dab-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span><span class="sxs-lookup"><span data-stu-id="c2dab-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span></span>

<span data-ttu-id="c2dab-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span><span class="sxs-lookup"><span data-stu-id="c2dab-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span></span> <span data-ttu-id="c2dab-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span><span class="sxs-lookup"><span data-stu-id="c2dab-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="c2dab-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span><span class="sxs-lookup"><span data-stu-id="c2dab-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span></span>

<span data-ttu-id="c2dab-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span><span class="sxs-lookup"><span data-stu-id="c2dab-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span></span> 

<span data-ttu-id="c2dab-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span><span class="sxs-lookup"><span data-stu-id="c2dab-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="c2dab-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span><span class="sxs-lookup"><span data-stu-id="c2dab-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span></span>

1. <span data-ttu-id="c2dab-140">"VirtualAppliance" = A User Defined Route manually added to the table</span><span class="sxs-lookup"><span data-stu-id="c2dab-140">"VirtualAppliance" = A User Defined Route manually added to the table</span></span>
2. <span data-ttu-id="c2dab-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span><span class="sxs-lookup"><span data-stu-id="c2dab-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="c2dab-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="c2dab-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premise traffic to be routed to a network virtual appliance (NVA).</span><span class="sxs-lookup"><span data-stu-id="c2dab-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premise traffic to be routed to a network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-the-local-routes"></a><span data-ttu-id="c2dab-144">Creating the local routes</span><span class="sxs-lookup"><span data-stu-id="c2dab-144">Creating the local routes</span></span>
<span data-ttu-id="c2dab-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span><span class="sxs-lookup"><span data-stu-id="c2dab-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span></span> <span data-ttu-id="c2dab-146">Each table is loaded with static routes appropriate for the given subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-146">Each table is loaded with static routes appropriate for the given subnet.</span></span> <span data-ttu-id="c2dab-147">For the purpose of this example, each table has three routes:</span><span class="sxs-lookup"><span data-stu-id="c2dab-147">For the purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="c2dab-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span></span>
2. <span data-ttu-id="c2dab-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span><span class="sxs-lookup"><span data-stu-id="c2dab-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span></span>
3. <span data-ttu-id="c2dab-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span></span>

<span data-ttu-id="c2dab-151">Once the routing tables are created they are bound to their subnets.</span><span class="sxs-lookup"><span data-stu-id="c2dab-151">Once the routing tables are created they are bound to their subnets.</span></span> <span data-ttu-id="c2dab-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span><span class="sxs-lookup"><span data-stu-id="c2dab-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="c2dab-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span><span class="sxs-lookup"><span data-stu-id="c2dab-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="c2dab-154">First the base routing table must be created.</span><span class="sxs-lookup"><span data-stu-id="c2dab-154">First the base routing table must be created.</span></span> <span data-ttu-id="c2dab-155">This snippet shows the creation of the table for the Backend subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-155">This snippet shows the creation of the table for the Backend subnet.</span></span> <span data-ttu-id="c2dab-156">In the script, a corresponding table is also created for the Frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-156">In the script, a corresponding table is also created for the Frontend subnet.</span></span>
   
     <span data-ttu-id="c2dab-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="c2dab-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="c2dab-158">Once the route table is created, specific user defined routes can be added.</span><span class="sxs-lookup"><span data-stu-id="c2dab-158">Once the route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="c2dab-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span><span class="sxs-lookup"><span data-stu-id="c2dab-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span></span> <span data-ttu-id="c2dab-160">In the script, a corresponding rule is also created in the Frontend table.</span><span class="sxs-lookup"><span data-stu-id="c2dab-160">In the script, a corresponding rule is also created in the Frontend table.</span></span>
   
     <span data-ttu-id="c2dab-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="c2dab-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="c2dab-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span><span class="sxs-lookup"><span data-stu-id="c2dab-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span></span> <span data-ttu-id="c2dab-163">To correct this behavior the follow rule must be added.</span><span class="sxs-lookup"><span data-stu-id="c2dab-163">To correct this behavior the follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="c2dab-164">At this point there is a choice to be made.</span><span class="sxs-lookup"><span data-stu-id="c2dab-164">At this point there is a choice to be made.</span></span> <span data-ttu-id="c2dab-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="c2dab-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span><span class="sxs-lookup"><span data-stu-id="c2dab-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="c2dab-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="c2dab-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="c2dab-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span></span> <span data-ttu-id="c2dab-169">In the script, the front end route table is also bound to the Frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-169">In the script, the front end route table is also bound to the Frontend subnet.</span></span> <span data-ttu-id="c2dab-170">Here is the binding script for the back end subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-170">Here is the binding script for the back end subnet.</span></span>
   
     <span data-ttu-id="c2dab-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="c2dab-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="c2dab-172">IP Forwarding</span><span class="sxs-lookup"><span data-stu-id="c2dab-172">IP Forwarding</span></span>
<span data-ttu-id="c2dab-173">A companion feature to UDR, is IP Forwarding.</span><span class="sxs-lookup"><span data-stu-id="c2dab-173">A companion feature to UDR, is IP Forwarding.</span></span> <span data-ttu-id="c2dab-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span><span class="sxs-lookup"><span data-stu-id="c2dab-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span></span>

<span data-ttu-id="c2dab-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span></span> <span data-ttu-id="c2dab-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="c2dab-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="c2dab-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span><span class="sxs-lookup"><span data-stu-id="c2dab-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c2dab-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span><span class="sxs-lookup"><span data-stu-id="c2dab-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="c2dab-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span><span class="sxs-lookup"><span data-stu-id="c2dab-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="c2dab-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span><span class="sxs-lookup"><span data-stu-id="c2dab-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span></span>

1. <span data-ttu-id="c2dab-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span><span class="sxs-lookup"><span data-stu-id="c2dab-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="c2dab-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span><span class="sxs-lookup"><span data-stu-id="c2dab-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span></span>
   
     <span data-ttu-id="c2dab-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="c2dab-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="c2dab-184">Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="c2dab-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="c2dab-185">In this example, a NSG group is built and then loaded with a single rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="c2dab-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span><span class="sxs-lookup"><span data-stu-id="c2dab-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span></span> <span data-ttu-id="c2dab-187">Declaratively the following rule is being built:</span><span class="sxs-lookup"><span data-stu-id="c2dab-187">Declaratively the following rule is being built:</span></span>

1. <span data-ttu-id="c2dab-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span><span class="sxs-lookup"><span data-stu-id="c2dab-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="c2dab-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span><span class="sxs-lookup"><span data-stu-id="c2dab-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="c2dab-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span><span class="sxs-lookup"><span data-stu-id="c2dab-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span></span> <span data-ttu-id="c2dab-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span><span class="sxs-lookup"><span data-stu-id="c2dab-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span></span> <span data-ttu-id="c2dab-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="c2dab-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span></span> <span data-ttu-id="c2dab-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span><span class="sxs-lookup"><span data-stu-id="c2dab-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="c2dab-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet `
        from the Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="c2dab-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span></span> <span data-ttu-id="c2dab-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="c2dab-197">Firewall Rules</span><span class="sxs-lookup"><span data-stu-id="c2dab-197">Firewall Rules</span></span>
<span data-ttu-id="c2dab-198">On the firewall, forwarding rules will need to be created.</span><span class="sxs-lookup"><span data-stu-id="c2dab-198">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="c2dab-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span><span class="sxs-lookup"><span data-stu-id="c2dab-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="c2dab-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span></span> <span data-ttu-id="c2dab-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span><span class="sxs-lookup"><span data-stu-id="c2dab-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span></span> <span data-ttu-id="c2dab-202">The following figure is a logical view of the firewall rules for this example:</span><span class="sxs-lookup"><span data-stu-id="c2dab-202">The following figure is a logical view of the firewall rules for this example:</span></span>

<span data-ttu-id="c2dab-203">![Logical View of the Firewall Rules][2]</span><span class="sxs-lookup"><span data-stu-id="c2dab-203">![Logical View of the Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="c2dab-204">Based on the Network Virtual Appliance used, the management ports will vary.</span><span class="sxs-lookup"><span data-stu-id="c2dab-204">Based on the Network Virtual Appliance used, the management ports will vary.</span></span> <span data-ttu-id="c2dab-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span><span class="sxs-lookup"><span data-stu-id="c2dab-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="c2dab-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span><span class="sxs-lookup"><span data-stu-id="c2dab-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="c2dab-207">Logical Rule Description</span><span class="sxs-lookup"><span data-stu-id="c2dab-207">Logical Rule Description</span></span>
<span data-ttu-id="c2dab-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span><span class="sxs-lookup"><span data-stu-id="c2dab-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span></span> <span data-ttu-id="c2dab-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span><span class="sxs-lookup"><span data-stu-id="c2dab-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="c2dab-210">For this example, we need 7 types of rules, these rule types are described as follows:</span><span class="sxs-lookup"><span data-stu-id="c2dab-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="c2dab-211">External Rules (for inbound traffic):</span><span class="sxs-lookup"><span data-stu-id="c2dab-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="c2dab-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span><span class="sxs-lookup"><span data-stu-id="c2dab-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span></span>
  2. <span data-ttu-id="c2dab-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span><span class="sxs-lookup"><span data-stu-id="c2dab-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span></span> <span data-ttu-id="c2dab-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span><span class="sxs-lookup"><span data-stu-id="c2dab-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="c2dab-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span><span class="sxs-lookup"><span data-stu-id="c2dab-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="c2dab-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span><span class="sxs-lookup"><span data-stu-id="c2dab-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="c2dab-217">The first rule will allow the actual application traffic to reach the application server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-217">The first rule will allow the actual application traffic to reach the application server.</span></span> <span data-ttu-id="c2dab-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span><span class="sxs-lookup"><span data-stu-id="c2dab-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="c2dab-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span><span class="sxs-lookup"><span data-stu-id="c2dab-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span> <span data-ttu-id="c2dab-220">The redirected traffic session would be NAT’d to the internal server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-220">The redirected traffic session would be NAT’d to the internal server.</span></span>
     * <span data-ttu-id="c2dab-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span><span class="sxs-lookup"><span data-stu-id="c2dab-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="c2dab-222">Internal Rules (for intra-VNet traffic)</span><span class="sxs-lookup"><span data-stu-id="c2dab-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="c2dab-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span><span class="sxs-lookup"><span data-stu-id="c2dab-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span></span> <span data-ttu-id="c2dab-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span><span class="sxs-lookup"><span data-stu-id="c2dab-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span></span> <span data-ttu-id="c2dab-225">This rule should be enabled for this example.</span><span class="sxs-lookup"><span data-stu-id="c2dab-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="c2dab-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="c2dab-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="c2dab-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span><span class="sxs-lookup"><span data-stu-id="c2dab-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span></span>
* <span data-ttu-id="c2dab-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span><span class="sxs-lookup"><span data-stu-id="c2dab-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span></span>
  1. <span data-ttu-id="c2dab-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="c2dab-231">This is a default rule and usually activated, no modifications are generally needed.</span><span class="sxs-lookup"><span data-stu-id="c2dab-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="c2dab-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="c2dab-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span><span class="sxs-lookup"><span data-stu-id="c2dab-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="c2dab-234">For this example, the rules are in priority order.</span><span class="sxs-lookup"><span data-stu-id="c2dab-234">For this example, the rules are in priority order.</span></span> <span data-ttu-id="c2dab-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span><span class="sxs-lookup"><span data-stu-id="c2dab-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span></span> <span data-ttu-id="c2dab-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="c2dab-237">Rule Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c2dab-237">Rule Prerequisites</span></span>
<span data-ttu-id="c2dab-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span><span class="sxs-lookup"><span data-stu-id="c2dab-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span></span> <span data-ttu-id="c2dab-239">For the firewall to process traffic the appropriate public endpoints must be open.</span><span class="sxs-lookup"><span data-stu-id="c2dab-239">For the firewall to process traffic the appropriate public endpoints must be open.</span></span> <span data-ttu-id="c2dab-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span><span class="sxs-lookup"><span data-stu-id="c2dab-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="c2dab-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2dab-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="c2dab-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span><span class="sxs-lookup"><span data-stu-id="c2dab-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="c2dab-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span><span class="sxs-lookup"><span data-stu-id="c2dab-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="c2dab-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span><span class="sxs-lookup"><span data-stu-id="c2dab-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="c2dab-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span><span class="sxs-lookup"><span data-stu-id="c2dab-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="c2dab-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span><span class="sxs-lookup"><span data-stu-id="c2dab-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="c2dab-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="c2dab-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span></span> <span data-ttu-id="c2dab-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span></span>

<span data-ttu-id="c2dab-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span><span class="sxs-lookup"><span data-stu-id="c2dab-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="c2dab-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span><span class="sxs-lookup"><span data-stu-id="c2dab-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="c2dab-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span><span class="sxs-lookup"><span data-stu-id="c2dab-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="c2dab-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="c2dab-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="c2dab-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span><span class="sxs-lookup"><span data-stu-id="c2dab-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span></span>

<span data-ttu-id="c2dab-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span><span class="sxs-lookup"><span data-stu-id="c2dab-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span></span> <span data-ttu-id="c2dab-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span><span class="sxs-lookup"><span data-stu-id="c2dab-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span></span> <span data-ttu-id="c2dab-257">The network object can now be created, by adding the name and the prefix:</span><span class="sxs-lookup"><span data-stu-id="c2dab-257">The network object can now be created, by adding the name and the prefix:</span></span>

<span data-ttu-id="c2dab-258">![Create a FrontEnd Network Object][3]</span><span class="sxs-lookup"><span data-stu-id="c2dab-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="c2dab-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span><span class="sxs-lookup"><span data-stu-id="c2dab-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span></span> <span data-ttu-id="c2dab-260">Now the subnets can be more easily referenced by name in the firewall rules.</span><span class="sxs-lookup"><span data-stu-id="c2dab-260">Now the subnets can be more easily referenced by name in the firewall rules.</span></span>

<span data-ttu-id="c2dab-261">For the DNS Server Object:</span><span class="sxs-lookup"><span data-stu-id="c2dab-261">For the DNS Server Object:</span></span>

<span data-ttu-id="c2dab-262">![Create a DNS Server Object][4]</span><span class="sxs-lookup"><span data-stu-id="c2dab-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="c2dab-263">This single IP address reference will be utilized in a DNS rule later in the document.</span><span class="sxs-lookup"><span data-stu-id="c2dab-263">This single IP address reference will be utilized in a DNS rule later in the document.</span></span>

<span data-ttu-id="c2dab-264">The second prerequisite objects are Services objects.</span><span class="sxs-lookup"><span data-stu-id="c2dab-264">The second prerequisite objects are Services objects.</span></span> <span data-ttu-id="c2dab-265">These will represent the RDP connection ports for each server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-265">These will represent the RDP connection ports for each server.</span></span> <span data-ttu-id="c2dab-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span><span class="sxs-lookup"><span data-stu-id="c2dab-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span></span> <span data-ttu-id="c2dab-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span><span class="sxs-lookup"><span data-stu-id="c2dab-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="c2dab-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span><span class="sxs-lookup"><span data-stu-id="c2dab-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span></span> <span data-ttu-id="c2dab-269">Right-click and select copy, then right-click and select Paste.</span><span class="sxs-lookup"><span data-stu-id="c2dab-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="c2dab-270">There is now a RDP-Copy1 Service Object that can be edited.</span><span class="sxs-lookup"><span data-stu-id="c2dab-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="c2dab-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span><span class="sxs-lookup"><span data-stu-id="c2dab-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="c2dab-272">![Copy of Default RDP Rule][5]</span><span class="sxs-lookup"><span data-stu-id="c2dab-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="c2dab-273">The values can then be edited to represent the RDP service for a specific server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-273">The values can then be edited to represent the RDP service for a specific server.</span></span> <span data-ttu-id="c2dab-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span><span class="sxs-lookup"><span data-stu-id="c2dab-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span></span>

<span data-ttu-id="c2dab-275">![AppVM01 Rule][6]</span><span class="sxs-lookup"><span data-stu-id="c2dab-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="c2dab-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span><span class="sxs-lookup"><span data-stu-id="c2dab-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="c2dab-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span><span class="sxs-lookup"><span data-stu-id="c2dab-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="c2dab-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span><span class="sxs-lookup"><span data-stu-id="c2dab-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="c2dab-279">Firewall Rules Creation</span><span class="sxs-lookup"><span data-stu-id="c2dab-279">Firewall Rules Creation</span></span>
<span data-ttu-id="c2dab-280">There are three types of firewall rules used in this example, they all have distinct icons:</span><span class="sxs-lookup"><span data-stu-id="c2dab-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="c2dab-281">The Application Redirect rule: ![Application Redirect Icon][7]</span><span class="sxs-lookup"><span data-stu-id="c2dab-281">The Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="c2dab-282">The Destination NAT rule: ![Destination NAT Icon][8]</span><span class="sxs-lookup"><span data-stu-id="c2dab-282">The Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="c2dab-283">The Pass rule: ![Pass Icon][9]</span><span class="sxs-lookup"><span data-stu-id="c2dab-283">The Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="c2dab-284">More information on these rules can be found at the Barracuda web site.</span><span class="sxs-lookup"><span data-stu-id="c2dab-284">More information on these rules can be found at the Barracuda web site.</span></span>

<span data-ttu-id="c2dab-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span><span class="sxs-lookup"><span data-stu-id="c2dab-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="c2dab-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="c2dab-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span><span class="sxs-lookup"><span data-stu-id="c2dab-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span></span> <span data-ttu-id="c2dab-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="c2dab-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span><span class="sxs-lookup"><span data-stu-id="c2dab-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span></span> <span data-ttu-id="c2dab-290">The push and activation process is described below the details rule descriptions.</span><span class="sxs-lookup"><span data-stu-id="c2dab-290">The push and activation process is described below the details rule descriptions.</span></span>

<span data-ttu-id="c2dab-291">The specifics of each rule required to complete this example are described as follows:</span><span class="sxs-lookup"><span data-stu-id="c2dab-291">The specifics of each rule required to complete this example are described as follows:</span></span>

* <span data-ttu-id="c2dab-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="c2dab-293">The management ports are 801, 807 and optionally 22.</span><span class="sxs-lookup"><span data-stu-id="c2dab-293">The management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="c2dab-294">The external and internal ports are the same (i.e. no port translation).</span><span class="sxs-lookup"><span data-stu-id="c2dab-294">The external and internal ports are the same (i.e. no port translation).</span></span> <span data-ttu-id="c2dab-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span><span class="sxs-lookup"><span data-stu-id="c2dab-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="c2dab-296">![Firewall Management Rule][10]</span><span class="sxs-lookup"><span data-stu-id="c2dab-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="c2dab-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span><span class="sxs-lookup"><span data-stu-id="c2dab-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span></span>
> 
> 

* <span data-ttu-id="c2dab-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span><span class="sxs-lookup"><span data-stu-id="c2dab-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span></span>
  <span data-ttu-id="c2dab-299">There are four critical fields needed to create this rule:</span><span class="sxs-lookup"><span data-stu-id="c2dab-299">There are four critical fields needed to create this rule:</span></span>
  
  1. <span data-ttu-id="c2dab-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span><span class="sxs-lookup"><span data-stu-id="c2dab-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span></span>
  2. <span data-ttu-id="c2dab-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span><span class="sxs-lookup"><span data-stu-id="c2dab-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span></span> <span data-ttu-id="c2dab-302">This specific rule is for RDP access to AppVM01.</span><span class="sxs-lookup"><span data-stu-id="c2dab-302">This specific rule is for RDP access to AppVM01.</span></span>
  3. <span data-ttu-id="c2dab-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span><span class="sxs-lookup"><span data-stu-id="c2dab-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="c2dab-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span><span class="sxs-lookup"><span data-stu-id="c2dab-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="c2dab-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span><span class="sxs-lookup"><span data-stu-id="c2dab-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span></span>
  4. <span data-ttu-id="c2dab-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span><span class="sxs-lookup"><span data-stu-id="c2dab-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span></span> <span data-ttu-id="c2dab-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span><span class="sxs-lookup"><span data-stu-id="c2dab-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span></span> <span data-ttu-id="c2dab-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span><span class="sxs-lookup"><span data-stu-id="c2dab-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span></span>
     
     <span data-ttu-id="c2dab-309">![Firewall RDP Rule][11]</span><span class="sxs-lookup"><span data-stu-id="c2dab-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="c2dab-310">A total of four RDP rules will need to be created:</span><span class="sxs-lookup"><span data-stu-id="c2dab-310">A total of four RDP rules will need to be created:</span></span> 
     
     | <span data-ttu-id="c2dab-311">Rule Name</span><span class="sxs-lookup"><span data-stu-id="c2dab-311">Rule Name</span></span> | <span data-ttu-id="c2dab-312">Server</span><span class="sxs-lookup"><span data-stu-id="c2dab-312">Server</span></span> | <span data-ttu-id="c2dab-313">Service</span><span class="sxs-lookup"><span data-stu-id="c2dab-313">Service</span></span> | <span data-ttu-id="c2dab-314">Target List</span><span class="sxs-lookup"><span data-stu-id="c2dab-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="c2dab-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-315">RDP-to-IIS01</span></span> |<span data-ttu-id="c2dab-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-316">IIS01</span></span> |<span data-ttu-id="c2dab-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="c2dab-317">IIS01 RDP</span></span> |<span data-ttu-id="c2dab-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="c2dab-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="c2dab-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-319">RDP-to-DNS01</span></span> |<span data-ttu-id="c2dab-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-320">DNS01</span></span> |<span data-ttu-id="c2dab-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="c2dab-321">DNS01 RDP</span></span> |<span data-ttu-id="c2dab-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="c2dab-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="c2dab-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2dab-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="c2dab-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2dab-324">AppVM01</span></span> |<span data-ttu-id="c2dab-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="c2dab-325">AppVM01 RDP</span></span> |<span data-ttu-id="c2dab-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="c2dab-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="c2dab-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="c2dab-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="c2dab-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="c2dab-328">AppVM02</span></span> |<span data-ttu-id="c2dab-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="c2dab-329">AppVm02 RDP</span></span> |<span data-ttu-id="c2dab-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="c2dab-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="c2dab-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span><span class="sxs-lookup"><span data-stu-id="c2dab-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span></span> <span data-ttu-id="c2dab-332">The most limited scope that will allow functionality should be used.</span><span class="sxs-lookup"><span data-stu-id="c2dab-332">The most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="c2dab-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span><span class="sxs-lookup"><span data-stu-id="c2dab-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="c2dab-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span><span class="sxs-lookup"><span data-stu-id="c2dab-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="c2dab-335">First discussed is the front end rule for web traffic:</span><span class="sxs-lookup"><span data-stu-id="c2dab-335">First discussed is the front end rule for web traffic:</span></span>
  
    <span data-ttu-id="c2dab-336">![Firewall Web Rule][12]</span><span class="sxs-lookup"><span data-stu-id="c2dab-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="c2dab-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span></span> <span data-ttu-id="c2dab-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span><span class="sxs-lookup"><span data-stu-id="c2dab-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="c2dab-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span><span class="sxs-lookup"><span data-stu-id="c2dab-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span>
  
    <span data-ttu-id="c2dab-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span></span> <span data-ttu-id="c2dab-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span><span class="sxs-lookup"><span data-stu-id="c2dab-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span></span>
  
    <span data-ttu-id="c2dab-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span><span class="sxs-lookup"><span data-stu-id="c2dab-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="c2dab-343">![Firewall AppVM01 Rule][13]</span><span class="sxs-lookup"><span data-stu-id="c2dab-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="c2dab-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span><span class="sxs-lookup"><span data-stu-id="c2dab-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span></span>
  
    <span data-ttu-id="c2dab-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span><span class="sxs-lookup"><span data-stu-id="c2dab-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span></span> <span data-ttu-id="c2dab-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span><span class="sxs-lookup"><span data-stu-id="c2dab-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span></span> <span data-ttu-id="c2dab-347">This is up to the administrator of the firewall as to which method will be used.</span><span class="sxs-lookup"><span data-stu-id="c2dab-347">This is up to the administrator of the firewall as to which method will be used.</span></span> <span data-ttu-id="c2dab-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span><span class="sxs-lookup"><span data-stu-id="c2dab-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span></span>
  
    <span data-ttu-id="c2dab-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span><span class="sxs-lookup"><span data-stu-id="c2dab-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span></span>
  
    <span data-ttu-id="c2dab-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="c2dab-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="c2dab-352">However, this is not a recommended practice.</span><span class="sxs-lookup"><span data-stu-id="c2dab-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="c2dab-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span><span class="sxs-lookup"><span data-stu-id="c2dab-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="c2dab-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span><span class="sxs-lookup"><span data-stu-id="c2dab-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span></span> <span data-ttu-id="c2dab-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span><span class="sxs-lookup"><span data-stu-id="c2dab-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="c2dab-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span><span class="sxs-lookup"><span data-stu-id="c2dab-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="c2dab-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span><span class="sxs-lookup"><span data-stu-id="c2dab-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span></span> <span data-ttu-id="c2dab-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span><span class="sxs-lookup"><span data-stu-id="c2dab-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="c2dab-359">Right-clicking on this rule can access the Activate Rule command.</span><span class="sxs-lookup"><span data-stu-id="c2dab-359">Right-clicking on this rule can access the Activate Rule command.</span></span> <span data-ttu-id="c2dab-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span></span>
  
    <span data-ttu-id="c2dab-361">![Firewall Outbound Rule][14]</span><span class="sxs-lookup"><span data-stu-id="c2dab-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="c2dab-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="c2dab-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span><span class="sxs-lookup"><span data-stu-id="c2dab-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="c2dab-364">![Firewall DNS Rule][15]</span><span class="sxs-lookup"><span data-stu-id="c2dab-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="c2dab-365">**Note**: In this screen shot the Connection Method is included.</span><span class="sxs-lookup"><span data-stu-id="c2dab-365">**Note**: In this screen shot the Connection Method is included.</span></span> <span data-ttu-id="c2dab-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="c2dab-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span><span class="sxs-lookup"><span data-stu-id="c2dab-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span></span> <span data-ttu-id="c2dab-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span><span class="sxs-lookup"><span data-stu-id="c2dab-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span></span>
  
    <span data-ttu-id="c2dab-369">![Firewall Intra-VNet Rule][16]</span><span class="sxs-lookup"><span data-stu-id="c2dab-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="c2dab-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span><span class="sxs-lookup"><span data-stu-id="c2dab-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span></span> <span data-ttu-id="c2dab-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span><span class="sxs-lookup"><span data-stu-id="c2dab-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="c2dab-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="c2dab-373">This is a default rule and usually activated, no modifications are generally needed.</span><span class="sxs-lookup"><span data-stu-id="c2dab-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="c2dab-374">![Firewall Deny Rule][17]</span><span class="sxs-lookup"><span data-stu-id="c2dab-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2dab-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span><span class="sxs-lookup"><span data-stu-id="c2dab-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="c2dab-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span><span class="sxs-lookup"><span data-stu-id="c2dab-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="c2dab-377">Rule Activation</span><span class="sxs-lookup"><span data-stu-id="c2dab-377">Rule Activation</span></span>
<span data-ttu-id="c2dab-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span><span class="sxs-lookup"><span data-stu-id="c2dab-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span></span>

<span data-ttu-id="c2dab-379">![Firewall Rule Activation][18]</span><span class="sxs-lookup"><span data-stu-id="c2dab-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="c2dab-380">In the upper right hand corner of the management client are a cluster of buttons.</span><span class="sxs-lookup"><span data-stu-id="c2dab-380">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="c2dab-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span><span class="sxs-lookup"><span data-stu-id="c2dab-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="c2dab-382">With the activation of the firewall ruleset this example environment build is complete.</span><span class="sxs-lookup"><span data-stu-id="c2dab-382">With the activation of the firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="c2dab-383">Traffic Scenarios</span><span class="sxs-lookup"><span data-stu-id="c2dab-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c2dab-384">A key takeway is to remember that **all** traffic will come through the firewall.</span><span class="sxs-lookup"><span data-stu-id="c2dab-384">A key takeway is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="c2dab-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span><span class="sxs-lookup"><span data-stu-id="c2dab-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="c2dab-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span><span class="sxs-lookup"><span data-stu-id="c2dab-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="c2dab-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="c2dab-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="c2dab-388">For these scenarios, the following firewall rules should be in place:</span><span class="sxs-lookup"><span data-stu-id="c2dab-388">For these scenarios, the following firewall rules should be in place:</span></span>

1. <span data-ttu-id="c2dab-389">Firewall Management</span><span class="sxs-lookup"><span data-stu-id="c2dab-389">Firewall Management</span></span>
2. <span data-ttu-id="c2dab-390">RDP to IIS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-390">RDP to IIS01</span></span>
3. <span data-ttu-id="c2dab-391">RDP to DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-391">RDP to DNS01</span></span>
4. <span data-ttu-id="c2dab-392">RDP to AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2dab-392">RDP to AppVM01</span></span>
5. <span data-ttu-id="c2dab-393">RDP to AppVM02</span><span class="sxs-lookup"><span data-stu-id="c2dab-393">RDP to AppVM02</span></span>
6. <span data-ttu-id="c2dab-394">App Traffic to the Web</span><span class="sxs-lookup"><span data-stu-id="c2dab-394">App Traffic to the Web</span></span>
7. <span data-ttu-id="c2dab-395">App Traffic to AppVM01</span><span class="sxs-lookup"><span data-stu-id="c2dab-395">App Traffic to AppVM01</span></span>
8. <span data-ttu-id="c2dab-396">Outbound to the Internet</span><span class="sxs-lookup"><span data-stu-id="c2dab-396">Outbound to the Internet</span></span>
9. <span data-ttu-id="c2dab-397">Frontend to DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-397">Frontend to DNS01</span></span>
10. <span data-ttu-id="c2dab-398">Intra-Subnet Traffic (back end to front end only)</span><span class="sxs-lookup"><span data-stu-id="c2dab-398">Intra-Subnet Traffic (back end to front end only)</span></span>
11. <span data-ttu-id="c2dab-399">Deny All</span><span class="sxs-lookup"><span data-stu-id="c2dab-399">Deny All</span></span>

<span data-ttu-id="c2dab-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span><span class="sxs-lookup"><span data-stu-id="c2dab-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span></span> <span data-ttu-id="c2dab-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span><span class="sxs-lookup"><span data-stu-id="c2dab-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span></span> <span data-ttu-id="c2dab-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span><span class="sxs-lookup"><span data-stu-id="c2dab-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span></span> <span data-ttu-id="c2dab-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span><span class="sxs-lookup"><span data-stu-id="c2dab-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="c2dab-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span><span class="sxs-lookup"><span data-stu-id="c2dab-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span></span>

<span data-ttu-id="c2dab-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span><span class="sxs-lookup"><span data-stu-id="c2dab-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="c2dab-406">(Allowed) Internet to Web Server</span><span class="sxs-lookup"><span data-stu-id="c2dab-406">(Allowed) Internet to Web Server</span></span>
1. <span data-ttu-id="c2dab-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="c2dab-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="c2dab-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="c2dab-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="c2dab-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="c2dab-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="c2dab-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="c2dab-411">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="c2dab-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="c2dab-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="c2dab-415">The Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-415">The Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="c2dab-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="c2dab-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="c2dab-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span><span class="sxs-lookup"><span data-stu-id="c2dab-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
8. <span data-ttu-id="c2dab-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span><span class="sxs-lookup"><span data-stu-id="c2dab-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="c2dab-420">The UDR route on Frontend subnet makes the firewall the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-420">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
10. <span data-ttu-id="c2dab-421">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="c2dab-422">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="c2dab-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="c2dab-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span></span>
    4. <span data-ttu-id="c2dab-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="c2dab-427">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-427">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="c2dab-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="c2dab-430">AppVM01 receives the request and initiates the session and responds</span><span class="sxs-lookup"><span data-stu-id="c2dab-430">AppVM01 receives the request and initiates the session and responds</span></span>
14. <span data-ttu-id="c2dab-431">The UDR route on Backend subnet makes the firewall the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-431">The UDR route on Backend subnet makes the firewall the next hop</span></span>
15. <span data-ttu-id="c2dab-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
16. <span data-ttu-id="c2dab-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span></span>
17. <span data-ttu-id="c2dab-434">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="c2dab-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="c2dab-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span><span class="sxs-lookup"><span data-stu-id="c2dab-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span></span>
19. <span data-ttu-id="c2dab-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
20. <span data-ttu-id="c2dab-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span></span>
21. <span data-ttu-id="c2dab-440">The firewall then redirects the response back to the Internet User</span><span class="sxs-lookup"><span data-stu-id="c2dab-440">The firewall then redirects the response back to the Internet User</span></span>
22. <span data-ttu-id="c2dab-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span><span class="sxs-lookup"><span data-stu-id="c2dab-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-internet-rdp-to-backend"></a><span data-ttu-id="c2dab-442">(Allowed) Internet RDP to Backend</span><span class="sxs-lookup"><span data-stu-id="c2dab-442">(Allowed) Internet RDP to Backend</span></span>
1. <span data-ttu-id="c2dab-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span></span>
2. <span data-ttu-id="c2dab-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="c2dab-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="c2dab-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="c2dab-446">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="c2dab-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="c2dab-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="c2dab-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="c2dab-451">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-451">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="c2dab-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="c2dab-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="c2dab-454">AppVM01 is listening for RDP traffic and responds</span><span class="sxs-lookup"><span data-stu-id="c2dab-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="c2dab-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="c2dab-456">UDR routes outbound traffic to the firewall as the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-456">UDR routes outbound traffic to the firewall as the next hop</span></span>
9. <span data-ttu-id="c2dab-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span><span class="sxs-lookup"><span data-stu-id="c2dab-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span></span>
10. <span data-ttu-id="c2dab-458">RDP session is enabled</span><span class="sxs-lookup"><span data-stu-id="c2dab-458">RDP session is enabled</span></span>
11. <span data-ttu-id="c2dab-459">AppVM01 prompts for user name password</span><span class="sxs-lookup"><span data-stu-id="c2dab-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="c2dab-460">(Allowed) Web Server DNS lookup on DNS server</span><span class="sxs-lookup"><span data-stu-id="c2dab-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="c2dab-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span><span class="sxs-lookup"><span data-stu-id="c2dab-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="c2dab-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="c2dab-463">UDR routes outbound traffic to the firewall as the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-463">UDR routes outbound traffic to the firewall as the next hop</span></span>
4. <span data-ttu-id="c2dab-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="c2dab-465">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="c2dab-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="c2dab-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="c2dab-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="c2dab-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="c2dab-471">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-471">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="c2dab-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="c2dab-474">DNS server receives the request</span><span class="sxs-lookup"><span data-stu-id="c2dab-474">DNS server receives the request</span></span>
8. <span data-ttu-id="c2dab-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span><span class="sxs-lookup"><span data-stu-id="c2dab-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
9. <span data-ttu-id="c2dab-476">UDR routes outbound traffic to the firewall as the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-476">UDR routes outbound traffic to the firewall as the next hop</span></span>
10. <span data-ttu-id="c2dab-477">No outbound NSG rules on Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="c2dab-478">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="c2dab-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="c2dab-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
    4. <span data-ttu-id="c2dab-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span><span class="sxs-lookup"><span data-stu-id="c2dab-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span></span>
12. <span data-ttu-id="c2dab-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span></span>
13. <span data-ttu-id="c2dab-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span></span>
14. <span data-ttu-id="c2dab-485">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-485">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="c2dab-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="c2dab-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span></span>
16. <span data-ttu-id="c2dab-489">The UDR route on backend subnet makes the firewall the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-489">The UDR route on backend subnet makes the firewall the next hop</span></span>
17. <span data-ttu-id="c2dab-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="c2dab-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span><span class="sxs-lookup"><span data-stu-id="c2dab-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span></span>
19. <span data-ttu-id="c2dab-492">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="c2dab-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="c2dab-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="c2dab-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
20. <span data-ttu-id="c2dab-495">IIS01 receives the response from DNS01</span><span class="sxs-lookup"><span data-stu-id="c2dab-495">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-backend-server-to-frontend-server"></a><span data-ttu-id="c2dab-496">(Allowed) Backend server to Frontend server</span><span class="sxs-lookup"><span data-stu-id="c2dab-496">(Allowed) Backend server to Frontend server</span></span>
1. <span data-ttu-id="c2dab-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span><span class="sxs-lookup"><span data-stu-id="c2dab-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="c2dab-498">The UDR route on Backend subnet makes the firewall the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-498">The UDR route on Backend subnet makes the firewall the next hop</span></span>
3. <span data-ttu-id="c2dab-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
4. <span data-ttu-id="c2dab-500">Firewall begins rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="c2dab-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="c2dab-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="c2dab-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="c2dab-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="c2dab-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="c2dab-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="c2dab-507">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="c2dab-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="c2dab-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span><span class="sxs-lookup"><span data-stu-id="c2dab-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span></span>
7. <span data-ttu-id="c2dab-511">The UDR route on Frontend subnet makes the firewall the next hop</span><span class="sxs-lookup"><span data-stu-id="c2dab-511">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
8. <span data-ttu-id="c2dab-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span><span class="sxs-lookup"><span data-stu-id="c2dab-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
9. <span data-ttu-id="c2dab-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span><span class="sxs-lookup"><span data-stu-id="c2dab-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span></span>
10. <span data-ttu-id="c2dab-514">Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="c2dab-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="c2dab-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="c2dab-517">AppVM02 receives the response</span><span class="sxs-lookup"><span data-stu-id="c2dab-517">AppVM02 receives the response</span></span>

#### <a name="denied-internet-direct-to-web-server"></a><span data-ttu-id="c2dab-518">(Denied) Internet direct to Web Server</span><span class="sxs-lookup"><span data-stu-id="c2dab-518">(Denied) Internet direct to Web Server</span></span>
1. <span data-ttu-id="c2dab-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="c2dab-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="c2dab-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="c2dab-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="c2dab-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span><span class="sxs-lookup"><span data-stu-id="c2dab-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="c2dab-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span><span class="sxs-lookup"><span data-stu-id="c2dab-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-backend-server"></a><span data-ttu-id="c2dab-523">(Denied) Internet to Backend Server</span><span class="sxs-lookup"><span data-stu-id="c2dab-523">(Denied) Internet to Backend Server</span></span>
1. <span data-ttu-id="c2dab-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="c2dab-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="c2dab-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="c2dab-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="c2dab-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span><span class="sxs-lookup"><span data-stu-id="c2dab-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="c2dab-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span><span class="sxs-lookup"><span data-stu-id="c2dab-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-to-backend-server"></a><span data-ttu-id="c2dab-528">(Denied) Frontend server to Backend Server</span><span class="sxs-lookup"><span data-stu-id="c2dab-528">(Denied) Frontend server to Backend Server</span></span>
1. <span data-ttu-id="c2dab-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span><span class="sxs-lookup"><span data-stu-id="c2dab-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span></span>
2. <span data-ttu-id="c2dab-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span><span class="sxs-lookup"><span data-stu-id="c2dab-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span></span> <span data-ttu-id="c2dab-531">This is not something that can be altered by the compromised VM.</span><span class="sxs-lookup"><span data-stu-id="c2dab-531">This is not something that can be altered by the compromised VM.</span></span>
3. <span data-ttu-id="c2dab-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span><span class="sxs-lookup"><span data-stu-id="c2dab-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span></span> <span data-ttu-id="c2dab-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span><span class="sxs-lookup"><span data-stu-id="c2dab-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="c2dab-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span><span class="sxs-lookup"><span data-stu-id="c2dab-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="c2dab-535">(Denied) Internet DNS lookup on DNS server</span><span class="sxs-lookup"><span data-stu-id="c2dab-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="c2dab-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="c2dab-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="c2dab-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="c2dab-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="c2dab-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span><span class="sxs-lookup"><span data-stu-id="c2dab-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="c2dab-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span><span class="sxs-lookup"><span data-stu-id="c2dab-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-sql-access-through-firewall"></a><span data-ttu-id="c2dab-540">(Denied) Internet to SQL access through Firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-540">(Denied) Internet to SQL access through Firewall</span></span>
1. <span data-ttu-id="c2dab-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="c2dab-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="c2dab-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span><span class="sxs-lookup"><span data-stu-id="c2dab-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="c2dab-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span><span class="sxs-lookup"><span data-stu-id="c2dab-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="c2dab-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="c2dab-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="c2dab-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="c2dab-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="c2dab-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="c2dab-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span></span>
   7. <span data-ttu-id="c2dab-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="c2dab-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="c2dab-551">References</span><span class="sxs-lookup"><span data-stu-id="c2dab-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="c2dab-552">Main Script and Network Config</span><span class="sxs-lookup"><span data-stu-id="c2dab-552">Main Script and Network Config</span></span>
<span data-ttu-id="c2dab-553">Save the Full Script in a PowerShell script file.</span><span class="sxs-lookup"><span data-stu-id="c2dab-553">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="c2dab-554">Save the Network Config into a file named “NetworkConf2.xml”.</span><span class="sxs-lookup"><span data-stu-id="c2dab-554">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="c2dab-555">Modify the user defined variables as needed.</span><span class="sxs-lookup"><span data-stu-id="c2dab-555">Modify the user defined variables as needed.</span></span> <span data-ttu-id="c2dab-556">Run the script, then follow the Firewall rule setup instruction above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-556">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="c2dab-557">Full Script</span><span class="sxs-lookup"><span data-stu-id="c2dab-557">Full Script</span></span>
<span data-ttu-id="c2dab-558">This script will, based on the user defined variables:</span><span class="sxs-lookup"><span data-stu-id="c2dab-558">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="c2dab-559">Connect to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c2dab-559">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="c2dab-560">Create a new storage account</span><span class="sxs-lookup"><span data-stu-id="c2dab-560">Create a new storage account</span></span>
3. <span data-ttu-id="c2dab-561">Create a new VNet and three subnets as defined in the Network Config file</span><span class="sxs-lookup"><span data-stu-id="c2dab-561">Create a new VNet and three subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="c2dab-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span><span class="sxs-lookup"><span data-stu-id="c2dab-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="c2dab-563">Configure UDR including:</span><span class="sxs-lookup"><span data-stu-id="c2dab-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="c2dab-564">Creating two new route tables</span><span class="sxs-lookup"><span data-stu-id="c2dab-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="c2dab-565">Add routes to the tables</span><span class="sxs-lookup"><span data-stu-id="c2dab-565">Add routes to the tables</span></span>
   3. <span data-ttu-id="c2dab-566">Bind tables to appropriate subnets</span><span class="sxs-lookup"><span data-stu-id="c2dab-566">Bind tables to appropriate subnets</span></span>
6. <span data-ttu-id="c2dab-567">Enable IP Forwarding on the NVA</span><span class="sxs-lookup"><span data-stu-id="c2dab-567">Enable IP Forwarding on the NVA</span></span>
7. <span data-ttu-id="c2dab-568">Configure NSG including:</span><span class="sxs-lookup"><span data-stu-id="c2dab-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="c2dab-569">Creating a NSG</span><span class="sxs-lookup"><span data-stu-id="c2dab-569">Creating a NSG</span></span>
   2. <span data-ttu-id="c2dab-570">Adding a rule</span><span class="sxs-lookup"><span data-stu-id="c2dab-570">Adding a rule</span></span>
   3. <span data-ttu-id="c2dab-571">Binding the NSG to the appropriate subnets</span><span class="sxs-lookup"><span data-stu-id="c2dab-571">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="c2dab-572">This PowerShell script should be run locally on an internet connected PC or server.</span><span class="sxs-lookup"><span data-stu-id="c2dab-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2dab-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2dab-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="c2dab-574">Only error messages in red are cause for concern.</span><span class="sxs-lookup"><span data-stu-id="c2dab-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on the FrontEnd Subnet
       - Three Servers on the BackEnd Subnet
       - IP Forwading from the FireWall out to the internet
       - User Defined Routing FrontEnd and BackEnd Subnets to the NVA

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind the appropriate
      layer(s) of protection. This script serves as an example of some of the techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and the appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: To ensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be the NVA.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "The SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all the EndPoints we'll need once we're up and running
                # Note: All traffic goes through the firewall, so we'll need to set up all ports here.
                #       Also, the firewall will be redirecting traffic to a new IP and Port in a forwarding
                #       rule, so all of these endpoint have the same public and local port and the firewall
                #       will do the mapping, NATing, and/or redirection as declared in the firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create the Route Tables
        Write-Host "Creating the Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes to Route Tables
        Write-Host "Adding Routes to the Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate the Route Tables with the Subnets
        Write-Host "Binding Route Tables to the Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on the Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign the NSG to two Subnets
        # The NSG is *not* bound to the Security Subnet. The result
        # is that internet traffic flows only to the Security subnet
        # since the NSG bound to the Frontend and Backback subnets
        # will Deny internet traffic to those subnets.
        Write-Host "Binding the NSG to two subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="c2dab-575">Network Config File</span><span class="sxs-lookup"><span data-stu-id="c2dab-575">Network Config File</span></span>
<span data-ttu-id="c2dab-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span><span class="sxs-lookup"><span data-stu-id="c2dab-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="c2dab-577">Sample Application Scripts</span><span class="sxs-lookup"><span data-stu-id="c2dab-577">Sample Application Scripts</span></span>
<span data-ttu-id="c2dab-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="c2dab-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bi-directional DMZ with NVA, NSG, and UDR"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logical View of the Firewall Rules"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Create a FrontEnd Network Object"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Create a DNS Server Object"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copy of Default RDP Rule"
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 Rule"
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Application Redirect Icon"
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Destination NAT Icon"
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass Icon"
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewall Management Rule"
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Firewall RDP Rule"
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Firewall Web Rule"
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Firewall AppVM01 Rule"
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Firewall Outbound Rule"
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Firewall DNS Rule"
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Firewall Intra-VNet Rule"
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Firewall Deny Rule"
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Firewall Rule Activation"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md


















