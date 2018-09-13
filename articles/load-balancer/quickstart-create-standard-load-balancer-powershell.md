---
title: Quickstart:Create a Standard Load Balancer - Azure PowerShell | Microsoft Docs
description: This quickstart shows how to create a Standard Load Balancer using PowerShell
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
tags: azure-resource-manager
Customer intent: I want to create a Standard Load balancer so that I can load balance internet traffic to VMs.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/22/2018
ms.author: kumud
ms:custom: mvc
ms.openlocfilehash: 67d514fe6315604016dc10b7dfc8154c3919f914
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969010"
---
# <a name="get-started"></a><span data-ttu-id="77014-103">Quickstart: Create a Standard Load Balancer using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77014-103">Quickstart: Create a Standard Load Balancer using Azure PowerShell</span></span>
<span data-ttu-id="77014-104">This quickstart shows you how to create a Standard Load Balancer using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77014-104">This quickstart shows you how to create a Standard Load Balancer using Azure PowerShell.</span></span> <span data-ttu-id="77014-105">To test the load balancer, you deploy two virtual machines (VMs) running Windows server and load balance a web app between the VMs.</span><span class="sxs-lookup"><span data-stu-id="77014-105">To test the load balancer, you deploy two virtual machines (VMs) running Windows server and load balance a web app between the VMs.</span></span> <span data-ttu-id="77014-106">To learn more about Standard Load Balancer, see [What is Standard Load Balancer](load-balancer-standard-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77014-106">To learn more about Standard Load Balancer, see [What is Standard Load Balancer](load-balancer-standard-overview.md).</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="77014-107">If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later.</span><span class="sxs-lookup"><span data-stu-id="77014-107">If you choose to install and use PowerShell locally, this article requires the Azure PowerShell module version 5.4.1 or later.</span></span> <span data-ttu-id="77014-108">Run `Get-Module -ListAvailable AzureRM` to find the installed version.</span><span class="sxs-lookup"><span data-stu-id="77014-108">Run `Get-Module -ListAvailable AzureRM` to find the installed version.</span></span> <span data-ttu-id="77014-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="77014-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="77014-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="77014-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="77014-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="77014-111">Create a resource group</span></span>

<span data-ttu-id="77014-112">Before you can create your load balancer, you must create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="77014-112">Before you can create your load balancer, you must create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="77014-113">The following example creates a resource group named *myResourceGroupLB* in the *EastUS* location:</span><span class="sxs-lookup"><span data-stu-id="77014-113">The following example creates a resource group named *myResourceGroupLB* in the *EastUS* location:</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup `
  -ResourceGroupName "myResourceGroupLB" `
  -Location "EastUS"
```
## <a name="create-a-public-ip-address"></a><span data-ttu-id="77014-114">Create a public IP address</span><span class="sxs-lookup"><span data-stu-id="77014-114">Create a public IP address</span></span>
<span data-ttu-id="77014-115">To access your app on the Internet, you need a public IP address for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-115">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="77014-116">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="77014-116">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="77014-117">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLB* resource group:</span><span class="sxs-lookup"><span data-stu-id="77014-117">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLB* resource group:</span></span>

```azurepowershell-interactive
$publicIP = New-AzureRmPublicIpAddress `
-Name "myPublicIP" `
-ResourceGroupName "myResourceGroupLB" `
-Location "EastUS" `
-Sku "Standard" `
-AllocationMethod "Static"
  
```
## <a name="create-standard-load-balancer"></a><span data-ttu-id="77014-118">Create Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="77014-118">Create Standard Load Balancer</span></span>
 <span data-ttu-id="77014-119">In this section, you configure the frontend IP and the backend address pool for the load balancer and then create the Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-119">In this section, you configure the frontend IP and the backend address pool for the load balancer and then create the Basic Load Balancer.</span></span>
 
### <a name="create-frontend-ip"></a><span data-ttu-id="77014-120">Create frontend IP</span><span class="sxs-lookup"><span data-stu-id="77014-120">Create frontend IP</span></span>
<span data-ttu-id="77014-121">Create a frontend IP with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-121">Create a frontend IP with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="77014-122">The following example creates a frontend IP configuration named *myFrontEnd* and attaches the *myPublicIP* address:</span><span class="sxs-lookup"><span data-stu-id="77014-122">The following example creates a frontend IP configuration named *myFrontEnd* and attaches the *myPublicIP* address:</span></span> 

