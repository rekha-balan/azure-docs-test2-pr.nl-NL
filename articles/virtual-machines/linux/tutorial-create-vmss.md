---
title: Create a highly available app in Azure using Virtual Machine Scale Sets | Microsoft Docs
description: Create and deploy a highly available application on Linux VMs using a virtual machine scale set and the Azure CLI.
services: virtual-machine-scale-sets
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: 0630debe6439e7e576a64bc1d4abc8005bda9414
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564453"
---
# <a name="create-a-highly-available-application-on-linux-with-virtual-machine-scale-sets"></a><span data-ttu-id="b6c19-103">Create a highly available application on Linux with Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="b6c19-103">Create a highly available application on Linux with Virtual Machine Scale Sets</span></span>
<span data-ttu-id="b6c19-104">This tutorial shows you how to create a highly available application in a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="b6c19-104">This tutorial shows you how to create a highly available application in a virtual machine scale set.</span></span> <span data-ttu-id="b6c19-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span><span class="sxs-lookup"><span data-stu-id="b6c19-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> 


## <a name="step-1---create-a-resource-group"></a><span data-ttu-id="b6c19-106">Step 1 - Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b6c19-106">Step 1 - Create a resource group</span></span>
<span data-ttu-id="b6c19-107">To complete this tutorial, make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6c19-107">To complete this tutorial, make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="b6c19-108">If you are not already logged in to your Azure subscription, log in with [az login](/cli/azure/#login) and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="b6c19-108">If you are not already logged in to your Azure subscription, log in with [az login](/cli/azure/#login) and follow the on-screen directions.</span></span>

<span data-ttu-id="b6c19-109">Create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b6c19-109">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b6c19-110">The following example creates a resource group named `myResourceGroupVMSS` in the `westus` location:</span><span class="sxs-lookup"><span data-stu-id="b6c19-110">The following example creates a resource group named `myResourceGroupVMSS` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroupVMSS --location westus
```


## <a name="step-2---define-your-app"></a><span data-ttu-id="b6c19-111">Step 2 - Define your app</span><span class="sxs-lookup"><span data-stu-id="b6c19-111">Step 2 - Define your app</span></span>
<span data-ttu-id="b6c19-112">You use the same **cloud-init** config from the tutorial where you created a highly available, load balanced app.</span><span class="sxs-lookup"><span data-stu-id="b6c19-112">You use the same **cloud-init** config from the tutorial where you created a highly available, load balanced app.</span></span> <span data-ttu-id="b6c19-113">For more information about using **cloud-init**, see [Use cloud-init to customize a Linux VM during creation](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6c19-113">For more information about using **cloud-init**, see [Use cloud-init to customize a Linux VM during creation](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b6c19-114">Create a file named `cloud-init.txt` and paste the following configuration:</span><span class="sxs-lookup"><span data-stu-id="b6c19-114">Create a file named `cloud-init.txt` and paste the following configuration:</span></span>

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


## <a name="step-3---create-scale-set"></a><span data-ttu-id="b6c19-115">Step 3 - Create scale set</span><span class="sxs-lookup"><span data-stu-id="b6c19-115">Step 3 - Create scale set</span></span>
<span data-ttu-id="b6c19-116">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b6c19-116">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="b6c19-117">Scale sets use the same components as you learned about in the tutorial to [Build a highly available app on Azure](tutorial-load-balance-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b6c19-117">Scale sets use the same components as you learned about in the tutorial to [Build a highly available app on Azure](tutorial-load-balance-nodejs.md).</span></span> <span data-ttu-id="b6c19-118">These components include as availability sets, fault and update domains, and load balancers.</span><span class="sxs-lookup"><span data-stu-id="b6c19-118">These components include as availability sets, fault and update domains, and load balancers.</span></span>

<span data-ttu-id="b6c19-119">With a scale set, these resources are created and managed for you.</span><span class="sxs-lookup"><span data-stu-id="b6c19-119">With a scale set, these resources are created and managed for you.</span></span> <span data-ttu-id="b6c19-120">The number of VMs in your scale set can automatically increase or decrease based on defined rules.</span><span class="sxs-lookup"><span data-stu-id="b6c19-120">The number of VMs in your scale set can automatically increase or decrease based on defined rules.</span></span> <span data-ttu-id="b6c19-121">You can [use a custom image](capture-image.md) as the source for your virtual machine, or configure the VMs during deployment with **cloud-init** as in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b6c19-121">You can [use a custom image](capture-image.md) as the source for your virtual machine, or configure the VMs during deployment with **cloud-init** as in this tutorial.</span></span>

<span data-ttu-id="b6c19-122">Create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="b6c19-122">Create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="b6c19-123">The following example creates a scale set named `myScaleSet`:</span><span class="sxs-lookup"><span data-stu-id="b6c19-123">The following example creates a scale set named `myScaleSet`:</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupVMSS \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="b6c19-124">It takes a few minutes to create and configure all the scale set resources and VMs.</span><span class="sxs-lookup"><span data-stu-id="b6c19-124">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="step-4---configure-firewall"></a><span data-ttu-id="b6c19-125">Step 4 - Configure firewall</span><span class="sxs-lookup"><span data-stu-id="b6c19-125">Step 4 - Configure firewall</span></span>
<span data-ttu-id="b6c19-126">A load balancer was created automatically as part of the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="b6c19-126">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="b6c19-127">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span><span class="sxs-lookup"><span data-stu-id="b6c19-127">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="b6c19-128">To allow traffic to reach the web app, create a rule with [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="b6c19-128">To allow traffic to reach the web app, create a rule with [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="b6c19-129">The following example creates a rule named `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="b6c19-129">The following example creates a rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
az network lb rule create \
  --resource-group myResourceGroupVMSS \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="step-5---test-your-app"></a><span data-ttu-id="b6c19-130">Step 5 - Test your app</span><span class="sxs-lookup"><span data-stu-id="b6c19-130">Step 5 - Test your app</span></span>
