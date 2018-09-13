---
title: Create an internal Basic Load Balancer - Azure CLI 2.0 | Microsoft Docs
description: Learn how to create an internal load balancer using the Azure CLI 2.0
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/27/2018
ms.author: kumud
ms.openlocfilehash: bd4dda835279a21509f77814f4d5f9e30e8a42c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818602"
---
# <a name="create-an-internal-load-balancer-to-load-balance-vms-using-azure-cli-20"></a><span data-ttu-id="6cc26-103">Create an internal load balancer to load balance VMs using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6cc26-103">Create an internal load balancer to load balance VMs using Azure CLI 2.0</span></span>

<span data-ttu-id="6cc26-104">This article shows you how to create an internal load balancer to load balance VMs.</span><span class="sxs-lookup"><span data-stu-id="6cc26-104">This article shows you how to create an internal load balancer to load balance VMs.</span></span> <span data-ttu-id="6cc26-105">To test the load balancer, you deploy two virtual machines (VMs) running Ubuntu server to load balance a web app.</span><span class="sxs-lookup"><span data-stu-id="6cc26-105">To test the load balancer, you deploy two virtual machines (VMs) running Ubuntu server to load balance a web app.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)] 

<span data-ttu-id="6cc26-106">If you choose to install and use the CLI locally, this tutorial requires that you are running a version of the Azure CLI version 2.0.28 or later.</span><span class="sxs-lookup"><span data-stu-id="6cc26-106">If you choose to install and use the CLI locally, this tutorial requires that you are running a version of the Azure CLI version 2.0.28 or later.</span></span> <span data-ttu-id="6cc26-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6cc26-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="6cc26-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6cc26-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6cc26-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="6cc26-109">Create a resource group</span></span>

