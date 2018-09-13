---
title: Load balance zone-redundant VMs using Azure CLI | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zone redundant frontend using Azure CLI
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/09/2018
ms.author: kumud
ms.openlocfilehash: dbefe5324acb699abb0e06b8f3f464a91a6fa2e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871039"
---
#  <a name="load-balance-vms-across-all-availability-zones-using-azure-cli"></a><span data-ttu-id="58d66-103">Load balance VMs across all availability zones using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="58d66-103">Load balance VMs across all availability zones using Azure CLI</span></span>

<span data-ttu-id="58d66-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend to achieve zone-redundancy without dependency on multiple DNS records.</span><span class="sxs-lookup"><span data-stu-id="58d66-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zone-redundant frontend to achieve zone-redundancy without dependency on multiple DNS records.</span></span> <span data-ttu-id="58d66-105">A single front-end IP address is automatically zone-redundant.</span><span class="sxs-lookup"><span data-stu-id="58d66-105">A single front-end IP address is automatically zone-redundant.</span></span>  <span data-ttu-id="58d66-106">Using a zone redundant frontend for your load balancer, with a single IP address you can now reach any VM in a virtual network within a region that is across all Availability Zones.</span><span class="sxs-lookup"><span data-stu-id="58d66-106">Using a zone redundant frontend for your load balancer, with a single IP address you can now reach any VM in a virtual network within a region that is across all Availability Zones.</span></span> <span data-ttu-id="58d66-107">Use availability zones to protect your apps and data from an unlikely failure or loss of an entire datacenter.</span><span class="sxs-lookup"><span data-stu-id="58d66-107">Use availability zones to protect your apps and data from an unlikely failure or loss of an entire datacenter.</span></span>

<span data-ttu-id="58d66-108">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="58d66-108">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span></span>

<span data-ttu-id="58d66-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="58d66-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)] 

<span data-ttu-id="58d66-110">If you choose to install and use the CLI locally, this tutorial requires that you are running Azure CLI version 2.0.17 or higher.</span><span class="sxs-lookup"><span data-stu-id="58d66-110">If you choose to install and use the CLI locally, this tutorial requires that you are running Azure CLI version 2.0.17 or higher.</span></span>  <span data-ttu-id="58d66-111">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="58d66-111">To find the version, run `az --version`.</span></span> <span data-ttu-id="58d66-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="58d66-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="58d66-113">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="58d66-113">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="58d66-114">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="58d66-114">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="58d66-115">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58d66-115">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>  

## <a name="create-a-resource-group"></a><span data-ttu-id="58d66-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="58d66-116">Create a resource group</span></span>

<span data-ttu-id="58d66-117">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-117">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span></span> <span data-ttu-id="58d66-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="58d66-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="58d66-119">The following example creates a resource group named *myResourceGroupSLB* in the *westeurope* location:</span><span class="sxs-lookup"><span data-stu-id="58d66-119">The following example creates a resource group named *myResourceGroupSLB* in the *westeurope* location:</span></span>

```azurecli-interactive
az group create \
--name myResourceGroupSLB \
--location westeurope
```

## <a name="create-a-zone-redundant-public-ip-standard"></a><span data-ttu-id="58d66-120">Create a zone redundant public IP Standard</span><span class="sxs-lookup"><span data-stu-id="58d66-120">Create a zone redundant public IP Standard</span></span>
<span data-ttu-id="58d66-121">To access your app on the Internet, you need a public IP address for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="58d66-121">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="58d66-122">A zone-redundant front-end is served by all availability zones in a region simultaneously.</span><span class="sxs-lookup"><span data-stu-id="58d66-122">A zone-redundant front-end is served by all availability zones in a region simultaneously.</span></span> <span data-ttu-id="58d66-123">Create a zone redundant public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="58d66-123">Create a zone redundant public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="58d66-124">When you create a Standard Public  IP address, it is zone redundant by default.</span><span class="sxs-lookup"><span data-stu-id="58d66-124">When you create a Standard Public  IP address, it is zone redundant by default.</span></span>

<span data-ttu-id="58d66-125">The following example creates a zone redundant public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group.</span><span class="sxs-lookup"><span data-stu-id="58d66-125">The following example creates a zone redundant public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group.</span></span>

```azurecli-interactive
az network public-ip create \
--resource-group myResourceGroupSLB \
--name myPublicIP \
--sku Standard
```

