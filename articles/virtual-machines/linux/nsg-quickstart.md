---
title: Open ports to a Linux VM with Azure CLI 2.0 | Microsoft Docs
description: Learn how to open a port / create an endpoint to your Linux VM using the Azure resource manager deployment model and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 12/13/2017
ms.author: cynthn
ms.openlocfilehash: 7bb1f848f83e8d373f4a8037dbe14307288121da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787181"
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="8fc80-103">Open ports and endpoints to a Linux VM with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fc80-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="8fc80-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span><span class="sxs-lookup"><span data-stu-id="8fc80-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="8fc80-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span><span class="sxs-lookup"><span data-stu-id="8fc80-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="8fc80-106">Let's use a common example of web traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="8fc80-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="8fc80-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8fc80-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="8fc80-108">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="8fc80-108">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="8fc80-109">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8fc80-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8fc80-110">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8fc80-110">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>


## <a name="quickly-open-a-port-for-a-vm"></a><span data-ttu-id="8fc80-111">Quickly open a port for a VM</span><span class="sxs-lookup"><span data-stu-id="8fc80-111">Quickly open a port for a VM</span></span>
<span data-ttu-id="8fc80-112">If you need to quickly open a port for a VM in a dev/test scenario, you can use the [az vm open-port](/cli/azure/vm#az_vm_open_port) command.</span><span class="sxs-lookup"><span data-stu-id="8fc80-112">If you need to quickly open a port for a VM in a dev/test scenario, you can use the [az vm open-port](/cli/azure/vm#az_vm_open_port) command.</span></span> <span data-ttu-id="8fc80-113">This command creates a Network Security Group, adds a rule, and applies it to a VM or subnet.</span><span class="sxs-lookup"><span data-stu-id="8fc80-113">This command creates a Network Security Group, adds a rule, and applies it to a VM or subnet.</span></span> <span data-ttu-id="8fc80-114">The following example opens port *80* on the VM named *myVM* in the resource group named *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8fc80-114">The following example opens port *80* on the VM named *myVM* in the resource group named *myResourceGroup*.</span></span>

```azure-cli
az vm open-port --resource-group myResourceGroup --name myVM --port 80
```

<span data-ttu-id="8fc80-115">For more control over the rules, such as defining a source IP address range, continue with the additional steps in this article.</span><span class="sxs-lookup"><span data-stu-id="8fc80-115">For more control over the rules, such as defining a source IP address range, continue with the additional steps in this article.</span></span>


## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="8fc80-116">Create a Network Security Group and rules</span><span class="sxs-lookup"><span data-stu-id="8fc80-116">Create a Network Security Group and rules</span></span>
<span data-ttu-id="8fc80-117">Create the network security group with [az network nsg create](/cli/azure/network/nsg#az_network_nsg_create).</span><span class="sxs-lookup"><span data-stu-id="8fc80-117">Create the network security group with [az network nsg create](/cli/azure/network/nsg#az_network_nsg_create).</span></span> <span data-ttu-id="8fc80-118">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="8fc80-118">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8fc80-119">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#az_network_nsg_rule_create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span><span class="sxs-lookup"><span data-stu-id="8fc80-119">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#az_network_nsg_rule_create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="8fc80-120">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span><span class="sxs-lookup"><span data-stu-id="8fc80-120">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```


## <a name="apply-network-security-group-to-vm"></a><span data-ttu-id="8fc80-121">Apply Network Security Group to VM</span><span class="sxs-lookup"><span data-stu-id="8fc80-121">Apply Network Security Group to VM</span></span>
<span data-ttu-id="8fc80-122">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#az_network_nic_update).</span><span class="sxs-lookup"><span data-stu-id="8fc80-122">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#az_network_nic_update).</span></span> <span data-ttu-id="8fc80-123">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8fc80-123">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="8fc80-124">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_update) rather than just to the network interface on a single VM.</span><span class="sxs-lookup"><span data-stu-id="8fc80-124">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="8fc80-125">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8fc80-125">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8fc80-126">More information on Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="8fc80-126">More information on Network Security Groups</span></span>
<span data-ttu-id="8fc80-127">The quick commands here allow you to get up and running with traffic flowing to your VM.</span><span class="sxs-lookup"><span data-stu-id="8fc80-127">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="8fc80-128">Network Security Groups provide many great features and granularity for controlling access to your resources.</span><span class="sxs-lookup"><span data-stu-id="8fc80-128">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="8fc80-129">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="8fc80-129">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="8fc80-130">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8fc80-130">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8fc80-131">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span><span class="sxs-lookup"><span data-stu-id="8fc80-131">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8fc80-132">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8fc80-132">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc80-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fc80-133">Next steps</span></span>
<span data-ttu-id="8fc80-134">In this example, you created a simple rule to allow HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="8fc80-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="8fc80-135">You can find information on creating more detailed environments in the following articles:</span><span class="sxs-lookup"><span data-stu-id="8fc80-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="8fc80-136">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="8fc80-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8fc80-137">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="8fc80-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/security-overview.md)