```azurepowershell-interactive
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name "myFrontEnd" `
  -PublicIpAddress $publicIP
```

### <a name="configure-backend-address-pool"></a><span data-ttu-id="77014-123">Configure backend address pool</span><span class="sxs-lookup"><span data-stu-id="77014-123">Configure backend address pool</span></span>

<span data-ttu-id="77014-124">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-124">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="77014-125">The VMs attach to this backend pool in the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="77014-125">The VMs attach to this backend pool in the remaining steps.</span></span> <span data-ttu-id="77014-126">The following example creates a backend address pool named *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="77014-126">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```azurepowershell-interactive
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "myBackEndPool"
```
### <a name="create-a-health-probe"></a><span data-ttu-id="77014-127">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="77014-127">Create a health probe</span></span>
<span data-ttu-id="77014-128">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="77014-128">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="77014-129">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="77014-129">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="77014-130">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span><span class="sxs-lookup"><span data-stu-id="77014-130">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="77014-131">You create a health probe based on a protocol or a specific health check page for your app.</span><span class="sxs-lookup"><span data-stu-id="77014-131">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="77014-132">The following example creates a TCP probe.</span><span class="sxs-lookup"><span data-stu-id="77014-132">The following example creates a TCP probe.</span></span> <span data-ttu-id="77014-133">You can also create custom HTTP probes for more fine grained health checks.</span><span class="sxs-lookup"><span data-stu-id="77014-133">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="77014-134">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="77014-134">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="77014-135">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span><span class="sxs-lookup"><span data-stu-id="77014-135">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="77014-136">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-136">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="77014-137">The following example creates a health probe named *myHealthProbe* that monitors each VM on *HTTP* port *80*:</span><span class="sxs-lookup"><span data-stu-id="77014-137">The following example creates a health probe named *myHealthProbe* that monitors each VM on *HTTP* port *80*:</span></span>

```azurepowershell-interactive
$probe = New-AzureRmLoadBalancerProbeConfig `
  -Name "myHealthProbe" `
  -RequestPath healthcheck2.aspx `
  -Protocol http `
  -Port 80 `
  -IntervalInSeconds 16 `
  -ProbeCount 2
  ```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="77014-138">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="77014-138">Create a load balancer rule</span></span>
<span data-ttu-id="77014-139">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="77014-139">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="77014-140">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="77014-140">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="77014-141">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span><span class="sxs-lookup"><span data-stu-id="77014-141">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="77014-142">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-142">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="77014-143">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on *TCP* port *80*:</span><span class="sxs-lookup"><span data-stu-id="77014-143">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on *TCP* port *80*:</span></span>

```azurepowershell-interactive
$lbrule = New-AzureRmLoadBalancerRuleConfig `
  -Name "myLoadBalancerRule" `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

### <a name="create-the-nat-rules"></a><span data-ttu-id="77014-144">Create the NAT rules</span><span class="sxs-lookup"><span data-stu-id="77014-144">Create the NAT rules</span></span>

<span data-ttu-id="77014-145">Create NAT rules with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-145">Create NAT rules with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig).</span></span> <span data-ttu-id="77014-146">The following example creates NAT rules named *myLoadBalancerRDP1* and *myLoadBalancerRDP2* to allow RDP connections to the backend servers with port 4221 and 4222:</span><span class="sxs-lookup"><span data-stu-id="77014-146">The following example creates NAT rules named *myLoadBalancerRDP1* and *myLoadBalancerRDP2* to allow RDP connections to the backend servers with port 4221 and 4222:</span></span>

```azurepowershell-interactive
$natrule1 = New-AzureRmLoadBalancerInboundNatRuleConfig `
-Name 'myLoadBalancerRDP1' `
-FrontendIpConfiguration $frontendIP `
-Protocol tcp `
-FrontendPort 4221 `
-BackendPort 3389

$natrule2 = New-AzureRmLoadBalancerInboundNatRuleConfig `
-Name 'myLoadBalancerRDP2' `
-FrontendIpConfiguration $frontendIP `
-Protocol tcp `
-FrontendPort 4222 `
-BackendPort 3389
```

