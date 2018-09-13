---
title: Diagnose a virtual machine network traffic filter problem - quickstart - Azure PowerShell | Microsoft Docs
description: In this quickstart, you learn how to diagnose a virtual machine network traffic filter problem using the IP flow verify  capability of Azure Network Watcher.
services: network-watcher
documentationcenter: network-watcher
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I need to diagnose a virtual machine (VM) network traffic filter problem that prevents communication to and from a VM.
ms.assetid: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: network-watcher
ms.workload: infrastructure
ms.date: 04/20/2018
ms.author: jdial
ms.custom: mvc
ms.openlocfilehash: d98a804961defc80bebe3e3a838dd229c23044bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865854"
---
# <a name="quickstart-diagnose-a-virtual-machine-network-traffic-filter-problem---azure-powershell"></a><span data-ttu-id="03e26-103">Quickstart: Diagnose a virtual machine network traffic filter problem - Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="03e26-103">Quickstart: Diagnose a virtual machine network traffic filter problem - Azure PowerShell</span></span>

<span data-ttu-id="03e26-104">In this quickstart, you deploy a virtual machine (VM), and then check communications to an IP address and URL and from an IP address.</span><span class="sxs-lookup"><span data-stu-id="03e26-104">In this quickstart, you deploy a virtual machine (VM), and then check communications to an IP address and URL and from an IP address.</span></span> <span data-ttu-id="03e26-105">You determine the cause of a communication failure and how you can resolve it.</span><span class="sxs-lookup"><span data-stu-id="03e26-105">You determine the cause of a communication failure and how you can resolve it.</span></span>

<span data-ttu-id="03e26-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="03e26-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="03e26-107">If you choose to install and use PowerShell locally, this quickstart requires the AzureRM PowerShell module version 5.4.1 or later.</span><span class="sxs-lookup"><span data-stu-id="03e26-107">If you choose to install and use PowerShell locally, this quickstart requires the AzureRM PowerShell module version 5.4.1 or later.</span></span> <span data-ttu-id="03e26-108">To find the installed version, run ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="03e26-108">To find the installed version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="03e26-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="03e26-109">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="03e26-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="03e26-110">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="03e26-111">Create a VM</span><span class="sxs-lookup"><span data-stu-id="03e26-111">Create a VM</span></span>

<span data-ttu-id="03e26-112">Before you can create a VM, you must create a resource group to contain the VM.</span><span class="sxs-lookup"><span data-stu-id="03e26-112">Before you can create a VM, you must create a resource group to contain the VM.</span></span> <span data-ttu-id="03e26-113">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/AzureRM.Resources/New-AzureRmResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="03e26-113">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/AzureRM.Resources/New-AzureRmResourceGroup).</span></span> <span data-ttu-id="03e26-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="03e26-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

<span data-ttu-id="03e26-115">Create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="03e26-115">Create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="03e26-116">When running this step, you are prompted for credentials.</span><span class="sxs-lookup"><span data-stu-id="03e26-116">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="03e26-117">The values that you enter are configured as the user name and password for the VM.</span><span class="sxs-lookup"><span data-stu-id="03e26-117">The values that you enter are configured as the user name and password for the VM.</span></span>

```azurepowershell-interactive
$vM = New-AzureRmVm `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVm" `
    -Location "East US"
```

<span data-ttu-id="03e26-118">The VM takes a few minutes to create.</span><span class="sxs-lookup"><span data-stu-id="03e26-118">The VM takes a few minutes to create.</span></span> <span data-ttu-id="03e26-119">Don't continue with remaining steps until the VM is created and PowerShell returns output.</span><span class="sxs-lookup"><span data-stu-id="03e26-119">Don't continue with remaining steps until the VM is created and PowerShell returns output.</span></span>

## <a name="test-network-communication"></a><span data-ttu-id="03e26-120">Test network communication</span><span class="sxs-lookup"><span data-stu-id="03e26-120">Test network communication</span></span>

<span data-ttu-id="03e26-121">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's IP flow verify capability to test communication.</span><span class="sxs-lookup"><span data-stu-id="03e26-121">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's IP flow verify capability to test communication.</span></span>

### <a name="enable-network-watcher"></a><span data-ttu-id="03e26-122">Enable network watcher</span><span class="sxs-lookup"><span data-stu-id="03e26-122">Enable network watcher</span></span>

<span data-ttu-id="03e26-123">If you already have a network watcher enabled in the East US region, use [Get-AzureRmNetworkWatcher](/powershell/module/azurerm.network/get-azurermnetworkwatcher) to retrieve the network watcher.</span><span class="sxs-lookup"><span data-stu-id="03e26-123">If you already have a network watcher enabled in the East US region, use [Get-AzureRmNetworkWatcher](/powershell/module/azurerm.network/get-azurermnetworkwatcher) to retrieve the network watcher.</span></span> <span data-ttu-id="03e26-124">The following example retrieves an existing network watcher named *NetworkWatcher_eastus* that is in the *NetworkWatcherRG* resource group:</span><span class="sxs-lookup"><span data-stu-id="03e26-124">The following example retrieves an existing network watcher named *NetworkWatcher_eastus* that is in the *NetworkWatcherRG* resource group:</span></span>

```azurepowershell-interactive
$networkWatcher = Get-AzureRmNetworkWatcher `
  -Name NetworkWatcher_eastus `
  -ResourceGroupName NetworkWatcherRG
