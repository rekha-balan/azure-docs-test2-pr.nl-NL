---
title: Troubleshoot Network Security Groups - PowerShell | Microsoft Docs
description: Learn how to troubleshoot Network Security Groups in the Azure Resource Manager deployment model using Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: ''
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 8dbb8a0134e784e95c70a0a856a499e6c60ffb14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555013"
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="79aab-103">Troubleshoot Network Security Groups using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="79aab-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="79aab-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span><span class="sxs-lookup"><span data-stu-id="79aab-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="79aab-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="79aab-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="79aab-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span><span class="sxs-lookup"><span data-stu-id="79aab-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="79aab-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span><span class="sxs-lookup"><span data-stu-id="79aab-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="79aab-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span><span class="sxs-lookup"><span data-stu-id="79aab-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="79aab-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span><span class="sxs-lookup"><span data-stu-id="79aab-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="79aab-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="79aab-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="79aab-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span><span class="sxs-lookup"><span data-stu-id="79aab-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="79aab-114">Using Effective Security Rules to troubleshoot VM traffic flow</span><span class="sxs-lookup"><span data-stu-id="79aab-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="79aab-115">The scenario that follows is an example of a common connection problem:</span><span class="sxs-lookup"><span data-stu-id="79aab-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="79aab-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span><span class="sxs-lookup"><span data-stu-id="79aab-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="79aab-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span><span class="sxs-lookup"><span data-stu-id="79aab-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="79aab-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="79aab-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="79aab-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span><span class="sxs-lookup"><span data-stu-id="79aab-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="79aab-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span><span class="sxs-lookup"><span data-stu-id="79aab-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="79aab-121">Detailed Troubleshooting Steps</span><span class="sxs-lookup"><span data-stu-id="79aab-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="79aab-122">Complete the following steps to troubleshoot NSGs for a VM:</span><span class="sxs-lookup"><span data-stu-id="79aab-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="79aab-123">Start an Azure PowerShell session and login to Azure.</span><span class="sxs-lookup"><span data-stu-id="79aab-123">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="79aab-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span><span class="sxs-lookup"><span data-stu-id="79aab-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span></span>
2. <span data-ttu-id="79aab-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span><span class="sxs-lookup"><span data-stu-id="79aab-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > If you don't know the name of a NIC, enter the following command to retrieve the names of all NICs in a resource group: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="79aab-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="79aab-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="79aab-128">Note the following information in the output:</span><span class="sxs-lookup"><span data-stu-id="79aab-128">Note the following information in the output:</span></span>
   
   * <span data-ttu-id="79aab-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span><span class="sxs-lookup"><span data-stu-id="79aab-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="79aab-130">In this example, an NSG has been applied to each.</span><span class="sxs-lookup"><span data-stu-id="79aab-130">In this example, an NSG has been applied to each.</span></span>
   * <span data-ttu-id="79aab-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span><span class="sxs-lookup"><span data-stu-id="79aab-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="79aab-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span><span class="sxs-lookup"><span data-stu-id="79aab-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span></span> 
   * <span data-ttu-id="79aab-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span><span class="sxs-lookup"><span data-stu-id="79aab-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="79aab-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span><span class="sxs-lookup"><span data-stu-id="79aab-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="79aab-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span><span class="sxs-lookup"><span data-stu-id="79aab-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span></span>
   * <span data-ttu-id="79aab-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span><span class="sxs-lookup"><span data-stu-id="79aab-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span></span> <span data-ttu-id="79aab-137">Tags represent multiple address prefixes.</span><span class="sxs-lookup"><span data-stu-id="79aab-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="79aab-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span><span class="sxs-lookup"><span data-stu-id="79aab-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="79aab-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span><span class="sxs-lookup"><span data-stu-id="79aab-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span></span>
     
     > [!NOTE]
     > The command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both. A VM may have multiple NICs with different NSGs applied. When troubleshooting, run the command for each NIC.
     > 
     > 
3. <span data-ttu-id="79aab-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span><span class="sxs-lookup"><span data-stu-id="79aab-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="79aab-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="79aab-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span></span>
   
    ![Rules list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="79aab-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span><span class="sxs-lookup"><span data-stu-id="79aab-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="79aab-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span><span class="sxs-lookup"><span data-stu-id="79aab-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span></span> <span data-ttu-id="79aab-148">For inbound rules, NSGs applied to the subnet are processed first.</span><span class="sxs-lookup"><span data-stu-id="79aab-148">For inbound rules, NSGs applied to the subnet are processed first.</span></span> <span data-ttu-id="79aab-149">If a match is found, the NSG applied to the network interface is not processed.</span><span class="sxs-lookup"><span data-stu-id="79aab-149">If a match is found, the NSG applied to the network interface is not processed.</span></span> <span data-ttu-id="79aab-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="79aab-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span></span>
   
   > [!NOTE]
   > A VM may have multiple NICs attached to it. Each may be connected to a different subnet. Since the commands in the previous steps are run against a NIC, it's important to ensure that you specify the NIC you're having the connectivity failure to. If you're not sure, you can always run the commands against each NIC attached to the VM.
   > 
   > 
5. <span data-ttu-id="79aab-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="79aab-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="79aab-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span><span class="sxs-lookup"><span data-stu-id="79aab-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="79aab-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="79aab-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="79aab-158">You can or remove rules from an NSG by using the information in the output from the following command:</span><span class="sxs-lookup"><span data-stu-id="79aab-158">You can or remove rules from an NSG by using the information in the output from the following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="79aab-159">Considerations</span><span class="sxs-lookup"><span data-stu-id="79aab-159">Considerations</span></span>
<span data-ttu-id="79aab-160">Consider the following points when troubleshooting connectivity problems:</span><span class="sxs-lookup"><span data-stu-id="79aab-160">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="79aab-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="79aab-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="79aab-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span><span class="sxs-lookup"><span data-stu-id="79aab-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="79aab-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span><span class="sxs-lookup"><span data-stu-id="79aab-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="79aab-164">Firewall software running within the VM's operating system</span><span class="sxs-lookup"><span data-stu-id="79aab-164">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="79aab-165">Routes configured for virtual appliances or on-premises traffic.</span><span class="sxs-lookup"><span data-stu-id="79aab-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="79aab-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span><span class="sxs-lookup"><span data-stu-id="79aab-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="79aab-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span><span class="sxs-lookup"><span data-stu-id="79aab-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="79aab-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span><span class="sxs-lookup"><span data-stu-id="79aab-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="79aab-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span><span class="sxs-lookup"><span data-stu-id="79aab-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="79aab-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span><span class="sxs-lookup"><span data-stu-id="79aab-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="79aab-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span><span class="sxs-lookup"><span data-stu-id="79aab-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="79aab-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span><span class="sxs-lookup"><span data-stu-id="79aab-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="79aab-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span><span class="sxs-lookup"><span data-stu-id="79aab-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>  


