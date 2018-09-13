---
title: Diagnose a virtual machine network traffic filter problem - quickstart - Azure CLI | Microsoft Docs
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
ms.openlocfilehash: 2f6011103c86895c455b284a0982636a0d31fbe7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865097"
---
# <a name="quickstart-diagnose-a-virtual-machine-network-traffic-filter-problem---azure-cli"></a><span data-ttu-id="0a814-103">Quickstart: Diagnose a virtual machine network traffic filter problem - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a814-103">Quickstart: Diagnose a virtual machine network traffic filter problem - Azure CLI</span></span>

<span data-ttu-id="0a814-104">In this quickstart you deploy a virtual machine (VM), and then check communications to an IP address and URL and from an IP address.</span><span class="sxs-lookup"><span data-stu-id="0a814-104">In this quickstart you deploy a virtual machine (VM), and then check communications to an IP address and URL and from an IP address.</span></span> <span data-ttu-id="0a814-105">You determine the cause of a communication failure and how you can resolve it.</span><span class="sxs-lookup"><span data-stu-id="0a814-105">You determine the cause of a communication failure and how you can resolve it.</span></span>

<span data-ttu-id="0a814-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="0a814-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a814-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.28 or later.</span><span class="sxs-lookup"><span data-stu-id="0a814-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.28 or later.</span></span> <span data-ttu-id="0a814-108">To find the installed version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="0a814-108">To find the installed version, run `az --version`.</span></span> <span data-ttu-id="0a814-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0a814-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="0a814-110">After you verify the CLI version, run `az login`  to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="0a814-110">After you verify the CLI version, run `az login`  to create a connection with Azure.</span></span> <span data-ttu-id="0a814-111">The CLI commands in this quickstart are formatted to run in a Bash shell.</span><span class="sxs-lookup"><span data-stu-id="0a814-111">The CLI commands in this quickstart are formatted to run in a Bash shell.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="0a814-112">Create a VM</span><span class="sxs-lookup"><span data-stu-id="0a814-112">Create a VM</span></span>

<span data-ttu-id="0a814-113">Before you can create a VM, you must create a resource group to contain the VM.</span><span class="sxs-lookup"><span data-stu-id="0a814-113">Before you can create a VM, you must create a resource group to contain the VM.</span></span> <span data-ttu-id="0a814-114">Create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="0a814-114">Create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="0a814-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="0a814-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0a814-116">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span><span class="sxs-lookup"><span data-stu-id="0a814-116">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span></span> <span data-ttu-id="0a814-117">If SSH keys do not already exist in a default key location, the command creates them.</span><span class="sxs-lookup"><span data-stu-id="0a814-117">If SSH keys do not already exist in a default key location, the command creates them.</span></span> <span data-ttu-id="0a814-118">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="0a814-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span> <span data-ttu-id="0a814-119">The following example creates a VM named *myVm*:</span><span class="sxs-lookup"><span data-stu-id="0a814-119">The following example creates a VM named *myVm*:</span></span>

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVm \
  --image UbuntuLTS \
  --generate-ssh-keys
```

<span data-ttu-id="0a814-120">The VM takes a few minutes to create.</span><span class="sxs-lookup"><span data-stu-id="0a814-120">The VM takes a few minutes to create.</span></span> <span data-ttu-id="0a814-121">Don't continue with remaining steps until the VM is created and the CLI returns output.</span><span class="sxs-lookup"><span data-stu-id="0a814-121">Don't continue with remaining steps until the VM is created and the CLI returns output.</span></span>

## <a name="test-network-communication"></a><span data-ttu-id="0a814-122">Test network communication</span><span class="sxs-lookup"><span data-stu-id="0a814-122">Test network communication</span></span>

<span data-ttu-id="0a814-123">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's IP flow verify capability to test communication.</span><span class="sxs-lookup"><span data-stu-id="0a814-123">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's IP flow verify capability to test communication.</span></span>

### <a name="enable-network-watcher"></a><span data-ttu-id="0a814-124">Enable network watcher</span><span class="sxs-lookup"><span data-stu-id="0a814-124">Enable network watcher</span></span>

<span data-ttu-id="0a814-125">If you already have a network watcher enabled in the East US region, skip to [Use IP flow verify](#use-ip-flow-verify).</span><span class="sxs-lookup"><span data-stu-id="0a814-125">If you already have a network watcher enabled in the East US region, skip to [Use IP flow verify](#use-ip-flow-verify).</span></span> <span data-ttu-id="0a814-126">Use the [az network watcher configure](/cli/azure/network/watcher#az-network-watcher-configure) command to create a network watcher in the EastUS region:</span><span class="sxs-lookup"><span data-stu-id="0a814-126">Use the [az network watcher configure](/cli/azure/network/watcher#az-network-watcher-configure) command to create a network watcher in the EastUS region:</span></span>

```azurecli-interactive
az network watcher configure \
  --resource-group NetworkWatcherRG \
  --locations eastus \
  --enabled