```

<span data-ttu-id="03e26-125">If you don't already have a network watcher enabled in the East US region, use [New-AzureRmNetworkWatcher](/powershell/module/azurerm.network/new-azurermnetworkwatcher) to create a network watcher in the East US region:</span><span class="sxs-lookup"><span data-stu-id="03e26-125">If you don't already have a network watcher enabled in the East US region, use [New-AzureRmNetworkWatcher](/powershell/module/azurerm.network/new-azurermnetworkwatcher) to create a network watcher in the East US region:</span></span>

```azurepowershell-interactive
$networkWatcher = New-AzureRmNetworkWatcher `
  -Name "NetworkWatcher_eastus" `
  -ResourceGroupName "NetworkWatcherRG" `
  -Location "East US"
```

### <a name="use-ip-flow-verify"></a><span data-ttu-id="03e26-126">Use IP flow verify</span><span class="sxs-lookup"><span data-stu-id="03e26-126">Use IP flow verify</span></span>

<span data-ttu-id="03e26-127">When you create a VM, Azure allows and denies network traffic to and from the VM, by default.</span><span class="sxs-lookup"><span data-stu-id="03e26-127">When you create a VM, Azure allows and denies network traffic to and from the VM, by default.</span></span> <span data-ttu-id="03e26-128">You might later override Azure's defaults, allowing or denying additional types of traffic.</span><span class="sxs-lookup"><span data-stu-id="03e26-128">You might later override Azure's defaults, allowing or denying additional types of traffic.</span></span> <span data-ttu-id="03e26-129">To test whether traffic is allowed or denied to different destinations and from a source IP address, use the [Test-AzureRmNetworkWatcherIPFlow](/powershell/module/azurerm.network/test-azurermnetworkwatcheripflow) command.</span><span class="sxs-lookup"><span data-stu-id="03e26-129">To test whether traffic is allowed or denied to different destinations and from a source IP address, use the [Test-AzureRmNetworkWatcherIPFlow](/powershell/module/azurerm.network/test-azurermnetworkwatcheripflow) command.</span></span>

<span data-ttu-id="03e26-130">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span><span class="sxs-lookup"><span data-stu-id="03e26-130">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span></span>

```azurepowershell-interactive
Test-AzureRmNetworkWatcherIPFlow `
  -NetworkWatcher $networkWatcher `
  -TargetVirtualMachineId $vM.Id `
  -Direction Outbound `
  -Protocol TCP `
  -LocalIPAddress 192.168.1.4 `
  -LocalPort 60000 `
  -RemoteIPAddress 13.107.21.200 `
  -RemotePort 80
```

<span data-ttu-id="03e26-131">After several seconds, the result returned informs you that access is allowed by a security rule named **AllowInternetOutbound**.</span><span class="sxs-lookup"><span data-stu-id="03e26-131">After several seconds, the result returned informs you that access is allowed by a security rule named **AllowInternetOutbound**.</span></span>

<span data-ttu-id="03e26-132">Test outbound communication from the VM to 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="03e26-132">Test outbound communication from the VM to 172.31.0.100:</span></span>

```azurepowershell-interactive
Test-AzureRmNetworkWatcherIPFlow `
  -NetworkWatcher $networkWatcher `
  -TargetVirtualMachineId $vM.Id `
  -Direction Outbound `
  -Protocol TCP `
  -LocalIPAddress 192.168.1.4 `
  -LocalPort 60000 `
  -RemoteIPAddress 172.31.0.100 `
  -RemotePort 80
```

