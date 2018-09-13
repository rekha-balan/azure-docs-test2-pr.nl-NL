---
title: Azure Resource Manager template variables | Microsoft Docs
description: Describes how to define variables in an Azure Resource Manager templates using declarative JSON syntax.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2017
ms.author: tomfitz
ms.openlocfilehash: 08728a3c0b4d4578939004e2d1b1ee2d30a682ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864577"
---
# <a name="variables-section-of-azure-resource-manager-templates"></a><span data-ttu-id="02c40-103">Variables section of Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="02c40-103">Variables section of Azure Resource Manager templates</span></span>
<span data-ttu-id="02c40-104">In the variables section, you construct values that can be used throughout your template.</span><span class="sxs-lookup"><span data-stu-id="02c40-104">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="02c40-105">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span><span class="sxs-lookup"><span data-stu-id="02c40-105">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

## <a name="define-and-use-a-variable"></a><span data-ttu-id="02c40-106">Define and use a variable</span><span class="sxs-lookup"><span data-stu-id="02c40-106">Define and use a variable</span></span>

<span data-ttu-id="02c40-107">The following example shows a variable definition.</span><span class="sxs-lookup"><span data-stu-id="02c40-107">The following example shows a variable definition.</span></span> <span data-ttu-id="02c40-108">It creates a string value for a storage account name.</span><span class="sxs-lookup"><span data-stu-id="02c40-108">It creates a string value for a storage account name.</span></span> <span data-ttu-id="02c40-109">It uses several template functions to get a parameter value, and concatenate it to a unique string.</span><span class="sxs-lookup"><span data-stu-id="02c40-109">It uses several template functions to get a parameter value, and concatenate it to a unique string.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="02c40-110">You use the variable when defining the resource.</span><span class="sxs-lookup"><span data-stu-id="02c40-110">You use the variable when defining the resource.</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    ...
```

## <a name="available-definitions"></a><span data-ttu-id="02c40-111">Available definitions</span><span class="sxs-lookup"><span data-stu-id="02c40-111">Available definitions</span></span>

<span data-ttu-id="02c40-112">The preceding example showed one way to define a variable.</span><span class="sxs-lookup"><span data-stu-id="02c40-112">The preceding example showed one way to define a variable.</span></span> <span data-ttu-id="02c40-113">You can use any of the following definitions:</span><span class="sxs-lookup"><span data-stu-id="02c40-113">You can use any of the following definitions:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    },
    "<variable-object-name>": {
        "copy": [
            {
                "name": "<name-of-array-property>",
                "count": <number-of-iterations>,
                "input": {
                    <properties-to-repeat>
                }
            }
        ]
    },
    "copy": [
        {
            "name": "<variable-array-name>",
            "count": <number-of-iterations>,
            "input": {
                <properties-to-repeat>
            }
        }
    ]
}
```

## <a name="configuration-variables"></a><span data-ttu-id="02c40-114">Configuration variables</span><span class="sxs-lookup"><span data-stu-id="02c40-114">Configuration variables</span></span>

<span data-ttu-id="02c40-115">You can use complex JSON types to define related values for an environment.</span><span class="sxs-lookup"><span data-stu-id="02c40-115">You can use complex JSON types to define related values for an environment.</span></span> 

```json
"variables": {
    "environmentSettings": {
        "test": {
            "instanceSize": "Small",
            "instanceCount": 1
        },
        "prod": {
            "instanceSize": "Large",
            "instanceCount": 4
        }
    }
},
```