```

### <a name="use-ip-flow-verify"></a><span data-ttu-id="0a814-127">Use IP flow verify</span><span class="sxs-lookup"><span data-stu-id="0a814-127">Use IP flow verify</span></span>

<span data-ttu-id="0a814-128">When you create a VM, Azure allows and denies network traffic to and from the VM, by default.</span><span class="sxs-lookup"><span data-stu-id="0a814-128">When you create a VM, Azure allows and denies network traffic to and from the VM, by default.</span></span> <span data-ttu-id="0a814-129">You might later override Azure's defaults, allowing or denying additional types of traffic.</span><span class="sxs-lookup"><span data-stu-id="0a814-129">You might later override Azure's defaults, allowing or denying additional types of traffic.</span></span> <span data-ttu-id="0a814-130">To test whether traffic is allowed or denied to different destinations and from a source IP address, use the [az network watcher test-ip-flow](/cli/azure/network/watcher#az-network-watcher-test-ip-flow) command.</span><span class="sxs-lookup"><span data-stu-id="0a814-130">To test whether traffic is allowed or denied to different destinations and from a source IP address, use the [az network watcher test-ip-flow](/cli/azure/network/watcher#az-network-watcher-test-ip-flow) command.</span></span>

<span data-ttu-id="0a814-131">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span><span class="sxs-lookup"><span data-stu-id="0a814-131">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span></span>

```azurecli-interactive
az network watcher test-ip-flow \
  --direction outbound \
  --local 10.0.0.4:60000 \
  --protocol TCP \
  --remote 13.107.21.200:80 \
  --vm myVm \
  --nic myVmVMNic \
  --resource-group myResourceGroup \
  --out table
```

<span data-ttu-id="0a814-132">After several seconds, the result returned informs you that access is allowed by a security rule named **AllowInternetOutbound**.</span><span class="sxs-lookup"><span data-stu-id="0a814-132">After several seconds, the result returned informs you that access is allowed by a security rule named **AllowInternetOutbound**.</span></span>

<span data-ttu-id="0a814-133">Test outbound communication from the VM to 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="0a814-133">Test outbound communication from the VM to 172.31.0.100:</span></span>

```azurecli-interactive
az network watcher test-ip-flow \
  --direction outbound \
  --local 10.0.0.4:60000 \
  --protocol TCP \
  --remote 172.31.0.100:80 \
  --vm myVm \
  --nic myVmVMNic \
  --resource-group myResourceGroup \
  --out table
```

<span data-ttu-id="0a814-134">The result returned informs you that access is denied by a security rule named **DefaultOutboundDenyAll**.</span><span class="sxs-lookup"><span data-stu-id="0a814-134">The result returned informs you that access is denied by a security rule named **DefaultOutboundDenyAll**.</span></span>

<span data-ttu-id="0a814-135">Test inbound communication to the VM from 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="0a814-135">Test inbound communication to the VM from 172.31.0.100:</span></span>

```azurecli-interactive
az network watcher test-ip-flow \
  --direction inbound \
  --local 10.0.0.4:80 \
  --protocol TCP \
  --remote 172.31.0.100:60000 \
  --vm myVm \
  --nic myVmVMNic \
  --resource-group myResourceGroup \
  --out table