<span data-ttu-id="03e26-133">The result returned informs you that access is denied by a security rule named **DefaultOutboundDenyAll**.</span><span class="sxs-lookup"><span data-stu-id="03e26-133">The result returned informs you that access is denied by a security rule named **DefaultOutboundDenyAll**.</span></span>

<span data-ttu-id="03e26-134">Test inbound communication to the VM from 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="03e26-134">Test inbound communication to the VM from 172.31.0.100:</span></span>

```azurepowershell-interactive
Test-AzureRmNetworkWatcherIPFlow `
  -NetworkWatcher $networkWatcher `
  -TargetVirtualMachineId $vM.Id `
  -Direction Inbound `
  -Protocol TCP `
  -LocalIPAddress 192.168.1.4 `
  -LocalPort 80 `
  -RemoteIPAddress 172.31.0.100 `
  -RemotePort 60000
```

<span data-ttu-id="03e26-135">The result returned informs you that access is denied because of a security rule named **DefaultInboundDenyAll**.</span><span class="sxs-lookup"><span data-stu-id="03e26-135">The result returned informs you that access is denied because of a security rule named **DefaultInboundDenyAll**.</span></span> <span data-ttu-id="03e26-136">Now that you know which security rules are allowing or denying traffic to or from a VM, you can determine how to resolve the problems.</span><span class="sxs-lookup"><span data-stu-id="03e26-136">Now that you know which security rules are allowing or denying traffic to or from a VM, you can determine how to resolve the problems.</span></span>

## <a name="view-details-of-a-security-rule"></a><span data-ttu-id="03e26-137">View details of a security rule</span><span class="sxs-lookup"><span data-stu-id="03e26-137">View details of a security rule</span></span>