<span data-ttu-id="6cc26-110">Create a resource group with [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6cc26-110">Create a resource group with [az group create](https://docs.microsoft.com/cli/azure/group#create).</span></span> <span data-ttu-id="6cc26-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="6cc26-111">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="6cc26-112">The following example creates a resource group named *myResourceGroupILB* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="6cc26-112">The following example creates a resource group named *myResourceGroupILB* in the *eastus* location:</span></span>

```azurecli-interactive
  az group create \
    --name myResourceGroupILB \
    --location eastus
```
## <a name="create-a-virtual-network"></a><span data-ttu-id="6cc26-113">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="6cc26-113">Create a virtual network</span></span>

<span data-ttu-id="6cc26-114">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the *myResourceGroup* using [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="6cc26-114">Create a virtual network named *myVnet* with a subnet named *mySubnet* in the *myResourceGroup* using [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create).</span></span>

```azurecli-interactive
  az network vnet create \
    --name myVnet \
    --resource-group myResourceGroupILB \
    --location eastus \
    --subnet-name mySubnet
```
## <a name="create-basic-load-balancer"></a><span data-ttu-id="6cc26-115">Create Basic Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6cc26-115">Create Basic Load Balancer</span></span>

<span data-ttu-id="6cc26-116">This section details how you can create and configure the following components of the load balancer:</span><span class="sxs-lookup"><span data-stu-id="6cc26-116">This section details how you can create and configure the following components of the load balancer:</span></span>
  - <span data-ttu-id="6cc26-117">a frontend IP configuration that receives the incoming network traffic on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc26-117">a frontend IP configuration that receives the incoming network traffic on the load balancer.</span></span>
  - <span data-ttu-id="6cc26-118">a backend IP pool where the frontend pool sends the load balanced network traffic.</span><span class="sxs-lookup"><span data-stu-id="6cc26-118">a backend IP pool where the frontend pool sends the load balanced network traffic.</span></span>
  - <span data-ttu-id="6cc26-119">a health probe that determines health of the backend VM instances.</span><span class="sxs-lookup"><span data-stu-id="6cc26-119">a health probe that determines health of the backend VM instances.</span></span>
  - <span data-ttu-id="6cc26-120">a load balancer rule that defines how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="6cc26-120">a load balancer rule that defines how traffic is distributed to the VMs.</span></span>

### <a name="create-the-load-balancer"></a><span data-ttu-id="6cc26-121">Create the load balancer</span><span class="sxs-lookup"><span data-stu-id="6cc26-121">Create the load balancer</span></span>

<span data-ttu-id="6cc26-122">Create a public Basic Load Balancer with [az network lb create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) named **myLoadBalancer** that includes a frontend IP configuration named **myFrontEnd**, a back-end pool named **myBackEndPool** that is associated with a private IP address \*\*10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="6cc26-122">Create a public Basic Load Balancer with [az network lb create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) named **myLoadBalancer** that includes a frontend IP configuration named **myFrontEnd**, a back-end pool named **myBackEndPool** that is associated with a private IP address \*\*10.0.0.7.</span></span>

```azurecli-interactive
  az network lb create \
    --resource-group myResourceGroupILB \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEnd \
    --private-ip-address 10.0.0.7 \
    --backend-pool-name myBackEndPool \
    --vnet-name myVnet \
    --subnet mySubnet      
  ```
### <a name="create-the-health-probe"></a><span data-ttu-id="6cc26-123">Create the health probe</span><span class="sxs-lookup"><span data-stu-id="6cc26-123">Create the health probe</span></span>

<span data-ttu-id="6cc26-124">A health probe checks all virtual machine instances to make sure they can receive network traffic.</span><span class="sxs-lookup"><span data-stu-id="6cc26-124">A health probe checks all virtual machine instances to make sure they can receive network traffic.</span></span> <span data-ttu-id="6cc26-125">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span><span class="sxs-lookup"><span data-stu-id="6cc26-125">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span> <span data-ttu-id="6cc26-126">Create a health probe with [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe?view=azure-cli-latest#create) to monitor the health of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6cc26-126">Create a health probe with [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe?view=azure-cli-latest#create) to monitor the health of the virtual machines.</span></span> 

```azurecli-interactive
  az network lb probe create \
    --resource-group myResourceGroupILB \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80   
```

### <a name="create-the-load-balancer-rule"></a><span data-ttu-id="6cc26-127">Create the load balancer rule</span><span class="sxs-lookup"><span data-stu-id="6cc26-127">Create the load balancer rule</span></span>

<span data-ttu-id="6cc26-128">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="6cc26-128">A load balancer rule defines the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="6cc26-129">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule?view=azure-cli-latest#create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="6cc26-129">Create a load balancer rule *myLoadBalancerRuleWeb* with [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule?view=azure-cli-latest#create) for listening to port 80 in the frontend pool *myFrontEndPool* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

```azurecli-interactive
  az network lb rule create \
    --resource-group myResourceGroupILB \
    --lb-name myLoadBalancer \
    --name myHTTPRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe  
```

## <a name="create-servers-for-the-backend-address-pool"></a><span data-ttu-id="6cc26-130">Create servers for the backend address pool</span><span class="sxs-lookup"><span data-stu-id="6cc26-130">Create servers for the backend address pool</span></span>

<span data-ttu-id="6cc26-131">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span><span class="sxs-lookup"><span data-stu-id="6cc26-131">Before you deploy some VMs and can test your load balancer, create the supporting virtual network resources.</span></span>

### <a name="create-nics"></a><span data-ttu-id="6cc26-132">Create NICs</span><span class="sxs-lookup"><span data-stu-id="6cc26-132">Create NICs</span></span>

<span data-ttu-id="6cc26-133">Create two network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the private IP address.</span><span class="sxs-lookup"><span data-stu-id="6cc26-133">Create two network interfaces with [az network nic create](/cli/azure/network/nic#az-network-nic-create) and associate them with the private IP address.</span></span> 

```azurecli-interactive
for i in `seq 1 2`; do
  az network nic create \
    --resource-group myResourceGroupILB \
    --name myNic$i \
    --vnet-name myVnet \
    --subnet mySubnet \
    --lb-name myLoadBalancer \
    --lb-address-pools myBackEndPool
done
```

## <a name="create-backend-servers"></a><span data-ttu-id="6cc26-134">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="6cc26-134">Create backend servers</span></span>

<span data-ttu-id="6cc26-135">In this example, you create two virtual machines to be used as backend servers for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc26-135">In this example, you create two virtual machines to be used as backend servers for the load balancer.</span></span> <span data-ttu-id="6cc26-136">To verify that the load balancer was successfully created, you also install NGINX on the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6cc26-136">To verify that the load balancer was successfully created, you also install NGINX on the virtual machines.</span></span>

### <a name="create-an-availability-set"></a><span data-ttu-id="6cc26-137">Create an Availability set</span><span class="sxs-lookup"><span data-stu-id="6cc26-137">Create an Availability set</span></span>

<span data-ttu-id="6cc26-138">Create an availability set with [az vm availabilityset create](/cli/azure/network/nic#az-network-availabilityset-create)</span><span class="sxs-lookup"><span data-stu-id="6cc26-138">Create an availability set with [az vm availabilityset create](/cli/azure/network/nic#az-network-availabilityset-create)</span></span>

 ```azurecli-interactive
  az vm availability-set create \
    --resource-group myResourceGroupILB \
    --name myAvailabilitySet
```

### <a name="create-two-virtual-machines"></a><span data-ttu-id="6cc26-139">Create two virtual machines</span><span class="sxs-lookup"><span data-stu-id="6cc26-139">Create two virtual machines</span></span>

<span data-ttu-id="6cc26-140">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6cc26-140">You can use a cloud-init configuration file to install NGINX and run a 'Hello World' Node.js app on a Linux virtual machine.</span></span> <span data-ttu-id="6cc26-141">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span><span class="sxs-lookup"><span data-stu-id="6cc26-141">In your current shell, create a file named cloud-init.txt and copy and paste the following configuration into the shell.</span></span> <span data-ttu-id="6cc26-142">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="6cc26-142">Make sure that you copy the whole cloud-init file correctly, especially the first line:</span></span>

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
 
<span data-ttu-id="6cc26-143">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="6cc26-143">Create the virtual machines with [az vm create](/cli/azure/vm#az-vm-create).</span></span>

 ```azurecli-interactive
for i in `seq 1 2`; do
  az vm create \
    --resource-group myResourceGroupILB \
    --name myVM$i \
    --availability-set myAvailabilitySet \
    --nics myNic$i \
    --image UbuntuLTS \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
    done
```
<span data-ttu-id="6cc26-144">It may take a few minutes for the VMs to get deployed.</span><span class="sxs-lookup"><span data-stu-id="6cc26-144">It may take a few minutes for the VMs to get deployed.</span></span>

### <a name="create-a-vm-for-testing-the-load-balancer"></a><span data-ttu-id="6cc26-145">Create a VM for testing the load balancer</span><span class="sxs-lookup"><span data-stu-id="6cc26-145">Create a VM for testing the load balancer</span></span>

<span data-ttu-id="6cc26-146">To test the load balancer, create a virtual machine, *myVMTest*, and associate it to *myNic3*.</span><span class="sxs-lookup"><span data-stu-id="6cc26-146">To test the load balancer, create a virtual machine, *myVMTest*, and associate it to *myNic3*.</span></span>

```azurecli-interactive
 az vm create \
    --resource-group myResourceGroupILB \
    --name myVMTest \
    --image win2016datacenter \
    --admin-username azureuser \
    --admin-password myPassword123456!
```

## <a name="test-the-internal-load-balancer"></a><span data-ttu-id="6cc26-147">Test the internal load balancer</span><span class="sxs-lookup"><span data-stu-id="6cc26-147">Test the internal load balancer</span></span>

<span data-ttu-id="6cc26-148">To test the load balancer, you must first obtain the private IP address of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc26-148">To test the load balancer, you must first obtain the private IP address of the load balancer.</span></span> <span data-ttu-id="6cc26-149">Next, sign in to virtual machine myVMTest, and type the private IP address into the address bar of its web browser.</span><span class="sxs-lookup"><span data-stu-id="6cc26-149">Next, sign in to virtual machine myVMTest, and type the private IP address into the address bar of its web browser.</span></span>

<span data-ttu-id="6cc26-150">To get the private IP address of the load balancer, use [az network lb show](/cli/azure/network/public-ip##az-network-lb-show).</span><span class="sxs-lookup"><span data-stu-id="6cc26-150">To get the private IP address of the load balancer, use [az network lb show](/cli/azure/network/public-ip##az-network-lb-show).</span></span> <span data-ttu-id="6cc26-151">Copy the private IP address, and then paste it into the address bar of a web browser of your virtual machine - *myVMTest*.</span><span class="sxs-lookup"><span data-stu-id="6cc26-151">Copy the private IP address, and then paste it into the address bar of a web browser of your virtual machine - *myVMTest*.</span></span>

```azurecli-interactive
  az network lb show \
    --name myLoadBalancer \
    --resource-group myResourceGroupILB
``` 
![Test load balancer](./media/load-balancer-get-started-ilb-arm-cli/load-balancer-test.png)

## <a name="clean-up-resources"></a><span data-ttu-id="6cc26-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6cc26-153">Clean up resources</span></span>

<span data-ttu-id="6cc26-154">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6cc26-154">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, load balancer, and all related resources.</span></span>

```azurecli-interactive 
  az group delete --name myResourceGroupILB
```


## <a name="next-steps"></a><span data-ttu-id="6cc26-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="6cc26-155">Next steps</span></span>
<span data-ttu-id="6cc26-156">In this article, you created an internal Basic Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="6cc26-156">In this article, you created an internal Basic Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="6cc26-157">To learn more about load balancers and their associated resources, continue to the how-to articles.</span><span class="sxs-lookup"><span data-stu-id="6cc26-157">To learn more about load balancers and their associated resources, continue to the how-to articles.</span></span>