```

<span data-ttu-id="0a814-136">The result returned informs you that access is denied because of a security rule named **DefaultInboundDenyAll**.</span><span class="sxs-lookup"><span data-stu-id="0a814-136">The result returned informs you that access is denied because of a security rule named **DefaultInboundDenyAll**.</span></span> <span data-ttu-id="0a814-137">Now that you know which security rules are allowing or denying traffic to or from a VM, you can determine how to resolve the problems.</span><span class="sxs-lookup"><span data-stu-id="0a814-137">Now that you know which security rules are allowing or denying traffic to or from a VM, you can determine how to resolve the problems.</span></span>

## <a name="view-details-of-a-security-rule"></a><span data-ttu-id="0a814-138">View details of a security rule</span><span class="sxs-lookup"><span data-stu-id="0a814-138">View details of a security rule</span></span>

<span data-ttu-id="0a814-139">To determine why the rules in [Use IP flow verify](#use-ip-flow-verify) are allowing or preventing communication, review the effective security rules for the network interface with the [az network nic list-effective-nsg](/cli/azure/network/nic#az-network-nic-list-effective-nsg) command:</span><span class="sxs-lookup"><span data-stu-id="0a814-139">To determine why the rules in [Use IP flow verify](#use-ip-flow-verify) are allowing or preventing communication, review the effective security rules for the network interface with the [az network nic list-effective-nsg](/cli/azure/network/nic#az-network-nic-list-effective-nsg) command:</span></span>

```azurecli-interactive
az network nic list-effective-nsg \
  --resource-group myResourceGroup \
  --name myVmVMNic