<span data-ttu-id="03e26-138">To determine why the rules in [Test network communication](#test-network-communication) are allowing or preventing communication, review the effective security rules for the network interface with [Get-AzureRmEffectiveNetworkSecurityGroup](/powershell/module/azurerm.network/get-azurermeffectivenetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="03e26-138">To determine why the rules in [Test network communication](#test-network-communication) are allowing or preventing communication, review the effective security rules for the network interface with [Get-AzureRmEffectiveNetworkSecurityGroup](/powershell/module/azurerm.network/get-azurermeffectivenetworksecuritygroup):</span></span>

```azurepowershell-interactive
Get-AzureRmEffectiveNetworkSecurityGroup `
  -NetworkInterfaceName myVm `
  -ResourceGroupName myResourceGroup
```

<span data-ttu-id="03e26-139">The returned output includes the following text for the **AllowInternetOutbound** rule that allowed outbound access to www.bing.com in [Use IP flow verify](#use-ip-flow-verify):</span><span class="sxs-lookup"><span data-stu-id="03e26-139">The returned output includes the following text for the **AllowInternetOutbound** rule that allowed outbound access to www.bing.com in [Use IP flow verify](#use-ip-flow-verify):</span></span>

```powershell
{
  "Name":
"defaultSecurityRules/AllowInternetOutBound",
  "Protocol": "All",
  "SourcePortRange": [
    "0-65535"
  ],
  "DestinationPortRange": [
    "0-65535"
  ],
  "SourceAddressPrefix": [
    "0.0.0.0/0"
  ],
  "DestinationAddressPrefix": [
    "Internet"
  ],
  "ExpandedSourceAddressPrefix": [],
  "ExpandedDestinationAddressPrefix": [
    "1.0.0.0/8",
    "2.0.0.0/7",
    "4.0.0.0/6",
    "8.0.0.0/7",
    "11.0.0.0/8",
    "12.0.0.0/6",
    ...
    ],
    "Access": "Allow",
    "Priority": 65001,
    "Direction": "Outbound"
  },
```

<span data-ttu-id="03e26-140">You can see in the output that **DestinationAddressPrefix** is **Internet**.</span><span class="sxs-lookup"><span data-stu-id="03e26-140">You can see in the output that **DestinationAddressPrefix** is **Internet**.</span></span> <span data-ttu-id="03e26-141">It's not clear how 13.107.21.200, the address you tested in [Use IP flow verify](#use-ip-flow-verify), relates to **Internet** though.</span><span class="sxs-lookup"><span data-stu-id="03e26-141">It's not clear how 13.107.21.200, the address you tested in [Use IP flow verify](#use-ip-flow-verify), relates to **Internet** though.</span></span> <span data-ttu-id="03e26-142">You see several address prefixes listed under **ExpandedDestinationAddressPrefix**.</span><span class="sxs-lookup"><span data-stu-id="03e26-142">You see several address prefixes listed under **ExpandedDestinationAddressPrefix**.</span></span> <span data-ttu-id="03e26-143">One of the prefixes in the list is **12.0.0.0/6**, which encompasses the 12.0.0.1-15.255.255.254 range of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="03e26-143">One of the prefixes in the list is **12.0.0.0/6**, which encompasses the 12.0.0.1-15.255.255.254 range of IP addresses.</span></span> <span data-ttu-id="03e26-144">Since 13.107.21.200 is within that address range, the **AllowInternetOutBound** rule allows the outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="03e26-144">Since 13.107.21.200 is within that address range, the **AllowInternetOutBound** rule allows the outbound traffic.</span></span> <span data-ttu-id="03e26-145">Additionally, there are no higher **priority** (lower number) rules listed in the output returned by `Get-AzureRmEffectiveNetworkSecurityGroup`, that override this rule.</span><span class="sxs-lookup"><span data-stu-id="03e26-145">Additionally, there are no higher **priority** (lower number) rules listed in the output returned by `Get-AzureRmEffectiveNetworkSecurityGroup`, that override this rule.</span></span> <span data-ttu-id="03e26-146">To deny outbound communication to 13.107.21.200, you could add a security rule with a higher priority, that denies port 80 outbound to the IP address.</span><span class="sxs-lookup"><span data-stu-id="03e26-146">To deny outbound communication to 13.107.21.200, you could add a security rule with a higher priority, that denies port 80 outbound to the IP address.</span></span>

<span data-ttu-id="03e26-147">When you ran the `Test-AzureRmNetworkWatcherIPFlow` command to test outbound communication to 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultOutboundDenyAll** rule denied the communication.</span><span class="sxs-lookup"><span data-stu-id="03e26-147">When you ran the `Test-AzureRmNetworkWatcherIPFlow` command to test outbound communication to 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultOutboundDenyAll** rule denied the communication.</span></span> <span data-ttu-id="03e26-148">The **DefaultOutboundDenyAll** rule equates to the **DenyAllOutBound** rule listed in the following output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command:</span><span class="sxs-lookup"><span data-stu-id="03e26-148">The **DefaultOutboundDenyAll** rule equates to the **DenyAllOutBound** rule listed in the following output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command:</span></span>

```powershell
{
"Name": "defaultSecurityRules/DenyAllOutBound",
"Protocol": "All",
"SourcePortRange": [
  "0-65535"
],
"DestinationPortRange": [
  "0-65535"
],
"SourceAddressPrefix": [
  "0.0.0.0/0"
],
"DestinationAddressPrefix": [
  "0.0.0.0/0"
],
"ExpandedSourceAddressPrefix": [],
"ExpandedDestinationAddressPrefix": [],
"Access": "Deny",
"Priority": 65500,
"Direction": "Outbound"
}
```

<span data-ttu-id="03e26-149">The rule lists **0.0.0.0/0** as the **DestinationAddressPrefix**.</span><span class="sxs-lookup"><span data-stu-id="03e26-149">The rule lists **0.0.0.0/0** as the **DestinationAddressPrefix**.</span></span> <span data-ttu-id="03e26-150">The rule denies the outbound communication to 172.131.0.100, because the address is not within the **DestinationAddressPrefix** of any of the other outbound rules in the output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command.</span><span class="sxs-lookup"><span data-stu-id="03e26-150">The rule denies the outbound communication to 172.131.0.100, because the address is not within the **DestinationAddressPrefix** of any of the other outbound rules in the output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command.</span></span> <span data-ttu-id="03e26-151">To allow the outbound communication, you could add a security rule with a higher priority, that allows outbound traffic to port 80 at 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="03e26-151">To allow the outbound communication, you could add a security rule with a higher priority, that allows outbound traffic to port 80 at 172.131.0.100.</span></span>

<span data-ttu-id="03e26-152">When you ran the `Test-AzureRmNetworkWatcherIPFlow` command to test inbound communication from 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultInboundDenyAll** rule denied the communication.</span><span class="sxs-lookup"><span data-stu-id="03e26-152">When you ran the `Test-AzureRmNetworkWatcherIPFlow` command to test inbound communication from 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultInboundDenyAll** rule denied the communication.</span></span> <span data-ttu-id="03e26-153">The **DefaultInboundDenyAll** rule equates to the **DenyAllInBound** rule listed in the following output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command:</span><span class="sxs-lookup"><span data-stu-id="03e26-153">The **DefaultInboundDenyAll** rule equates to the **DenyAllInBound** rule listed in the following output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command:</span></span>

```powershell
{
"Name": "defaultSecurityRules/DenyAllInBound",
"Protocol": "All",
"SourcePortRange": [
  "0-65535"
],
"DestinationPortRange": [
  "0-65535"
],
"SourceAddressPrefix": [
  "0.0.0.0/0"
],
"DestinationAddressPrefix": [
  "0.0.0.0/0"
],
"ExpandedSourceAddressPrefix": [],
"ExpandedDestinationAddressPrefix": [],
"Access": "Deny",
"Priority": 65500,
"Direction": "Inbound"
},
```

<span data-ttu-id="03e26-154">The **DenyAllInBound** rule is applied because, as shown in the output, no other higher priority rule exists in the output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command that allows port 80 inbound to the VM from 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="03e26-154">The **DenyAllInBound** rule is applied because, as shown in the output, no other higher priority rule exists in the output from the `Get-AzureRmEffectiveNetworkSecurityGroup` command that allows port 80 inbound to the VM from 172.131.0.100.</span></span> <span data-ttu-id="03e26-155">To allow the inbound communication, you could add a security rule with a higher priority that allows port 80 inbound from 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="03e26-155">To allow the inbound communication, you could add a security rule with a higher priority that allows port 80 inbound from 172.131.0.100.</span></span>

<span data-ttu-id="03e26-156">The checks in this quickstart tested Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="03e26-156">The checks in this quickstart tested Azure configuration.</span></span> <span data-ttu-id="03e26-157">If the checks return expected results and you still have network problems, ensure that you don't have a firewall between your VM and the endpoint you're communicating with and that the operating system in your VM doesn't have a firewall that is allowing or denying communication.</span><span class="sxs-lookup"><span data-stu-id="03e26-157">If the checks return expected results and you still have network problems, ensure that you don't have a firewall between your VM and the endpoint you're communicating with and that the operating system in your VM doesn't have a firewall that is allowing or denying communication.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="03e26-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="03e26-158">Clean up resources</span></span>

<span data-ttu-id="03e26-159">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="03e26-159">When no longer needed, you can use [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) to remove the resource group and all of the resources it contains:</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="03e26-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="03e26-160">Next steps</span></span>

<span data-ttu-id="03e26-161">In this quickstart, you created a VM and diagnosed inbound and outbound network traffic filters.</span><span class="sxs-lookup"><span data-stu-id="03e26-161">In this quickstart, you created a VM and diagnosed inbound and outbound network traffic filters.</span></span> <span data-ttu-id="03e26-162">You learned that network security group rules allow or deny traffic to and from a VM.</span><span class="sxs-lookup"><span data-stu-id="03e26-162">You learned that network security group rules allow or deny traffic to and from a VM.</span></span> <span data-ttu-id="03e26-163">Learn more about [security rules](../virtual-network/security-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create security rules](../virtual-network/manage-network-security-group.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-security-rule).</span><span class="sxs-lookup"><span data-stu-id="03e26-163">Learn more about [security rules](../virtual-network/security-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create security rules](../virtual-network/manage-network-security-group.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-security-rule).</span></span>

<span data-ttu-id="03e26-164">Even with the proper network traffic filters in place, communication to a VM can still fail, due to routing configuration.</span><span class="sxs-lookup"><span data-stu-id="03e26-164">Even with the proper network traffic filters in place, communication to a VM can still fail, due to routing configuration.</span></span> <span data-ttu-id="03e26-165">To learn how to diagnose VM network routing problems, see [Diagnose VM routing problems](diagnose-vm-network-routing-problem-powershell.md) or, to diagnose outbound routing, latency, and traffic filtering problems, with one tool, see [Connection troubleshoot](network-watcher-connectivity-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="03e26-165">To learn how to diagnose VM network routing problems, see [Diagnose VM routing problems](diagnose-vm-network-routing-problem-powershell.md) or, to diagnose outbound routing, latency, and traffic filtering problems, with one tool, see [Connection troubleshoot](network-watcher-connectivity-powershell.md).</span></span>