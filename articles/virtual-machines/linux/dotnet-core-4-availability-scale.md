---
title: Availability and Scale in Azure Resource Manager Templates | Microsoft Docs
description: Azure Virtual Machine DotNet Core Tutorial
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/21/2016
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 411b9c44f0f8c1634dd2f08d83de0a15f1d18c36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564304"
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="56ffd-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="56ffd-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="56ffd-104">Availability and scale refer to uptime and the ability to meet demand.</span><span class="sxs-lookup"><span data-stu-id="56ffd-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="56ffd-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span><span class="sxs-lookup"><span data-stu-id="56ffd-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="56ffd-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span><span class="sxs-lookup"><span data-stu-id="56ffd-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="56ffd-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span><span class="sxs-lookup"><span data-stu-id="56ffd-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="56ffd-108">Scale on the other hand refers to an applications ability to serve demand.</span><span class="sxs-lookup"><span data-stu-id="56ffd-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="56ffd-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span><span class="sxs-lookup"><span data-stu-id="56ffd-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="56ffd-110">This document details how the Music Store sample deployment is configured for availability and scale.</span><span class="sxs-lookup"><span data-stu-id="56ffd-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="56ffd-111">All dependencies and unique configurations are highlighted.</span><span class="sxs-lookup"><span data-stu-id="56ffd-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="56ffd-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="56ffd-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="56ffd-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="56ffd-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="56ffd-114">Availability Set</span><span class="sxs-lookup"><span data-stu-id="56ffd-114">Availability Set</span></span>
<span data-ttu-id="56ffd-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span><span class="sxs-lookup"><span data-stu-id="56ffd-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="56ffd-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span><span class="sxs-lookup"><span data-stu-id="56ffd-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="56ffd-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span><span class="sxs-lookup"><span data-stu-id="56ffd-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="56ffd-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="56ffd-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="56ffd-119">An Availability Set is declared as a property of a Virtual Machine resource.</span><span class="sxs-lookup"><span data-stu-id="56ffd-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="56ffd-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="56ffd-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="56ffd-121">The availability set as seen from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56ffd-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="56ffd-122">Each virtual machine and details about the configuration are detailed here.</span><span class="sxs-lookup"><span data-stu-id="56ffd-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Availability Set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="56ffd-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56ffd-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="56ffd-125">Network Load Balancer</span><span class="sxs-lookup"><span data-stu-id="56ffd-125">Network Load Balancer</span></span>
<span data-ttu-id="56ffd-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span><span class="sxs-lookup"><span data-stu-id="56ffd-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="56ffd-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span><span class="sxs-lookup"><span data-stu-id="56ffd-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="56ffd-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span><span class="sxs-lookup"><span data-stu-id="56ffd-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="56ffd-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="56ffd-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="56ffd-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="56ffd-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="56ffd-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span><span class="sxs-lookup"><span data-stu-id="56ffd-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="56ffd-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="56ffd-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="56ffd-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span><span class="sxs-lookup"><span data-stu-id="56ffd-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Network Load Balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="56ffd-135">Load Balancer Rule</span><span class="sxs-lookup"><span data-stu-id="56ffd-135">Load Balancer Rule</span></span>
<span data-ttu-id="56ffd-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span><span class="sxs-lookup"><span data-stu-id="56ffd-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="56ffd-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span><span class="sxs-lookup"><span data-stu-id="56ffd-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="56ffd-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="56ffd-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="56ffd-139">A view of the network load balancer rule from the portal.</span><span class="sxs-lookup"><span data-stu-id="56ffd-139">A view of the network load balancer rule from the portal.</span></span>

![Network Load Balancer Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="56ffd-141">Load Balancer Probe</span><span class="sxs-lookup"><span data-stu-id="56ffd-141">Load Balancer Probe</span></span>
<span data-ttu-id="56ffd-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span><span class="sxs-lookup"><span data-stu-id="56ffd-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="56ffd-143">This monitoring takes place by constant probing of a pre-defined port.</span><span class="sxs-lookup"><span data-stu-id="56ffd-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="56ffd-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span><span class="sxs-lookup"><span data-stu-id="56ffd-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="56ffd-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="56ffd-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="56ffd-146">The load balancer probe seen from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56ffd-146">The load balancer probe seen from the Azure portal.</span></span>

![Network Load Balancer Probe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="56ffd-148">Inbound NAT Rules</span><span class="sxs-lookup"><span data-stu-id="56ffd-148">Inbound NAT Rules</span></span>
<span data-ttu-id="56ffd-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="56ffd-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="56ffd-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span><span class="sxs-lookup"><span data-stu-id="56ffd-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="56ffd-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span><span class="sxs-lookup"><span data-stu-id="56ffd-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="56ffd-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="56ffd-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="56ffd-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span><span class="sxs-lookup"><span data-stu-id="56ffd-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="56ffd-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span><span class="sxs-lookup"><span data-stu-id="56ffd-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="56ffd-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="56ffd-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="56ffd-156">One example inbound NAT rule as seen in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="56ffd-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="56ffd-157">An SSH NAT rule is created for each virtual machine in the deployment.</span><span class="sxs-lookup"><span data-stu-id="56ffd-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![Inbound NAT Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="56ffd-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56ffd-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="56ffd-160">Deploy multiple VMs</span><span class="sxs-lookup"><span data-stu-id="56ffd-160">Deploy multiple VMs</span></span>
<span data-ttu-id="56ffd-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span><span class="sxs-lookup"><span data-stu-id="56ffd-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="56ffd-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span><span class="sxs-lookup"><span data-stu-id="56ffd-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="56ffd-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span><span class="sxs-lookup"><span data-stu-id="56ffd-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="56ffd-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span><span class="sxs-lookup"><span data-stu-id="56ffd-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="56ffd-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span><span class="sxs-lookup"><span data-stu-id="56ffd-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="56ffd-166">This number is used throughout the template when creating virtual machines and related resources.</span><span class="sxs-lookup"><span data-stu-id="56ffd-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

<span data-ttu-id="56ffd-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span><span class="sxs-lookup"><span data-stu-id="56ffd-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="56ffd-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="56ffd-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="56ffd-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span><span class="sxs-lookup"><span data-stu-id="56ffd-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="56ffd-170">The value of the copy index function can be used to name virtual machines and other resources.</span><span class="sxs-lookup"><span data-stu-id="56ffd-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="56ffd-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span><span class="sxs-lookup"><span data-stu-id="56ffd-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="56ffd-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span><span class="sxs-lookup"><span data-stu-id="56ffd-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="56ffd-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span><span class="sxs-lookup"><span data-stu-id="56ffd-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="56ffd-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span><span class="sxs-lookup"><span data-stu-id="56ffd-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="56ffd-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="56ffd-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="56ffd-176">The `copyIndex` function is used several times in the Music Store sample template.</span><span class="sxs-lookup"><span data-stu-id="56ffd-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="56ffd-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span><span class="sxs-lookup"><span data-stu-id="56ffd-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="56ffd-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="56ffd-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="56ffd-179">Next step</span><span class="sxs-lookup"><span data-stu-id="56ffd-179">Next step</span></span>
<hr>

[<span data-ttu-id="56ffd-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="56ffd-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)






