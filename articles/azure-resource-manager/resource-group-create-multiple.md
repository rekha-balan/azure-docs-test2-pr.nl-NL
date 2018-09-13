---
title: Deploy multiple instances of Azure resources | Microsoft Docs
description: Use copy operation and arrays in an Azure Resource Manager template to iterate multiple times when deploying resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: ''
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8ecf7c058b90fd18e41fd4e1cbc29e22dfeb0883
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670873"
---
# <a name="deploy-multiple-instances-of-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="d57ad-103">Deploy multiple instances of resources in Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="d57ad-103">Deploy multiple instances of resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="d57ad-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource.</span><span class="sxs-lookup"><span data-stu-id="d57ad-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource.</span></span>

## <a name="copy-and-copyindex"></a><span data-ttu-id="d57ad-105">copy and copyIndex</span><span class="sxs-lookup"><span data-stu-id="d57ad-105">copy and copyIndex</span></span>
<span data-ttu-id="d57ad-106">The resource to create multiple times takes the following format:</span><span class="sxs-lookup"><span data-stu-id="d57ad-106">The resource to create multiple times takes the following format:</span></span>

```json
"resources": [ 
  { 
      "name": "[concat('examplecopy-', copyIndex())", 
      "type": "Microsoft.Web/sites", 
      "location": "East US", 
      "apiVersion": "2015-08-01",
      "copy": { 
         "name": "websitescopy", 
         "count": "[parameters('count')]" 
      }, 
      "properties": {
          "serverFarmId": "hostingPlanName"
      } 
  } 
]
```

<span data-ttu-id="d57ad-107">Notice that the number of times to iterate is specified in the copy object:</span><span class="sxs-lookup"><span data-stu-id="d57ad-107">Notice that the number of times to iterate is specified in the copy object:</span></span>

```json
"copy": { 
    "name": "websitescopy", 
    "count": "[parameters('count')]" 
} 
```

<span data-ttu-id="d57ad-108">The count value must be a positive integer and cannot exceed 800.</span><span class="sxs-lookup"><span data-stu-id="d57ad-108">The count value must be a positive integer and cannot exceed 800.</span></span>

<span data-ttu-id="d57ad-109">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span><span class="sxs-lookup"><span data-stu-id="d57ad-109">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span>

```json
"name": "[concat('examplecopy-', copyIndex())]",
```

<span data-ttu-id="d57ad-110">If you deploy three web sites, they are named:</span><span class="sxs-lookup"><span data-stu-id="d57ad-110">If you deploy three web sites, they are named:</span></span>

* <span data-ttu-id="d57ad-111">examplecopy-0</span><span class="sxs-lookup"><span data-stu-id="d57ad-111">examplecopy-0</span></span>
* <span data-ttu-id="d57ad-112">examplecopy-1</span><span class="sxs-lookup"><span data-stu-id="d57ad-112">examplecopy-1</span></span>
* <span data-ttu-id="d57ad-113">examplecopy-2.</span><span class="sxs-lookup"><span data-stu-id="d57ad-113">examplecopy-2.</span></span>

<span data-ttu-id="d57ad-114">To offset the index value, you can pass a value in the copyIndex() function, such as `copyIndex(1)`.</span><span class="sxs-lookup"><span data-stu-id="d57ad-114">To offset the index value, you can pass a value in the copyIndex() function, such as `copyIndex(1)`.</span></span> <span data-ttu-id="d57ad-115">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span><span class="sxs-lookup"><span data-stu-id="d57ad-115">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="d57ad-116">So, using the same template as the previous example, but specifying copyIndex(1) would deploy three web sites named:</span><span class="sxs-lookup"><span data-stu-id="d57ad-116">So, using the same template as the previous example, but specifying copyIndex(1) would deploy three web sites named:</span></span>

* <span data-ttu-id="d57ad-117">examplecopy-1</span><span class="sxs-lookup"><span data-stu-id="d57ad-117">examplecopy-1</span></span>
* <span data-ttu-id="d57ad-118">examplecopy-2</span><span class="sxs-lookup"><span data-stu-id="d57ad-118">examplecopy-2</span></span>
* <span data-ttu-id="d57ad-119">examplecopy-3</span><span class="sxs-lookup"><span data-stu-id="d57ad-119">examplecopy-3</span></span>