<span data-ttu-id="02c40-116">In parameters, you create a value that indicates which configuration values to use.</span><span class="sxs-lookup"><span data-stu-id="02c40-116">In parameters, you create a value that indicates which configuration values to use.</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
```

<span data-ttu-id="02c40-117">You retrieve the current settings with:</span><span class="sxs-lookup"><span data-stu-id="02c40-117">You retrieve the current settings with:</span></span>

```json
"[variables('environmentSettings')[parameters('environmentName')].instanceSize]"
```

## <a name="use-copy-element-in-variable-definition"></a><span data-ttu-id="02c40-118">Use copy element in variable definition</span><span class="sxs-lookup"><span data-stu-id="02c40-118">Use copy element in variable definition</span></span>

<span data-ttu-id="02c40-119">You can use the **copy** syntax to create a variable with an array of multiple elements.</span><span class="sxs-lookup"><span data-stu-id="02c40-119">You can use the **copy** syntax to create a variable with an array of multiple elements.</span></span> <span data-ttu-id="02c40-120">You provide a count for the number of elements.</span><span class="sxs-lookup"><span data-stu-id="02c40-120">You provide a count for the number of elements.</span></span> <span data-ttu-id="02c40-121">Each element contains the properties within the **input** object.</span><span class="sxs-lookup"><span data-stu-id="02c40-121">Each element contains the properties within the **input** object.</span></span> <span data-ttu-id="02c40-122">You can use copy either within a variable or to create the variable.</span><span class="sxs-lookup"><span data-stu-id="02c40-122">You can use copy either within a variable or to create the variable.</span></span> <span data-ttu-id="02c40-123">When you define a variable and use **copy** within that variable, you create an object that has an array property.</span><span class="sxs-lookup"><span data-stu-id="02c40-123">When you define a variable and use **copy** within that variable, you create an object that has an array property.</span></span> <span data-ttu-id="02c40-124">When you use **copy** at the top level and define one or more variables within it, you create one or more arrays.</span><span class="sxs-lookup"><span data-stu-id="02c40-124">When you use **copy** at the top level and define one or more variables within it, you create one or more arrays.</span></span> <span data-ttu-id="02c40-125">Both approaches are shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="02c40-125">Both approaches are shown in the following example:</span></span>

```json
"variables": {
    "disk-array-on-object": {
        "copy": [
            {
                "name": "disks",
                "count": 3,
                "input": {
                    "name": "[concat('myDataDisk', copyIndex('disks', 1))]",
                    "diskSizeGB": "1",
                    "diskIndex": "[copyIndex('disks')]"
                }
            }
        ]
    },
    "copy": [
        {
            "name": "disks-top-level-array",
            "count": 3,
            "input": {
                "name": "[concat('myDataDisk', copyIndex('disks-top-level-array', 1))]",
                "diskSizeGB": "1",
                "diskIndex": "[copyIndex('disks-top-level-array')]"
            }
        }
    ]
},
```

<span data-ttu-id="02c40-126">The variable **disk-array-on-object** contains the following object with an array named **disks**:</span><span class="sxs-lookup"><span data-stu-id="02c40-126">The variable **disk-array-on-object** contains the following object with an array named **disks**:</span></span>

```json
{
  "disks": [
    {
      "name": "myDataDisk1",
      "diskSizeGB": "1",
      "diskIndex": 0
    },
    {
      "name": "myDataDisk2",
      "diskSizeGB": "1",
      "diskIndex": 1
    },
    {
      "name": "myDataDisk3",
      "diskSizeGB": "1",
      "diskIndex": 2
    }
  ]
}
```

<span data-ttu-id="02c40-127">The variable **disks-top-level-array** contains the following array:</span><span class="sxs-lookup"><span data-stu-id="02c40-127">The variable **disks-top-level-array** contains the following array:</span></span>

```json
[
  {
    "name": "myDataDisk1",
    "diskSizeGB": "1",
    "diskIndex": 0
  },
  {
    "name": "myDataDisk2",
    "diskSizeGB": "1",
    "diskIndex": 1
  },
  {
    "name": "myDataDisk3",
    "diskSizeGB": "1",
    "diskIndex": 2
  }
]
```

<span data-ttu-id="02c40-128">You can also specify more than one object when using copy to create variables.</span><span class="sxs-lookup"><span data-stu-id="02c40-128">You can also specify more than one object when using copy to create variables.</span></span> <span data-ttu-id="02c40-129">The following example defines two arrays as variables.</span><span class="sxs-lookup"><span data-stu-id="02c40-129">The following example defines two arrays as variables.</span></span> <span data-ttu-id="02c40-130">One is named **disks-top-level-array** and has five elements.</span><span class="sxs-lookup"><span data-stu-id="02c40-130">One is named **disks-top-level-array** and has five elements.</span></span> <span data-ttu-id="02c40-131">The other is named **a-different-array** and has three elements.</span><span class="sxs-lookup"><span data-stu-id="02c40-131">The other is named **a-different-array** and has three elements.</span></span>

```json
"variables": {
    "copy": [
        {
            "name": "disks-top-level-array",
            "count": 5,
            "input": {
                "name": "[concat('oneDataDisk', copyIndex('disks-top-level-array', 1))]",
                "diskSizeGB": "1",
                "diskIndex": "[copyIndex('disks-top-level-array')]"
            }
        },
        {
            "name": "a-different-array",
            "count": 3,
            "input": {
                "name": "[concat('twoDataDisk', copyIndex('a-different-array', 1))]",
                "diskSizeGB": "1",
                "diskIndex": "[copyIndex('a-different-array')]"
            }
        }
    ]
},
```

<span data-ttu-id="02c40-132">This approach works well when you need to take parameter values and make sure they are in the correct format for a template value.</span><span class="sxs-lookup"><span data-stu-id="02c40-132">This approach works well when you need to take parameter values and make sure they are in the correct format for a template value.</span></span> <span data-ttu-id="02c40-133">The following example formats parameter values for use in defining security rules:</span><span class="sxs-lookup"><span data-stu-id="02c40-133">The following example formats parameter values for use in defining security rules:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "securityRules": {
      "type": "array"
    }
  },
  "variables": {
    "copy": [
      {
        "name": "securityRules",
        "count": "[length(parameters('securityRules'))]",
        "input": {
          "name": "[parameters('securityRules')[copyIndex('securityRules')].name]",
          "properties": {
            "description": "[parameters('securityRules')[copyIndex('securityRules')].description]",
            "priority": "[parameters('securityRules')[copyIndex('securityRules')].priority]",
            "protocol": "[parameters('securityRules')[copyIndex('securityRules')].protocol]",
            "sourcePortRange": "[parameters('securityRules')[copyIndex('securityRules')].sourcePortRange]",
            "destinationPortRange": "[parameters('securityRules')[copyIndex('securityRules')].destinationPortRange]",
            "sourceAddressPrefix": "[parameters('securityRules')[copyIndex('securityRules')].sourceAddressPrefix]",
            "destinationAddressPrefix": "[parameters('securityRules')[copyIndex('securityRules')].destinationAddressPrefix]",
            "access": "[parameters('securityRules')[copyIndex('securityRules')].access]",
            "direction": "[parameters('securityRules')[copyIndex('securityRules')].direction]"
          }
        }
      }
    ]
  },
  "resources": [
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkSecurityGroups",
      "name": "NSG1",
      "location": "[resourceGroup().location]",
      "properties": {
        "securityRules": "[variables('securityRules')]"
      }
    }
  ],
  "outputs": {}
}
```