## <a name="create-azure-load-balancer-standard"></a><span data-ttu-id="58d66-126">Create Azure Load Balancer Standard</span><span class="sxs-lookup"><span data-stu-id="58d66-126">Create Azure Load Balancer Standard</span></span>
<span data-ttu-id="58d66-127">This section details how you can create and configure the following components of the load balancer:</span><span class="sxs-lookup"><span data-stu-id="58d66-127">This section details how you can create and configure the following components of the load balancer:</span></span>
- <span data-ttu-id="58d66-128">a frontend IP pool that receives the incoming network traffic on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="58d66-128">a frontend IP pool that receives the incoming network traffic on the load balancer.</span></span>
- <span data-ttu-id="58d66-129">a backend IP pool where the frontend pool sends the load balanced network traffic.</span><span class="sxs-lookup"><span data-stu-id="58d66-129">a backend IP pool where the frontend pool sends the load balanced network traffic.</span></span>
- <span data-ttu-id="58d66-130">a health probe that determines health of the backend VM instances.</span><span class="sxs-lookup"><span data-stu-id="58d66-130">a health probe that determines health of the backend VM instances.</span></span>
- <span data-ttu-id="58d66-131">a load balancer rule that defines how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="58d66-131">a load balancer rule that defines how traffic is distributed to the VMs.</span></span>

### <a name="create-the-load-balancer"></a><span data-ttu-id="58d66-132">Create the load balancer</span><span class="sxs-lookup"><span data-stu-id="58d66-132">Create the load balancer</span></span>
<span data-ttu-id="58d66-133">Create a Standard load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-133">Create a Standard load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create).</span></span> <span data-ttu-id="58d66-134">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="58d66-134">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration.</span></span>

```azurecli-interactive
az network lb create \
--resource-group myResourceGroupSLB \
--name myLoadBalancer \
--public-ip-address myPublicIP \
--frontend-ip-name myFrontEnd \
--backend-pool-name myBackEndPool \
--sku Standard
```

## <a name="create-health-probe-on-port-80"></a><span data-ttu-id="58d66-135">Create health probe on port 80</span><span class="sxs-lookup"><span data-stu-id="58d66-135">Create health probe on port 80</span></span>

<span data-ttu-id="58d66-136">A health probe checks all virtual machine instances to make sure they can send network traffic.</span><span class="sxs-lookup"><span data-stu-id="58d66-136">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="58d66-137">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span><span class="sxs-lookup"><span data-stu-id="58d66-137">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span> <span data-ttu-id="58d66-138">Create a health probe with az network lb probe create to monitor the health of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="58d66-138">Create a health probe with az network lb probe create to monitor the health of the virtual machines.</span></span> <span data-ttu-id="58d66-139">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-139">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create).</span></span> <span data-ttu-id="58d66-140">The following example creates a health probe named *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="58d66-140">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive
az network lb probe create \
--resource-group myResourceGroupSLB \
--lb-name myLoadBalancer \
--name myHealthProbe \
--protocol tcp \
--port 80
```

## <a name="create-load-balancer-rule-for-port-80"></a><span data-ttu-id="58d66-141">Create load balancer rule for port 80</span><span class="sxs-lookup"><span data-stu-id="58d66-141">Create load balancer rule for port 80</span></span>
<span data-ttu-id="58d66-142">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="58d66-142">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="58d66-143">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="58d66-143">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span>

```azurecli-interactive
az network lb rule create \
--resource-group myResourceGroupSLB \
--lb-name myLoadBalancer \
--name myLoadBalancerRuleWeb \
--protocol tcp \
--frontend-port 80 \
--backend-port 80 \
--frontend-ip-name myFrontEnd \
--backend-pool-name myBackEndPool \
--probe-name myHealthProbe
```

## <a name="configure-virtual-network"></a><span data-ttu-id="58d66-144">Configure virtual network</span><span class="sxs-lookup"><span data-stu-id="58d66-144">Configure virtual network</span></span>
<span data-ttu-id="58d66-145">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span><span class="sxs-lookup"><span data-stu-id="58d66-145">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="58d66-146">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="58d66-146">Create a virtual network</span></span>

<span data-ttu-id="58d66-147">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the myResourceGroup using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-147">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the myResourceGroup using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span></span>


```azurecli-interactive
az network vnet create \
--resource-group myResourceGroupSLB \
--location westeurope \
--name myVnet \
--subnet-name mySubnet
```

### <a name="create-a-network-security-group"></a><span data-ttu-id="58d66-148">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="58d66-148">Create a network security group</span></span>

<span data-ttu-id="58d66-149">Create network security group named *myNetworkSecurityGroup* to define inbound connections to your virtual network  with [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-149">Create network security group named *myNetworkSecurityGroup* to define inbound connections to your virtual network  with [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create).</span></span>

```azurecli-interactive
az network nsg create \
--resource-group myResourceGroupSLB \
--name myNetworkSecurityGroup
```

<span data-ttu-id="58d66-150">Create a network security group rule named *myNetworkSecurityGroupRule* for port 80 with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).</span><span class="sxs-lookup"><span data-stu-id="58d66-150">Create a network security group rule named *myNetworkSecurityGroupRule* for port 80 with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).</span></span>

```azurecli-interactive
az network nsg rule create \
--resource-group myResourceGroupSLB \
--nsg-name myNetworkSecurityGroup \
--name myNetworkSecurityGroupRule \
--protocol tcp \
--direction inbound \
--source-address-prefix '*' \
--source-port-range '*' \
--destination-address-prefix '*' \
--destination-port-range 80 \
--access allow \
--priority 200
```
### <a name="create-nics"></a><span data-ttu-id="58d66-151">Create NICs</span><span class="sxs-lookup"><span data-stu-id="58d66-151">Create NICs</span></span>
<span data-ttu-id="58d66-152">Create three virtual NICs with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span><span class="sxs-lookup"><span data-stu-id="58d66-152">Create three virtual NICs with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span></span> <span data-ttu-id="58d66-153">The following example creates six virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="58d66-153">The following example creates six virtual NICs.</span></span> <span data-ttu-id="58d66-154">(One virtual NIC for each VM you create for your app in the following steps).</span><span class="sxs-lookup"><span data-stu-id="58d66-154">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="58d66-155">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span><span class="sxs-lookup"><span data-stu-id="58d66-155">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupSLB \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```
## <a name="create-backend-servers"></a><span data-ttu-id="58d66-156">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="58d66-156">Create backend servers</span></span>
<span data-ttu-id="58d66-157">In this example, you create three virtual machines located in zone 1, zone 2, and zone 3 to be used as backend servers for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="58d66-157">In this example, you create three virtual machines located in zone 1, zone 2, and zone 3 to be used as backend servers for the load balancer.</span></span> <span data-ttu-id="58d66-158">You also install NGINX on the virtual machines to verify that the load balancer was successfully created.</span><span class="sxs-lookup"><span data-stu-id="58d66-158">You also install NGINX on the virtual machines to verify that the load balancer was successfully created.</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="58d66-159">Create cloud-init config</span><span class="sxs-lookup"><span data-stu-id="58d66-159">Create cloud-init config</span></span>

