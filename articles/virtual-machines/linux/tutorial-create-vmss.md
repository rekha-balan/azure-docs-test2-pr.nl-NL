---
title: Tutorial - Create a virtual machine scale set for Linux in Azure | Microsoft Docs
description: In this tutorial, you learn how to use the Azure CLI 2.0 to create and deploy a highly available application on Linux VMs using a virtual machine scale set
services: virtual-machine-scale-sets
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: tutorial
ms.date: 06/01/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: b8e25934dfd1bfa9d94d3452044443e7a5002534
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773142"
---
# <a name="tutorial-create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux-with-the-azure-cli-20"></a><span data-ttu-id="4b608-103">Tutorial: Create a virtual machine scale set and deploy a highly available app on Linux with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4b608-103">Tutorial: Create a virtual machine scale set and deploy a highly available app on Linux with the Azure CLI 2.0</span></span>

<span data-ttu-id="4b608-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span><span class="sxs-lookup"><span data-stu-id="4b608-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="4b608-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on resource usage such as CPU, memory demand, or network traffic.</span><span class="sxs-lookup"><span data-stu-id="4b608-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on resource usage such as CPU, memory demand, or network traffic.</span></span> <span data-ttu-id="4b608-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span><span class="sxs-lookup"><span data-stu-id="4b608-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="4b608-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="4b608-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b608-108">Use cloud-init to create an app to scale</span><span class="sxs-lookup"><span data-stu-id="4b608-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="4b608-109">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="4b608-110">Increase or decrease the number of instances in a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="4b608-111">Create autoscale rules</span><span class="sxs-lookup"><span data-stu-id="4b608-111">Create autoscale rules</span></span>
> * <span data-ttu-id="4b608-112">View connection info for scale set instances</span><span class="sxs-lookup"><span data-stu-id="4b608-112">View connection info for scale set instances</span></span>
> * <span data-ttu-id="4b608-113">Use data disks in a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-113">Use data disks in a scale set</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4b608-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.30 or later.</span><span class="sxs-lookup"><span data-stu-id="4b608-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.30 or later.</span></span> <span data-ttu-id="4b608-115">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="4b608-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="4b608-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4b608-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="scale-set-overview"></a><span data-ttu-id="4b608-117">Scale Set overview</span><span class="sxs-lookup"><span data-stu-id="4b608-117">Scale Set overview</span></span>
<span data-ttu-id="4b608-118">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span><span class="sxs-lookup"><span data-stu-id="4b608-118">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="4b608-119">VMs in a scale set are distributed across logic fault and update domains in one or more *placement groups*.</span><span class="sxs-lookup"><span data-stu-id="4b608-119">VMs in a scale set are distributed across logic fault and update domains in one or more *placement groups*.</span></span> <span data-ttu-id="4b608-120">These are groups of similarly configured VMs, similar to [availability sets](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="4b608-120">These are groups of similarly configured VMs, similar to [availability sets](tutorial-availability-sets.md).</span></span>

<span data-ttu-id="4b608-121">VMs are created as needed in a scale set.</span><span class="sxs-lookup"><span data-stu-id="4b608-121">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="4b608-122">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span><span class="sxs-lookup"><span data-stu-id="4b608-122">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="4b608-123">These rules can be triggered based on metrics such as CPU load, memory usage, or network traffic.</span><span class="sxs-lookup"><span data-stu-id="4b608-123">These rules can be triggered based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="4b608-124">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span><span class="sxs-lookup"><span data-stu-id="4b608-124">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="4b608-125">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="4b608-125">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="4b608-126">You can create up to 300 VMs in a scale set when using a custom image.</span><span class="sxs-lookup"><span data-stu-id="4b608-126">You can create up to 300 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="4b608-127">Create an app to scale</span><span class="sxs-lookup"><span data-stu-id="4b608-127">Create an app to scale</span></span>
<span data-ttu-id="4b608-128">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span><span class="sxs-lookup"><span data-stu-id="4b608-128">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="4b608-129">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span><span class="sxs-lookup"><span data-stu-id="4b608-129">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="4b608-130">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span><span class="sxs-lookup"><span data-stu-id="4b608-130">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="4b608-131">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span><span class="sxs-lookup"><span data-stu-id="4b608-131">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="4b608-132">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span><span class="sxs-lookup"><span data-stu-id="4b608-132">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="4b608-133">For example, create the file in the Cloud Shell not on your local machine.</span><span class="sxs-lookup"><span data-stu-id="4b608-133">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="4b608-134">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span><span class="sxs-lookup"><span data-stu-id="4b608-134">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="4b608-135">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span><span class="sxs-lookup"><span data-stu-id="4b608-135">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="4b608-136">Create a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-136">Create a scale set</span></span>
<span data-ttu-id="4b608-137">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="4b608-137">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#az-group-create).</span></span> <span data-ttu-id="4b608-138">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="4b608-138">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="4b608-139">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="4b608-139">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#az-vmss-create).</span></span> <span data-ttu-id="4b608-140">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span><span class="sxs-lookup"><span data-stu-id="4b608-140">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys
```

<span data-ttu-id="4b608-141">It takes a few minutes to create and configure all the scale set resources and VMs.</span><span class="sxs-lookup"><span data-stu-id="4b608-141">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="4b608-142">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span><span class="sxs-lookup"><span data-stu-id="4b608-142">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="4b608-143">It may be another couple of minutes before you can access the app.</span><span class="sxs-lookup"><span data-stu-id="4b608-143">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="4b608-144">Allow web traffic</span><span class="sxs-lookup"><span data-stu-id="4b608-144">Allow web traffic</span></span>
<span data-ttu-id="4b608-145">A load balancer was created automatically as part of the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="4b608-145">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="4b608-146">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span><span class="sxs-lookup"><span data-stu-id="4b608-146">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="4b608-147">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="4b608-147">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="4b608-148">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create).</span><span class="sxs-lookup"><span data-stu-id="4b608-148">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#az-network-lb-rule-create).</span></span> <span data-ttu-id="4b608-149">The following example creates a rule named *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="4b608-149">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="4b608-150">Test your app</span><span class="sxs-lookup"><span data-stu-id="4b608-150">Test your app</span></span>
<span data-ttu-id="4b608-151">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span><span class="sxs-lookup"><span data-stu-id="4b608-151">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#az-network-public-ip-show).</span></span> <span data-ttu-id="4b608-152">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span><span class="sxs-lookup"><span data-stu-id="4b608-152">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="4b608-153">Enter the public IP address in to a web browser.</span><span class="sxs-lookup"><span data-stu-id="4b608-153">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="4b608-154">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span><span class="sxs-lookup"><span data-stu-id="4b608-154">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Running Node.js app](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="4b608-156">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span><span class="sxs-lookup"><span data-stu-id="4b608-156">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="4b608-157">Management tasks</span><span class="sxs-lookup"><span data-stu-id="4b608-157">Management tasks</span></span>
<span data-ttu-id="4b608-158">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span><span class="sxs-lookup"><span data-stu-id="4b608-158">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="4b608-159">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span><span class="sxs-lookup"><span data-stu-id="4b608-159">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="4b608-160">The Azure CLI 2.0 provides a quick way to do those tasks.</span><span class="sxs-lookup"><span data-stu-id="4b608-160">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="4b608-161">Here are a few common tasks.</span><span class="sxs-lookup"><span data-stu-id="4b608-161">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="4b608-162">View VMs in a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-162">View VMs in a scale set</span></span>
<span data-ttu-id="4b608-163">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#az-vmss-list-instances) as follows:</span><span class="sxs-lookup"><span data-stu-id="4b608-163">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#az-vmss-list-instances) as follows:</span></span>

```azurecli-interactive
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="4b608-164">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="4b608-164">The output is similar to the following example:</span></span>

```bash
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="manually-increase-or-decrease-vm-instances"></a><span data-ttu-id="4b608-165">Manually increase or decrease VM instances</span><span class="sxs-lookup"><span data-stu-id="4b608-165">Manually increase or decrease VM instances</span></span>
<span data-ttu-id="4b608-166">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#az-vmss-show) and query on *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="4b608-166">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#az-vmss-show) and query on *sku.capacity*:</span></span>

```azurecli-interactive
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="4b608-167">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#az-vmss-scale).</span><span class="sxs-lookup"><span data-stu-id="4b608-167">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#az-vmss-scale).</span></span> <span data-ttu-id="4b608-168">The following example sets the number of VMs in your scale set to *3*:</span><span class="sxs-lookup"><span data-stu-id="4b608-168">The following example sets the number of VMs in your scale set to *3*:</span></span>

```azurecli-interactive
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 3
```

### <a name="get-connection-info"></a><span data-ttu-id="4b608-169">Get connection info</span><span class="sxs-lookup"><span data-stu-id="4b608-169">Get connection info</span></span>
<span data-ttu-id="4b608-170">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#az-vmss-list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="4b608-170">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#az-vmss-list-instance-connection-info).</span></span> <span data-ttu-id="4b608-171">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span><span class="sxs-lookup"><span data-stu-id="4b608-171">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="4b608-172">Use data disks with scale sets</span><span class="sxs-lookup"><span data-stu-id="4b608-172">Use data disks with scale sets</span></span>
<span data-ttu-id="4b608-173">You can create and use data disks with scale sets.</span><span class="sxs-lookup"><span data-stu-id="4b608-173">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="4b608-174">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span><span class="sxs-lookup"><span data-stu-id="4b608-174">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="4b608-175">Create scale set with data disks</span><span class="sxs-lookup"><span data-stu-id="4b608-175">Create scale set with data disks</span></span>
<span data-ttu-id="4b608-176">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#az-vmss-create) command.</span><span class="sxs-lookup"><span data-stu-id="4b608-176">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#az-vmss-create) command.</span></span> <span data-ttu-id="4b608-177">The following example creates a scale set with *50*Gb data disks attached to each instance:</span><span class="sxs-lookup"><span data-stu-id="4b608-177">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="4b608-178">When instances are removed from a scale set, any attached data disks are also removed.</span><span class="sxs-lookup"><span data-stu-id="4b608-178">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="4b608-179">Add data disks</span><span class="sxs-lookup"><span data-stu-id="4b608-179">Add data disks</span></span>
<span data-ttu-id="4b608-180">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#az-vmss-disk-attach).</span><span class="sxs-lookup"><span data-stu-id="4b608-180">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#az-vmss-disk-attach).</span></span> <span data-ttu-id="4b608-181">The following example adds a *50*Gb disk to each instance:</span><span class="sxs-lookup"><span data-stu-id="4b608-181">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="4b608-182">Detach data disks</span><span class="sxs-lookup"><span data-stu-id="4b608-182">Detach data disks</span></span>
<span data-ttu-id="4b608-183">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#az-vmss-disk-detach).</span><span class="sxs-lookup"><span data-stu-id="4b608-183">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#az-vmss-disk-detach).</span></span> <span data-ttu-id="4b608-184">The following example removes the data disk at LUN *2* from each instance:</span><span class="sxs-lookup"><span data-stu-id="4b608-184">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="4b608-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b608-185">Next steps</span></span>
<span data-ttu-id="4b608-186">In this tutorial, you created a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="4b608-186">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="4b608-187">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="4b608-187">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b608-188">Use cloud-init to create an app to scale</span><span class="sxs-lookup"><span data-stu-id="4b608-188">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="4b608-189">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-189">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="4b608-190">Increase or decrease the number of instances in a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-190">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="4b608-191">Create autoscale rules</span><span class="sxs-lookup"><span data-stu-id="4b608-191">Create autoscale rules</span></span>
> * <span data-ttu-id="4b608-192">View connection info for scale set instances</span><span class="sxs-lookup"><span data-stu-id="4b608-192">View connection info for scale set instances</span></span>
> * <span data-ttu-id="4b608-193">Use data disks in a scale set</span><span class="sxs-lookup"><span data-stu-id="4b608-193">Use data disks in a scale set</span></span>

<span data-ttu-id="4b608-194">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span><span class="sxs-lookup"><span data-stu-id="4b608-194">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b608-195">Load balance virtual machines</span><span class="sxs-lookup"><span data-stu-id="4b608-195">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
