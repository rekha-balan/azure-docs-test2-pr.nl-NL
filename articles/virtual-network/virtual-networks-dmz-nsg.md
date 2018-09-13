---
title: Azure DMZ Example – Build a Simple DMZ with NSGs | Microsoft Docs
description: Build a DMZ with Network Security Groups (NSG)
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: fa6c1f39c80653f7558b030b6d7279348bd19226
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550977"
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="de065-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="de065-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="de065-104">[Return to the Security Boundary Best Practices Page][HOME]</span><span class="sxs-lookup"><span data-stu-id="de065-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager Template](virtual-networks-dmz-nsg.md)
> * [Classic - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="de065-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="de065-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="de065-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span><span class="sxs-lookup"><span data-stu-id="de065-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="de065-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span><span class="sxs-lookup"><span data-stu-id="de065-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="de065-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span><span class="sxs-lookup"><span data-stu-id="de065-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="de065-111">![Inbound DMZ with NSG][1]</span><span class="sxs-lookup"><span data-stu-id="de065-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="de065-112">Environment description</span><span class="sxs-lookup"><span data-stu-id="de065-112">Environment description</span></span>
<span data-ttu-id="de065-113">In this example a subscription contains the following resources:</span><span class="sxs-lookup"><span data-stu-id="de065-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="de065-114">A single resource group</span><span class="sxs-lookup"><span data-stu-id="de065-114">A single resource group</span></span>
* <span data-ttu-id="de065-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="de065-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="de065-116">A Network Security Group that is applied to both subnets</span><span class="sxs-lookup"><span data-stu-id="de065-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="de065-117">A Windows Server that represents an application web server (“IIS01”)</span><span class="sxs-lookup"><span data-stu-id="de065-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="de065-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="de065-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="de065-119">A Windows server that represents a DNS server (“DNS01”)</span><span class="sxs-lookup"><span data-stu-id="de065-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="de065-120">A public IP address associated with the application web server</span><span class="sxs-lookup"><span data-stu-id="de065-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="de065-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span><span class="sxs-lookup"><span data-stu-id="de065-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="de065-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span><span class="sxs-lookup"><span data-stu-id="de065-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="de065-123">**To build this environment** (detailed instructions are in the references section of this document);</span><span class="sxs-lookup"><span data-stu-id="de065-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="de065-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span><span class="sxs-lookup"><span data-stu-id="de065-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="de065-125">Install the sample application at: [Sample Application Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="de065-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
>To RDP to any back-end servers in this instance, the IIS server is used as a "jump box." First RDP to the IIS server and then from the IIS Server RDP to the back-end server. Alternately a Public IP can be associated with each server NIC for easier RDP.
> 
>

<span data-ttu-id="de065-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span><span class="sxs-lookup"><span data-stu-id="de065-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="de065-130">Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="de065-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="de065-131">For this example, an NSG group is built and then loaded with six rules.</span><span class="sxs-lookup"><span data-stu-id="de065-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
>Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last. The assigned priority dictates which rules are evaluated first. Once traffic is found to apply to a specific rule, no further rules are evaluated. NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).
>
>

