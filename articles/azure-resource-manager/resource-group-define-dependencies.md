---
title: Set deployment order for Azure resources | Microsoft Docs
description: Describes how to set one resource as dependent on another resource during deployment to ensure resources are deployed in the correct order.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: ''
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 006d8e10acd6b4b756c0b78988176f71c3802080
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553526"
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="b840b-103">Define the order for deploying resources in Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="b840b-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="b840b-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span><span class="sxs-lookup"><span data-stu-id="b840b-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="b840b-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span><span class="sxs-lookup"><span data-stu-id="b840b-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="b840b-106">You define this relationship by marking one resource as dependent on the other resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="b840b-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span><span class="sxs-lookup"><span data-stu-id="b840b-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="b840b-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span><span class="sxs-lookup"><span data-stu-id="b840b-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="b840b-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span><span class="sxs-lookup"><span data-stu-id="b840b-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="b840b-110">You only need to define dependencies for resources that are deployed in the same template.</span><span class="sxs-lookup"><span data-stu-id="b840b-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="b840b-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="b840b-111">dependsOn</span></span>
<span data-ttu-id="b840b-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span><span class="sxs-lookup"><span data-stu-id="b840b-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="b840b-113">Its value can be a comma-separated list of resource names.</span><span class="sxs-lookup"><span data-stu-id="b840b-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="b840b-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span><span class="sxs-lookup"><span data-stu-id="b840b-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="b840b-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span><span class="sxs-lookup"><span data-stu-id="b840b-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="b840b-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="b840b-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="b840b-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b840b-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="b840b-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span><span class="sxs-lookup"><span data-stu-id="b840b-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="b840b-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span><span class="sxs-lookup"><span data-stu-id="b840b-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="b840b-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span><span class="sxs-lookup"><span data-stu-id="b840b-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="b840b-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span><span class="sxs-lookup"><span data-stu-id="b840b-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="b840b-122">You cannot query which resources were defined in the dependsOn element after deployment.</span><span class="sxs-lookup"><span data-stu-id="b840b-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="b840b-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="b840b-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="b840b-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="b840b-125">Child resources</span><span class="sxs-lookup"><span data-stu-id="b840b-125">Child resources</span></span>
<span data-ttu-id="b840b-126">The resources property allows you to specify child resources that are related to the resource being defined.</span><span class="sxs-lookup"><span data-stu-id="b840b-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="b840b-127">Child resources can only be defined five levels deep.</span><span class="sxs-lookup"><span data-stu-id="b840b-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="b840b-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="b840b-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span><span class="sxs-lookup"><span data-stu-id="b840b-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="b840b-130">Each parent resource accepts only certain resource types as child resources.</span><span class="sxs-lookup"><span data-stu-id="b840b-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="b840b-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="b840b-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="b840b-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="b840b-133">The following example shows a SQL server and SQL database.</span><span class="sxs-lookup"><span data-stu-id="b840b-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="b840b-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span><span class="sxs-lookup"><span data-stu-id="b840b-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="b840b-135">reference function</span><span class="sxs-lookup"><span data-stu-id="b840b-135">reference function</span></span>
<span data-ttu-id="b840b-136">The [reference function](resource-group-template-functions.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span><span class="sxs-lookup"><span data-stu-id="b840b-136">The [reference function](resource-group-template-functions.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="b840b-137">Reference expressions implicitly declare that one resource depends on another.</span><span class="sxs-lookup"><span data-stu-id="b840b-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="b840b-138">The general format is:</span><span class="sxs-lookup"><span data-stu-id="b840b-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="b840b-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span><span class="sxs-lookup"><span data-stu-id="b840b-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="b840b-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="b840b-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="b840b-142">To learn more, see [reference function](resource-group-template-functions.md#reference).</span><span class="sxs-lookup"><span data-stu-id="b840b-142">To learn more, see [reference function](resource-group-template-functions.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="b840b-143">Recommendations for setting dependencies</span><span class="sxs-lookup"><span data-stu-id="b840b-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="b840b-144">When deciding what dependencies to set, use the following guidelines:</span><span class="sxs-lookup"><span data-stu-id="b840b-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="b840b-145">Set as few dependencies as possible.</span><span class="sxs-lookup"><span data-stu-id="b840b-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="b840b-146">Set a child resource as dependent on its parent resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="b840b-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span><span class="sxs-lookup"><span data-stu-id="b840b-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="b840b-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="b840b-149">This approach reduces the risk of having unnecessary dependencies.</span><span class="sxs-lookup"><span data-stu-id="b840b-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="b840b-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="b840b-151">Do not set a dependency if the resources only interact after deployment.</span><span class="sxs-lookup"><span data-stu-id="b840b-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="b840b-152">Let dependencies cascade without setting them explicitly.</span><span class="sxs-lookup"><span data-stu-id="b840b-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="b840b-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b840b-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="b840b-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span><span class="sxs-lookup"><span data-stu-id="b840b-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="b840b-155">This approach clarifies the dependency order and makes it easier to change the template later.</span><span class="sxs-lookup"><span data-stu-id="b840b-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="b840b-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="b840b-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="b840b-158">This guidance does not always work because some resources verify the existence of the other resource.</span><span class="sxs-lookup"><span data-stu-id="b840b-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="b840b-159">If you receive an error, add a dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="b840b-160">Resource Manager identifies circular dependencies during template validation.</span><span class="sxs-lookup"><span data-stu-id="b840b-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="b840b-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span><span class="sxs-lookup"><span data-stu-id="b840b-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="b840b-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span><span class="sxs-lookup"><span data-stu-id="b840b-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="b840b-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span><span class="sxs-lookup"><span data-stu-id="b840b-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="b840b-164">You can deploy them in the following order:</span><span class="sxs-lookup"><span data-stu-id="b840b-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="b840b-165">vm1</span><span class="sxs-lookup"><span data-stu-id="b840b-165">vm1</span></span>
2. <span data-ttu-id="b840b-166">vm2</span><span class="sxs-lookup"><span data-stu-id="b840b-166">vm2</span></span>
3. <span data-ttu-id="b840b-167">Extension on vm1 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="b840b-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="b840b-168">The extension sets values on vm1 that it gets from vm2.</span><span class="sxs-lookup"><span data-stu-id="b840b-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="b840b-169">Extension on vm2 depends on vm1 and vm2.</span><span class="sxs-lookup"><span data-stu-id="b840b-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="b840b-170">The extension sets values on vm2 that it gets from vm1.</span><span class="sxs-lookup"><span data-stu-id="b840b-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="b840b-171">For information about assessing the deployment order and resolving dependency errors, see [Check deployment sequence](resource-manager-common-deployment-errors.md#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="b840b-171">For information about assessing the deployment order and resolving dependency errors, see [Check deployment sequence](resource-manager-common-deployment-errors.md#check-deployment-sequence).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b840b-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="b840b-172">Next steps</span></span>
* <span data-ttu-id="b840b-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b840b-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b840b-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b840b-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="b840b-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="b840b-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

