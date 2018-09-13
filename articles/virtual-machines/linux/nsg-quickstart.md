---
title: Open ports to a Linux VM with Azure CLI 2.0 | Microsoft Docs
description: Learn how to open a port / create an endpoint to your Linux VM using the Azure resource manager deployment model and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: fd076dbec5d2805827d820c5378f6c360fc607c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564399"
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="b4ba9-103">Open ports and endpoints to a Linux VM with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4ba9-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="b4ba9-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="b4ba9-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="b4ba9-106">Let's use a common example of web traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="b4ba9-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="b4ba9-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b4ba9-109">Quick commands</span><span class="sxs-lookup"><span data-stu-id="b4ba9-109">Quick commands</span></span>
<span data-ttu-id="b4ba9-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b4ba9-111">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b4ba9-112">Example parameter names include `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-112">Example parameter names include `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span></span>

<span data-ttu-id="b4ba9-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b4ba9-114">The following example creates a network security group named `myNetworkSecurityGroup` in the `westus` location:</span><span class="sxs-lookup"><span data-stu-id="b4ba9-114">The following example creates a network security group named `myNetworkSecurityGroup` in the `westus` location:</span></span>

```azurecli
az network nsg create --resource-group myResourceGroup --location westus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="b4ba9-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="b4ba9-116">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span><span class="sxs-lookup"><span data-stu-id="b4ba9-116">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1000 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 80 --access allow
```

<span data-ttu-id="b4ba9-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="b4ba9-118">The following example associates an existing NIC named `myNic` with the Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4ba9-118">The following example associates an existing NIC named `myNic` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nic update --resource-group myResourceGroup --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="b4ba9-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="b4ba9-120">The following example associates an existing subnet named `mySubnet` in the `myVnet` virtual network with the Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4ba9-120">The following example associates an existing subnet named `mySubnet` in the `myVnet` virtual network with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update --resource-group myResourceGroup \
    --vnet-name myVnet --name mySubnet --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="b4ba9-121">More information on Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="b4ba9-121">More information on Network Security Groups</span></span>
<span data-ttu-id="b4ba9-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="b4ba9-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="b4ba9-124">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-124">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="b4ba9-125">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-125">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="b4ba9-126">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-126">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="b4ba9-127">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-127">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="b4ba9-128">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-128">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="b4ba9-129">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b4ba9-129">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ba9-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4ba9-130">Next steps</span></span>
<span data-ttu-id="b4ba9-131">In this example, you created a simple rule to allow HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="b4ba9-131">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="b4ba9-132">You can find information on creating more detailed environments in the following articles:</span><span class="sxs-lookup"><span data-stu-id="b4ba9-132">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="b4ba9-133">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="b4ba9-133">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="b4ba9-134">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="b4ba9-134">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b4ba9-135">Azure Resource Manager Overview for Load Balancers</span><span class="sxs-lookup"><span data-stu-id="b4ba9-135">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

