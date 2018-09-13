---
title: Quickstart:Create a public Standard Load Balancer - Azure CLI | Microsoft Docs
description: This quickstart shows how to create a public load balancer using the Azure CLI
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I want to create a Standard Load balancer so that I can load balance internet traffic to VMs.
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 2b6623b614a254635cb758f615271dac826f08b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865092"
---
# <a name="quickstart-create-a-standard-load-balancer-to-load-balance-vms-using-azure-cli-20"></a><span data-ttu-id="b04c4-103">Quickstart: Create a Standard Load Balancer to load balance VMS using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b04c4-103">Quickstart: Create a Standard Load Balancer to load balance VMS using Azure CLI 2.0</span></span>

<span data-ttu-id="b04c4-104">This quickstart shows you how to create Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-104">This quickstart shows you how to create Standard Load Balancer.</span></span> <span data-ttu-id="b04c4-105">To test the load balancer, you deploy two virtual machines (VMs) running Ubuntu server and load balance a web app between the two VMs.</span><span class="sxs-lookup"><span data-stu-id="b04c4-105">To test the load balancer, you deploy two virtual machines (VMs) running Ubuntu server and load balance a web app between the two VMs.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)] 

<span data-ttu-id="b04c4-106">If you choose to install and use the CLI locally, this tutorial requires that you are running a version of the Azure CLI version 2.0.28 or later.</span><span class="sxs-lookup"><span data-stu-id="b04c4-106">If you choose to install and use the CLI locally, this tutorial requires that you are running a version of the Azure CLI version 2.0.28 or later.</span></span> <span data-ttu-id="b04c4-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="b04c4-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="b04c4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b04c4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b04c4-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b04c4-109">Create a resource group</span></span>