## <a name="recommendations"></a><span data-ttu-id="02c40-134">Recommendations</span><span class="sxs-lookup"><span data-stu-id="02c40-134">Recommendations</span></span>
<span data-ttu-id="02c40-135">The following information can be helpful when you work with variables:</span><span class="sxs-lookup"><span data-stu-id="02c40-135">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="02c40-136">Use variables for values that you need to use more than once in a template.</span><span class="sxs-lookup"><span data-stu-id="02c40-136">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="02c40-137">If a value is used only once, a hard-coded value makes your template easier to read.</span><span class="sxs-lookup"><span data-stu-id="02c40-137">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="02c40-138">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span><span class="sxs-lookup"><span data-stu-id="02c40-138">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="02c40-139">The **reference** function derives its value from the resource's runtime state.</span><span class="sxs-lookup"><span data-stu-id="02c40-139">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="02c40-140">However, variables are resolved during the initial parsing of the template.</span><span class="sxs-lookup"><span data-stu-id="02c40-140">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="02c40-141">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span><span class="sxs-lookup"><span data-stu-id="02c40-141">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="02c40-142">Include variables for resource names that must be unique.</span><span class="sxs-lookup"><span data-stu-id="02c40-142">Include variables for resource names that must be unique.</span></span>

## <a name="example-templates"></a><span data-ttu-id="02c40-143">Example templates</span><span class="sxs-lookup"><span data-stu-id="02c40-143">Example templates</span></span>

