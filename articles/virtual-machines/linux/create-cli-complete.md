---
title: Create a Linux environment with the Azure CLI 2.0 | Microsoft Docs
description: Create storage, a Linux VM, a virtual network and subnet, a load balancer, an NIC, a public IP, and a network security group, all from the ground up by using the Azure CLI 2.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: b3f9ac921a96176c669c8f62b32b8c80254ad316
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564299"
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-20"></a><span data-ttu-id="69ae2-103">Create a complete Linux environment with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69ae2-103">Create a complete Linux environment with the Azure CLI 2.0</span></span>
<span data-ttu-id="69ae2-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span><span class="sxs-lookup"><span data-stu-id="69ae2-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="69ae2-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span><span class="sxs-lookup"><span data-stu-id="69ae2-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="69ae2-106">Then you can move on to more complex networks and environments.</span><span class="sxs-lookup"><span data-stu-id="69ae2-106">Then you can move on to more complex networks and environments.</span></span> <span data-ttu-id="69ae2-107">This article details how to build the environment with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="69ae2-107">This article details how to build the environment with the Azure CLI 2.0.</span></span> <span data-ttu-id="69ae2-108">You can also perform these steps with the [Azure CLI 1.0](create-cli-complete-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-108">You can also perform these steps with the [Azure CLI 1.0](create-cli-complete-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="69ae2-109">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span><span class="sxs-lookup"><span data-stu-id="69ae2-109">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="69ae2-110">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-110">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="69ae2-111">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span><span class="sxs-lookup"><span data-stu-id="69ae2-111">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="69ae2-112">The environment contains:</span><span class="sxs-lookup"><span data-stu-id="69ae2-112">The environment contains:</span></span>

* <span data-ttu-id="69ae2-113">Two VMs inside an availability set.</span><span class="sxs-lookup"><span data-stu-id="69ae2-113">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="69ae2-114">A load balancer with a load-balancing rule on port 80.</span><span class="sxs-lookup"><span data-stu-id="69ae2-114">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="69ae2-115">Network security group (NSG) rules to protect your VM from unwanted traffic.</span><span class="sxs-lookup"><span data-stu-id="69ae2-115">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

![Basic environment overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/create-cli-complete/environment_overview.png)

## <a name="quick-commands"></a><span data-ttu-id="69ae2-117">Quick commands</span><span class="sxs-lookup"><span data-stu-id="69ae2-117">Quick commands</span></span>
<span data-ttu-id="69ae2-118">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span><span class="sxs-lookup"><span data-stu-id="69ae2-118">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="69ae2-119">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="69ae2-119">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="69ae2-120">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="69ae2-120">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="69ae2-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="69ae2-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="69ae2-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="69ae2-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="69ae2-123">First, create the resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-123">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="69ae2-124">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span><span class="sxs-lookup"><span data-stu-id="69ae2-124">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="69ae2-125">This next step is optional.</span><span class="sxs-lookup"><span data-stu-id="69ae2-125">This next step is optional.</span></span> <span data-ttu-id="69ae2-126">The default action when you create a VM with the Azure CLI 2.0 is to use Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-126">The default action when you create a VM with the Azure CLI 2.0 is to use Azure Managed Disks.</span></span> <span data-ttu-id="69ae2-127">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69ae2-127">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="69ae2-128">If you instead wish to use unmanaged disks, you need to create a storage account with [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-128">If you instead wish to use unmanaged disks, you need to create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="69ae2-129">The following example creates a storage account named `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="69ae2-129">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="69ae2-130">(The storage account name must be unique, so provide your own unique name.)</span><span class="sxs-lookup"><span data-stu-id="69ae2-130">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westeurope \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="69ae2-131">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-131">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="69ae2-132">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-132">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create --resource-group myResourceGroup --location westeurope --name myVnet \
  --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="69ae2-133">Create a public IP with [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-133">Create a public IP with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="69ae2-134">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="69ae2-134">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="69ae2-135">(The DNS name must be unique, so provide your own unique name.)</span><span class="sxs-lookup"><span data-stu-id="69ae2-135">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
az network public-ip create --resource-group myResourceGroup --location westeurope \
  --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
```

<span data-ttu-id="69ae2-136">Create the load balancer with [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-136">Create the load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="69ae2-137">The following example:</span><span class="sxs-lookup"><span data-stu-id="69ae2-137">The following example:</span></span>

- <span data-ttu-id="69ae2-138">creates a load balancer named `myLoadBalancer`</span><span class="sxs-lookup"><span data-stu-id="69ae2-138">creates a load balancer named `myLoadBalancer`</span></span>
- <span data-ttu-id="69ae2-139">associates the public IP `myPublicIP`</span><span class="sxs-lookup"><span data-stu-id="69ae2-139">associates the public IP `myPublicIP`</span></span>
- <span data-ttu-id="69ae2-140">creates a front-end IP pool named `mySubnetPool`</span><span class="sxs-lookup"><span data-stu-id="69ae2-140">creates a front-end IP pool named `mySubnetPool`</span></span>
- <span data-ttu-id="69ae2-141">creates a back-end IP pool named `myBackEndPool`</span><span class="sxs-lookup"><span data-stu-id="69ae2-141">creates a back-end IP pool named `myBackEndPool`</span></span>

```azurecli
az network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer --public-ip-address myPublicIP \
  --frontend-ip-name myFrontEndPool --backend-pool-name myBackEndPool
```

<span data-ttu-id="69ae2-142">Create SSH inbound network address translation (NAT) rules for the load balancer with [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-142">Create SSH inbound network address translation (NAT) rules for the load balancer with [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#create).</span></span> <span data-ttu-id="69ae2-143">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-143">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
az network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 --protocol tcp \
  --frontend-port 4222 --backend-port 22 --frontend-ip-name myFrontEndPool
az network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22 --frontend-ip-name myFrontEndPool
```

<span data-ttu-id="69ae2-144">Create the load balancer health probe with [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-144">Create the load balancer health probe with [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="69ae2-145">The following example creates a TCP probe named `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-145">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
az network lb probe create --resource-group myResourceGroup --lb-name myLoadBalancer \
  --name myHealthProbe --protocol tcp --port 80 --interval 15 --threshold 4
```

<span data-ttu-id="69ae2-146">Create the web inbound NAT rules for the load balancer with [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-146">Create the web inbound NAT rules for the load balancer with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="69ae2-147">The following example creates a load balancer rule named `myLoadBalancerRuleWeb` and associates it with the `myHealthProbe` probe:</span><span class="sxs-lookup"><span data-stu-id="69ae2-147">The following example creates a load balancer rule named `myLoadBalancerRuleWeb` and associates it with the `myHealthProbe` probe:</span></span>

```azurecli
az network lb rule create --resource-group myResourceGroup --lb-name myLoadBalancer \
  --name myLoadBalancerRuleWeb --protocol tcp --frontend-port 80 --backend-port 80 \
  --frontend-ip-name myFrontEndPool --backend-pool-name myBackEndPool \
  --probe-name myHealthProbe
```

<span data-ttu-id="69ae2-148">Verify the load balancer, IP pools, and NAT rules with [az network lb show](/cli/azure/network/lb#show):</span><span class="sxs-lookup"><span data-stu-id="69ae2-148">Verify the load balancer, IP pools, and NAT rules with [az network lb show](/cli/azure/network/lb#show):</span></span>

```azurecli
az network lb show --resource-group myResourceGroup --name myLoadBalancer
```

<span data-ttu-id="69ae2-149">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-149">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="69ae2-150">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-150">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="69ae2-151">Add two inbound rules for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-151">Add two inbound rules for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="69ae2-152">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-152">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRuleSSH \
  --protocol tcp --direction inbound --priority 1000 --source-address-prefix '*' \
  --source-port-range '*' --destination-address-prefix '*' --destination-port-range 22 \
  --access allow
az network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRuleHTTP \
  --protocol tcp --direction inbound --priority 1001 --source-address-prefix '*' \
  --source-port-range '*' --destination-address-prefix '*' --destination-port-range 80 \
  --access allow
```

<span data-ttu-id="69ae2-153">Create the first network interface card (NIC) with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-153">Create the first network interface card (NIC) with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="69ae2-154">The following example creates a NIC named `myNic1` and attaches it to the load balancer `myLoadBalancer` and appropriate pools, and also attaches it to the `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-154">The following example creates a NIC named `myNic1` and attaches it to the load balancer `myLoadBalancer` and appropriate pools, and also attaches it to the `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nic create --resource-group myResourceGroup --location westeurope --name myNic1 \
  --vnet-name myVnet --subnet mySubnet --network-security-group myNetworkSecurityGroup \
  --lb-name myLoadBalancer --lb-address-pools myBackEndPool \
  --lb-inbound-nat-rules myLoadBalancerRuleSSH1
```

<span data-ttu-id="69ae2-155">Create the second NIC, again with **az network nic create**.</span><span class="sxs-lookup"><span data-stu-id="69ae2-155">Create the second NIC, again with **az network nic create**.</span></span> <span data-ttu-id="69ae2-156">The following example creates a NIC named `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-156">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
az network nic create --resource-group myResourceGroup --location westeurope --name myNic2 \
  --vnet-name myVnet --subnet mySubnet --network-security-group myNetworkSecurityGroup \
  --lb-name myLoadBalancer --lb-address-pools myBackEndPool \
  --lb-inbound-nat-rules myLoadBalancerRuleSSH2
```

<span data-ttu-id="69ae2-157">Create the availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-157">Create the availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="69ae2-158">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-158">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
az vm availability-set create --resource-group myResourceGroup --location westeurope \
  --name myAvailabilitySet \
  --platform-fault-domain-count 3 --platform-update-domain-count 2
```

<span data-ttu-id="69ae2-159">Create the first Linux VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-159">Create the first Linux VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="69ae2-160">The following example creates a VM named `myVM1` using Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-160">The following example creates a VM named `myVM1` using Azure Managed Disks.</span></span> <span data-ttu-id="69ae2-161">If you wish to use unmanaged disks, see the additional note below.</span><span class="sxs-lookup"><span data-stu-id="69ae2-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --availability-set myAvailabilitySet \
    --nics myNic1 \
    --image UbuntuLTS \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="69ae2-162">If you use Azure Managed Disks, skip this step.</span><span class="sxs-lookup"><span data-stu-id="69ae2-162">If you use Azure Managed Disks, skip this step.</span></span> <span data-ttu-id="69ae2-163">If you wish to use unmanaged disks and you created a storage account in the previous steps, you need to add some additional parameters to the proceeding command.</span><span class="sxs-lookup"><span data-stu-id="69ae2-163">If you wish to use unmanaged disks and you created a storage account in the previous steps, you need to add some additional parameters to the proceeding command.</span></span> <span data-ttu-id="69ae2-164">Add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-164">Add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
  --use-unmanaged-disk \
  --storage-account mystorageaccount
```

<span data-ttu-id="69ae2-165">Create the second Linux VM, again with **az vm create**.</span><span class="sxs-lookup"><span data-stu-id="69ae2-165">Create the second Linux VM, again with **az vm create**.</span></span> <span data-ttu-id="69ae2-166">The following example creates a VM named `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-166">The following example creates a VM named `myVM2`:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --availability-set myAvailabilitySet \
    --nics myNic2 \
    --image UbuntuLTS \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="69ae2-167">Again, if you do not use the default Azure Managed Disks, add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-167">Again, if you do not use the default Azure Managed Disks, add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span></span>

```azurecli
  --use-unmanaged-disk \
  --storage-account mystorageaccount
``` 

<span data-ttu-id="69ae2-168">Verify that everything that was built correctly with [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="69ae2-168">Verify that everything that was built correctly with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM1
az vm show --resource-group myResourceGroup --name myVM2
```

<span data-ttu-id="69ae2-169">Export your new environment to a template with [az group export](/cli/azure/group#export) to quickly re-create new instances:</span><span class="sxs-lookup"><span data-stu-id="69ae2-169">Export your new environment to a template with [az group export](/cli/azure/group#export) to quickly re-create new instances:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="69ae2-170">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="69ae2-170">Detailed walkthrough</span></span>
<span data-ttu-id="69ae2-171">The detailed steps that follow explain what each command is doing as you build out your environment.</span><span class="sxs-lookup"><span data-stu-id="69ae2-171">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="69ae2-172">These concepts are helpful when you build your own custom environments for development or production.</span><span class="sxs-lookup"><span data-stu-id="69ae2-172">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="69ae2-173">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="69ae2-173">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="69ae2-174">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="69ae2-174">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="69ae2-175">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="69ae2-175">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="69ae2-176">Create resource groups and choose deployment locations</span><span class="sxs-lookup"><span data-stu-id="69ae2-176">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="69ae2-177">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span><span class="sxs-lookup"><span data-stu-id="69ae2-177">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="69ae2-178">Create the resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-178">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="69ae2-179">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span><span class="sxs-lookup"><span data-stu-id="69ae2-179">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="69ae2-180">By default, the output is in JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="69ae2-180">By default, the output is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="69ae2-181">To output as a list or table, for example, use [az configure --output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="69ae2-181">To output as a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="69ae2-182">You can also add `--output` to any command for a one time change in output format.</span><span class="sxs-lookup"><span data-stu-id="69ae2-182">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="69ae2-183">The following example shows the JSON output from the **az group create** command:</span><span class="sxs-lookup"><span data-stu-id="69ae2-183">The following example shows the JSON output from the **az group create** command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-storage-account"></a><span data-ttu-id="69ae2-184">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="69ae2-184">Create a storage account</span></span>
<span data-ttu-id="69ae2-185">This next step is optional.</span><span class="sxs-lookup"><span data-stu-id="69ae2-185">This next step is optional.</span></span> <span data-ttu-id="69ae2-186">The default action when you create a VM with the Azure CLI 2.0 is to use Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-186">The default action when you create a VM with the Azure CLI 2.0 is to use Azure Managed Disks.</span></span> <span data-ttu-id="69ae2-187">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="69ae2-187">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="69ae2-188">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69ae2-188">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="69ae2-189">Skip to [Create a virtual network and subnet](#create-a-virtual-network-and-subnet) if you wish to use Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-189">Skip to [Create a virtual network and subnet](#create-a-virtual-network-and-subnet) if you wish to use Azure Managed Disks.</span></span> 

<span data-ttu-id="69ae2-190">If you wish to use unmanaged disks, you need to create a storage account for your VM disks and for any additional data disks that you want to add.</span><span class="sxs-lookup"><span data-stu-id="69ae2-190">If you wish to use unmanaged disks, you need to create a storage account for your VM disks and for any additional data disks that you want to add.</span></span>

<span data-ttu-id="69ae2-191">Here we use [az storage account create](/cli/azure/storage/account#create), and pass the location of the account, the resource group that controls it, and the type of storage support you want.</span><span class="sxs-lookup"><span data-stu-id="69ae2-191">Here we use [az storage account create](/cli/azure/storage/account#create), and pass the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="69ae2-192">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-192">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westeurope \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="69ae2-193">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-193">Output:</span></span>

```json
{
  "accessTier": null,
  "creationTime": "2016-12-07T17:59:50.090092+00:00",
  "customDomain": null,
  "encryption": null,
  "id": "/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
  "kind": "Storage",
  "lastGeoFailoverTime": null,
  "location": "westeurope",
  "name": "mystorageaccount",
  "primaryEndpoints": {
    "blob": "https://mystorageaccount.blob.core.windows.net/",
    "file": "https://mystorageaccount.file.core.windows.net/",
    "queue": "https://mystorageaccount.queue.core.windows.net/",
    "table": "https://mystorageaccount.table.core.windows.net/"
  },
  "primaryLocation": "westeurope",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "secondaryEndpoints": null,
  "secondaryLocation": null,
  "sku": {
    "name": "Standard_LRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "Available",
  "statusOfSecondary": null,
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="69ae2-194">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span><span class="sxs-lookup"><span data-stu-id="69ae2-194">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="69ae2-195">Use [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string).</span><span class="sxs-lookup"><span data-stu-id="69ae2-195">Use [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string).</span></span> <span data-ttu-id="69ae2-196">Replace the name of the storage account in the following example with a name that you choose:</span><span class="sxs-lookup"><span data-stu-id="69ae2-196">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(az storage account show-connection-string --resource-group myResourceGroup --name mystorageaccount --query connectionString)"
```

<span data-ttu-id="69ae2-197">Then you can view your storage information with [az storage container list](/cli/azure/storage/container#list):</span><span class="sxs-lookup"><span data-stu-id="69ae2-197">Then you can view your storage information with [az storage container list](/cli/azure/storage/container#list):</span></span>

```azurecli
az storage container list
```

<span data-ttu-id="69ae2-198">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-198">Output:</span></span>

```azurecli
[
  {
    "metadata": null,
    "name": "vhds",
    "properties": {
      "etag": "\"0x8D41F912D472F94\"",
      "lastModified": "2016-12-08T17:39:35+00:00",
      "lease": {
        "duration": null,
        "state": null,
        "status": null
      },
      "leaseDuration": "infinite",
      "leaseState": "leased",
      "leaseStatus": "locked"
    }
  }
]
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="69ae2-199">Create a virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="69ae2-199">Create a virtual network and subnet</span></span>
<span data-ttu-id="69ae2-200">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-200">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="69ae2-201">The following example uses [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named `myVnet` with the `192.168.0.0/16` address prefix, and a subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-201">The following example uses [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named `myVnet` with the `192.168.0.0/16` address prefix, and a subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
az network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefix 192.168.0.0/16 \
  --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="69ae2-202">Output shows the subnet as logically created inside the virtual network:</span><span class="sxs-lookup"><span data-stu-id="69ae2-202">Output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "westeurope",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="69ae2-203">Create a public IP address</span><span class="sxs-lookup"><span data-stu-id="69ae2-203">Create a public IP address</span></span>
<span data-ttu-id="69ae2-204">Now let's create the public IP address (PIP) that we assign to your load balancer.</span><span class="sxs-lookup"><span data-stu-id="69ae2-204">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="69ae2-205">It enables you to connect to your VMs from the Internet by using the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span><span class="sxs-lookup"><span data-stu-id="69ae2-205">It enables you to connect to your VMs from the Internet by using the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="69ae2-206">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span><span class="sxs-lookup"><span data-stu-id="69ae2-206">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="69ae2-207">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="69ae2-207">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="69ae2-208">Because the DNS name must be unique, you provide your own unique DNS name:</span><span class="sxs-lookup"><span data-stu-id="69ae2-208">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create --resource-group myResourceGroup --location westeurope \
  --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
```

<span data-ttu-id="69ae2-209">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-209">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.westeurope.cloudapp.azure.com",
      "reverseFqdn": ""
    },
    "idleTimeoutInMinutes": 4,
    "ipAddress": "52.174.48.109",
    "provisioningState": "Succeeded",
    "publicIPAllocationMethod": "Static",
    "resourceGuid": "78218510-ea54-42d7-b2c2-44773fc14af5"
  }
}
```

<span data-ttu-id="69ae2-210">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span><span class="sxs-lookup"><span data-stu-id="69ae2-210">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="69ae2-211">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span><span class="sxs-lookup"><span data-stu-id="69ae2-211">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="69ae2-212">Create a load balancer and IP pools</span><span class="sxs-lookup"><span data-stu-id="69ae2-212">Create a load balancer and IP pools</span></span>
<span data-ttu-id="69ae2-213">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-213">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="69ae2-214">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span><span class="sxs-lookup"><span data-stu-id="69ae2-214">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="69ae2-215">The following example uses [az network lb create](/cli/azure/network/lb#create) to create a load balancer named `myLoadBalancer`, a front-end IP pool named `myFrontEndPool`, and hooks up the `myPublicIP` resource:</span><span class="sxs-lookup"><span data-stu-id="69ae2-215">The following example uses [az network lb create](/cli/azure/network/lb#create) to create a load balancer named `myLoadBalancer`, a front-end IP pool named `myFrontEndPool`, and hooks up the `myPublicIP` resource:</span></span>

```azurecli
az network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer --public-ip-address myPublicIP --frontend-ip-name myFrontEndPool
```

<span data-ttu-id="69ae2-216">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-216">Output:</span></span>

```json
{
  "loadBalancer": {
    "backendAddressPools": [
      {
        "etag": "W/\"7a05df7a-5ee2-4581-b411-4b6f048ab291\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myLoadBalancerbepool",
        "name": "myLoadBalancerbepool",
        "properties": {
          "provisioningState": "Succeeded"
        },
        "resourceGroup": "myResourceGroup"
      }
    ],
    "frontendIPConfigurations": [
      {
        "etag": "W/\"7a05df7a-5ee2-4581-b411-4b6f048ab291\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/frontendIPConfigurations/myFrontEndPool",
        "name": "myFrontEndPool",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "provisioningState": "Succeeded",
          "publicIPAddress": {
            "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
            "resourceGroup": "myResourceGroup"
          }
        },
        "resourceGroup": "myResourceGroup"
      }
    ],
    "inboundNatPools": [],
    "inboundNatRules": [],
    "loadBalancingRules": [],
    "outboundNatRules": [],
    "probes": [],
    "provisioningState": "Succeeded",
    "resourceGuid": "f4879d84-5ae8-4e06-8b9b-1419baa875d9"
  }
}
```

<span data-ttu-id="69ae2-217">Note how we used the `--public-ip-address` switch to pass in the `myPublicIP` that we created earlier.</span><span class="sxs-lookup"><span data-stu-id="69ae2-217">Note how we used the `--public-ip-address` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="69ae2-218">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span><span class="sxs-lookup"><span data-stu-id="69ae2-218">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="69ae2-219">We use a back-end pool as a location for our VMs to connect to.</span><span class="sxs-lookup"><span data-stu-id="69ae2-219">We use a back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="69ae2-220">That way, the traffic can flow through the load balancer to the VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-220">That way, the traffic can flow through the load balancer to the VMs.</span></span> <span data-ttu-id="69ae2-221">Let's create the IP pool for our back-end traffic with [az network lb address-pool create](/cli/azure/network/lb/address-pool#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-221">Let's create the IP pool for our back-end traffic with [az network lb address-pool create](/cli/azure/network/lb/address-pool#create).</span></span> <span data-ttu-id="69ae2-222">The following example creates a back-end pool named `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-222">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
az network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="69ae2-223">Snipped output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-223">Snipped output:</span></span>

```json
  "backendAddressPools": [
    {
      "backendIpConfigurations": null,
      "etag": "W/\"a61814bc-ce4c-4fb2-9d6a-5b1949078345\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myLoadBalancerbepool",
      "loadBalancingRules": null,
      "name": "myLoadBalancerbepool",
      "outboundNatRule": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup"
    },
    {
      "backendIpConfigurations": null,
      "etag": "W/\"a61814bc-ce4c-4fb2-9d6a-5b1949078345\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool",
      "loadBalancingRules": null,
      "name": "myBackEndPool",
      "outboundNatRule": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup"
    }
  ],
  "etag": "W/\"a61814bc-ce4c-4fb2-9d6a-5b1949078345\"",
```


## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="69ae2-224">Create load balancer NAT rules</span><span class="sxs-lookup"><span data-stu-id="69ae2-224">Create load balancer NAT rules</span></span>
<span data-ttu-id="69ae2-225">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span><span class="sxs-lookup"><span data-stu-id="69ae2-225">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="69ae2-226">You can specify the protocol to use, then map external ports to internal ports as desired.</span><span class="sxs-lookup"><span data-stu-id="69ae2-226">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="69ae2-227">For our environment, let's create some rules that allow SSH through our load balancer to our VMs with [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-227">For our environment, let's create some rules that allow SSH through our load balancer to our VMs with [az network lb inbound-nat-rule create](/cli/azure/network/lb/inbound-nat-rule#create).</span></span> <span data-ttu-id="69ae2-228">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span><span class="sxs-lookup"><span data-stu-id="69ae2-228">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="69ae2-229">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span><span class="sxs-lookup"><span data-stu-id="69ae2-229">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
az network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 --protocol tcp \
  --frontend-port 4222 --backend-port 22 --frontend-ip-name myFrontEndPool
```

<span data-ttu-id="69ae2-230">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-230">Output:</span></span>

```json
{
  "backendIpConfiguration": null,
  "backendPort": 22,
  "enableFloatingIp": false,
  "etag": "W/\"72843cf8-b5fb-4655-9ac8-9cbbbbf1205a\"",
  "frontendIpConfiguration": {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/frontendIPConfigurations/myFrontEndPool",
    "resourceGroup": "myResourceGroup"
  },
  "frontendPort": 4222,
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
  "idleTimeoutInMinutes": 4,
  "name": "myLoadBalancerRuleSSH1",
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="69ae2-231">Repeat the procedure for your second NAT rule for SSH.</span><span class="sxs-lookup"><span data-stu-id="69ae2-231">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="69ae2-232">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span><span class="sxs-lookup"><span data-stu-id="69ae2-232">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
az network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22 --frontend-ip-name myFrontEndPool
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="69ae2-233">Create a load balancer health probe</span><span class="sxs-lookup"><span data-stu-id="69ae2-233">Create a load balancer health probe</span></span>
<span data-ttu-id="69ae2-234">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span><span class="sxs-lookup"><span data-stu-id="69ae2-234">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="69ae2-235">If not, they're removed from operation to ensure that users aren't being directed to them.</span><span class="sxs-lookup"><span data-stu-id="69ae2-235">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="69ae2-236">You can define custom checks for the health probe, along with intervals and timeout values.</span><span class="sxs-lookup"><span data-stu-id="69ae2-236">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="69ae2-237">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-237">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="69ae2-238">The following example uses [az network lb probe create](/cli/azure/network/lb/probe#create) to create a TCP health probed named `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-238">The following example uses [az network lb probe create](/cli/azure/network/lb/probe#create) to create a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
az network lb probe create --resource-group myResourceGroup --lb-name myLoadBalancer \
  --name myHealthProbe --protocol tcp --port 80 --interval 15 --threshold 4
```

<span data-ttu-id="69ae2-239">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-239">Output:</span></span>

```json
{
  "etag": "W/\"757018f6-b70a-4651-b717-48b511d82ba0\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe",
  "intervalInSeconds": 15,
  "loadBalancingRules": null,
  "name": "myHealthProbe",
  "numberOfProbes": 4,
  "port": 80,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "requestPath": null,
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="69ae2-240">Here, we specified an interval of 15 seconds for our health checks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-240">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="69ae2-241">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span><span class="sxs-lookup"><span data-stu-id="69ae2-241">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

<span data-ttu-id="69ae2-242">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span><span class="sxs-lookup"><span data-stu-id="69ae2-242">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="69ae2-243">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span><span class="sxs-lookup"><span data-stu-id="69ae2-243">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="69ae2-244">The load balancer automatically adjusts the flow of traffic.</span><span class="sxs-lookup"><span data-stu-id="69ae2-244">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="69ae2-245">The following example uses [az network lb rule create](/cli/azure/network/lb/rule#create) to create a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80, and hooks up the health probe named `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-245">The following example uses [az network lb rule create](/cli/azure/network/lb/rule#create) to create a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80, and hooks up the health probe named `myHealthProbe`:</span></span>

```azurecli
az network lb rule create --resource-group myResourceGroup --lb-name myLoadBalancer \
  --name myLoadBalancerRuleWeb --protocol tcp --frontend-port 80 --backend-port 80 \
  --frontend-ip-name myFrontEndPool --backend-pool-name myBackEndPool \
  --probe-name myHealthProbe
```

<span data-ttu-id="69ae2-246">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-246">Output:</span></span>

```json
{
  "backendAddressPool": {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool",
    "resourceGroup": "myResourceGroup"
  },
  "backendPort": 80,
  "enableFloatingIp": false,
  "etag": "W/\"f0d77680-bf42-4d11-bfab-5d2c541bee56\"",
  "frontendIpConfiguration": {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/frontendIPConfigurations/myFrontEndPool",
    "resourceGroup": "myResourceGroup"
  },
  "frontendPort": 80,
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
  "idleTimeoutInMinutes": 4,
  "loadDistribution": "Default",
  "name": "myLoadBalancerRuleWeb",
  "probe": {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe",
    "resourceGroup": "myResourceGroup"
  },
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="verify-the-load-balancer"></a><span data-ttu-id="69ae2-247">Verify the load balancer</span><span class="sxs-lookup"><span data-stu-id="69ae2-247">Verify the load balancer</span></span>
<span data-ttu-id="69ae2-248">Now the load balancer configuration is done.</span><span class="sxs-lookup"><span data-stu-id="69ae2-248">Now the load balancer configuration is done.</span></span> <span data-ttu-id="69ae2-249">Here are the steps you took:</span><span class="sxs-lookup"><span data-stu-id="69ae2-249">Here are the steps you took:</span></span>

1. <span data-ttu-id="69ae2-250">You created a load balancer.</span><span class="sxs-lookup"><span data-stu-id="69ae2-250">You created a load balancer.</span></span>
2. <span data-ttu-id="69ae2-251">You created a front-end IP pool and assigned a public IP to it.</span><span class="sxs-lookup"><span data-stu-id="69ae2-251">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="69ae2-252">You created a back-end IP pool that VMs can connect to.</span><span class="sxs-lookup"><span data-stu-id="69ae2-252">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="69ae2-253">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span><span class="sxs-lookup"><span data-stu-id="69ae2-253">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="69ae2-254">You added a health probe to periodically check the VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-254">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="69ae2-255">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span><span class="sxs-lookup"><span data-stu-id="69ae2-255">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="69ae2-256">Let's review what your load balancer looks like now with [az network lb show](/cli/azure/network/lb#show) :</span><span class="sxs-lookup"><span data-stu-id="69ae2-256">Let's review what your load balancer looks like now with [az network lb show](/cli/azure/network/lb#show) :</span></span>

```azurecli
az network lb show --resource-group myResourceGroup --name myLoadBalancer
```

<span data-ttu-id="69ae2-257">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-257">Output:</span></span>

```json
{
  "backendAddressPools": [
    {
      "backendIpConfigurations": null,
      "etag": "W/\"a0e313a1-6de1-48be-aeb6-df57188d708c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myLoadBalancerbepool",
      "loadBalancingRules": null,
      "name": "myLoadBalancerbepool",
      "outboundNatRule": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup"
    },
    {
      "backendIpConfigurations": null,
      "etag": "W/\"a0e313a1-6de1-48be-aeb6-df57188d708c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool",
      "loadBalancingRules": null,
      "name": "myBackEndPool",
      "outboundNatRule": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup"
    }
  ],
  "etag": "W/\"a0e313a1-6de1-48be-aeb6-df57188d708c\"",
  "frontendIpConfigurations": [
    {
      "etag": "W/\"a0e313a1-6de1-48be-aeb6-df57188d708c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/frontendIPConfigurations/LoadBalancerFrontEnd",
      "inboundNatPools": null,
      "inboundNatRules": null,
      "loadBalancingRules": null,
      "name": "LoadBalancerFrontEnd",
      "outboundNatRules": null,
      "privateIpAddress": null,
      "privateIpAllocationMethod": "Dynamic",
      "provisioningState": "Succeeded",
      "publicIpAddress": {
        "dnsSettings": null,
        "etag": null,
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/PublicIPmyLoadBalancer",
        "idleTimeoutInMinutes": null,
        "ipAddress": null,
        "ipConfiguration": null,
        "location": null,
        "name": null,
        "provisioningState": null,
        "publicIpAddressVersion": null,
        "publicIpAllocationMethod": null,
        "resourceGroup": "myResourceGroup",
        "resourceGuid": null,
        "tags": null,
        "type": null
      },
      "resourceGroup": "myResourceGroup",
      "subnet": null
    },
    {
      "etag": "W/\"a0e313a1-6de1-48be-aeb6-df57188d708c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/frontendIPConfigurations/myFrontEndPool",
      "inboundNatPools": null,
      "inboundNatRules": null,
      "loadBalancingRules": null,
      "name": "myFrontEndPool",
      "outboundNatRules": null,
      "privateIpAddress": null,
      "privateIpAllocationMethod": "Dynamic",
      "provisioningState": "Succeeded",
      "publicIpAddress": {
        "dnsSettings": null,
        "etag": null,
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
        "idleTimeoutInMinutes": null,
        "ipAddress": null,
        "ipConfiguration": null,
        "location": null,
        "name": null,
        "provisioningState": null,
        "publicIpAddressVersion": null,
        "publicIpAllocationMethod": null,
        "resourceGroup": "myResourceGroup",
        "resourceGuid": null,
        "tags": null,
        "type": null
      },
      "resourceGroup": "myResourceGroup",
      "subnet": null
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "inboundNatPools": [],
  "inboundNatRules": [],
  "loadBalancingRules": [],
  "location": "westeurope",
  "name": "myLoadBalancer",
  "outboundNatRules": [],
  "probes": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "b5815801-b53d-4c22-aafc-2a9064f90f3c",
  "tags": {},
  "type": "Microsoft.Network/loadBalancers"
}
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="69ae2-258">Create a network security group and rules</span><span class="sxs-lookup"><span data-stu-id="69ae2-258">Create a network security group and rules</span></span>
<span data-ttu-id="69ae2-259">Now we create a network security group and the inbound rules that govern access to the NIC.</span><span class="sxs-lookup"><span data-stu-id="69ae2-259">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="69ae2-260">A network security group can be applied to a NIC or subnet.</span><span class="sxs-lookup"><span data-stu-id="69ae2-260">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="69ae2-261">You define rules to control the flow of traffic in and out of your VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-261">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="69ae2-262">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-262">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="69ae2-263">Let's add the inbound rule for the NSG with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow inbound connections on port 22 (to support SSH).</span><span class="sxs-lookup"><span data-stu-id="69ae2-263">Let's add the inbound rule for the NSG with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="69ae2-264">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span><span class="sxs-lookup"><span data-stu-id="69ae2-264">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRuleSSH \
  --protocol tcp --direction inbound --priority 1000 \
  --source-address-prefix '*' --source-port-range '*' \
  --destination-address-prefix '*' --destination-port-range 22 --access allow
```

<span data-ttu-id="69ae2-265">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span><span class="sxs-lookup"><span data-stu-id="69ae2-265">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="69ae2-266">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span><span class="sxs-lookup"><span data-stu-id="69ae2-266">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --name myNetworkSecurityGroupRuleHTTP \
  --protocol tcp --direction inbound --priority 1001 \
  --source-address-prefix '*' --source-port-range '*' \
  --destination-address-prefix '*' --destination-port-range 80 --access allow
```

> [!NOTE]
> <span data-ttu-id="69ae2-267">The inbound rule is a filter for inbound network connections.</span><span class="sxs-lookup"><span data-stu-id="69ae2-267">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="69ae2-268">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span><span class="sxs-lookup"><span data-stu-id="69ae2-268">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="69ae2-269">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span><span class="sxs-lookup"><span data-stu-id="69ae2-269">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="69ae2-270">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span><span class="sxs-lookup"><span data-stu-id="69ae2-270">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="69ae2-271">Ports are typically dynamic.</span><span class="sxs-lookup"><span data-stu-id="69ae2-271">Ports are typically dynamic.</span></span>

<span data-ttu-id="69ae2-272">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="69ae2-272">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="69ae2-273">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-273">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBound",
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "westeurope",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "79c2c293-ee3e-4616-bf9c-4741ff1f708a",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"2b656589-f332-4ba4-92f3-afb3be5c192c\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleHTTP",
      "name": "myNetworkSecurityGroupRuleHTTP",
      "priority": 1001,
      "protocol": "tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": {},
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="69ae2-274">Create an NIC to use with the Linux VM</span><span class="sxs-lookup"><span data-stu-id="69ae2-274">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="69ae2-275">NICs are programmatically available because you can apply rules to their use.</span><span class="sxs-lookup"><span data-stu-id="69ae2-275">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="69ae2-276">You can also have more than one.</span><span class="sxs-lookup"><span data-stu-id="69ae2-276">You can also have more than one.</span></span> <span data-ttu-id="69ae2-277">In the following [az network nic create](https://docs.microsoft.com/en-us/cli/azure/network/nic#create) command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic and network security group.</span><span class="sxs-lookup"><span data-stu-id="69ae2-277">In the following [az network nic create](https://docs.microsoft.com/en-us/cli/azure/network/nic#create) command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic and network security group.</span></span>

<span data-ttu-id="69ae2-278">The following example creates a NIC named `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-278">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
az network nic create --resource-group myResourceGroup --location westeurope --name myNic1 \
  --vnet-name myVnet --subnet mySubnet --network-security-group myNetworkSecurityGroup \
  --lb-name myLoadBalancer --lb-address-pools myBackEndPool \
  --lb-inbound-nat-rules myLoadBalancerRuleSSH1
```

<span data-ttu-id="69ae2-279">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-279">Output:</span></span>

```json
{
  "newNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": []
    },
    "enableIPForwarding": false,
    "ipConfigurations": [
      {
        "etag": "W/\"a76b5c0d-14e1-4a99-afd4-5cd8ac0465ca\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/ipconfig1",
        "name": "ipconfig1",
        "properties": {
          "loadBalancerBackendAddressPools": [
            {
              "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool",
              "resourceGroup": "myResourceGroup"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
              "resourceGroup": "myResourceGroup"
            }
          ],
          "primary": true,
          "privateIPAddress": "192.168.1.4",
          "privateIPAllocationMethod": "Dynamic",
          "provisioningState": "Succeeded",
          "subnet": {
            "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
            "resourceGroup": "myResourceGroup"
          }
        },
        "resourceGroup": "myResourceGroup"
      }
    ],
    "networkSecurityGroup": {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "resourceGroup": "myResourceGroup"
    },
    "provisioningState": "Succeeded",
    "resourceGuid": "838977cb-cf4b-4c4a-9a32-0ddec7dc818b"
  }
}
```

<span data-ttu-id="69ae2-280">Now we create the second NIC, hooking in to our back-end IP pool again.</span><span class="sxs-lookup"><span data-stu-id="69ae2-280">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="69ae2-281">This time the second NAT rule permits SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="69ae2-281">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="69ae2-282">The following example creates a NIC named `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-282">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
az network nic create --resource-group myResourceGroup --location westeurope --name myNic2 \
  --vnet-name myVnet --subnet mySubnet --network-security-group myNetworkSecurityGroup \
  --lb-name myLoadBalancer --lb-address-pools myBackEndPool \
  --lb-inbound-nat-rules myLoadBalancerRuleSSH2
```


## <a name="create-an-availability-set"></a><span data-ttu-id="69ae2-283">Create an availability set</span><span class="sxs-lookup"><span data-stu-id="69ae2-283">Create an availability set</span></span>
<span data-ttu-id="69ae2-284">Availability sets help spread your VMs across fault domains and upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="69ae2-284">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="69ae2-285">Let's create an availability set for your VMs with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="69ae2-285">Let's create an availability set for your VMs with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="69ae2-286">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-286">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
az vm availability-set create --resource-group myResourceGroup --location westeurope \
  --name myAvailabilitySet \
  --platform-fault-domain-count 3 --platform-update-domain-count 2
```

<span data-ttu-id="69ae2-287">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span><span class="sxs-lookup"><span data-stu-id="69ae2-287">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="69ae2-288">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span><span class="sxs-lookup"><span data-stu-id="69ae2-288">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="69ae2-289">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span><span class="sxs-lookup"><span data-stu-id="69ae2-289">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="69ae2-290">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span><span class="sxs-lookup"><span data-stu-id="69ae2-290">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="69ae2-291">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span><span class="sxs-lookup"><span data-stu-id="69ae2-291">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="69ae2-292">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span><span class="sxs-lookup"><span data-stu-id="69ae2-292">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="69ae2-293">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span><span class="sxs-lookup"><span data-stu-id="69ae2-293">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="69ae2-294">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-294">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-the-linux-vms"></a><span data-ttu-id="69ae2-295">Create the Linux VMs</span><span class="sxs-lookup"><span data-stu-id="69ae2-295">Create the Linux VMs</span></span>
<span data-ttu-id="69ae2-296">You've created the network resources to support Internet-accessible VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-296">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="69ae2-297">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span><span class="sxs-lookup"><span data-stu-id="69ae2-297">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="69ae2-298">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span><span class="sxs-lookup"><span data-stu-id="69ae2-298">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="69ae2-299">We locate that image information by using [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-299">We locate that image information by using [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="69ae2-300">We also specify an SSH key to use for authentication.</span><span class="sxs-lookup"><span data-stu-id="69ae2-300">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="69ae2-301">If you do not have any SSH keys, you can create them by using [these instructions](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-301">If you do not have any SSH keys, you can create them by using [these instructions](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="69ae2-302">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span><span class="sxs-lookup"><span data-stu-id="69ae2-302">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="69ae2-303">This method is typically less secure.</span><span class="sxs-lookup"><span data-stu-id="69ae2-303">This method is typically less secure.</span></span>

<span data-ttu-id="69ae2-304">We create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span><span class="sxs-lookup"><span data-stu-id="69ae2-304">We create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="69ae2-305">The following example creates a VM named `myVM1` using Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="69ae2-305">The following example creates a VM named `myVM1` using Azure Managed Disks.</span></span> <span data-ttu-id="69ae2-306">If you wish to use unmanaged disks, see the additional note below.</span><span class="sxs-lookup"><span data-stu-id="69ae2-306">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --availability-set myAvailabilitySet \
    --nics myNic1 \
    --image UbuntuLTS \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="69ae2-307">If you use Azure Managed Disks, skip this step.</span><span class="sxs-lookup"><span data-stu-id="69ae2-307">If you use Azure Managed Disks, skip this step.</span></span> <span data-ttu-id="69ae2-308">If you wish to use unmanaged disks and you created a storage account in the previous steps, you need to add some additional parameters to the proceeding command.</span><span class="sxs-lookup"><span data-stu-id="69ae2-308">If you wish to use unmanaged disks and you created a storage account in the previous steps, you need to add some additional parameters to the proceeding command.</span></span> <span data-ttu-id="69ae2-309">Add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-309">Add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
  --use-unmanaged-disk \
  --storage-account mystorageaccount
```

<span data-ttu-id="69ae2-310">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-310">Output:</span></span>

```json
{
  "fqdn": "",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1",
  "macAddress": "",
  "privateIpAddress": "",
  "publicIpAddress": "",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="69ae2-311">You can connect to your VM immediately by using your default SSH keys.</span><span class="sxs-lookup"><span data-stu-id="69ae2-311">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="69ae2-312">Make sure that you specify the appropriate port since we're passing through the load balancer.</span><span class="sxs-lookup"><span data-stu-id="69ae2-312">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="69ae2-313">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span><span class="sxs-lookup"><span data-stu-id="69ae2-313">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222 -i ~/.ssh/id_rsa.pub
```

<span data-ttu-id="69ae2-314">Output:</span><span class="sxs-lookup"><span data-stu-id="69ae2-314">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="69ae2-315">Go ahead and create your second VM in the same manner:</span><span class="sxs-lookup"><span data-stu-id="69ae2-315">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --availability-set myAvailabilitySet \
    --nics myNic2 \
    --image UbuntuLTS \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="69ae2-316">Again, if you do not use the default Azure Managed Disks, add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="69ae2-316">Again, if you do not use the default Azure Managed Disks, add the following additional parameters to the proceeding command to create the unmanaged disks in the storage account named `mystorageaccount`:</span></span>

```azurecli
  --use-unmanaged-disk \
  --storage-account mystorageaccount
``` 

<span data-ttu-id="69ae2-317">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span><span class="sxs-lookup"><span data-stu-id="69ae2-317">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="69ae2-318">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-318">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="69ae2-319">Export the environment as a template</span><span class="sxs-lookup"><span data-stu-id="69ae2-319">Export the environment as a template</span></span>
<span data-ttu-id="69ae2-320">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span><span class="sxs-lookup"><span data-stu-id="69ae2-320">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="69ae2-321">Resource Manager uses JSON templates that define all the parameters for your environment.</span><span class="sxs-lookup"><span data-stu-id="69ae2-321">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="69ae2-322">You build out entire environments by referencing this JSON template.</span><span class="sxs-lookup"><span data-stu-id="69ae2-322">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="69ae2-323">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span><span class="sxs-lookup"><span data-stu-id="69ae2-323">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="69ae2-324">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span><span class="sxs-lookup"><span data-stu-id="69ae2-324">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="69ae2-325">This command creates the `myResourceGroup.json` file in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="69ae2-325">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="69ae2-326">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-326">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="69ae2-327">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the **az group export** command that was shown earlier.</span><span class="sxs-lookup"><span data-stu-id="69ae2-327">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the **az group export** command that was shown earlier.</span></span> <span data-ttu-id="69ae2-328">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span><span class="sxs-lookup"><span data-stu-id="69ae2-328">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="69ae2-329">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span><span class="sxs-lookup"><span data-stu-id="69ae2-329">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="69ae2-330">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69ae2-330">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="69ae2-331">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span><span class="sxs-lookup"><span data-stu-id="69ae2-331">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69ae2-332">Next steps</span><span class="sxs-lookup"><span data-stu-id="69ae2-332">Next steps</span></span>
<span data-ttu-id="69ae2-333">Now you're ready to begin working with multiple networking components and VMs.</span><span class="sxs-lookup"><span data-stu-id="69ae2-333">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="69ae2-334">You can use this sample environment to build out your application by using the core components introduced here.</span><span class="sxs-lookup"><span data-stu-id="69ae2-334">You can use this sample environment to build out your application by using the core components introduced here.</span></span>

