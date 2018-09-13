---
title: Tutorial - Build a highly available application on Azure VMs | Microsoft Docs
description: Learn how to create a highly available and secure application across three Linux VMs with a load balancer in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: iainfou
ms.openlocfilehash: 0d5ae0d361bbd41204038421f0306cb66f4283d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554013"
---
# <a name="build-a-load-balanced-highly-available-application-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="54330-103">Build a load balanced, highly available application on Linux virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="54330-103">Build a load balanced, highly available application on Linux virtual machines in Azure</span></span>
<span data-ttu-id="54330-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span><span class="sxs-lookup"><span data-stu-id="54330-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="54330-105">The app uses a load balancer, an availability set, and three Linux virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="54330-105">The app uses a load balancer, an availability set, and three Linux virtual machines (VMs).</span></span> <span data-ttu-id="54330-106">This tutorial builds a Node.js app, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span><span class="sxs-lookup"><span data-stu-id="54330-106">This tutorial builds a Node.js app, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span>

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="54330-107">Step 1 - Azure prerequisites</span><span class="sxs-lookup"><span data-stu-id="54330-107">Step 1 - Azure prerequisites</span></span>
<span data-ttu-id="54330-108">To complete this tutorial, open a terminal window and make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54330-108">To complete this tutorial, open a terminal window and make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="54330-109">If you are not already logged in to your Azure subscription, log in with [az login](/cli/azure/#login) and follow the on-screen directions:</span><span class="sxs-lookup"><span data-stu-id="54330-109">If you are not already logged in to your Azure subscription, log in with [az login](/cli/azure/#login) and follow the on-screen directions:</span></span>

```azurecli
az login
```

<span data-ttu-id="54330-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="54330-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="54330-111">Before you can create any other Azure resources, you need to create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="54330-111">Before you can create any other Azure resources, you need to create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="54330-112">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span><span class="sxs-lookup"><span data-stu-id="54330-112">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```


## <a name="step-2---create-availability-set"></a><span data-ttu-id="54330-113">Step 2 - Create availability set</span><span class="sxs-lookup"><span data-stu-id="54330-113">Step 2 - Create availability set</span></span>
<span data-ttu-id="54330-114">Virtual machines can be created across logical fault and update domains.</span><span class="sxs-lookup"><span data-stu-id="54330-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="54330-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="54330-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="54330-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span><span class="sxs-lookup"><span data-stu-id="54330-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="54330-117">This distribution maintains the availability of your app should a hardware component undergo maintenance.</span><span class="sxs-lookup"><span data-stu-id="54330-117">This distribution maintains the availability of your app should a hardware component undergo maintenance.</span></span> <span data-ttu-id="54330-118">Availability sets let you define these logical fault and update domains.</span><span class="sxs-lookup"><span data-stu-id="54330-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="54330-119">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="54330-119">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="54330-120">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="54330-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 3 \
    --platform-update-domain-count 2
```


## <a name="step-3---create-load-balancer"></a><span data-ttu-id="54330-121">Step 3 - Create load balancer</span><span class="sxs-lookup"><span data-stu-id="54330-121">Step 3 - Create load balancer</span></span>
<span data-ttu-id="54330-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span><span class="sxs-lookup"><span data-stu-id="54330-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="54330-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span><span class="sxs-lookup"><span data-stu-id="54330-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-a-public-ip-address"></a><span data-ttu-id="54330-124">Create a public IP address</span><span class="sxs-lookup"><span data-stu-id="54330-124">Create a public IP address</span></span>
<span data-ttu-id="54330-125">To access your app on the Internet, assign a public IP address to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="54330-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="54330-126">Create a public IP address with [az network public-ip create](/cli/azure/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="54330-126">Create a public IP address with [az network public-ip create](/cli/azure/public-ip#create).</span></span> <span data-ttu-id="54330-127">The following example creates a public IP address named `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="54330-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```azurecli
az network public-ip create --resource-group myResourceGroup --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="54330-128">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="54330-128">Create a load balancer</span></span>
<span data-ttu-id="54330-129">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="54330-129">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="54330-130">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span><span class="sxs-lookup"><span data-stu-id="54330-130">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```azurecli
az network lb create \
    --resource-group myResourceGroup \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="54330-131">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="54330-131">Create a health probe</span></span>
