---
title: Availability and Scale in Azure Resource Manager Templates | Microsoft Docs
description: Azure Virtual Machine DotNet Core Tutorial
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d488858ffa78e1d3764777f2f8de39da36c9be6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556669"
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="0ef85-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span><span class="sxs-lookup"><span data-stu-id="0ef85-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="0ef85-104">Availability and scale refer to uptime and the ability to meet demand.</span><span class="sxs-lookup"><span data-stu-id="0ef85-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="0ef85-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span><span class="sxs-lookup"><span data-stu-id="0ef85-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="0ef85-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span><span class="sxs-lookup"><span data-stu-id="0ef85-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="0ef85-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span><span class="sxs-lookup"><span data-stu-id="0ef85-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="0ef85-108">Scale on the other hand refers to an applications ability to serve demand.</span><span class="sxs-lookup"><span data-stu-id="0ef85-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="0ef85-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span><span class="sxs-lookup"><span data-stu-id="0ef85-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="0ef85-110">This document details how the Music Store sample deployment is configured for availability and scale.</span><span class="sxs-lookup"><span data-stu-id="0ef85-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="0ef85-111">All dependencies and unique configurations are highlighted.</span><span class="sxs-lookup"><span data-stu-id="0ef85-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="0ef85-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0ef85-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="0ef85-113">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="0ef85-113">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="0ef85-114">Availability Set</span><span class="sxs-lookup"><span data-stu-id="0ef85-114">Availability Set</span></span>
<span data-ttu-id="0ef85-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span><span class="sxs-lookup"><span data-stu-id="0ef85-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="0ef85-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span><span class="sxs-lookup"><span data-stu-id="0ef85-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="0ef85-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span><span class="sxs-lookup"><span data-stu-id="0ef85-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="0ef85-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="0ef85-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="0ef85-119">An Availability Set is declared as a property of a Virtual Machine resource.</span><span class="sxs-lookup"><span data-stu-id="0ef85-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="0ef85-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="0ef85-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="0ef85-121">The availability set as seen from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ef85-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="0ef85-122">Each virtual machine and details about the configuration are detailed here.</span><span class="sxs-lookup"><span data-stu-id="0ef85-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Availability Set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="0ef85-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ef85-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="0ef85-125">Network Load Balancer</span><span class="sxs-lookup"><span data-stu-id="0ef85-125">Network Load Balancer</span></span>
<span data-ttu-id="0ef85-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span><span class="sxs-lookup"><span data-stu-id="0ef85-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="0ef85-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span><span class="sxs-lookup"><span data-stu-id="0ef85-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="0ef85-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span><span class="sxs-lookup"><span data-stu-id="0ef85-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="0ef85-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0ef85-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="0ef85-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="0ef85-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="0ef85-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span><span class="sxs-lookup"><span data-stu-id="0ef85-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="0ef85-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="0ef85-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="0ef85-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span><span class="sxs-lookup"><span data-stu-id="0ef85-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Network Load Balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="0ef85-135">Load Balancer Rule</span><span class="sxs-lookup"><span data-stu-id="0ef85-135">Load Balancer Rule</span></span>
<span data-ttu-id="0ef85-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span><span class="sxs-lookup"><span data-stu-id="0ef85-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="0ef85-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span><span class="sxs-lookup"><span data-stu-id="0ef85-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="0ef85-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="0ef85-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

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

<span data-ttu-id="0ef85-139">A view of the network load balancer rule from the portal.</span><span class="sxs-lookup"><span data-stu-id="0ef85-139">A view of the network load balancer rule from the portal.</span></span>