<span data-ttu-id="b6c19-131">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="b6c19-131">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="b6c19-132">The following example obtains the IP address for `myScaleSetLBPublicIP` created as part of the scale set:</span><span class="sxs-lookup"><span data-stu-id="b6c19-132">The following example obtains the IP address for `myScaleSetLBPublicIP` created as part of the scale set:</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroupVMSS \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="b6c19-133">Enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="b6c19-133">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="b6c19-134">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span><span class="sxs-lookup"><span data-stu-id="b6c19-134">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Running Node.js app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/tutorial-load-balance-nodejs/running-nodejs-app.png)

<span data-ttu-id="b6c19-136">Force-refresh your web browser to see the load balancer distribute traffic across all the VMs in the scale set running your app.</span><span class="sxs-lookup"><span data-stu-id="b6c19-136">Force-refresh your web browser to see the load balancer distribute traffic across all the VMs in the scale set running your app.</span></span>


## <a name="step-6---management-tasks"></a><span data-ttu-id="b6c19-137">Step 6 - Management tasks</span><span class="sxs-lookup"><span data-stu-id="b6c19-137">Step 6 - Management tasks</span></span>
<span data-ttu-id="b6c19-138">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span><span class="sxs-lookup"><span data-stu-id="b6c19-138">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="b6c19-139">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span><span class="sxs-lookup"><span data-stu-id="b6c19-139">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="b6c19-140">The Azure CLI 2.0 provides a quick way to do those tasks.</span><span class="sxs-lookup"><span data-stu-id="b6c19-140">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="b6c19-141">Here are a few common tasks.</span><span class="sxs-lookup"><span data-stu-id="b6c19-141">Here are a few common tasks.</span></span>

### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="b6c19-142">Increase or decrease VM instances</span><span class="sxs-lookup"><span data-stu-id="b6c19-142">Increase or decrease VM instances</span></span>
<span data-ttu-id="b6c19-143">You can manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="b6c19-143">You can manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="b6c19-144">The following example increases the number of VMs in your scale set to `5`:</span><span class="sxs-lookup"><span data-stu-id="b6c19-144">The following example increases the number of VMs in your scale set to `5`:</span></span>

```azurecli
az vmss scale --resource-group myResourceGroupVMSS --name myScaleSet --new-capacity 5
```

<span data-ttu-id="b6c19-145">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span><span class="sxs-lookup"><span data-stu-id="b6c19-145">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="b6c19-146">Currently, these rules cannot be set in Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b6c19-146">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="b6c19-147">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span><span class="sxs-lookup"><span data-stu-id="b6c19-147">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="b6c19-148">Get connection info</span><span class="sxs-lookup"><span data-stu-id="b6c19-148">Get connection info</span></span>
<span data-ttu-id="b6c19-149">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="b6c19-149">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="b6c19-150">This command outputs the public IP address and ports for each VM that allows you to connect with SSH:</span><span class="sxs-lookup"><span data-stu-id="b6c19-150">This command outputs the public IP address and ports for each VM that allows you to connect with SSH:</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroupVMSS --name myScaleSet
```

### <a name="delete-resource-group"></a><span data-ttu-id="b6c19-151">Delete resource group</span><span class="sxs-lookup"><span data-stu-id="b6c19-151">Delete resource group</span></span>
<span data-ttu-id="b6c19-152">Deleting a resource group also deletes all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="b6c19-152">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroupVMSS
```


## <a name="next-steps"></a><span data-ttu-id="b6c19-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6c19-153">Next steps</span></span>
<span data-ttu-id="b6c19-154">In this tutorial, we defined the web app with **cloud-init** and configured each VM during deployment.</span><span class="sxs-lookup"><span data-stu-id="b6c19-154">In this tutorial, we defined the web app with **cloud-init** and configured each VM during deployment.</span></span> <span data-ttu-id="b6c19-155">For information on capturing a VM to use as the source image in your scale set, see [How to generalize and capture a Linux virtual machine](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="b6c19-155">For information on capturing a VM to use as the source image in your scale set, see [How to generalize and capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="b6c19-156">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span><span class="sxs-lookup"><span data-stu-id="b6c19-156">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="b6c19-157">Azure Virtual Machine Scale Sets overview</span><span class="sxs-lookup"><span data-stu-id="b6c19-157">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="b6c19-158">Azure Load Balancer overview</span><span class="sxs-lookup"><span data-stu-id="b6c19-158">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="b6c19-159">Control network traffic flow with network security groups</span><span class="sxs-lookup"><span data-stu-id="b6c19-159">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)