### <a name="create-load-balancer"></a><span data-ttu-id="77014-147">Create load balancer</span><span class="sxs-lookup"><span data-stu-id="77014-147">Create load balancer</span></span>

<span data-ttu-id="77014-148">Create the Standard Load Balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="77014-148">Create the Standard Load Balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="77014-149">The following example creates a public Basic Load Balancer named myLoadBalancer using the frontend IP configuration, backend pool, health probe, load balancing rule, and NAT rules that you created in the preceding steps:</span><span class="sxs-lookup"><span data-stu-id="77014-149">The following example creates a public Basic Load Balancer named myLoadBalancer using the frontend IP configuration, backend pool, health probe, load balancing rule, and NAT rules that you created in the preceding steps:</span></span>

```azurepowershell-interactive
$lb = New-AzureRmLoadBalancer `
-ResourceGroupName 'myResourceGroupLB' `
-Name 'MyLoadBalancer' `
-Location 'eastus' `
-FrontendIpConfiguration $frontendIP `
-BackendAddressPool $backendPool `
-Probe $probe `
-LoadBalancingRule $lbrule `
-InboundNatRule $natrule1,$natrule2 `
-sku Standard
```

## <a name="create-network-resources"></a><span data-ttu-id="77014-150">Create network resources</span><span class="sxs-lookup"><span data-stu-id="77014-150">Create network resources</span></span>
<span data-ttu-id="77014-151">Before you deploy some VMs and can test your balancer, you must create supporting network resources - virtual network and virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="77014-151">Before you deploy some VMs and can test your balancer, you must create supporting network resources - virtual network and virtual NICs.</span></span> 

### <a name="create-a-virtual-network"></a><span data-ttu-id="77014-152">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="77014-152">Create a virtual network</span></span>
<span data-ttu-id="77014-153">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="77014-153">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="77014-154">The following example creates a virtual network named *myVnet* with *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="77014-154">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```azurepowershell-interactive
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.2.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupLB" `
  -Location "EastUS" `
  -Name "myVnet" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnetConfig
```
### <a name="create-network-security-group"></a><span data-ttu-id="77014-155">Create network security group</span><span class="sxs-lookup"><span data-stu-id="77014-155">Create network security group</span></span>
<span data-ttu-id="77014-156">Create network security group to define inbound connections to your virtual network.</span><span class="sxs-lookup"><span data-stu-id="77014-156">Create network security group to define inbound connections to your virtual network.</span></span>

#### <a name="create-a-network-security-group-rule-for-port-3389"></a><span data-ttu-id="77014-157">Create a network security group rule for port 3389</span><span class="sxs-lookup"><span data-stu-id="77014-157">Create a network security group rule for port 3389</span></span>
<span data-ttu-id="77014-158">Create a network security group rule to allow RDP connections through port 3389 with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-158">Create a network security group rule to allow RDP connections through port 3389 with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span>

```azurepowershell-interactive

$rule1 = New-AzureRmNetworkSecurityRuleConfig `
-Name 'myNetworkSecurityGroupRuleRDP' `
-Description 'Allow RDP' `
-Access Allow `
-Protocol Tcp `
-Direction Inbound `
-Priority 1000 `
-SourceAddressPrefix Internet `
-SourcePortRange * `
-DestinationAddressPrefix * `
-DestinationPortRange 3389
```

#### <a name="create-a-network-security-group-rule-for-port-80"></a><span data-ttu-id="77014-159">Create a network security group rule for port 80</span><span class="sxs-lookup"><span data-stu-id="77014-159">Create a network security group rule for port 80</span></span>
<span data-ttu-id="77014-160">Create a network security group rule to allow inbound connections through port 80 with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="77014-160">Create a network security group rule to allow inbound connections through port 80 with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span>

```azurepowershell-interactive
$rule2 = New-AzureRmNetworkSecurityRuleConfig `
-Name 'myNetworkSecurityGroupRuleHTTP' `
-Description 'Allow HTTP' `
-Access Allow `
-Protocol Tcp `
-Direction Inbound `
-Priority 2000 `
-SourceAddressPrefix Internet `
-SourcePortRange * `
-DestinationAddressPrefix * `
-DestinationPortRange 80
```
#### <a name="create-a-network-security-group"></a><span data-ttu-id="77014-161">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="77014-161">Create a network security group</span></span>

