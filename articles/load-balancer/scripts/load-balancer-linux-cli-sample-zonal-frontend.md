---
title: CLI Example - Load Balancer VMs within a zone - Azure | Microsoft Docs
description: This Azure CLI script example shows how to load balance traffic to VMs within a specific availability zone
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: jeconnoc
editor: tysonn
tags: ''
Customer intent: As an IT administrator, I want to create a load balancer that load balances incoming internet traffic to virtual machines within a specific zone in a region.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 06/14/2018
ms.author: kumud
ms.openlocfilehash: 888808c94115e2ea136e90eb635faf28e7d92fd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868403"
---
# <a name="azure-cli-script-example-load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="94518-103">Azure CLI script example: Load balance traffic to VMs for high availability</span><span class="sxs-lookup"><span data-stu-id="94518-103">Azure CLI script example: Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="94518-104">This Azure CLI script example creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration within a specific availability zone.</span><span class="sxs-lookup"><span data-stu-id="94518-104">This Azure CLI script example creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration within a specific availability zone.</span></span> <span data-ttu-id="94518-105">After running the script, you will have three virtual machines in a single availability zones within a region that are accessible through an Azure Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="94518-105">After running the script, you will have three virtual machines in a single availability zones within a region that are accessible through an Azure Standard Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="94518-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="94518-106">Sample script</span></span>

```azurecli-interactive
  #!/bin/bash

  # Create a resource group.
   az group create \
    --name myResourceGroup \
    --location westeurope

  # Create a virtual network.
   az network vnet create \
    --resource-group myResourceGroup \
    --location westeurope \
    --name myVnet \
    --subnet-name mySubnet

  # Create a zonal Standard public IP address.
   az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --sku Standard
    --zone 1

  # Create an Azure Load Balancer.
   az network lb create \
    --resource-group myResourceGroupLB \
    --name myLoadBalancer \
    --public-ip-address myPublicIP \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --sku Standard

  # Creates an LB probe on port 80.
   az network lb probe create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80

  # Creates an LB rule for port 80.
   az network lb rule create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRuleWeb \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe

  # Create three NAT rules for port 22.
   for i in `seq 1 3`; do
    az network lb inbound-nat-rule create \
     --resource-group myResourceGroup \
     --lb-name myLoadBalancer \
     --name myLoadBalancerRuleSSH$i \
     --protocol tcp \
     --frontend-port 422$i \
     --backend-port 22 \
     --frontend-ip-name myFrontEndPool
   done

  # Create a network security group
   az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup

  # Create a network security group rule for port 22.
   az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --direction inbound \
    --source-address-prefix '*' \
    --source-port-range '*'  \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow \
    --priority 1000

  # Create a network security group rule for port 80.
    az network nsg rule create \
     --resource-group myResourceGroup \
     --nsg-name myNetworkSecurityGroup \
     --name myNetworkSecurityGroupRuleHTTP \
     --protocol tcp \
     --direction inbound \
     --source-address-prefix '*' \
     --source-port-range '*' \
     --destination-address-prefix '*' \
     --destination-port-range 80 \
     --access allow \
     --priority 2000

  # Create three virtual network cards and associate with public IP address and NSG.
  for i in `seq 1 3`; do
   az network nic create \
     --resource-group myResourceGroup \
     --name myNic$i \
     --vnet-name myVnet \
     --subnet mySubnet \
     --network-security-group myNetworkSecurityGroup \
     --lb-name myLoadBalancer \
     --lb-address-pools myBackEndPool \
     --lb-inbound-nat-rules myLoadBalancerRuleSSH$i
  done

# Create three virtual machines, this creates SSH keys if not present.
for i in `seq 1 3`; do
  az vm create \
    --resource-group myResourceGroup \
    --name myVM$i \
    --zone 1 \
    --nics myNic$i \
    --image UbuntuLTS \
    --generate-ssh-keys \
    --no-wait
done

```

## <a name="clean-up-deployment"></a><span data-ttu-id="94518-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="94518-107">Clean up deployment</span></span> 

<span data-ttu-id="94518-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="94518-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="94518-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="94518-109">Script explanation</span></span>

<span data-ttu-id="94518-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="94518-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="94518-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="94518-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="94518-112">Command</span><span class="sxs-lookup"><span data-stu-id="94518-112">Command</span></span> | <span data-ttu-id="94518-113">Notes</span><span class="sxs-lookup"><span data-stu-id="94518-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94518-114">az group create</span><span class="sxs-lookup"><span data-stu-id="94518-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="94518-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="94518-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="94518-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="94518-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az-network-vnet-create) | <span data-ttu-id="94518-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="94518-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="94518-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="94518-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az-network-public-ip-create) | <span data-ttu-id="94518-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="94518-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="94518-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="94518-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az-network-lb-create) | <span data-ttu-id="94518-121">Creates an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="94518-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="94518-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="94518-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#az-network-lb-probe-create) | <span data-ttu-id="94518-123">Creates a load balancer probe.</span><span class="sxs-lookup"><span data-stu-id="94518-123">Creates a load balancer probe.</span></span> <span data-ttu-id="94518-124">A load balancer probe is used to monitor each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="94518-124">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="94518-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="94518-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="94518-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="94518-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az-network-lb-rule-create) | <span data-ttu-id="94518-127">Creates a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="94518-127">Creates a load balancer rule.</span></span> <span data-ttu-id="94518-128">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="94518-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="94518-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span><span class="sxs-lookup"><span data-stu-id="94518-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span></span> |
| [<span data-ttu-id="94518-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="94518-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-create) | <span data-ttu-id="94518-131">Creates load balancer Network Address Translation (NAT) rule.</span><span class="sxs-lookup"><span data-stu-id="94518-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="94518-132">NAT rules map a port of the load balancer to a port on a VM.</span><span class="sxs-lookup"><span data-stu-id="94518-132">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="94518-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="94518-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="94518-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="94518-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#az-network-nsg-create) | <span data-ttu-id="94518-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="94518-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="94518-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="94518-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#az-network-nsg-rule-create) | <span data-ttu-id="94518-137">Creates an NSG rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="94518-137">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="94518-138">In this sample, port 22 is opened for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="94518-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="94518-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="94518-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#az-network-nic-create) | <span data-ttu-id="94518-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="94518-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="94518-141">az vm create</span><span class="sxs-lookup"><span data-stu-id="94518-141">az vm create</span></span>](/cli/azure/vm#az-vm-create) | <span data-ttu-id="94518-142">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="94518-142">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="94518-143">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="94518-143">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="94518-144">az group delete</span><span class="sxs-lookup"><span data-stu-id="94518-144">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az-vm-extension-set) | <span data-ttu-id="94518-145">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="94518-145">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94518-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="94518-146">Next steps</span></span>

<span data-ttu-id="94518-147">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="94518-147">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="94518-148">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94518-148">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>