![Network Load Balancer Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="0ef85-141">Load Balancer Probe</span><span class="sxs-lookup"><span data-stu-id="0ef85-141">Load Balancer Probe</span></span>
<span data-ttu-id="0ef85-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span><span class="sxs-lookup"><span data-stu-id="0ef85-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="0ef85-143">This monitoring takes place by constant probing of a pre-defined port.</span><span class="sxs-lookup"><span data-stu-id="0ef85-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="0ef85-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span><span class="sxs-lookup"><span data-stu-id="0ef85-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="0ef85-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="0ef85-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

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

<span data-ttu-id="0ef85-146">The load balancer probe seen from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ef85-146">The load balancer probe seen from the Azure portal.</span></span>

![Network Load Balancer Probe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="0ef85-148">Inbound NAT Rules</span><span class="sxs-lookup"><span data-stu-id="0ef85-148">Inbound NAT Rules</span></span>
<span data-ttu-id="0ef85-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="0ef85-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="0ef85-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span><span class="sxs-lookup"><span data-stu-id="0ef85-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="0ef85-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span><span class="sxs-lookup"><span data-stu-id="0ef85-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="0ef85-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="0ef85-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="0ef85-153">With the Music Store application, a port starting at 5000 is mapped to port 3389 on each Virtual Machine for RDP access.</span><span class="sxs-lookup"><span data-stu-id="0ef85-153">With the Music Store application, a port starting at 5000 is mapped to port 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="0ef85-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span><span class="sxs-lookup"><span data-stu-id="0ef85-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span>

<span data-ttu-id="0ef85-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="0ef85-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
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
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="0ef85-156">One example inbound NAT rule as seen in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0ef85-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="0ef85-157">An RDP NAT rule is created for each virtual machine in the deployment.</span><span class="sxs-lookup"><span data-stu-id="0ef85-157">An RDP NAT rule is created for each virtual machine in the deployment.</span></span>

![Inbound NAT Rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="0ef85-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ef85-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="0ef85-160">Deploy multiple VMs</span><span class="sxs-lookup"><span data-stu-id="0ef85-160">Deploy multiple VMs</span></span>
<span data-ttu-id="0ef85-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span><span class="sxs-lookup"><span data-stu-id="0ef85-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="0ef85-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span><span class="sxs-lookup"><span data-stu-id="0ef85-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="0ef85-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span><span class="sxs-lookup"><span data-stu-id="0ef85-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="0ef85-164">The copy function consumes the number of instances to be created and handles deploying the proper number of virtual machines and associated resources.</span><span class="sxs-lookup"><span data-stu-id="0ef85-164">The copy function consumes the number of instances to be created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="0ef85-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span><span class="sxs-lookup"><span data-stu-id="0ef85-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="0ef85-166">This number is used throughout the template when creating virtual machines and related resources.</span><span class="sxs-lookup"><span data-stu-id="0ef85-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
},
```

<span data-ttu-id="0ef85-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span><span class="sxs-lookup"><span data-stu-id="0ef85-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="0ef85-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="0ef85-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="0ef85-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span><span class="sxs-lookup"><span data-stu-id="0ef85-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="0ef85-170">The value of the copy index function can be used to name virtual machines and other resources.</span><span class="sxs-lookup"><span data-stu-id="0ef85-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="0ef85-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span><span class="sxs-lookup"><span data-stu-id="0ef85-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="0ef85-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span><span class="sxs-lookup"><span data-stu-id="0ef85-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="0ef85-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span><span class="sxs-lookup"><span data-stu-id="0ef85-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="0ef85-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span><span class="sxs-lookup"><span data-stu-id="0ef85-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="0ef85-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="0ef85-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="0ef85-176">The `copyIndex` function is used several times in the Music Store sample template.</span><span class="sxs-lookup"><span data-stu-id="0ef85-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="0ef85-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such and network interface, load balancer rules, and any depends on functions.</span><span class="sxs-lookup"><span data-stu-id="0ef85-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="0ef85-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0ef85-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="0ef85-179">Next step</span><span class="sxs-lookup"><span data-stu-id="0ef85-179">Next step</span></span>
<hr>

[<span data-ttu-id="0ef85-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="0ef85-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)