<span data-ttu-id="58d66-160">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="58d66-160">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span></span> <span data-ttu-id="58d66-161">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span><span class="sxs-lookup"><span data-stu-id="58d66-161">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span></span> <span data-ttu-id="58d66-162">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="58d66-162">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-the-zonal-virtual-machines"></a><span data-ttu-id="58d66-163">Create the zonal virtual machines</span><span class="sxs-lookup"><span data-stu-id="58d66-163">Create the zonal virtual machines</span></span>
<span data-ttu-id="58d66-164">Create the VMs with [az vm create](/cli/azure/vm#az-vm-create) in zone 1, zone 2, and zone 3.</span><span class="sxs-lookup"><span data-stu-id="58d66-164">Create the VMs with [az vm create](/cli/azure/vm#az-vm-create) in zone 1, zone 2, and zone 3.</span></span> <span data-ttu-id="58d66-165">The following example creates a VM in each zone and generates SSH keys if they do not already exist:</span><span class="sxs-lookup"><span data-stu-id="58d66-165">The following example creates a VM in each zone and generates SSH keys if they do not already exist:</span></span>

<span data-ttu-id="58d66-166">Create a VM in each zone (zone 1, zone2, and zone 3) of the *westeurope* location.</span><span class="sxs-lookup"><span data-stu-id="58d66-166">Create a VM in each zone (zone 1, zone2, and zone 3) of the *westeurope* location.</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
  az vm create \
    --resource-group myResourceGroupSLB \
    --name myVM$i \
    --nics myNic$i \
    --image UbuntuLTS \
    --generate-ssh-keys \
    --zone $i \
    --custom-data cloud-init.txt
done
```
## <a name="test-the-load-balancer"></a><span data-ttu-id="58d66-167">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="58d66-167">Test the load balancer</span></span>

<span data-ttu-id="58d66-168">Get the public IP address of the load balancer using [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="58d66-168">Get the public IP address of the load balancer using [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> 

```azurecli-interactive
  az network public-ip show \
    --resource-group myResourceGroupSLB \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
``` 
<span data-ttu-id="58d66-169">You can then enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="58d66-169">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="58d66-170">Remember - it takes a few minutes for the VMs to be ready before the load balancer starts to distribute traffic to them.</span><span class="sxs-lookup"><span data-stu-id="58d66-170">Remember - it takes a few minutes for the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="58d66-171">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span><span class="sxs-lookup"><span data-stu-id="58d66-171">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Running Node.js app](./media/load-balancer-standard-public-zone-redundant-cli/running-nodejs-app.png)

<span data-ttu-id="58d66-173">To see the load balancer distribute traffic across VMs in all three availability zones running your app, you can stop a VM in a particular zone and refresh your browser.</span><span class="sxs-lookup"><span data-stu-id="58d66-173">To see the load balancer distribute traffic across VMs in all three availability zones running your app, you can stop a VM in a particular zone and refresh your browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58d66-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="58d66-174">Next steps</span></span>
- <span data-ttu-id="58d66-175">Learn more about [Standard Load Balancer](./load-balancer-standard-overview.md)</span><span class="sxs-lookup"><span data-stu-id="58d66-175">Learn more about [Standard Load Balancer](./load-balancer-standard-overview.md)</span></span>



