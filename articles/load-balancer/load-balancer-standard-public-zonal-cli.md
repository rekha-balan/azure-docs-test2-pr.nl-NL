---
title: Create a public Load Balancer Standard with zonal Public IP address frontend using Azure CLI | Microsoft Docs
description: Learn how to create a public Load Balancer Standard with zonal Public IP address frontend using Azure CLI
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
ms.date: 03/26/2018
ms.author: kumud
ms.openlocfilehash: b4bb0cdb9be59ae35b640ef67b12c382bb621a19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865900"
---
#  <a name="create-a-public-load-balancer-standard-with-zonal-frontend-using-azure-cli"></a><span data-ttu-id="bca3e-103">Create a public Load Balancer Standard with zonal frontend using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bca3e-103">Create a public Load Balancer Standard with zonal frontend using Azure CLI</span></span>

<span data-ttu-id="bca3e-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend using a Public IP Standard address.</span><span class="sxs-lookup"><span data-stu-id="bca3e-104">This article steps through creating a public [Load Balancer Standard](https://aka.ms/azureloadbalancerstandard) with a zonal frontend using a Public IP Standard address.</span></span> <span data-ttu-id="bca3e-105">In this scenario, you specify a particular zone for your front-end and back-end instances, to align your data path and resources with a specific zone.</span><span class="sxs-lookup"><span data-stu-id="bca3e-105">In this scenario, you specify a particular zone for your front-end and back-end instances, to align your data path and resources with a specific zone.</span></span>

<span data-ttu-id="bca3e-106">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="bca3e-106">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span></span>

<span data-ttu-id="bca3e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="bca3e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>
 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bca3e-108">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span><span class="sxs-lookup"><span data-stu-id="bca3e-108">If you choose to install and use the CLI locally, make sure that you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) and are logged in to an Azure account with [az login](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest#az-login).</span></span>

