---
title: Open ports to a Linux VM with Azure CLI 1.0 | Microsoft Docs
description: Learn how to open a port / create an endpoint to your Linux VM using the Azure resource manager deployment model and the Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5fc4655e8795a85ce678d0255318f998f88834bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555696"
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="329e9-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="329e9-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="329e9-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span><span class="sxs-lookup"><span data-stu-id="329e9-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="329e9-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span><span class="sxs-lookup"><span data-stu-id="329e9-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="329e9-106">Let's use a common example of web traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="329e9-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="329e9-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="329e9-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="329e9-108">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="329e9-108">CLI versions to complete the task</span></span>
<span data-ttu-id="329e9-109">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="329e9-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="329e9-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="329e9-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="329e9-111">[Azure CLI 2.0](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="329e9-111">[Azure CLI 2.0](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="329e9-112">Quick commands</span><span class="sxs-lookup"><span data-stu-id="329e9-112">Quick commands</span></span>
<span data-ttu-id="329e9-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="329e9-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="329e9-114">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="329e9-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="329e9-115">Example parameter names included `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="329e9-115">Example parameter names included `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span></span>

<span data-ttu-id="329e9-116">Create your Network Security Group, entering your own names and location appropriately.</span><span class="sxs-lookup"><span data-stu-id="329e9-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="329e9-117">The following example creates a Network Security Group named `myNetworkSecurityGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="329e9-117">The following example creates a Network Security Group named `myNetworkSecurityGroup` in the `WestUS` location:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="329e9-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span><span class="sxs-lookup"><span data-stu-id="329e9-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="329e9-119">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span><span class="sxs-lookup"><span data-stu-id="329e9-119">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRule \
    --protocol tcp --direction inbound --priority 1000 \
    --destination-port-range 80 --access allow
```

<span data-ttu-id="329e9-120">Associate the Network Security Group with your VM's network interface (NIC).</span><span class="sxs-lookup"><span data-stu-id="329e9-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="329e9-121">The following example associates an existing NIC named `myNic` with the Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="329e9-121">The following example associates an existing NIC named `myNic` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup --name myNic
```

<span data-ttu-id="329e9-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span><span class="sxs-lookup"><span data-stu-id="329e9-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="329e9-123">The following example associates an existing subnet named `mySubnet` in the `myVnet` virtual network with the Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="329e9-123">The following example associates an existing subnet named `mySubnet` in the `myVnet` virtual network with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network vnet subnet set --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="329e9-124">More information on Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="329e9-124">More information on Network Security Groups</span></span>
<span data-ttu-id="329e9-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span><span class="sxs-lookup"><span data-stu-id="329e9-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="329e9-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span><span class="sxs-lookup"><span data-stu-id="329e9-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="329e9-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="329e9-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="329e9-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="329e9-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="329e9-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="329e9-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="329e9-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span><span class="sxs-lookup"><span data-stu-id="329e9-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="329e9-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span><span class="sxs-lookup"><span data-stu-id="329e9-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="329e9-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="329e9-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="329e9-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="329e9-133">Next steps</span></span>
<span data-ttu-id="329e9-134">In this example, you created a simple rule to allow HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="329e9-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="329e9-135">You can find information on creating more detailed environments in the following articles:</span><span class="sxs-lookup"><span data-stu-id="329e9-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="329e9-136">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="329e9-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="329e9-137">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="329e9-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="329e9-138">Azure Resource Manager Overview for Load Balancers</span><span class="sxs-lookup"><span data-stu-id="329e9-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

