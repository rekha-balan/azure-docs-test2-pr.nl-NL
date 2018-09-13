---
title: Azure DMZ Example – Build a Simple DMZ with NSGs | Microsoft Docs
description: Build a DMZ with Network Security Groups (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: ''
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 6e1fea17878a355c7062c132c7e81112d1957eb8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555362"
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="bc320-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc320-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="bc320-104">[Return to the Security Boundary Best Practices Page][HOME]</span><span class="sxs-lookup"><span data-stu-id="bc320-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager Template](virtual-networks-dmz-nsg.md)
> * [Classic - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="bc320-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="bc320-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="bc320-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span><span class="sxs-lookup"><span data-stu-id="bc320-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="bc320-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span><span class="sxs-lookup"><span data-stu-id="bc320-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="bc320-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span><span class="sxs-lookup"><span data-stu-id="bc320-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="bc320-111">![Inbound DMZ with NSG][1]</span><span class="sxs-lookup"><span data-stu-id="bc320-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="bc320-112">Environment description</span><span class="sxs-lookup"><span data-stu-id="bc320-112">Environment description</span></span>
<span data-ttu-id="bc320-113">In this example a subscription contains the following resources:</span><span class="sxs-lookup"><span data-stu-id="bc320-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="bc320-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="bc320-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="bc320-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="bc320-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="bc320-116">A Network Security Group that is applied to both subnets</span><span class="sxs-lookup"><span data-stu-id="bc320-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="bc320-117">A Windows Server that represents an application web server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="bc320-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="bc320-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="bc320-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="bc320-119">A Windows server that represents a DNS server (“DNS01”)</span><span class="sxs-lookup"><span data-stu-id="bc320-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="bc320-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span><span class="sxs-lookup"><span data-stu-id="bc320-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="bc320-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span><span class="sxs-lookup"><span data-stu-id="bc320-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="bc320-122">To build the environment;</span><span class="sxs-lookup"><span data-stu-id="bc320-122">To build the environment;</span></span>

1. <span data-ttu-id="bc320-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span><span class="sxs-lookup"><span data-stu-id="bc320-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="bc320-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span><span class="sxs-lookup"><span data-stu-id="bc320-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="bc320-125">Execute the script in PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc320-125">Execute the script in PowerShell</span></span>

>[!Note]
>The region signified in the PowerShell script must match the region signified in the network configuration xml file.
>
>

<span data-ttu-id="bc320-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span><span class="sxs-lookup"><span data-stu-id="bc320-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="bc320-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="bc320-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="bc320-129">Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="bc320-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="bc320-130">For this example, an NSG group is built and then loaded with six rules.</span><span class="sxs-lookup"><span data-stu-id="bc320-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last. The assigned priority dictates which rules are evaluated first. Once traffic is found to apply to a specific rule, no further rules are evaluated. NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).
> 
> 