<span data-ttu-id="77014-162">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="77014-162">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span>

```azurepowershell-interactive
$nsg = New-AzureRmNetworkSecurityGroup`
-ResourceGroupName 'myResourceGroupLB' `
-Location 'EastUS' `
-Name 'myNetworkSecurityGroup'`
-SecurityRules $rule1,$rule2
```

###<a name="create-nics"></a><span data-ttu-id="77014-163">Create NICs</span><span class="sxs-lookup"><span data-stu-id="77014-163">Create NICs</span></span>
<span data-ttu-id="77014-164">Create virtual NICs created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="77014-164">Create virtual NICs created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="77014-165">The following example creates two virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="77014-165">The following example creates two virtual NICs.</span></span> <span data-ttu-id="77014-166">(One virtual NIC for each VM you create for your app in the following steps).</span><span class="sxs-lookup"><span data-stu-id="77014-166">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="77014-167">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span><span class="sxs-lookup"><span data-stu-id="77014-167">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```azurepowershell-interactive
# Create NIC for VM1
$nicVM1 = New-AzureRmNetworkInterface `
-ResourceGroupName 'myResourceGroupLB' `
-Location 'EastUS' `
-Name 'MyNic1' `
-LoadBalancerBackendAddressPool $backendPool `
-NetworkSecurityGroup $nsg `
-LoadBalancerInboundNatRule $natrule1 `
-Subnet $vnet.Subnets[0]

# Create NIC for VM2
$nicVM2 = New-AzureRmNetworkInterface `
-ResourceGroupName 'myResourceGroupLB' `
-Location 'EastUS' `
-Name 'MyNic2' `
-LoadBalancerBackendAddressPool $backendPool `
-NetworkSecurityGroup $nsg `
-LoadBalancerInboundNatRule $natrule2 `
-Subnet $vnet.Subnets[0]

```

### <a name="create-virtual-machines"></a><span data-ttu-id="77014-168">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="77014-168">Create virtual machines</span></span>
<span data-ttu-id="77014-169">To improve the high availability of your app, place your VMs in an availability set.</span><span class="sxs-lookup"><span data-stu-id="77014-169">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="77014-170">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="77014-170">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="77014-171">The following example creates an availability set named *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="77014-171">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurepowershell-interactive
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName "myResourceGroupLB" `
  -Name "myAvailabilitySet" `
  -Location "EastUS" `
  -Sku aligned `
  -PlatformFaultDomainCount 2 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="77014-172">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="77014-172">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```azurepowershell-interactive
$cred = Get-Credential
```

<span data-ttu-id="77014-173">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="77014-173">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="77014-174">The following example creates two VMs and the required virtual network components if they do not already exist:</span><span class="sxs-lookup"><span data-stu-id="77014-174">The following example creates two VMs and the required virtual network components if they do not already exist:</span></span>

```azurepowershell-interactive
for ($i=1; $i -le 2; $i++)
{
    New-AzureRmVm `
        -ResourceGroupName "myResourceGroupLB" `
        -Name "myVM$i" `
        -Location "East US" `
        -VirtualNetworkName "myVnet" `
        -SubnetName "mySubnet" `
        -SecurityGroupName "myNetworkSecurityGroup" `
        -OpenPorts 80 `
        -AvailabilitySetName "myAvailabilitySet" `
        -Credential $cred `
        -AsJob
}
```

<span data-ttu-id="77014-175">The `-AsJob` parameter creates the VM as a background task, so the PowerShell prompts return to you.</span><span class="sxs-lookup"><span data-stu-id="77014-175">The `-AsJob` parameter creates the VM as a background task, so the PowerShell prompts return to you.</span></span> <span data-ttu-id="77014-176">You can view details of background jobs with the `Job` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77014-176">You can view details of background jobs with the `Job` cmdlet.</span></span> <span data-ttu-id="77014-177">It takes a few minutes to create and configure the two VMs.</span><span class="sxs-lookup"><span data-stu-id="77014-177">It takes a few minutes to create and configure the two VMs.</span></span>