<span data-ttu-id="b04c4-110">Create a resource group with [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b04c4-110">Create a resource group with [az group create](https://docs.microsoft.com/cli/azure/group#create).</span></span> <span data-ttu-id="b04c4-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="b04c4-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="b04c4-112">The following example creates a resource group named *myResourceGroupSLB* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="b04c4-112">The following example creates a resource group named *myResourceGroupSLB* in the *eastus* location:</span></span>

```azurecli-interactive
  az group create \
    --name myResourceGroupSLB \
    --location eastus
```

## <a name="create-a-public-standard-ip-address"></a><span data-ttu-id="b04c4-113">Create a public Standard IP address</span><span class="sxs-lookup"><span data-stu-id="b04c4-113">Create a public Standard IP address</span></span>

<span data-ttu-id="b04c4-114">To access your web app on the Internet, you need a public IP address for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-114">To access your web app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="b04c4-115">A Standard Load Balancer only supports Standard Public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b04c4-115">A Standard Load Balancer only supports Standard Public IP addresses.</span></span> <span data-ttu-id="b04c4-116">Use [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) to create a Standard Public IP address named *myPublicIP* in *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="b04c4-116">Use [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) to create a Standard Public IP address named *myPublicIP* in *myResourceGroupSLB*.</span></span>

```azurecli-interactive
  az network public-ip create --resource-group myResourceGroupSLB --name myPublicIP --sku standard
```

## <a name="create-azure-load-balancer"></a><span data-ttu-id="b04c4-117">Create Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="b04c4-117">Create Azure load balancer</span></span>

<span data-ttu-id="b04c4-118">This section details how you can create and configure the following components of the load balancer:</span><span class="sxs-lookup"><span data-stu-id="b04c4-118">This section details how you can create and configure the following components of the load balancer:</span></span>
  - <span data-ttu-id="b04c4-119">a frontend IP pool that receives the incoming network traffic on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-119">a frontend IP pool that receives the incoming network traffic on the load balancer.</span></span>
  - <span data-ttu-id="b04c4-120">a backend IP pool where the frontend pool sends the load balanced network traffic.</span><span class="sxs-lookup"><span data-stu-id="b04c4-120">a backend IP pool where the frontend pool sends the load balanced network traffic.</span></span>
  - <span data-ttu-id="b04c4-121">a health probe that determines health of the backend VM instances.</span><span class="sxs-lookup"><span data-stu-id="b04c4-121">a health probe that determines health of the backend VM instances.</span></span>
  - <span data-ttu-id="b04c4-122">a load balancer rule that defines how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="b04c4-122">a load balancer rule that defines how traffic is distributed to the VMs.</span></span>

### <a name="create-the-load-balancer"></a><span data-ttu-id="b04c4-123">Create the load balancer</span><span class="sxs-lookup"><span data-stu-id="b04c4-123">Create the load balancer</span></span>

<span data-ttu-id="b04c4-124">Create a public Azure Load Balancer with [az network lb create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) named **myLoadBalancer** that includes a frontend pool named **myFrontEnd**, a backend pool named **myBackEndPool** that is associated with the public IP address **myPublicIP** that you created in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="b04c4-124">Create a public Azure Load Balancer with [az network lb create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) named **myLoadBalancer** that includes a frontend pool named **myFrontEnd**, a backend pool named **myBackEndPool** that is associated with the public IP address **myPublicIP** that you created in the preceding step.</span></span>

```azurecli-interactive
  az network lb create \
    --resource-group myResourceGroupSLB \
    --name myLoadBalancer \
    --sku standard
    --public-ip-address myPublicIP \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool       
  ```

### <a name="create-the-health-probe"></a><span data-ttu-id="b04c4-125">Create the health probe</span><span class="sxs-lookup"><span data-stu-id="b04c4-125">Create the health probe</span></span>

<span data-ttu-id="b04c4-126">A health probe checks all virtual machine instances to make sure they can send network traffic.</span><span class="sxs-lookup"><span data-stu-id="b04c4-126">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="b04c4-127">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span><span class="sxs-lookup"><span data-stu-id="b04c4-127">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span> <span data-ttu-id="b04c4-128">Create a health probe with [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe?view=azure-cli-latest#create) to monitor the health of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b04c4-128">Create a health probe with [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe?view=azure-cli-latest#create) to monitor the health of the virtual machines.</span></span> 

```azurecli-interactive
  az network lb probe create \
    --resource-group myResourceGroupSLB \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80   
```

### <a name="create-the-load-balancer-rule"></a><span data-ttu-id="b04c4-129">Create the load balancer rule</span><span class="sxs-lookup"><span data-stu-id="b04c4-129">Create the load balancer rule</span></span>

<span data-ttu-id="b04c4-130">A load balancer rule defines the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="b04c4-130">A load balancer rule defines the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="b04c4-131">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule?view=azure-cli-latest#create) for listening to port 80 in the frontend pool *myFrontEnd* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="b04c4-131">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule?view=azure-cli-latest#create) for listening to port 80 in the frontend pool *myFrontEnd* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

```azurecli-interactive
  az network lb rule create \
    --resource-group myResourceGroupSLB \
    --lb-name myLoadBalancer \
    --name myHTTPRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe  
```

## <a name="configure-virtual-network"></a><span data-ttu-id="b04c4-132">Configure virtual network</span><span class="sxs-lookup"><span data-stu-id="b04c4-132">Configure virtual network</span></span>

<span data-ttu-id="b04c4-133">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span><span class="sxs-lookup"><span data-stu-id="b04c4-133">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="b04c4-134">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="b04c4-134">Create a virtual network</span></span>

<span data-ttu-id="b04c4-135">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the *myResourceGroup* using [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b04c4-135">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the *myResourceGroup* using [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create).</span></span>

```azurecli-interactive
  az network vnet create \
    --resource-group myResourceGroupSLB \
    --location eastus \
    --name myVnet \
    --subnet-name mySubnet
```
###  <a name="create-a-network-security-group"></a><span data-ttu-id="b04c4-136">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="b04c4-136">Create a network security group</span></span>

<span data-ttu-id="b04c4-137">For a Standard Load Balancer, the VMs in the backend address for are required to have NICs that belong to a Network Security group.</span><span class="sxs-lookup"><span data-stu-id="b04c4-137">For a Standard Load Balancer, the VMs in the backend address for are required to have NICs that belong to a Network Security group.</span></span> <span data-ttu-id="b04c4-138">Create network security group to define inbound connections to your virtual network.</span><span class="sxs-lookup"><span data-stu-id="b04c4-138">Create network security group to define inbound connections to your virtual network.</span></span>

```azurecli-interactive
  az network nsg create \
    --resource-group myResourceGroupSLB \
    --name myNetworkSecurityGroup
```

### <a name="create-a-network-security-group-rule"></a><span data-ttu-id="b04c4-139">Create a network security group rule</span><span class="sxs-lookup"><span data-stu-id="b04c4-139">Create a network security group rule</span></span>

<span data-ttu-id="b04c4-140">Create a network security group rule to allow inbound connections through port 80.</span><span class="sxs-lookup"><span data-stu-id="b04c4-140">Create a network security group rule to allow inbound connections through port 80.</span></span>

```azurecli-interactive
  az network nsg rule create \
    --resource-group myResourceGroupSLB \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleHTTP \
    --protocol tcp \
    --direction inbound \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 80 \
    --access allow \
    --priority 200
```
### <a name="create-nics"></a><span data-ttu-id="b04c4-141">Create NICs</span><span class="sxs-lookup"><span data-stu-id="b04c4-141">Create NICs</span></span>

<span data-ttu-id="b04c4-142">Create three network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span><span class="sxs-lookup"><span data-stu-id="b04c4-142">Create three network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the Public IP address and the network security group.</span></span> 

```azurecli-interactive
for i in `seq 1 2`; do
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


## <a name="create-backend-servers"></a><span data-ttu-id="b04c4-143">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="b04c4-143">Create backend servers</span></span>

<span data-ttu-id="b04c4-144">In this example, you create three virtual machines to be used as backend servers for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-144">In this example, you create three virtual machines to be used as backend servers for the load balancer.</span></span> <span data-ttu-id="b04c4-145">To verify that the load balancer was successfully created, you also install NGINX on the virtual machines .</span><span class="sxs-lookup"><span data-stu-id="b04c4-145">To verify that the load balancer was successfully created, you also install NGINX on the virtual machines .</span></span>

### <a name="create-an-availability-set"></a><span data-ttu-id="b04c4-146">Create an Availability set</span><span class="sxs-lookup"><span data-stu-id="b04c4-146">Create an Availability set</span></span>

<span data-ttu-id="b04c4-147">Create an availability set with [az vm availabilityset create](/cli/azure/network/nic#az-network-availabilityset-create)</span><span class="sxs-lookup"><span data-stu-id="b04c4-147">Create an availability set with [az vm availabilityset create](/cli/azure/network/nic#az-network-availabilityset-create)</span></span>

 ```azurecli-interactive
  az vm availability-set create \
    --resource-group myResourceGroupSLB \
    --name myAvailabilitySet
```

### <a name="create-two-virtual-machines"></a><span data-ttu-id="b04c4-148">Create two virtual machines</span><span class="sxs-lookup"><span data-stu-id="b04c4-148">Create two virtual machines</span></span>

<span data-ttu-id="b04c4-149">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b04c4-149">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span></span> <span data-ttu-id="b04c4-150">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span><span class="sxs-lookup"><span data-stu-id="b04c4-150">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span></span> <span data-ttu-id="b04c4-151">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="b04c4-151">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span></span>

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
 
<span data-ttu-id="b04c4-152">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="b04c4-152">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span></span>

 ```azurecli-interactive
for i in `seq 1 2`; do
  az vm create \
    --resource-group myResourceGroupSLB \
    --name myVM$i \
    --availability-set myAvailabilitySet \
    --nics myNic$i \
    --image UbuntuLTS \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
    --no-wait
    done
```
<span data-ttu-id="b04c4-153">It may take a few minutes for the VMs to get deployed.</span><span class="sxs-lookup"><span data-stu-id="b04c4-153">It may take a few minutes for the VMs to get deployed.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="b04c4-154">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="b04c4-154">Test the load balancer</span></span>

<span data-ttu-id="b04c4-155">To get the public IP address of the load balancer, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="b04c4-155">To get the public IP address of the load balancer, use [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> <span data-ttu-id="b04c4-156">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="b04c4-156">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurecli-interactive
  az network public-ip show \
    --resource-group myResourceGroupSLB \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
``` 
   ![Test load balancer](./media/load-balancer-standard-public-cli/running-nodejs-app.png)

## <a name="clean-up-resources"></a><span data-ttu-id="b04c4-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b04c4-158">Clean up resources</span></span>

<span data-ttu-id="b04c4-159">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b04c4-159">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.</span></span>

```azurecli-interactive 
  az group delete --name myResourceGroupSLB
```
## <a name="next-step"></a><span data-ttu-id="b04c4-160">Next step</span><span class="sxs-lookup"><span data-stu-id="b04c4-160">Next step</span></span>
<span data-ttu-id="b04c4-161">In this quickstart, you created Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-161">In this quickstart, you created Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="b04c4-162">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="b04c4-162">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b04c4-163">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="b04c4-163">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-standard-public-zone-redundant-portal.md)