> [!NOTE]
 <span data-ttu-id="bca3e-109">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span><span class="sxs-lookup"><span data-stu-id="bca3e-109">Support for Availability Zones is available for select Azure resources and regions, and VM size families.</span></span> <span data-ttu-id="bca3e-110">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="bca3e-110">For more information on how to get started, and which Azure resources, regions, and VM size families you can try availability zones with, see [Overview of Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span> <span data-ttu-id="bca3e-111">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bca3e-111">For support, you can reach out on [StackOverflow](https://stackoverflow.com/questions/tagged/azure-availability-zones) or [open an Azure support ticket](../azure-supportability/how-to-create-azure-support-request.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>  

## <a name="create-a-resource-group"></a><span data-ttu-id="bca3e-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="bca3e-112">Create a resource group</span></span>

<span data-ttu-id="bca3e-113">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-113">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span></span> <span data-ttu-id="bca3e-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="bca3e-114">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="bca3e-115">The following example creates a resource group named *myResourceGroupLB* in the *westeurope* location:</span><span class="sxs-lookup"><span data-stu-id="bca3e-115">The following example creates a resource group named *myResourceGroupLB* in the *westeurope* location:</span></span>

```azurecli-interactive
az group create \
--name myResourceGroupLB \
--location westeurope
```

## <a name="create-a-zonal-public-ip-standard"></a><span data-ttu-id="bca3e-116">Create a zonal public IP Standard</span><span class="sxs-lookup"><span data-stu-id="bca3e-116">Create a zonal public IP Standard</span></span>
<span data-ttu-id="bca3e-117">To access your app on the Internet, you need a public IP address for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="bca3e-117">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="bca3e-118">A Public IP address that is created in a specific zone always exists only in that zone.</span><span class="sxs-lookup"><span data-stu-id="bca3e-118">A Public IP address that is created in a specific zone always exists only in that zone.</span></span> <span data-ttu-id="bca3e-119">It is not possible to change the zone of a Public IP address.</span><span class="sxs-lookup"><span data-stu-id="bca3e-119">It is not possible to change the zone of a Public IP address.</span></span>

<span data-ttu-id="bca3e-120">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bca3e-120">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="bca3e-121">The following example creates a zonal public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group in zone 1.</span><span class="sxs-lookup"><span data-stu-id="bca3e-121">The following example creates a zonal public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group in zone 1.</span></span>

```azurecli-interactive
az network public-ip create \
--resource-group myResourceGroupLB \
--name myPublicIP \
--sku Standard \
--zone 1
```

## <a name="create-azure-load-balancer-standard"></a><span data-ttu-id="bca3e-122">Create Azure Load Balancer Standard</span><span class="sxs-lookup"><span data-stu-id="bca3e-122">Create Azure Load Balancer Standard</span></span>
<span data-ttu-id="bca3e-123">This section details how you can create and configure the following components of the load balancer:</span><span class="sxs-lookup"><span data-stu-id="bca3e-123">This section details how you can create and configure the following components of the load balancer:</span></span>
- <span data-ttu-id="bca3e-124">a frontend IP pool that receives the incoming network traffic on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="bca3e-124">a frontend IP pool that receives the incoming network traffic on the load balancer.</span></span>
- <span data-ttu-id="bca3e-125">a backend IP pool where the frontend pool sends the load balanced network traffic.</span><span class="sxs-lookup"><span data-stu-id="bca3e-125">a backend IP pool where the frontend pool sends the load balanced network traffic.</span></span>
- <span data-ttu-id="bca3e-126">a health probe that determines health of the backend VM instances.</span><span class="sxs-lookup"><span data-stu-id="bca3e-126">a health probe that determines health of the backend VM instances.</span></span>
- <span data-ttu-id="bca3e-127">a load balancer rule that defines how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="bca3e-127">a load balancer rule that defines how traffic is distributed to the VMs.</span></span>

### <a name="create-the-load-balancer"></a><span data-ttu-id="bca3e-128">Create the load balancer</span><span class="sxs-lookup"><span data-stu-id="bca3e-128">Create the load balancer</span></span>
<span data-ttu-id="bca3e-129">Create a Standard load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-129">Create a Standard load balancer with [az network lb create](/cli/azure/network/lb#az-network-lb-create).</span></span> <span data-ttu-id="bca3e-130">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="bca3e-130">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration.</span></span>

```azurecli-interactive
az network lb create \
--resource-group myResourceGroupLB \
--name myLoadBalancer \
--public-ip-address myPublicIP \
--frontend-ip-name myFrontEndPool \
--backend-pool-name myBackEndPool \
--sku Standard
```

## <a name="create-health-probe-on-port-80"></a><span data-ttu-id="bca3e-131">Create health probe on port 80</span><span class="sxs-lookup"><span data-stu-id="bca3e-131">Create health probe on port 80</span></span>

<span data-ttu-id="bca3e-132">A health probe checks all virtual machine instances to make sure they can send network traffic.</span><span class="sxs-lookup"><span data-stu-id="bca3e-132">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="bca3e-133">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span><span class="sxs-lookup"><span data-stu-id="bca3e-133">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span> <span data-ttu-id="bca3e-134">Create a health probe with az network lb probe create to monitor the health of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="bca3e-134">Create a health probe with az network lb probe create to monitor the health of the virtual machines.</span></span> <span data-ttu-id="bca3e-135">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-135">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#az-network-lb-probe-create).</span></span> <span data-ttu-id="bca3e-136">The following example creates a health probe named *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="bca3e-136">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive
az network lb probe create \
--resource-group myResourceGroupLB \
--lb-name myLoadBalancer \
--name myHealthProbe \
--protocol tcp \
--port 80
```

## <a name="create-load-balancer-rule-for-port-80"></a><span data-ttu-id="bca3e-137">Create load balancer rule for port 80</span><span class="sxs-lookup"><span data-stu-id="bca3e-137">Create load balancer rule for port 80</span></span>
<span data-ttu-id="bca3e-138">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="bca3e-138">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="bca3e-139">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="bca3e-139">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span>

```azurecli-interactive
az network lb rule create \
--resource-group myResourceGroupLB \
--lb-name myLoadBalancer \
--name myLoadBalancerRuleWeb \
--protocol tcp \
--frontend-port 80 \
--backend-port 80 \
--frontend-ip-name myFrontEndPool \
--backend-pool-name myBackEndPool \
--probe-name myHealthProbe
```

## <a name="configure-virtual-network"></a><span data-ttu-id="bca3e-140">Configure virtual network</span><span class="sxs-lookup"><span data-stu-id="bca3e-140">Configure virtual network</span></span>
<span data-ttu-id="bca3e-141">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span><span class="sxs-lookup"><span data-stu-id="bca3e-141">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="bca3e-142">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="bca3e-142">Create a virtual network</span></span>

<span data-ttu-id="bca3e-143">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the myResourceGroup using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-143">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the myResourceGroup using [az network vnet create](/cli/azure/network/vnet#az-network-vnet-create).</span></span>


```azurecli-interactive
az network vnet create \
--resource-group myResourceGroupLB \
--location westeurope \
--name myVnet \
--subnet-name mySubnet
```

### <a name="create-a-network-security-group"></a><span data-ttu-id="bca3e-144">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="bca3e-144">Create a network security group</span></span>

<span data-ttu-id="bca3e-145">Create network security group named *myNetworkSecurityGroup* to define inbound connections to your virtual network  with [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-145">Create network security group named *myNetworkSecurityGroup* to define inbound connections to your virtual network  with [az network nsg create](/cli/azure/network/nsg#az-network-nsg-create).</span></span>

```azurecli-interactive
az network nsg create \
--resource-group myResourceGroupLB \
--name myNetworkSecurityGroup
```

<span data-ttu-id="bca3e-146">Create a network security group rule named *myNetworkSecurityGroupRule* for port 80 with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-146">Create a network security group rule named *myNetworkSecurityGroupRule* for port 80 with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create).</span></span>

```azurecli-interactive
az network nsg rule create \
--resource-group myResourceGroupLB \
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
### <a name="create-nics"></a><span data-ttu-id="bca3e-147">Create NICs</span><span class="sxs-lookup"><span data-stu-id="bca3e-147">Create NICs</span></span>
<span data-ttu-id="bca3e-148">Create three virtual NICs with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span><span class="sxs-lookup"><span data-stu-id="bca3e-148">Create three virtual NICs with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span></span> <span data-ttu-id="bca3e-149">The following example creates three virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="bca3e-149">The following example creates three virtual NICs.</span></span> <span data-ttu-id="bca3e-150">(One virtual NIC for each VM you create for your app in the following steps).</span><span class="sxs-lookup"><span data-stu-id="bca3e-150">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="bca3e-151">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span><span class="sxs-lookup"><span data-stu-id="bca3e-151">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLB \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```
## <a name="create-backend-servers"></a><span data-ttu-id="bca3e-152">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="bca3e-152">Create backend servers</span></span>
<span data-ttu-id="bca3e-153">In this example, you create three virtual machines located in zone 1 to be used as backend servers for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="bca3e-153">In this example, you create three virtual machines located in zone 1 to be used as backend servers for the load balancer.</span></span> <span data-ttu-id="bca3e-154">You also install NGINX on the virtual machines to verify that the load balancer was successfully created.</span><span class="sxs-lookup"><span data-stu-id="bca3e-154">You also install NGINX on the virtual machines to verify that the load balancer was successfully created.</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="bca3e-155">Create cloud-init config</span><span class="sxs-lookup"><span data-stu-id="bca3e-155">Create cloud-init config</span></span>

<span data-ttu-id="bca3e-156">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bca3e-156">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span></span> <span data-ttu-id="bca3e-157">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span><span class="sxs-lookup"><span data-stu-id="bca3e-157">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span></span> <span data-ttu-id="bca3e-158">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="bca3e-158">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span></span>

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

### <a name="create-the-zonal-virtual-machines"></a><span data-ttu-id="bca3e-159">Create the zonal virtual machines</span><span class="sxs-lookup"><span data-stu-id="bca3e-159">Create the zonal virtual machines</span></span>
<span data-ttu-id="bca3e-160">Create the VMs with [az vm create](/cli/azure/vm#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="bca3e-160">Create the VMs with [az vm create](/cli/azure/vm#az-vm-create).</span></span> <span data-ttu-id="bca3e-161">The following example creates three VMs in zone 1 and generates SSH keys if they do not already exist:</span><span class="sxs-lookup"><span data-stu-id="bca3e-161">The following example creates three VMs in zone 1 and generates SSH keys if they do not already exist:</span></span>

```azurecli-interactive
for i in `seq 1 3`; do
 az vm create \
--resource-group myResourceGroupLB \
--name myVM$i \
--nics myNic$i \
--image UbuntuLTS \
--generate-ssh-keys \
--zone 1 \
--custom-data cloud-init.txt
done
```

## <a name="test-the-load-balancer"></a><span data-ttu-id="bca3e-162">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="bca3e-162">Test the load balancer</span></span>
<span data-ttu-id="bca3e-163">Get the public IP address of the load balancer using [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="bca3e-163">Get the public IP address of the load balancer using [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> 

```azurecli-interactive
  az network public-ip show \
    --resource-group myResourceGroupSLB \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
``` 

<span data-ttu-id="bca3e-164">You can then enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="bca3e-164">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="bca3e-165">Remember - it takes a few minutes for the VMs to be ready before the load balancer starts to distribute traffic to them.</span><span class="sxs-lookup"><span data-stu-id="bca3e-165">Remember - it takes a few minutes for the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="bca3e-166">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span><span class="sxs-lookup"><span data-stu-id="bca3e-166">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Running Node.js app](./media/load-balancer-standard-public-zonal-cli/running-nodejs-app.png)

<span data-ttu-id="bca3e-168">To see the load balancer distribute traffic to VMs within zone 1 that are running your app, you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="bca3e-168">To see the load balancer distribute traffic to VMs within zone 1 that are running your app, you can force-refresh your web browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bca3e-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="bca3e-169">Next steps</span></span>
- <span data-ttu-id="bca3e-170">Learn more about [Standard Load Balancer](./load-balancer-standard-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bca3e-170">Learn more about [Standard Load Balancer](./load-balancer-standard-overview.md).</span></span>