<span data-ttu-id="d57ad-120">Resource Manager creates the resources in parallel.</span><span class="sxs-lookup"><span data-stu-id="d57ad-120">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="d57ad-121">Therefore, the order in which they are created is not guaranteed.</span><span class="sxs-lookup"><span data-stu-id="d57ad-121">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="d57ad-122">To create iterated resources in sequence, see [Sequential looping for Azure Resource Manager templates](resource-manager-sequential-loop.md).</span><span class="sxs-lookup"><span data-stu-id="d57ad-122">To create iterated resources in sequence, see [Sequential looping for Azure Resource Manager templates](resource-manager-sequential-loop.md).</span></span> 

<span data-ttu-id="d57ad-123">You can only apply the copy object to a top-level resource.</span><span class="sxs-lookup"><span data-stu-id="d57ad-123">You can only apply the copy object to a top-level resource.</span></span> <span data-ttu-id="d57ad-124">You cannot apply it to a property on a resource type, or to a child resource.</span><span class="sxs-lookup"><span data-stu-id="d57ad-124">You cannot apply it to a property on a resource type, or to a child resource.</span></span> <span data-ttu-id="d57ad-125">The following pseudo-code example shows where copy can be applied:</span><span class="sxs-lookup"><span data-stu-id="d57ad-125">The following pseudo-code example shows where copy can be applied:</span></span>

```json
"resources": [
  {
    "type": "{provider-namespace-and-type}",
    "name": "parentResource",
    "copy": {  
      /* Yes, copy can be applied here */
    },
    "properties": {
      "exampleProperty": {
        /* No, copy cannot be applied here */
      }
    },
    "resources": [
      {
        "type": "{provider-type}",
        "name": "childResource",
        /* No, copy cannot be applied here. The resource must be promoted to top-level. */ 
      }
    ]
  }
] 
```

