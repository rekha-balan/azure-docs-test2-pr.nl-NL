---
title: Tutorial - Build a highly available application on Azure VMs | Microsoft Docs
description: Learn how to create a highly available and secure application across three Windows VMs with a load balancer in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f55fd8514f32d7557eddbea85c86df22433e3633
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553789"
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="0403e-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="0403e-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="0403e-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span><span class="sxs-lookup"><span data-stu-id="0403e-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="0403e-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="0403e-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="0403e-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span><span class="sxs-lookup"><span data-stu-id="0403e-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="0403e-107">Step 1 - Azure prerequisites</span><span class="sxs-lookup"><span data-stu-id="0403e-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="0403e-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) module.</span><span class="sxs-lookup"><span data-stu-id="0403e-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) module.</span></span>

<span data-ttu-id="0403e-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="0403e-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0403e-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="0403e-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0403e-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v2.0.3/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0403e-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v2.0.3/new-azurermresourcegroup).</span></span> <span data-ttu-id="0403e-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span><span class="sxs-lookup"><span data-stu-id="0403e-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="0403e-113">Step 2 - Create availability set</span><span class="sxs-lookup"><span data-stu-id="0403e-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="0403e-114">Virtual machines can be created across logical fault and update domains.</span><span class="sxs-lookup"><span data-stu-id="0403e-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="0403e-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="0403e-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="0403e-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span><span class="sxs-lookup"><span data-stu-id="0403e-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="0403e-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span><span class="sxs-lookup"><span data-stu-id="0403e-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="0403e-118">Availability sets let you define these logical fault and update domains.</span><span class="sxs-lookup"><span data-stu-id="0403e-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="0403e-119">Create an availability set with [New-AzureRmAvailabilitySet](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="0403e-119">Create an availability set with [New-AzureRmAvailabilitySet](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermavailabilityset).</span></span> <span data-ttu-id="0403e-120">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="0403e-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="0403e-121">Step 3 - Create load balancer</span><span class="sxs-lookup"><span data-stu-id="0403e-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="0403e-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span><span class="sxs-lookup"><span data-stu-id="0403e-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="0403e-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span><span class="sxs-lookup"><span data-stu-id="0403e-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="0403e-124">Create public IP address</span><span class="sxs-lookup"><span data-stu-id="0403e-124">Create public IP address</span></span>

<span data-ttu-id="0403e-125">To access your app on the Internet, assign a public IP address to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="0403e-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="0403e-126">Create a public IP address with [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="0403e-126">Create a public IP address with [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermpublicipaddress).</span></span> <span data-ttu-id="0403e-127">The following example creates a public IP address named `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="0403e-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="0403e-128">Create load balancer</span><span class="sxs-lookup"><span data-stu-id="0403e-128">Create load balancer</span></span>

<span data-ttu-id="0403e-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="0403e-130">The following example creates a frontend IP address named `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="0403e-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="0403e-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="0403e-132">The following example creates a backend address pool named `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="0403e-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="0403e-133">Now, create the load balancer with [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="0403e-133">Now, create the load balancer with [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermloadbalancer).</span></span> <span data-ttu-id="0403e-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span><span class="sxs-lookup"><span data-stu-id="0403e-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="0403e-135">Create health probe</span><span class="sxs-lookup"><span data-stu-id="0403e-135">Create health probe</span></span>

<span data-ttu-id="0403e-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="0403e-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="0403e-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="0403e-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="0403e-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span><span class="sxs-lookup"><span data-stu-id="0403e-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="0403e-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="0403e-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span><span class="sxs-lookup"><span data-stu-id="0403e-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="0403e-141">Create load balancer rule</span><span class="sxs-lookup"><span data-stu-id="0403e-141">Create load balancer rule</span></span>

<span data-ttu-id="0403e-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="0403e-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="0403e-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v3.6.0/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v3.6.0/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="0403e-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span><span class="sxs-lookup"><span data-stu-id="0403e-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="0403e-145">Update the load balancer with [Set-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="0403e-145">Update the load balancer with [Set-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="0403e-146">Step 4 - Configure networking</span><span class="sxs-lookup"><span data-stu-id="0403e-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="0403e-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="0403e-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="0403e-148">This virtual network is secured to filter traffic based on defined access rules.</span><span class="sxs-lookup"><span data-stu-id="0403e-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="0403e-149">Create virtual network</span><span class="sxs-lookup"><span data-stu-id="0403e-149">Create virtual network</span></span>

<span data-ttu-id="0403e-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="0403e-151">The following example creates a subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="0403e-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="0403e-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="0403e-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="0403e-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="0403e-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="0403e-154">Configure network security</span><span class="sxs-lookup"><span data-stu-id="0403e-154">Configure network security</span></span>

<span data-ttu-id="0403e-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span><span class="sxs-lookup"><span data-stu-id="0403e-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="0403e-156">Network security group rules allow or deny network traffic on a specific port or port range.</span><span class="sxs-lookup"><span data-stu-id="0403e-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="0403e-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0403e-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="0403e-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="0403e-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="0403e-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="0403e-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="0403e-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="0403e-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="0403e-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="0403e-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="0403e-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="0403e-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="0403e-163">Update the virtual network with [Set-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="0403e-163">Update the virtual network with [Set-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="0403e-164">Create virtual network interface cards</span><span class="sxs-lookup"><span data-stu-id="0403e-164">Create virtual network interface cards</span></span>

<span data-ttu-id="0403e-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span><span class="sxs-lookup"><span data-stu-id="0403e-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="0403e-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="0403e-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="0403e-167">Create a virtual NIC with [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="0403e-167">Create a virtual NIC with [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworkinterface).</span></span> <span data-ttu-id="0403e-168">The following example creates three virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="0403e-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="0403e-169">(One virtual NIC for each VM you create for your app in the following steps):</span><span class="sxs-lookup"><span data-stu-id="0403e-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="0403e-170">Step 5 - Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="0403e-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="0403e-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span><span class="sxs-lookup"><span data-stu-id="0403e-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="0403e-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="0403e-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="0403e-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="0403e-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm).</span></span> <span data-ttu-id="0403e-174">The following example creates three VMs:</span><span class="sxs-lookup"><span data-stu-id="0403e-174">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="0403e-175">It takes several minutes to create and configure all three VMs.</span><span class="sxs-lookup"><span data-stu-id="0403e-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="0403e-176">The load balancer health probe automatically detects when the app is running on each VM.</span><span class="sxs-lookup"><span data-stu-id="0403e-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="0403e-177">Once the app is running, the load balancer rule starts to distribute traffic.</span><span class="sxs-lookup"><span data-stu-id="0403e-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="0403e-178">Install the app</span><span class="sxs-lookup"><span data-stu-id="0403e-178">Install the app</span></span> 

<span data-ttu-id="0403e-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span><span class="sxs-lookup"><span data-stu-id="0403e-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="0403e-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0403e-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="0403e-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span><span class="sxs-lookup"><span data-stu-id="0403e-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="0403e-182">When using the custom script extension, the Azure VM agent manages the script execution.</span><span class="sxs-lookup"><span data-stu-id="0403e-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="0403e-183">Use [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmextension) to install the custom script extension.</span><span class="sxs-lookup"><span data-stu-id="0403e-183">Use [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="0403e-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span><span class="sxs-lookup"><span data-stu-id="0403e-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="0403e-185">Test your app</span><span class="sxs-lookup"><span data-stu-id="0403e-185">Test your app</span></span>

<span data-ttu-id="0403e-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="0403e-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermpublicipaddress).</span></span> <span data-ttu-id="0403e-187">The following example obtains the IP address for `myPublicIP` created earlier:</span><span class="sxs-lookup"><span data-stu-id="0403e-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="0403e-188">Enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="0403e-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="0403e-189">With the NSG rule in place, the default IIS website is displayed.</span><span class="sxs-lookup"><span data-stu-id="0403e-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![IIS default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="0403e-191">Step 6 – Management tasks</span><span class="sxs-lookup"><span data-stu-id="0403e-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="0403e-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span><span class="sxs-lookup"><span data-stu-id="0403e-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="0403e-193">To deal with increased traffic to your app, you may need to add additional VMs.</span><span class="sxs-lookup"><span data-stu-id="0403e-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="0403e-194">This section shows you how to remove or add a VM from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="0403e-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="0403e-195">Remove a VM from the load balancer</span><span class="sxs-lookup"><span data-stu-id="0403e-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="0403e-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span><span class="sxs-lookup"><span data-stu-id="0403e-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="0403e-197">Get the network interface card with [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="0403e-197">Get the network interface card with [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="0403e-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span><span class="sxs-lookup"><span data-stu-id="0403e-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="0403e-199">Update the network interface card:</span><span class="sxs-lookup"><span data-stu-id="0403e-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="0403e-200">Add a VM to the load balancer</span><span class="sxs-lookup"><span data-stu-id="0403e-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="0403e-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="0403e-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="0403e-202">Get the load balancer:</span><span class="sxs-lookup"><span data-stu-id="0403e-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="0403e-203">Add the backend address pool of the load balancer to the network interface card:</span><span class="sxs-lookup"><span data-stu-id="0403e-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="0403e-204">Update the network interface card:</span><span class="sxs-lookup"><span data-stu-id="0403e-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="0403e-205">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0403e-205">Next Steps</span></span>

<span data-ttu-id="0403e-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0403e-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