### <a name="install-iis-with-custom-web-page"></a><span data-ttu-id="77014-178">Install IIS with Custom web page</span><span class="sxs-lookup"><span data-stu-id="77014-178">Install IIS with Custom web page</span></span>
 
<span data-ttu-id="77014-179">Install IIS with a custom web page on both backend VMs as follows:</span><span class="sxs-lookup"><span data-stu-id="77014-179">Install IIS with a custom web page on both backend VMs as follows:</span></span>

1. <span data-ttu-id="77014-180">Get the Public IP address of the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-180">Get the Public IP address of the Load Balancer.</span></span> <span data-ttu-id="77014-181">Using `Get-AzureRmPublicIPAdress`, obtain the Public IP address of the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-181">Using `Get-AzureRmPublicIPAdress`, obtain the Public IP address of the Load Balancer.</span></span>

  ```azurepowershell-interactive
    Get-AzureRmPublicIPAddress `
    -ResourceGroupName "myResourceGroupLB" `
    -Name "myPublicIP" | select IpAddress
  ```
2. <span data-ttu-id="77014-182">Create a remote desktop connection to VM1 using the Public Ip address that you obtained from the previous step.</span><span class="sxs-lookup"><span data-stu-id="77014-182">Create a remote desktop connection to VM1 using the Public Ip address that you obtained from the previous step.</span></span> 

  ```azurepowershell-interactive

      mstsc /v:PublicIpAddress:4221  
  
  ```
3. <span data-ttu-id="77014-183">Enter the credentials for *VM1* to start the RDP session.</span><span class="sxs-lookup"><span data-stu-id="77014-183">Enter the credentials for *VM1* to start the RDP session.</span></span>
4. <span data-ttu-id="77014-184">Launch Windows PowerShell on VM1 and using the following commands to install IIS server and update the default htm file.</span><span class="sxs-lookup"><span data-stu-id="77014-184">Launch Windows PowerShell on VM1 and using the following commands to install IIS server and update the default htm file.</span></span>
    ```azurepowershell-interactive
    # Install IIS
      Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # Remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    #Add custom htm file
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from host" + $env:computername)
    ```
5. <span data-ttu-id="77014-185">Close the RDP connection with *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="77014-185">Close the RDP connection with *myVM1*.</span></span>
6. <span data-ttu-id="77014-186">Create a RDP connection with *myVM2* by running `mstsc /v:PublicIpAddress:4222` command, and repeat step 4 for *VM2*.</span><span class="sxs-lookup"><span data-stu-id="77014-186">Create a RDP connection with *myVM2* by running `mstsc /v:PublicIpAddress:4222` command, and repeat step 4 for *VM2*.</span></span>

## <a name="test-load-balancer"></a><span data-ttu-id="77014-187">Test load balancer</span><span class="sxs-lookup"><span data-stu-id="77014-187">Test load balancer</span></span>
<span data-ttu-id="77014-188">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="77014-188">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="77014-189">The following example obtains the IP address for *myPublicIP* created earlier:</span><span class="sxs-lookup"><span data-stu-id="77014-189">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress `
  -ResourceGroupName "myResourceGroupLB" `
  -Name "myPublicIP" | select IpAddress
```

<span data-ttu-id="77014-190">You can then enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="77014-190">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="77014-191">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span><span class="sxs-lookup"><span data-stu-id="77014-191">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Test load balancer](media/quickstart-create-basic-load-balancer-powershell/load-balancer-test.png)

<span data-ttu-id="77014-193">To see the load balancer distribute traffic across all two VMs running your app, you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="77014-193">To see the load balancer distribute traffic across all two VMs running your app, you can force-refresh your web browser.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="77014-194">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="77014-194">Clean up resources</span></span>

<span data-ttu-id="77014-195">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="77014-195">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupLB
```

## <a name="next-steps"></a><span data-ttu-id="77014-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="77014-196">Next steps</span></span>

<span data-ttu-id="77014-197">In this quickstart, you created a Basic Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-197">In this quickstart, you created a Basic Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="77014-198">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="77014-198">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="77014-199">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="77014-199">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-basic-internal-portal.md)