<span data-ttu-id="d57ad-126">To iterate a child resource, see [Create multiple instances of a child resource](#create-multiple-instances-of-a-child-resource).</span><span class="sxs-lookup"><span data-stu-id="d57ad-126">To iterate a child resource, see [Create multiple instances of a child resource](#create-multiple-instances-of-a-child-resource).</span></span>

<span data-ttu-id="d57ad-127">Although you cannot apply copy to a property, that property is still part of the iterations of the resource that contains the property.</span><span class="sxs-lookup"><span data-stu-id="d57ad-127">Although you cannot apply copy to a property, that property is still part of the iterations of the resource that contains the property.</span></span> <span data-ttu-id="d57ad-128">Therefore, you can use copyIndex() within the property to specify values.</span><span class="sxs-lookup"><span data-stu-id="d57ad-128">Therefore, you can use copyIndex() within the property to specify values.</span></span> <span data-ttu-id="d57ad-129">To create multiple values for a property, see [Create multiple instances of property on resource type](resource-manager-property-copy.md).</span><span class="sxs-lookup"><span data-stu-id="d57ad-129">To create multiple values for a property, see [Create multiple instances of property on resource type](resource-manager-property-copy.md).</span></span>

## <a name="use-copy-with-array"></a><span data-ttu-id="d57ad-130">Use copy with array</span><span class="sxs-lookup"><span data-stu-id="d57ad-130">Use copy with array</span></span>
<span data-ttu-id="d57ad-131">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span><span class="sxs-lookup"><span data-stu-id="d57ad-131">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="d57ad-132">To deploy three web sites named:</span><span class="sxs-lookup"><span data-stu-id="d57ad-132">To deploy three web sites named:</span></span>

* <span data-ttu-id="d57ad-133">examplecopy-Contoso</span><span class="sxs-lookup"><span data-stu-id="d57ad-133">examplecopy-Contoso</span></span>
* <span data-ttu-id="d57ad-134">examplecopy-Fabrikam</span><span class="sxs-lookup"><span data-stu-id="d57ad-134">examplecopy-Fabrikam</span></span>
* <span data-ttu-id="d57ad-135">examplecopy-Coho</span><span class="sxs-lookup"><span data-stu-id="d57ad-135">examplecopy-Coho</span></span>

<span data-ttu-id="d57ad-136">Use the following template:</span><span class="sxs-lookup"><span data-stu-id="d57ad-136">Use the following template:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "Contoso", 
         "Fabrikam", 
         "Coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('examplecopy-', parameters('org')[copyIndex()])]", 
      "type": "Microsoft.Web/sites", 
      "location": "East US", 
      "apiVersion": "2015-08-01",
      "copy": { 
         "name": "websitescopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      "properties": {
          "serverFarmId": "hostingPlanName"
      } 
  } 
]
```

<span data-ttu-id="d57ad-137">Notice that the `length` function is used to specify the count.</span><span class="sxs-lookup"><span data-stu-id="d57ad-137">Notice that the `length` function is used to specify the count.</span></span> <span data-ttu-id="d57ad-138">You provide the array as the parameter to the length function.</span><span class="sxs-lookup"><span data-stu-id="d57ad-138">You provide the array as the parameter to the length function.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="d57ad-139">Depend on resources in a loop</span><span class="sxs-lookup"><span data-stu-id="d57ad-139">Depend on resources in a loop</span></span>
<span data-ttu-id="d57ad-140">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span><span class="sxs-lookup"><span data-stu-id="d57ad-140">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="d57ad-141">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span><span class="sxs-lookup"><span data-stu-id="d57ad-141">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="d57ad-142">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="d57ad-142">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="d57ad-143">The full Virtual Machine definition is not shown.</span><span class="sxs-lookup"><span data-stu-id="d57ad-143">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="d57ad-144">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="d57ad-144">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2015-06-15",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat('storage', uniqueString(resourceGroup().id), copyIndex())]",
            "location": "[resourceGroup().location]",
            "properties": {
                "accountType": "Standard_LRS"
            },
            "copy": { 
                "name": "storagecopy", 
                "count": 3 
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="d57ad-145">Create multiple instances of a child resource</span><span class="sxs-lookup"><span data-stu-id="d57ad-145">Create multiple instances of a child resource</span></span>
<span data-ttu-id="d57ad-146">You cannot use a copy loop for a child resource.</span><span class="sxs-lookup"><span data-stu-id="d57ad-146">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="d57ad-147">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span><span class="sxs-lookup"><span data-stu-id="d57ad-147">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="d57ad-148">You define the relationship with the parent resource through the type and name properties.</span><span class="sxs-lookup"><span data-stu-id="d57ad-148">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="d57ad-149">For example, suppose you typically define a dataset as a child resource within a data factory.</span><span class="sxs-lookup"><span data-stu-id="d57ad-149">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="d57ad-150">To create multiple instances of data sets, move it outside of the data factory.</span><span class="sxs-lookup"><span data-stu-id="d57ad-150">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="d57ad-151">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span><span class="sxs-lookup"><span data-stu-id="d57ad-151">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="d57ad-152">You preserve the relationship between data set and data factory through the type and name properties.</span><span class="sxs-lookup"><span data-stu-id="d57ad-152">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="d57ad-153">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="d57ad-153">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="d57ad-154">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span><span class="sxs-lookup"><span data-stu-id="d57ad-154">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="d57ad-155">Use the format: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="d57ad-155">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="d57ad-156">The following example shows the implementation:</span><span class="sxs-lookup"><span data-stu-id="d57ad-156">The following example shows the implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="next-steps"></a><span data-ttu-id="d57ad-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="d57ad-157">Next steps</span></span>
* <span data-ttu-id="d57ad-158">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d57ad-158">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d57ad-159">To create iterated resources in sequence, see [Sequential looping for Azure Resource Manager templates](resource-manager-sequential-loop.md).</span><span class="sxs-lookup"><span data-stu-id="d57ad-159">To create iterated resources in sequence, see [Sequential looping for Azure Resource Manager templates](resource-manager-sequential-loop.md).</span></span>
* <span data-ttu-id="d57ad-160">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d57ad-160">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