<span data-ttu-id="de065-136">Declaratively, the following rules are being built for inbound traffic:</span><span class="sxs-lookup"><span data-stu-id="de065-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="de065-137">Internal DNS traffic (port 53) is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="de065-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="de065-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="de065-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="de065-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span><span class="sxs-lookup"><span data-stu-id="de065-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="de065-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span><span class="sxs-lookup"><span data-stu-id="de065-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="de065-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span><span class="sxs-lookup"><span data-stu-id="de065-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="de065-144">Thus the HTTP request would be allowed to the web server.</span><span class="sxs-lookup"><span data-stu-id="de065-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="de065-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span><span class="sxs-lookup"><span data-stu-id="de065-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="de065-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span><span class="sxs-lookup"><span data-stu-id="de065-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="de065-147">There is a default outbound rule that allows traffic out to the internet.</span><span class="sxs-lookup"><span data-stu-id="de065-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="de065-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span><span class="sxs-lookup"><span data-stu-id="de065-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="de065-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span><span class="sxs-lookup"><span data-stu-id="de065-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="de065-150">Each rule is discussed in more detail as follows:</span><span class="sxs-lookup"><span data-stu-id="de065-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="de065-151">A Network Security Group resource must be instantiated to hold the rules:</span><span class="sxs-lookup"><span data-stu-id="de065-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="de065-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span><span class="sxs-lookup"><span data-stu-id="de065-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="de065-153">The rule has some important parameters:</span><span class="sxs-lookup"><span data-stu-id="de065-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="de065-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span><span class="sxs-lookup"><span data-stu-id="de065-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="de065-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span><span class="sxs-lookup"><span data-stu-id="de065-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="de065-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="de065-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="de065-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span><span class="sxs-lookup"><span data-stu-id="de065-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="de065-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span><span class="sxs-lookup"><span data-stu-id="de065-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="de065-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span><span class="sxs-lookup"><span data-stu-id="de065-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="de065-160">“Priority” sets the order in which a traffic flow is evaluated.</span><span class="sxs-lookup"><span data-stu-id="de065-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="de065-161">The lower the number the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="de065-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="de065-162">When a rule applies to a specific traffic flow, no further rules are processed.</span><span class="sxs-lookup"><span data-stu-id="de065-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="de065-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span><span class="sxs-lookup"><span data-stu-id="de065-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="de065-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span><span class="sxs-lookup"><span data-stu-id="de065-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="de065-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span><span class="sxs-lookup"><span data-stu-id="de065-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="de065-166">This rule allows inbound internet traffic to hit the web server.</span><span class="sxs-lookup"><span data-stu-id="de065-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="de065-167">This rule does not change the routing behavior.</span><span class="sxs-lookup"><span data-stu-id="de065-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="de065-168">The rule only allows traffic destined for IIS01 to pass.</span><span class="sxs-lookup"><span data-stu-id="de065-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="de065-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span><span class="sxs-lookup"><span data-stu-id="de065-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="de065-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span><span class="sxs-lookup"><span data-stu-id="de065-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="de065-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span><span class="sxs-lookup"><span data-stu-id="de065-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="de065-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span><span class="sxs-lookup"><span data-stu-id="de065-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="de065-173">To improve this rule, if the port is known that should be added.</span><span class="sxs-lookup"><span data-stu-id="de065-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="de065-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “\*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span><span class="sxs-lookup"><span data-stu-id="de065-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “\*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="de065-175">This rule denies traffic from the internet to any servers on the network.</span><span class="sxs-lookup"><span data-stu-id="de065-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="de065-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span><span class="sxs-lookup"><span data-stu-id="de065-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="de065-177">This rule is a "fail-safe" rule to block all unexpected flows.</span><span class="sxs-lookup"><span data-stu-id="de065-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="de065-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span><span class="sxs-lookup"><span data-stu-id="de065-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="de065-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span><span class="sxs-lookup"><span data-stu-id="de065-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="de065-180">Traffic scenarios</span><span class="sxs-lookup"><span data-stu-id="de065-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="de065-181">(*Allowed*) Internet to web server</span><span class="sxs-lookup"><span data-stu-id="de065-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="de065-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="de065-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="de065-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span><span class="sxs-lookup"><span data-stu-id="de065-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="de065-184">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="de065-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="de065-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="de065-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="de065-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="de065-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span><span class="sxs-lookup"><span data-stu-id="de065-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="de065-190">IIS01 asks the SQL Server on AppVM01 for information</span><span class="sxs-lookup"><span data-stu-id="de065-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="de065-191">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="de065-192">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="de065-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="de065-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="de065-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="de065-197">AppVM01 receives the SQL Query and responds</span><span class="sxs-lookup"><span data-stu-id="de065-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="de065-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="de065-199">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="de065-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="de065-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="de065-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="de065-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span><span class="sxs-lookup"><span data-stu-id="de065-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="de065-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span><span class="sxs-lookup"><span data-stu-id="de065-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="de065-204">(*Allowed*) RDP to IIS server</span><span class="sxs-lookup"><span data-stu-id="de065-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="de065-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span><span class="sxs-lookup"><span data-stu-id="de065-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="de065-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span><span class="sxs-lookup"><span data-stu-id="de065-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="de065-207">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="de065-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="de065-210">With no outbound rules, default rules apply and return traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="de065-211">RDP session is enabled</span><span class="sxs-lookup"><span data-stu-id="de065-211">RDP session is enabled</span></span>
6. <span data-ttu-id="de065-212">IIS01 prompts for the user name and password</span><span class="sxs-lookup"><span data-stu-id="de065-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
>To RDP to any back-end servers in this instance, the IIS server is used as a "jump box." First RDP to the IIS server and then from the IIS Server RDP to the back-end server.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="de065-215">(*Allowed*) Web server DNS look-up on DNS server</span><span class="sxs-lookup"><span data-stu-id="de065-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="de065-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span><span class="sxs-lookup"><span data-stu-id="de065-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="de065-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span><span class="sxs-lookup"><span data-stu-id="de065-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="de065-218">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="de065-219">Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="de065-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="de065-221">DNS server receives the request</span><span class="sxs-lookup"><span data-stu-id="de065-221">DNS server receives the request</span></span>
6. <span data-ttu-id="de065-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span><span class="sxs-lookup"><span data-stu-id="de065-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="de065-223">No outbound rules on Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="de065-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="de065-225">DNS server caches the response, and responds to the initial request back to IIS01</span><span class="sxs-lookup"><span data-stu-id="de065-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="de065-226">No outbound rules on Backend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="de065-227">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="de065-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="de065-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="de065-230">IIS01 receives the response from DNS01</span><span class="sxs-lookup"><span data-stu-id="de065-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="de065-231">(*Allowed*) Web server access file on AppVM01</span><span class="sxs-lookup"><span data-stu-id="de065-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="de065-232">IIS01 asks for a file on AppVM01</span><span class="sxs-lookup"><span data-stu-id="de065-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="de065-233">No outbound rules on Frontend subnet, traffic is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="de065-234">The Backend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="de065-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="de065-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="de065-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="de065-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span><span class="sxs-lookup"><span data-stu-id="de065-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="de065-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span><span class="sxs-lookup"><span data-stu-id="de065-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="de065-241">Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span><span class="sxs-lookup"><span data-stu-id="de065-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="de065-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="de065-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="de065-244">The IIS server receives the file</span><span class="sxs-lookup"><span data-stu-id="de065-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="de065-245">(*Denied*) RDP to backend</span><span class="sxs-lookup"><span data-stu-id="de065-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="de065-246">An internet user tries to RDP to server AppVM01</span><span class="sxs-lookup"><span data-stu-id="de065-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="de065-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="de065-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="de065-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span><span class="sxs-lookup"><span data-stu-id="de065-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
>To RDP to any back-end servers in this instance, the IIS server is used as a "jump box." First RDP to the IIS server and then from the IIS Server RDP to the back-end server.
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="de065-251">(*Denied*) Web to backend server</span><span class="sxs-lookup"><span data-stu-id="de065-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="de065-252">An internet user tries to access a file on AppVM01</span><span class="sxs-lookup"><span data-stu-id="de065-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="de065-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="de065-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="de065-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span><span class="sxs-lookup"><span data-stu-id="de065-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="de065-255">(*Denied*) Web DNS look-up on DNS server</span><span class="sxs-lookup"><span data-stu-id="de065-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="de065-256">An internet user tries to look up an internal DNS record on DNS01</span><span class="sxs-lookup"><span data-stu-id="de065-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="de065-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="de065-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="de065-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span><span class="sxs-lookup"><span data-stu-id="de065-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="de065-259">(*Denied*) SQL access on the web server</span><span class="sxs-lookup"><span data-stu-id="de065-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="de065-260">An internet user requests SQL data from IIS01</span><span class="sxs-lookup"><span data-stu-id="de065-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="de065-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span><span class="sxs-lookup"><span data-stu-id="de065-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="de065-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span><span class="sxs-lookup"><span data-stu-id="de065-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="de065-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="de065-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span><span class="sxs-lookup"><span data-stu-id="de065-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="de065-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span><span class="sxs-lookup"><span data-stu-id="de065-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="de065-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="de065-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="de065-267">IIS01 isn't listening on port 1433, so no response to the request</span><span class="sxs-lookup"><span data-stu-id="de065-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="de065-268">Conclusion</span><span class="sxs-lookup"><span data-stu-id="de065-268">Conclusion</span></span>
<span data-ttu-id="de065-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="de065-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="de065-270">More examples and an overview of network security boundaries can be found [here][HOME].</span><span class="sxs-lookup"><span data-stu-id="de065-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="de065-271">References</span><span class="sxs-lookup"><span data-stu-id="de065-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="de065-272">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="de065-272">Azure Resource Manager template</span></span>
<span data-ttu-id="de065-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span><span class="sxs-lookup"><span data-stu-id="de065-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="de065-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span><span class="sxs-lookup"><span data-stu-id="de065-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="de065-275">The main template is in the file named "azuredeploy.json."</span><span class="sxs-lookup"><span data-stu-id="de065-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="de065-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span><span class="sxs-lookup"><span data-stu-id="de065-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="de065-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span><span class="sxs-lookup"><span data-stu-id="de065-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="de065-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="de065-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="de065-279">From a browser, navigate to the [Template][Template]</span><span class="sxs-lookup"><span data-stu-id="de065-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="de065-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span><span class="sxs-lookup"><span data-stu-id="de065-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="de065-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span><span class="sxs-lookup"><span data-stu-id="de065-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="de065-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span><span class="sxs-lookup"><span data-stu-id="de065-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="de065-283">If necessary, change the Subscription and Location settings for your VNet.</span><span class="sxs-lookup"><span data-stu-id="de065-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="de065-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span><span class="sxs-lookup"><span data-stu-id="de065-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="de065-285">Click **Create** to begin the deployment of this template.</span><span class="sxs-lookup"><span data-stu-id="de065-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="de065-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span><span class="sxs-lookup"><span data-stu-id="de065-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
>This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal). To RDP to any back-end servers in this instance, the IIS server is used as a "jump box." First RDP to the IIS server and then from the IIS Server RDP to the back-end server.
>
>

<span data-ttu-id="de065-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span><span class="sxs-lookup"><span data-stu-id="de065-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="de065-291">Sample application scripts</span><span class="sxs-lookup"><span data-stu-id="de065-291">Sample application scripts</span></span>
<span data-ttu-id="de065-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span><span class="sxs-lookup"><span data-stu-id="de065-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="de065-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="de065-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="de065-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="de065-294">Next steps</span></span>

* <span data-ttu-id="de065-295">Deploy this example</span><span class="sxs-lookup"><span data-stu-id="de065-295">Deploy this example</span></span>
* <span data-ttu-id="de065-296">Build the sample application</span><span class="sxs-lookup"><span data-stu-id="de065-296">Build the sample application</span></span>
* <span data-ttu-id="de065-297">Test different traffic flows through this DMZ</span><span class="sxs-lookup"><span data-stu-id="de065-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md