```

<span data-ttu-id="0a814-140">The returned output includes the following text for the **AllowInternetOutbound** rule that allowed outbound access to www.bing.com in a previous step under [Use IP flow verify](#use-ip-flow-verify):</span><span class="sxs-lookup"><span data-stu-id="0a814-140">The returned output includes the following text for the **AllowInternetOutbound** rule that allowed outbound access to www.bing.com in a previous step under [Use IP flow verify](#use-ip-flow-verify):</span></span>

```azurecli
{
 "access": "Allow",
 "additionalProperties": {},
 "destinationAddressPrefix": "Internet",
 "destinationAddressPrefixes": [
  "Internet"
 ],
 "destinationPortRange": "0-65535",
 "destinationPortRanges": [
  "0-65535"
 ],
 "direction": "Outbound",
 "expandedDestinationAddressPrefix": [
  "1.0.0.0/8",
  "2.0.0.0/7",
  "4.0.0.0/6",
  "8.0.0.0/7",
  "11.0.0.0/8",
  "12.0.0.0/6",
  ...
 ],
 "expandedSourceAddressPrefix": null,
 "name": "defaultSecurityRules/AllowInternetOutBound",
 "priority": 65001,
 "protocol": "All",
 "sourceAddressPrefix": "0.0.0.0/0",
 "sourceAddressPrefixes": [
  "0.0.0.0/0"
 ],
 "sourcePortRange": "0-65535",
 "sourcePortRanges": [
  "0-65535"
 ]
},
```

<span data-ttu-id="0a814-141">You can see in the previous output that **destinationAddressPrefix** is **Internet**.</span><span class="sxs-lookup"><span data-stu-id="0a814-141">You can see in the previous output that **destinationAddressPrefix** is **Internet**.</span></span> <span data-ttu-id="0a814-142">It's not clear how 13.107.21.200 relates to **Internet** though.</span><span class="sxs-lookup"><span data-stu-id="0a814-142">It's not clear how 13.107.21.200 relates to **Internet** though.</span></span> <span data-ttu-id="0a814-143">You see several address prefixes listed under **expandedDestinationAddressPrefix**.</span><span class="sxs-lookup"><span data-stu-id="0a814-143">You see several address prefixes listed under **expandedDestinationAddressPrefix**.</span></span> <span data-ttu-id="0a814-144">One of the prefixes in the list is **12.0.0.0/6**, which encompasses the 12.0.0.1-15.255.255.254 range of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="0a814-144">One of the prefixes in the list is **12.0.0.0/6**, which encompasses the 12.0.0.1-15.255.255.254 range of IP addresses.</span></span> <span data-ttu-id="0a814-145">Since 13.107.21.200 is within that address range, the **AllowInternetOutBound** rule allows the outbound traffic.</span><span class="sxs-lookup"><span data-stu-id="0a814-145">Since 13.107.21.200 is within that address range, the **AllowInternetOutBound** rule allows the outbound traffic.</span></span> <span data-ttu-id="0a814-146">Additionally, there are no higher priority (lower number) rules shown in the previous output that override this rule.</span><span class="sxs-lookup"><span data-stu-id="0a814-146">Additionally, there are no higher priority (lower number) rules shown in the previous output that override this rule.</span></span> <span data-ttu-id="0a814-147">To deny outbound communication to an IP address, you could add a security rule with a higher priority, that denies port 80 outbound to the IP address.</span><span class="sxs-lookup"><span data-stu-id="0a814-147">To deny outbound communication to an IP address, you could add a security rule with a higher priority, that denies port 80 outbound to the IP address.</span></span>

<span data-ttu-id="0a814-148">When you ran the `az network watcher test-ip-flow` command to test outbound communication to 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultOutboundDenyAll** rule denied the communication.</span><span class="sxs-lookup"><span data-stu-id="0a814-148">When you ran the `az network watcher test-ip-flow` command to test outbound communication to 172.131.0.100 in [Use IP flow verify](#use-ip-flow-verify), the output informed you that the **DefaultOutboundDenyAll** rule denied the communication.</span></span> <span data-ttu-id="0a814-149">The **DefaultOutboundDenyAll** rule equates to the **DenyAllOutBound** rule listed in the following output from the `az network nic list-effective-nsg` command:</span><span class="sxs-lookup"><span data-stu-id="0a814-149">The **DefaultOutboundDenyAll** rule equates to the **DenyAllOutBound** rule listed in the following output from the `az network nic list-effective-nsg` command:</span></span>

```azurecli
{
 "access": "Deny",
 "additionalProperties": {},
 "destinationAddressPrefix": "0.0.0.0/0",
 "destinationAddressPrefixes": [
  "0.0.0.0/0"
 ],
 "destinationPortRange": "0-65535",
 "destinationPortRanges": [
  "0-65535"
 ],
 "direction": "Outbound",
 "expandedDestinationAddressPrefix": null,
 "expandedSourceAddressPrefix": null,
 "name": "defaultSecurityRules/DenyAllOutBound",
 "priority": 65500,
 "protocol": "All",
 "sourceAddressPrefix": "0.0.0.0/0",
 "sourceAddressPrefixes": [
  "0.0.0.0/0"
 ],
 "sourcePortRange": "0-65535",
 "sourcePortRanges": [
  "0-65535"
 ]
}
```

<span data-ttu-id="0a814-150">The rule lists **0.0.0.0/0** as the **destinationAddressPrefix**.</span><span class="sxs-lookup"><span data-stu-id="0a814-150">The rule lists **0.0.0.0/0** as the **destinationAddressPrefix**.</span></span> <span data-ttu-id="0a814-151">The rule denies the outbound communication to 172.131.0.100, because the address is not within the **destinationAddressPrefix** of any of the other outbound rules in the output from the `az network nic list-effective-nsg` command.</span><span class="sxs-lookup"><span data-stu-id="0a814-151">The rule denies the outbound communication to 172.131.0.100, because the address is not within the **destinationAddressPrefix** of any of the other outbound rules in the output from the `az network nic list-effective-nsg` command.</span></span> <span data-ttu-id="0a814-152">To allow the outbound communication, you could add a security rule with a higher priority, that allows outbound traffic to port 80 at 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="0a814-152">To allow the outbound communication, you could add a security rule with a higher priority, that allows outbound traffic to port 80 at 172.131.0.100.</span></span>

<span data-ttu-id="0a814-153">When you ran the `az network watcher test-ip-flow` command in [Use IP flow verify](#use-ip-flow-verify) to test inbound communication from 172.131.0.100, the output informed you that the **DefaultInboundDenyAll** rule denied the communication.</span><span class="sxs-lookup"><span data-stu-id="0a814-153">When you ran the `az network watcher test-ip-flow` command in [Use IP flow verify](#use-ip-flow-verify) to test inbound communication from 172.131.0.100, the output informed you that the **DefaultInboundDenyAll** rule denied the communication.</span></span> <span data-ttu-id="0a814-154">The **DefaultInboundDenyAll** rule equates to the **DenyAllInBound** rule listed in the following output from the `az network nic list-effective-nsg` command:</span><span class="sxs-lookup"><span data-stu-id="0a814-154">The **DefaultInboundDenyAll** rule equates to the **DenyAllInBound** rule listed in the following output from the `az network nic list-effective-nsg` command:</span></span>

```azurecli
{
 "access": "Deny",
 "additionalProperties": {},
 "destinationAddressPrefix": "0.0.0.0/0",
 "destinationAddressPrefixes": [
  "0.0.0.0/0"
 ],
 "destinationPortRange": "0-65535",
 "destinationPortRanges": [
  "0-65535"
 ],
 "direction": "Inbound",
 "expandedDestinationAddressPrefix": null,
 "expandedSourceAddressPrefix": null,
 "name": "defaultSecurityRules/DenyAllInBound",
 "priority": 65500,
 "protocol": "All",
 "sourceAddressPrefix": "0.0.0.0/0",
 "sourceAddressPrefixes": [
  "0.0.0.0/0"
 ],
 "sourcePortRange": "0-65535",
 "sourcePortRanges": [
  "0-65535"
 ]
},
```

<span data-ttu-id="0a814-155">The **DenyAllInBound** rule is applied because, as shown in the output, no other higher priority rule exists in the output from the `az network nic list-effective-nsg` command that allows port 80 inbound to the VM from 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="0a814-155">The **DenyAllInBound** rule is applied because, as shown in the output, no other higher priority rule exists in the output from the `az network nic list-effective-nsg` command that allows port 80 inbound to the VM from 172.131.0.100.</span></span> <span data-ttu-id="0a814-156">To allow the inbound communication, you could add a security rule with a higher priority that allows port 80 inbound from 172.131.0.100.</span><span class="sxs-lookup"><span data-stu-id="0a814-156">To allow the inbound communication, you could add a security rule with a higher priority that allows port 80 inbound from 172.131.0.100.</span></span>

<span data-ttu-id="0a814-157">The checks in this quickstart tested Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="0a814-157">The checks in this quickstart tested Azure configuration.</span></span> <span data-ttu-id="0a814-158">If the checks return expected results and you still have network problems, ensure that you don't have a firewall between your VM and the endpoint you're communicating with and that the operating system in your VM doesn't have a firewall that is allowing or denying communication.</span><span class="sxs-lookup"><span data-stu-id="0a814-158">If the checks return expected results and you still have network problems, ensure that you don't have a firewall between your VM and the endpoint you're communicating with and that the operating system in your VM doesn't have a firewall that is allowing or denying communication.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0a814-159">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0a814-159">Clean up resources</span></span>

<span data-ttu-id="0a814-160">When no longer needed, you can use [az group delete](/cli/azure/group#az_group_delete) to remove the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="0a814-160">When no longer needed, you can use [az group delete](/cli/azure/group#az_group_delete) to remove the resource group and all of the resources it contains:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="0a814-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a814-161">Next steps</span></span>

<span data-ttu-id="0a814-162">In this quickstart, you created a VM and diagnosed inbound and outbound network traffic filters.</span><span class="sxs-lookup"><span data-stu-id="0a814-162">In this quickstart, you created a VM and diagnosed inbound and outbound network traffic filters.</span></span> <span data-ttu-id="0a814-163">You learned that network security group rules allow or deny traffic to and from a VM.</span><span class="sxs-lookup"><span data-stu-id="0a814-163">You learned that network security group rules allow or deny traffic to and from a VM.</span></span> <span data-ttu-id="0a814-164">Learn more about [security rules](../virtual-network/security-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create security rules](../virtual-network/manage-network-security-group.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-security-rule).</span><span class="sxs-lookup"><span data-stu-id="0a814-164">Learn more about [security rules](../virtual-network/security-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create security rules](../virtual-network/manage-network-security-group.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-security-rule).</span></span>

<span data-ttu-id="0a814-165">Even with the proper network traffic filters in place, communication to a VM can still fail, due to routing configuration.</span><span class="sxs-lookup"><span data-stu-id="0a814-165">Even with the proper network traffic filters in place, communication to a VM can still fail, due to routing configuration.</span></span> <span data-ttu-id="0a814-166">To learn how to diagnose VM network routing problems, see [Diagnose VM routing problems](diagnose-vm-network-routing-problem-cli.md) or, to diagnose outbound routing, latency, and traffic filtering problems, with one tool, see [Connection troubleshoot](network-watcher-connectivity-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0a814-166">To learn how to diagnose VM network routing problems, see [Diagnose VM routing problems](diagnose-vm-network-routing-problem-cli.md) or, to diagnose outbound routing, latency, and traffic filtering problems, with one tool, see [Connection troubleshoot](network-watcher-connectivity-cli.md).</span></span>