<span data-ttu-id="02c40-144">These example templates demonstrate some scenarios for using variables.</span><span class="sxs-lookup"><span data-stu-id="02c40-144">These example templates demonstrate some scenarios for using variables.</span></span> <span data-ttu-id="02c40-145">Deploy them to test how variables are handled in different scenarios.</span><span class="sxs-lookup"><span data-stu-id="02c40-145">Deploy them to test how variables are handled in different scenarios.</span></span> 

|<span data-ttu-id="02c40-146">Template</span><span class="sxs-lookup"><span data-stu-id="02c40-146">Template</span></span>  |<span data-ttu-id="02c40-147">Description</span><span class="sxs-lookup"><span data-stu-id="02c40-147">Description</span></span>  |
|---------|---------|
| [<span data-ttu-id="02c40-148">variable definitions</span><span class="sxs-lookup"><span data-stu-id="02c40-148">variable definitions</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/variables.json) | <span data-ttu-id="02c40-149">Demonstrates the different types of variables.</span><span class="sxs-lookup"><span data-stu-id="02c40-149">Demonstrates the different types of variables.</span></span> <span data-ttu-id="02c40-150">The template does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="02c40-150">The template does not deploy any resources.</span></span> <span data-ttu-id="02c40-151">It constructs variable values and returns those values.</span><span class="sxs-lookup"><span data-stu-id="02c40-151">It constructs variable values and returns those values.</span></span> |
| [<span data-ttu-id="02c40-152">configuration variable</span><span class="sxs-lookup"><span data-stu-id="02c40-152">configuration variable</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/variablesconfigurations.json) | <span data-ttu-id="02c40-153">Demonstrates the use of a variable that defines configuration values.</span><span class="sxs-lookup"><span data-stu-id="02c40-153">Demonstrates the use of a variable that defines configuration values.</span></span> <span data-ttu-id="02c40-154">The template does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="02c40-154">The template does not deploy any resources.</span></span> <span data-ttu-id="02c40-155">It constructs variable values and returns those values.</span><span class="sxs-lookup"><span data-stu-id="02c40-155">It constructs variable values and returns those values.</span></span> |
| <span data-ttu-id="02c40-156">[network security rules](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/multiplesecurityrules.json) and [parameter file](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/multiplesecurityrules.parameters.json)</span><span class="sxs-lookup"><span data-stu-id="02c40-156">[network security rules](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/multiplesecurityrules.json) and [parameter file](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/multiplesecurityrules.parameters.json)</span></span> | <span data-ttu-id="02c40-157">Constructs an array in the correct format for assigning security rules to a network security group.</span><span class="sxs-lookup"><span data-stu-id="02c40-157">Constructs an array in the correct format for assigning security rules to a network security group.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="02c40-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="02c40-158">Next steps</span></span>
* <span data-ttu-id="02c40-159">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="02c40-159">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="02c40-160">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="02c40-160">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="02c40-161">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="02c40-161">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="02c40-162">You may need to use resources that exist within a different resource group.</span><span class="sxs-lookup"><span data-stu-id="02c40-162">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="02c40-163">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span><span class="sxs-lookup"><span data-stu-id="02c40-163">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="02c40-164">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="02c40-164">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>