<span data-ttu-id="54330-132">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="54330-132">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="54330-133">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="54330-133">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="54330-134">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span><span class="sxs-lookup"><span data-stu-id="54330-134">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="54330-135">You create a health probe based on a protocol or a specific health check page for your app.</span><span class="sxs-lookup"><span data-stu-id="54330-135">You create a health probe based on a protocol or a specific health check page for your app.</span></span> <span data-ttu-id="54330-136">The following example creates a TCP probe, though you can expand on this example and add `--path healthcheck.js`, for example.</span><span class="sxs-lookup"><span data-stu-id="54330-136">The following example creates a TCP probe, though you can expand on this example and add `--path healthcheck.js`, for example.</span></span> <span data-ttu-id="54330-137">The `healthcheck.js` must be created and return **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span><span class="sxs-lookup"><span data-stu-id="54330-137">The `healthcheck.js` must be created and return **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="54330-138">Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="54330-138">Create a health probe with [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="54330-139">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span><span class="sxs-lookup"><span data-stu-id="54330-139">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```azurecli
az network lb probe create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="54330-140">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="54330-140">Create a load balancer rule</span></span>
<span data-ttu-id="54330-141">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="54330-141">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="54330-142">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="54330-142">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="54330-143">The following example creates a rule named `myLoadBalancerRule`, uses the `myHealthProbe` health probe, and balances traffic on port `80`:</span><span class="sxs-lookup"><span data-stu-id="54330-143">The following example creates a rule named `myLoadBalancerRule`, uses the `myHealthProbe` health probe, and balances traffic on port `80`:</span></span>

```azurecli
az network lb rule create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="step-4---configure-networking"></a><span data-ttu-id="54330-144">Step 4 - Configure networking</span><span class="sxs-lookup"><span data-stu-id="54330-144">Step 4 - Configure networking</span></span>
<span data-ttu-id="54330-145">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="54330-145">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="54330-146">This virtual network is secured to filter traffic based on defined access rules.</span><span class="sxs-lookup"><span data-stu-id="54330-146">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="54330-147">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="54330-147">Create a virtual network</span></span>
<span data-ttu-id="54330-148">To provide network connectivity to your VMs, create a virtual network with [az network vnet create](/cli/azure/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="54330-148">To provide network connectivity to your VMs, create a virtual network with [az network vnet create](/cli/azure/vnet#create).</span></span> <span data-ttu-id="54330-149">The following example creates a virtual network named `myVnet` with a subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="54330-149">The following example creates a virtual network named `myVnet` with a subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create --resource-group myResourceGroup --name myVnet --subnet-name mySubnet
```

### <a name="configure-network-security"></a><span data-ttu-id="54330-150">Configure network security</span><span class="sxs-lookup"><span data-stu-id="54330-150">Configure network security</span></span>
<span data-ttu-id="54330-151">Network security groups use rules to control the traffic flow to and from VMs.</span><span class="sxs-lookup"><span data-stu-id="54330-151">Network security groups use rules to control the traffic flow to and from VMs.</span></span> <span data-ttu-id="54330-152">You define these rules, such as to allow traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="54330-152">You define these rules, such as to allow traffic on port 80.</span></span> <span data-ttu-id="54330-153">While the load balancer distributes traffic across the VMs, the network security group rules make sure only permitted traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="54330-153">While the load balancer distributes traffic across the VMs, the network security group rules make sure only permitted traffic is allowed.</span></span>

<span data-ttu-id="54330-154">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="54330-154">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="54330-155">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="54330-155">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="54330-156">To allow web traffic to reach your app, create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="54330-156">To allow web traffic to reach your app, create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="54330-157">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="54330-157">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="54330-158">Create virtual network interface cards</span><span class="sxs-lookup"><span data-stu-id="54330-158">Create virtual network interface cards</span></span> 
<span data-ttu-id="54330-159">Load balancers function with the virtual NIC resource rather than the actual VM.</span><span class="sxs-lookup"><span data-stu-id="54330-159">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="54330-160">The virtual NIC is connected to the load balancer, and then attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="54330-160">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="54330-161">Create a virtual NIC with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="54330-161">Create a virtual NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="54330-162">The following example creates three virtual NICs.</span><span class="sxs-lookup"><span data-stu-id="54330-162">The following example creates three virtual NICs.</span></span> <span data-ttu-id="54330-163">(One virtual NIC for each VM you create for your app in the following steps):</span><span class="sxs-lookup"><span data-stu-id="54330-163">(One virtual NIC for each VM you create for your app in the following steps):</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroup \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```


## <a name="step-5---build-your-app"></a><span data-ttu-id="54330-164">Step 5 - Build your app</span><span class="sxs-lookup"><span data-stu-id="54330-164">Step 5 - Build your app</span></span>
<span data-ttu-id="54330-165">**cloud-init** is a widely used approach to customizing a VM.</span><span class="sxs-lookup"><span data-stu-id="54330-165">**cloud-init** is a widely used approach to customizing a VM.</span></span> <span data-ttu-id="54330-166">You can use **cloud-init** to install packages and write files.</span><span class="sxs-lookup"><span data-stu-id="54330-166">You can use **cloud-init** to install packages and write files.</span></span> <span data-ttu-id="54330-167">As **cloud-init** runs during the initial deployment, there are no additional steps to get your app running.</span><span class="sxs-lookup"><span data-stu-id="54330-167">As **cloud-init** runs during the initial deployment, there are no additional steps to get your app running.</span></span> <span data-ttu-id="54330-168">The load balancer starts to distribute traffic once the VM has finished deploying and the app is running.</span><span class="sxs-lookup"><span data-stu-id="54330-168">The load balancer starts to distribute traffic once the VM has finished deploying and the app is running.</span></span> <span data-ttu-id="54330-169">For more information about using **cloud-init**, see [Use cloud-init to customize a Linux VM during creation](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54330-169">For more information about using **cloud-init**, see [Use cloud-init to customize a Linux VM during creation](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="54330-170">The following **cloud-init** configuration installs **nodejs** and **npm**, then installs and configures **nginx** as a web proxy for your app.</span><span class="sxs-lookup"><span data-stu-id="54330-170">The following **cloud-init** configuration installs **nodejs** and **npm**, then installs and configures **nginx** as a web proxy for your app.</span></span> <span data-ttu-id="54330-171">The configuration also creates a simple 'Hello World' Node.js app, then initializes and starts the app with **Express**.</span><span class="sxs-lookup"><span data-stu-id="54330-171">The configuration also creates a simple 'Hello World' Node.js app, then initializes and starts the app with **Express**.</span></span> <span data-ttu-id="54330-172">If you want to use a different application framework, adjust the packages and deployed application accordingly.</span><span class="sxs-lookup"><span data-stu-id="54330-172">If you want to use a different application framework, adjust the packages and deployed application accordingly.</span></span>

<span data-ttu-id="54330-173">Create a file named `cloud-init.txt` and paste the following configuration:</span><span class="sxs-lookup"><span data-stu-id="54330-173">Create a file named `cloud-init.txt` and paste the following configuration:</span></span>

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
  - nginx -s reload
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="step-6---create-virtual-machines"></a><span data-ttu-id="54330-174">Step 6 - Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="54330-174">Step 6 - Create virtual machines</span></span>
<span data-ttu-id="54330-175">With all the underlying components in place, you can now create highly available VMs to run your app.</span><span class="sxs-lookup"><span data-stu-id="54330-175">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span>

### <a name="create-vms"></a><span data-ttu-id="54330-176">Create VMs</span><span class="sxs-lookup"><span data-stu-id="54330-176">Create VMs</span></span>
<span data-ttu-id="54330-177">Create the VMs with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="54330-177">Create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="54330-178">The following example creates three VMs and generates SSH keys if they do not already exist:</span><span class="sxs-lookup"><span data-stu-id="54330-178">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroup \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image Canonical:UbuntuServer:14.04.4-LTS:latest \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="54330-179">It takes a few minutes to create and configure all three VMs.</span><span class="sxs-lookup"><span data-stu-id="54330-179">It takes a few minutes to create and configure all three VMs.</span></span> <span data-ttu-id="54330-180">The load balancer health probe automatically detects when the app is running on each VM.</span><span class="sxs-lookup"><span data-stu-id="54330-180">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="54330-181">Once the app is running, the load balancer rule starts to distribute traffic.</span><span class="sxs-lookup"><span data-stu-id="54330-181">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="54330-182">Test your app</span><span class="sxs-lookup"><span data-stu-id="54330-182">Test your app</span></span>
<span data-ttu-id="54330-183">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="54330-183">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="54330-184">The following example obtains the IP address for `myPublicIP` created earlier:</span><span class="sxs-lookup"><span data-stu-id="54330-184">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="54330-185">Enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="54330-185">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="54330-186">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span><span class="sxs-lookup"><span data-stu-id="54330-186">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Running Node.js app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/tutorial-load-balance-nodejs/running-nodejs-app.png)

<span data-ttu-id="54330-188">Force-refresh your web browser to see the load balancer distribute traffic across all three VMs running your app.</span><span class="sxs-lookup"><span data-stu-id="54330-188">Force-refresh your web browser to see the load balancer distribute traffic across all three VMs running your app.</span></span>


## <a name="step-7---management-tasks"></a><span data-ttu-id="54330-189">Step 7 - Management tasks</span><span class="sxs-lookup"><span data-stu-id="54330-189">Step 7 - Management tasks</span></span>
<span data-ttu-id="54330-190">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span><span class="sxs-lookup"><span data-stu-id="54330-190">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="54330-191">To deal with increased traffic to your app, you may need to add additional VMs.</span><span class="sxs-lookup"><span data-stu-id="54330-191">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="54330-192">This section shows you how to remove or add a VM from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="54330-192">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="54330-193">Remove a VM from the load balancer</span><span class="sxs-lookup"><span data-stu-id="54330-193">Remove a VM from the load balancer</span></span>
<span data-ttu-id="54330-194">Remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="54330-194">Remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="54330-195">The following example removes the virtual NIC for **myVM2** from `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="54330-195">The following example removes the virtual NIC for **myVM2** from `myLoadBalancer`:</span></span>

```azurecli
az network nic ip-config address-pool remove \
    --resource-group myResourceGroup \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="54330-196">Force-refresh your web browser to see the load balancer distribute traffic across the remaining two VMs running your app.</span><span class="sxs-lookup"><span data-stu-id="54330-196">Force-refresh your web browser to see the load balancer distribute traffic across the remaining two VMs running your app.</span></span> <span data-ttu-id="54330-197">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span><span class="sxs-lookup"><span data-stu-id="54330-197">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="54330-198">Add a VM to the load balancer</span><span class="sxs-lookup"><span data-stu-id="54330-198">Add a VM to the load balancer</span></span>
<span data-ttu-id="54330-199">After performing VM maintenance, or if you need to expand capacity, add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="54330-199">After performing VM maintenance, or if you need to expand capacity, add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="54330-200">The following example adds the virtual NIC for **myVM2** to `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="54330-200">The following example adds the virtual NIC for **myVM2** to `myLoadBalancer`:</span></span>

```azurecli
az network nic ip-config address-pool add \
    --resource-group myResourceGroup \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="54330-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="54330-201">Next steps</span></span>
<span data-ttu-id="54330-202">This tutorial builds out a highly available application infrastructure using the individual Azure resources.</span><span class="sxs-lookup"><span data-stu-id="54330-202">This tutorial builds out a highly available application infrastructure using the individual Azure resources.</span></span> <span data-ttu-id="54330-203">You can also use Virtual Machine Scale Sets to automatically scale up or down the number of VMs running your app.</span><span class="sxs-lookup"><span data-stu-id="54330-203">You can also use Virtual Machine Scale Sets to automatically scale up or down the number of VMs running your app.</span></span> <span data-ttu-id="54330-204">Continue on to the next tutorial - [Create a highly available application on Linux with Virtual Machine Scale Sets](tutorial-convert-to-vmss.md).</span><span class="sxs-lookup"><span data-stu-id="54330-204">Continue on to the next tutorial - [Create a highly available application on Linux with Virtual Machine Scale Sets](tutorial-convert-to-vmss.md).</span></span>

<span data-ttu-id="54330-205">To learn more about some of the high availability features introduced in this tutorial, see the following information:</span><span class="sxs-lookup"><span data-stu-id="54330-205">To learn more about some of the high availability features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="54330-206">Manage the availability of Linux virtual machines</span><span class="sxs-lookup"><span data-stu-id="54330-206">Manage the availability of Linux virtual machines</span></span>](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="54330-207">Azure Load Balancer overview</span><span class="sxs-lookup"><span data-stu-id="54330-207">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="54330-208">Control network traffic flow with network security groups</span><span class="sxs-lookup"><span data-stu-id="54330-208">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)
- [<span data-ttu-id="54330-209">Azure CLI sample scripts</span><span class="sxs-lookup"><span data-stu-id="54330-209">Azure CLI sample scripts</span></span>](../windows/cli-samples.md)
