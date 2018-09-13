---
title: Learn about virtual machine scale set templates | Microsoft Docs
description: Learn to create a minimum viable scale set template for virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: negat
ms.openlocfilehash: 3b978f5448c2cfbba4d02e3efd730dea7c7813c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564343"
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="4a566-103">Learn about virtual machine scale set templates</span><span class="sxs-lookup"><span data-stu-id="4a566-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="4a566-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span><span class="sxs-lookup"><span data-stu-id="4a566-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="4a566-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span><span class="sxs-lookup"><span data-stu-id="4a566-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span></span> <span data-ttu-id="4a566-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="4a566-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="4a566-107">This template is intended to be simple.</span><span class="sxs-lookup"><span data-stu-id="4a566-107">This template is intended to be simple.</span></span> <span data-ttu-id="4a566-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span><span class="sxs-lookup"><span data-stu-id="4a566-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span></span>

<span data-ttu-id="4a566-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span><span class="sxs-lookup"><span data-stu-id="4a566-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span></span>

## <a name="review-the-template"></a><span data-ttu-id="4a566-110">Review the template</span><span class="sxs-lookup"><span data-stu-id="4a566-110">Review the template</span></span>

<span data-ttu-id="4a566-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="4a566-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="4a566-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span><span class="sxs-lookup"><span data-stu-id="4a566-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="4a566-113">Define $schema and contentVersion</span><span class="sxs-lookup"><span data-stu-id="4a566-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="4a566-114">First, we define `$schema` and `contentVersion` in the template.</span><span class="sxs-lookup"><span data-stu-id="4a566-114">First, we define `$schema` and `contentVersion` in the template.</span></span> <span data-ttu-id="4a566-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span><span class="sxs-lookup"><span data-stu-id="4a566-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="4a566-116">The `contentVersion` element is not used by Azure.</span><span class="sxs-lookup"><span data-stu-id="4a566-116">The `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="4a566-117">Instead, it helps you keep track of the template version.</span><span class="sxs-lookup"><span data-stu-id="4a566-117">Instead, it helps you keep track of the template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="4a566-118">Define parameters</span><span class="sxs-lookup"><span data-stu-id="4a566-118">Define parameters</span></span>
<span data-ttu-id="4a566-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="4a566-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="4a566-120">Parameters are values you specify at the time of deployment.</span><span class="sxs-lookup"><span data-stu-id="4a566-120">Parameters are values you specify at the time of deployment.</span></span> <span data-ttu-id="4a566-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span><span class="sxs-lookup"><span data-stu-id="4a566-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="4a566-122">Later, these parameters are passed into the scale set configuration.</span><span class="sxs-lookup"><span data-stu-id="4a566-122">Later, these parameters are passed into the scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="4a566-123">Define variables</span><span class="sxs-lookup"><span data-stu-id="4a566-123">Define variables</span></span>
<span data-ttu-id="4a566-124">Resource Manager templates also let you define variables to be used later in the template.</span><span class="sxs-lookup"><span data-stu-id="4a566-124">Resource Manager templates also let you define variables to be used later in the template.</span></span> <span data-ttu-id="4a566-125">Our example doesn't use any variables, so we've left the JSON object empty.</span><span class="sxs-lookup"><span data-stu-id="4a566-125">Our example doesn't use any variables, so we've left the JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="4a566-126">Define resources</span><span class="sxs-lookup"><span data-stu-id="4a566-126">Define resources</span></span>
<span data-ttu-id="4a566-127">Next is the resources section of the template.</span><span class="sxs-lookup"><span data-stu-id="4a566-127">Next is the resources section of the template.</span></span> <span data-ttu-id="4a566-128">Here, you define what you actually want to deploy.</span><span class="sxs-lookup"><span data-stu-id="4a566-128">Here, you define what you actually want to deploy.</span></span> <span data-ttu-id="4a566-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span><span class="sxs-lookup"><span data-stu-id="4a566-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="4a566-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span><span class="sxs-lookup"><span data-stu-id="4a566-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="4a566-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="4a566-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="4a566-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="4a566-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="4a566-133">Specify location</span><span class="sxs-lookup"><span data-stu-id="4a566-133">Specify location</span></span>
<span data-ttu-id="4a566-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4a566-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="4a566-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="4a566-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="4a566-136">In this case, we use the `resourceGroup` function.</span><span class="sxs-lookup"><span data-stu-id="4a566-136">In this case, we use the `resourceGroup` function.</span></span> <span data-ttu-id="4a566-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span><span class="sxs-lookup"><span data-stu-id="4a566-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span></span> <span data-ttu-id="4a566-138">The resource group is set by the user at the time of deployment.</span><span class="sxs-lookup"><span data-stu-id="4a566-138">The resource group is set by the user at the time of deployment.</span></span> <span data-ttu-id="4a566-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span><span class="sxs-lookup"><span data-stu-id="4a566-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="4a566-140">Specify virtual network properties</span><span class="sxs-lookup"><span data-stu-id="4a566-140">Specify virtual network properties</span></span>
<span data-ttu-id="4a566-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span><span class="sxs-lookup"><span data-stu-id="4a566-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span></span> <span data-ttu-id="4a566-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="4a566-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="4a566-143">A scale set is always contained within one subnet.</span><span class="sxs-lookup"><span data-stu-id="4a566-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="4a566-144">It cannot span subnets.</span><span class="sxs-lookup"><span data-stu-id="4a566-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="4a566-145">Add dependsOn list</span><span class="sxs-lookup"><span data-stu-id="4a566-145">Add dependsOn list</span></span>
<span data-ttu-id="4a566-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span><span class="sxs-lookup"><span data-stu-id="4a566-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="4a566-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span><span class="sxs-lookup"><span data-stu-id="4a566-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="4a566-148">In this case, there is only one element in the list, the virtual network from the previous example.</span><span class="sxs-lookup"><span data-stu-id="4a566-148">In this case, there is only one element in the list, the virtual network from the previous example.</span></span> <span data-ttu-id="4a566-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span><span class="sxs-lookup"><span data-stu-id="4a566-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span></span> <span data-ttu-id="4a566-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span><span class="sxs-lookup"><span data-stu-id="4a566-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span></span> <span data-ttu-id="4a566-151">The format of each string in the dependsOn list is `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="4a566-151">The format of each string in the dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="4a566-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span><span class="sxs-lookup"><span data-stu-id="4a566-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="4a566-153">Specify scale set properties</span><span class="sxs-lookup"><span data-stu-id="4a566-153">Specify scale set properties</span></span>
<span data-ttu-id="4a566-154">Scale sets have many properties for customizing the VMs in the scale set.</span><span class="sxs-lookup"><span data-stu-id="4a566-154">Scale sets have many properties for customizing the VMs in the scale set.</span></span> <span data-ttu-id="4a566-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="4a566-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="4a566-156">For this tutorial, we will set only a few commonly used properties.</span><span class="sxs-lookup"><span data-stu-id="4a566-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="4a566-157">Supply VM size and capacity</span><span class="sxs-lookup"><span data-stu-id="4a566-157">Supply VM size and capacity</span></span>
<span data-ttu-id="4a566-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span><span class="sxs-lookup"><span data-stu-id="4a566-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span></span> <span data-ttu-id="4a566-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="4a566-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="4a566-160">Choose type of updates</span><span class="sxs-lookup"><span data-stu-id="4a566-160">Choose type of updates</span></span>
<span data-ttu-id="4a566-161">The scale set also needs to know how to handle updates on the scale set.</span><span class="sxs-lookup"><span data-stu-id="4a566-161">The scale set also needs to know how to handle updates on the scale set.</span></span> <span data-ttu-id="4a566-162">Currently, there are two options, `Manual` and `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="4a566-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="4a566-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="4a566-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="4a566-164">Choose VM operating system</span><span class="sxs-lookup"><span data-stu-id="4a566-164">Choose VM operating system</span></span>
<span data-ttu-id="4a566-165">The scale set needs to know what operating system to put on the VMs.</span><span class="sxs-lookup"><span data-stu-id="4a566-165">The scale set needs to know what operating system to put on the VMs.</span></span> <span data-ttu-id="4a566-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span><span class="sxs-lookup"><span data-stu-id="4a566-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="4a566-167">Specify computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="4a566-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="4a566-168">The scale set deploys multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="4a566-168">The scale set deploys multiple VMs.</span></span> <span data-ttu-id="4a566-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="4a566-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="4a566-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="4a566-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="4a566-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span><span class="sxs-lookup"><span data-stu-id="4a566-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span></span> <span data-ttu-id="4a566-172">We do this with the `parameters` template function.</span><span class="sxs-lookup"><span data-stu-id="4a566-172">We do this with the `parameters` template function.</span></span> <span data-ttu-id="4a566-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span><span class="sxs-lookup"><span data-stu-id="4a566-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="4a566-174">Specify VM network configuration</span><span class="sxs-lookup"><span data-stu-id="4a566-174">Specify VM network configuration</span></span>
<span data-ttu-id="4a566-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span><span class="sxs-lookup"><span data-stu-id="4a566-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span></span> <span data-ttu-id="4a566-176">In this case, we only need to specify the ID of the subnet created earlier.</span><span class="sxs-lookup"><span data-stu-id="4a566-176">In this case, we only need to specify the ID of the subnet created earlier.</span></span> <span data-ttu-id="4a566-177">This tells the scale set to put the network interfaces in this subnet.</span><span class="sxs-lookup"><span data-stu-id="4a566-177">This tells the scale set to put the network interfaces in this subnet.</span></span>

<span data-ttu-id="4a566-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span><span class="sxs-lookup"><span data-stu-id="4a566-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span></span> <span data-ttu-id="4a566-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span><span class="sxs-lookup"><span data-stu-id="4a566-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span></span> <span data-ttu-id="4a566-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="4a566-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="4a566-181">However, the identifier of the virtual network is not enough.</span><span class="sxs-lookup"><span data-stu-id="4a566-181">However, the identifier of the virtual network is not enough.</span></span> <span data-ttu-id="4a566-182">You must specify the specific subnet that the scale set VMs should be in.</span><span class="sxs-lookup"><span data-stu-id="4a566-182">You must specify the specific subnet that the scale set VMs should be in.</span></span> <span data-ttu-id="4a566-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4a566-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span></span> <span data-ttu-id="4a566-184">The result is the fully qualified ID of the subnet.</span><span class="sxs-lookup"><span data-stu-id="4a566-184">The result is the fully qualified ID of the subnet.</span></span> <span data-ttu-id="4a566-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span><span class="sxs-lookup"><span data-stu-id="4a566-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="4a566-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="4a566-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