<span data-ttu-id="bc320-135">Declaratively, the following rules are being built for inbound traffic:</span><span class="sxs-lookup"><span data-stu-id="bc320-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="bc320-136">Internal DNS traffic (port 53) is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="bc320-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="bc320-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="bc320-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="bc320-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span><span class="sxs-lookup"><span data-stu-id="bc320-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="bc320-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span><span class="sxs-lookup"><span data-stu-id="bc320-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="bc320-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span><span class="sxs-lookup"><span data-stu-id="bc320-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="bc320-143">Thus the HTTP request would be allowed to the web server.</span><span class="sxs-lookup"><span data-stu-id="bc320-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="bc320-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span><span class="sxs-lookup"><span data-stu-id="bc320-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="bc320-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span><span class="sxs-lookup"><span data-stu-id="bc320-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="bc320-146">There is a default outbound rule that allows traffic out to the internet.</span><span class="sxs-lookup"><span data-stu-id="bc320-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="bc320-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span><span class="sxs-lookup"><span data-stu-id="bc320-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="bc320-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span><span class="sxs-lookup"><span data-stu-id="bc320-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="bc320-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span><span class="sxs-lookup"><span data-stu-id="bc320-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="bc320-150">First a Network Security Group must be built to hold the rules:</span><span class="sxs-lookup"><span data-stu-id="bc320-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="bc320-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span><span class="sxs-lookup"><span data-stu-id="bc320-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="bc320-152">The rule has some important parameters:</span><span class="sxs-lookup"><span data-stu-id="bc320-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="bc320-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span><span class="sxs-lookup"><span data-stu-id="bc320-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="bc320-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span><span class="sxs-lookup"><span data-stu-id="bc320-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="bc320-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span><span class="sxs-lookup"><span data-stu-id="bc320-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="bc320-156">“Priority” sets the order in which a traffic flow is evaluated.</span><span class="sxs-lookup"><span data-stu-id="bc320-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="bc320-157">The lower the number the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="bc320-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="bc320-158">When a rule applies to a specific traffic flow, no further rules are processed.</span><span class="sxs-lookup"><span data-stu-id="bc320-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="bc320-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span><span class="sxs-lookup"><span data-stu-id="bc320-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="bc320-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span><span class="sxs-lookup"><span data-stu-id="bc320-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="bc320-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span><span class="sxs-lookup"><span data-stu-id="bc320-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="bc320-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span><span class="sxs-lookup"><span data-stu-id="bc320-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="bc320-163">These tags are an easy way to address a larger category of address prefixes.</span><span class="sxs-lookup"><span data-stu-id="bc320-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="bc320-164">This rule allows inbound internet traffic to hit the web server.</span><span class="sxs-lookup"><span data-stu-id="bc320-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="bc320-165">This rule does not change the routing behavior.</span><span class="sxs-lookup"><span data-stu-id="bc320-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="bc320-166">The rule only allows traffic destined for IIS01 to pass.</span><span class="sxs-lookup"><span data-stu-id="bc320-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="bc320-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span><span class="sxs-lookup"><span data-stu-id="bc320-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="bc320-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span><span class="sxs-lookup"><span data-stu-id="bc320-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="bc320-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span><span class="sxs-lookup"><span data-stu-id="bc320-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="bc320-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span><span class="sxs-lookup"><span data-stu-id="bc320-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="bc320-171">To improve this rule, if the port is known that should be added.</span><span class="sxs-lookup"><span data-stu-id="bc320-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="bc320-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “\*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span><span class="sxs-lookup"><span data-stu-id="bc320-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “\*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="bc320-173">This rule denies traffic from the internet to any servers on the network.</span><span class="sxs-lookup"><span data-stu-id="bc320-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="bc320-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span><span class="sxs-lookup"><span data-stu-id="bc320-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="bc320-175">This rule is a "fail-safe" rule to block all unexpected flows.</span><span class="sxs-lookup"><span data-stu-id="bc320-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="bc320-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span><span class="sxs-lookup"><span data-stu-id="bc320-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="bc320-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span><span class="sxs-lookup"><span data-stu-id="bc320-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="bc320-178">Traffic scenarios</span><span class="sxs-lookup"><span data-stu-id="bc320-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="bc320-179">(*Allowed*) Internet to web server</span><span class="sxs-lookup"><span data-stu-id="bc320-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="bc320-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="bc320-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="bc320-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span><span class="sxs-lookup"><span data-stu-id="bc320-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="bc320-182">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="bc320-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="bc320-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bc320-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="bc320-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="bc320-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span><span class="sxs-lookup"><span data-stu-id="bc320-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="bc320-188">IIS01 asks the SQL Server on AppVM01 for information</span><span class="sxs-lookup"><span data-stu-id="bc320-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="bc320-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="bc320-190">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="bc320-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="bc320-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="bc320-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="bc320-195">AppVM01 receives the SQL Query and responds</span><span class="sxs-lookup"><span data-stu-id="bc320-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="bc320-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="bc320-197">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="bc320-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="bc320-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="bc320-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="bc320-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="bc320-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span><span class="sxs-lookup"><span data-stu-id="bc320-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="bc320-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span><span class="sxs-lookup"><span data-stu-id="bc320-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="bc320-202">(*Allowed*) RDP to backend</span><span class="sxs-lookup"><span data-stu-id="bc320-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="bc320-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="bc320-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="bc320-204">Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="bc320-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="bc320-207">With no outbound rules, default rules apply and return traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="bc320-208">RDP session is enabled</span><span class="sxs-lookup"><span data-stu-id="bc320-208">RDP session is enabled</span></span>
5. <span data-ttu-id="bc320-209">AppVM01 prompts for the user name and password</span><span class="sxs-lookup"><span data-stu-id="bc320-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="bc320-210">(*Allowed*) Web server DNS look-up on DNS server</span><span class="sxs-lookup"><span data-stu-id="bc320-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="bc320-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span><span class="sxs-lookup"><span data-stu-id="bc320-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="bc320-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span><span class="sxs-lookup"><span data-stu-id="bc320-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="bc320-213">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="bc320-214">Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="bc320-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="bc320-216">DNS server receives the request</span><span class="sxs-lookup"><span data-stu-id="bc320-216">DNS server receives the request</span></span>
6. <span data-ttu-id="bc320-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span><span class="sxs-lookup"><span data-stu-id="bc320-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="bc320-218">No outbound rules on Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="bc320-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="bc320-220">DNS server caches the response, and responds to the initial request back to IIS01</span><span class="sxs-lookup"><span data-stu-id="bc320-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="bc320-221">No outbound rules on Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="bc320-222">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="bc320-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="bc320-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="bc320-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="bc320-225">IIS01 receives the response from DNS01</span><span class="sxs-lookup"><span data-stu-id="bc320-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="bc320-226">(*Allowed*) Web server access file on AppVM01</span><span class="sxs-lookup"><span data-stu-id="bc320-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="bc320-227">IIS01 asks for a file on AppVM01</span><span class="sxs-lookup"><span data-stu-id="bc320-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="bc320-228">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="bc320-229">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="bc320-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="bc320-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="bc320-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bc320-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span><span class="sxs-lookup"><span data-stu-id="bc320-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="bc320-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="bc320-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="bc320-236">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="bc320-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="bc320-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="bc320-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="bc320-239">The IIS server receives the file</span><span class="sxs-lookup"><span data-stu-id="bc320-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="bc320-240">(*Denied*) Web to backend server</span><span class="sxs-lookup"><span data-stu-id="bc320-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="bc320-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="bc320-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="bc320-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="bc320-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="bc320-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span><span class="sxs-lookup"><span data-stu-id="bc320-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="bc320-244">(*Denied*) Web DNS look-up on DNS server</span><span class="sxs-lookup"><span data-stu-id="bc320-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="bc320-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="bc320-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="bc320-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="bc320-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="bc320-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span><span class="sxs-lookup"><span data-stu-id="bc320-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="bc320-248">(*Denied*) Web to SQL access through firewall</span><span class="sxs-lookup"><span data-stu-id="bc320-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="bc320-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span><span class="sxs-lookup"><span data-stu-id="bc320-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="bc320-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span><span class="sxs-lookup"><span data-stu-id="bc320-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="bc320-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="bc320-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="bc320-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="bc320-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="bc320-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="bc320-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="bc320-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="bc320-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="bc320-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="bc320-256">IIS01 isn't listening on port 1433, so no response to the request</span><span class="sxs-lookup"><span data-stu-id="bc320-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="bc320-257">Conclusion</span><span class="sxs-lookup"><span data-stu-id="bc320-257">Conclusion</span></span>
<span data-ttu-id="bc320-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="bc320-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="bc320-259">More examples and an overview of network security boundaries can be found [here][HOME].</span><span class="sxs-lookup"><span data-stu-id="bc320-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="bc320-260">References</span><span class="sxs-lookup"><span data-stu-id="bc320-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="bc320-261">Main script and network config</span><span class="sxs-lookup"><span data-stu-id="bc320-261">Main script and network config</span></span>
<span data-ttu-id="bc320-262">Save the Full Script in a PowerShell script file.</span><span class="sxs-lookup"><span data-stu-id="bc320-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="bc320-263">Save the Network Config into a file named “NetworkConf1.xml.”</span><span class="sxs-lookup"><span data-stu-id="bc320-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="bc320-264">Modify the user-defined variables as needed and run the script.</span><span class="sxs-lookup"><span data-stu-id="bc320-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="bc320-265">Full script</span><span class="sxs-lookup"><span data-stu-id="bc320-265">Full script</span></span>
<span data-ttu-id="bc320-266">This script will, based on the user-defined variables;</span><span class="sxs-lookup"><span data-stu-id="bc320-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="bc320-267">Connect to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="bc320-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="bc320-268">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="bc320-268">Create a storage account</span></span>
3. <span data-ttu-id="bc320-269">Create a VNet and two subnets as defined in the Network Config file</span><span class="sxs-lookup"><span data-stu-id="bc320-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="bc320-270">Build four windows server VMs</span><span class="sxs-lookup"><span data-stu-id="bc320-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="bc320-271">Configure NSG including:</span><span class="sxs-lookup"><span data-stu-id="bc320-271">Configure NSG including:</span></span>
   * <span data-ttu-id="bc320-272">Creating an NSG</span><span class="sxs-lookup"><span data-stu-id="bc320-272">Creating an NSG</span></span>
   * <span data-ttu-id="bc320-273">Populating it with rules</span><span class="sxs-lookup"><span data-stu-id="bc320-273">Populating it with rules</span></span>
   * <span data-ttu-id="bc320-274">Binding the NSG to the appropriate subnets</span><span class="sxs-lookup"><span data-stu-id="bc320-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="bc320-275">This PowerShell script should be run locally on an internet connected PC or server.</span><span class="sxs-lookup"><span data-stu-id="bc320-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> When this script is run, there may be warnings or other informational messages that pop in PowerShell. Only error messages in red are cause for concern.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="bc320-278">Network config file</span><span class="sxs-lookup"><span data-stu-id="bc320-278">Network config file</span></span>
<span data-ttu-id="bc320-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span><span class="sxs-lookup"><span data-stu-id="bc320-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="bc320-280">Sample application scripts</span><span class="sxs-lookup"><span data-stu-id="bc320-280">Sample application scripts</span></span>
<span data-ttu-id="bc320-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="bc320-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc320-282">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc320-282">Next steps</span></span>
* <span data-ttu-id="bc320-283">Update and save XML file</span><span class="sxs-lookup"><span data-stu-id="bc320-283">Update and save XML file</span></span>
* <span data-ttu-id="bc320-284">Run the PowerShell script to build the environment</span><span class="sxs-lookup"><span data-stu-id="bc320-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="bc320-285">Install the sample application</span><span class="sxs-lookup"><span data-stu-id="bc320-285">Install the sample application</span></span>
* <span data-ttu-id="bc320-286">Test different traffic flows through this DMZ</span><span class="sxs-lookup"><span data-stu-id="bc320-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md


