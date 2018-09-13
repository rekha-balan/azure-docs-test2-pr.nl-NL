---
title: Azure Resource Manager template functions - numeric | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to work with numbers.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/08/2017
ms.author: tomfitz
ms.openlocfilehash: 4fc17b997c44560199e65edb01d20c6a24e49877
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869412"
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="d441c-103">Numeric functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="d441c-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="d441c-104">Resource Manager provides the following functions for working with integers:</span><span class="sxs-lookup"><span data-stu-id="d441c-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="d441c-105">add</span><span class="sxs-lookup"><span data-stu-id="d441c-105">add</span></span>](#add)
* [<span data-ttu-id="d441c-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="d441c-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="d441c-107">div</span><span class="sxs-lookup"><span data-stu-id="d441c-107">div</span></span>](#div)
* [<span data-ttu-id="d441c-108">float</span><span class="sxs-lookup"><span data-stu-id="d441c-108">float</span></span>](#float)
* [<span data-ttu-id="d441c-109">int</span><span class="sxs-lookup"><span data-stu-id="d441c-109">int</span></span>](#int)
* [<span data-ttu-id="d441c-110">max</span><span class="sxs-lookup"><span data-stu-id="d441c-110">max</span></span>](#max)
* [<span data-ttu-id="d441c-111">min</span><span class="sxs-lookup"><span data-stu-id="d441c-111">min</span></span>](#min)
* [<span data-ttu-id="d441c-112">mod</span><span class="sxs-lookup"><span data-stu-id="d441c-112">mod</span></span>](#mod)
* [<span data-ttu-id="d441c-113">mul</span><span class="sxs-lookup"><span data-stu-id="d441c-113">mul</span></span>](#mul)
* [<span data-ttu-id="d441c-114">sub</span><span class="sxs-lookup"><span data-stu-id="d441c-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="d441c-115">add</span><span class="sxs-lookup"><span data-stu-id="d441c-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="d441c-116">Returns the sum of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-117">Parameters</span></span>

| <span data-ttu-id="d441c-118">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-118">Parameter</span></span> | <span data-ttu-id="d441c-119">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-119">Required</span></span> | <span data-ttu-id="d441c-120">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-120">Type</span></span> | <span data-ttu-id="d441c-121">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="d441c-122">operand1</span><span class="sxs-lookup"><span data-stu-id="d441c-122">operand1</span></span> |<span data-ttu-id="d441c-123">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-123">Yes</span></span> |<span data-ttu-id="d441c-124">int</span><span class="sxs-lookup"><span data-stu-id="d441c-124">int</span></span> |<span data-ttu-id="d441c-125">First number to add.</span><span class="sxs-lookup"><span data-stu-id="d441c-125">First number to add.</span></span> |
|<span data-ttu-id="d441c-126">operand2</span><span class="sxs-lookup"><span data-stu-id="d441c-126">operand2</span></span> |<span data-ttu-id="d441c-127">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-127">Yes</span></span> |<span data-ttu-id="d441c-128">int</span><span class="sxs-lookup"><span data-stu-id="d441c-128">int</span></span> |<span data-ttu-id="d441c-129">Second number to add.</span><span class="sxs-lookup"><span data-stu-id="d441c-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-130">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-130">Return value</span></span>

<span data-ttu-id="d441c-131">An integer that contains the sum of the parameters.</span><span class="sxs-lookup"><span data-stu-id="d441c-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-132">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-132">Example</span></span>

<span data-ttu-id="d441c-133">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/add.json) adds two parameters.</span><span class="sxs-lookup"><span data-stu-id="d441c-133">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/add.json) adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="d441c-134">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-135">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-135">Name</span></span> | <span data-ttu-id="d441c-136">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-136">Type</span></span> | <span data-ttu-id="d441c-137">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-138">addResult</span><span class="sxs-lookup"><span data-stu-id="d441c-138">addResult</span></span> | <span data-ttu-id="d441c-139">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-139">Int</span></span> | <span data-ttu-id="d441c-140">8</span><span class="sxs-lookup"><span data-stu-id="d441c-140">8</span></span> |

<span data-ttu-id="d441c-141">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-141">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/add.json
```

<span data-ttu-id="d441c-142">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-142">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/add.json 
```

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="d441c-143">copyIndex</span><span class="sxs-lookup"><span data-stu-id="d441c-143">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="d441c-144">Returns the index of an iteration loop.</span><span class="sxs-lookup"><span data-stu-id="d441c-144">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="d441c-145">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-145">Parameters</span></span>

| <span data-ttu-id="d441c-146">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-146">Parameter</span></span> | <span data-ttu-id="d441c-147">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-147">Required</span></span> | <span data-ttu-id="d441c-148">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-148">Type</span></span> | <span data-ttu-id="d441c-149">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-149">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-150">loopName</span><span class="sxs-lookup"><span data-stu-id="d441c-150">loopName</span></span> | <span data-ttu-id="d441c-151">No</span><span class="sxs-lookup"><span data-stu-id="d441c-151">No</span></span> | <span data-ttu-id="d441c-152">string</span><span class="sxs-lookup"><span data-stu-id="d441c-152">string</span></span> | <span data-ttu-id="d441c-153">The name of the loop for getting the iteration.</span><span class="sxs-lookup"><span data-stu-id="d441c-153">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="d441c-154">offset</span><span class="sxs-lookup"><span data-stu-id="d441c-154">offset</span></span> |<span data-ttu-id="d441c-155">No</span><span class="sxs-lookup"><span data-stu-id="d441c-155">No</span></span> |<span data-ttu-id="d441c-156">int</span><span class="sxs-lookup"><span data-stu-id="d441c-156">int</span></span> |<span data-ttu-id="d441c-157">The number to add to the zero-based iteration value.</span><span class="sxs-lookup"><span data-stu-id="d441c-157">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="d441c-158">Remarks</span><span class="sxs-lookup"><span data-stu-id="d441c-158">Remarks</span></span>

<span data-ttu-id="d441c-159">This function is always used with a **copy** object.</span><span class="sxs-lookup"><span data-stu-id="d441c-159">This function is always used with a **copy** object.</span></span> <span data-ttu-id="d441c-160">If no value is provided for **offset**, the current iteration value is returned.</span><span class="sxs-lookup"><span data-stu-id="d441c-160">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="d441c-161">The iteration value starts at zero.</span><span class="sxs-lookup"><span data-stu-id="d441c-161">The iteration value starts at zero.</span></span> <span data-ttu-id="d441c-162">You can use iteration loops when defining either resources or variables.</span><span class="sxs-lookup"><span data-stu-id="d441c-162">You can use iteration loops when defining either resources or variables.</span></span>

<span data-ttu-id="d441c-163">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span><span class="sxs-lookup"><span data-stu-id="d441c-163">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="d441c-164">If no value is provided for **loopName**, the current resource type iteration is used.</span><span class="sxs-lookup"><span data-stu-id="d441c-164">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="d441c-165">Provide a value for **loopName** when iterating on a property.</span><span class="sxs-lookup"><span data-stu-id="d441c-165">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="d441c-166">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d441c-166">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="d441c-167">For an example of using **copyIndex** when defining a variable, see [Variables](resource-group-authoring-templates.md#variables).</span><span class="sxs-lookup"><span data-stu-id="d441c-167">For an example of using **copyIndex** when defining a variable, see [Variables](resource-group-authoring-templates.md#variables).</span></span>

### <a name="example"></a><span data-ttu-id="d441c-168">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-168">Example</span></span>

<span data-ttu-id="d441c-169">The following example shows a copy loop and the index value included in the name.</span><span class="sxs-lookup"><span data-stu-id="d441c-169">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="d441c-170">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-170">Return value</span></span>

<span data-ttu-id="d441c-171">An integer representing the current index of the iteration.</span><span class="sxs-lookup"><span data-stu-id="d441c-171">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="d441c-172">div</span><span class="sxs-lookup"><span data-stu-id="d441c-172">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="d441c-173">Returns the integer division of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-173">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-174">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-174">Parameters</span></span>

| <span data-ttu-id="d441c-175">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-175">Parameter</span></span> | <span data-ttu-id="d441c-176">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-176">Required</span></span> | <span data-ttu-id="d441c-177">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-177">Type</span></span> | <span data-ttu-id="d441c-178">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-178">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-179">operand1</span><span class="sxs-lookup"><span data-stu-id="d441c-179">operand1</span></span> |<span data-ttu-id="d441c-180">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-180">Yes</span></span> |<span data-ttu-id="d441c-181">int</span><span class="sxs-lookup"><span data-stu-id="d441c-181">int</span></span> |<span data-ttu-id="d441c-182">The number being divided.</span><span class="sxs-lookup"><span data-stu-id="d441c-182">The number being divided.</span></span> |
| <span data-ttu-id="d441c-183">operand2</span><span class="sxs-lookup"><span data-stu-id="d441c-183">operand2</span></span> |<span data-ttu-id="d441c-184">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-184">Yes</span></span> |<span data-ttu-id="d441c-185">int</span><span class="sxs-lookup"><span data-stu-id="d441c-185">int</span></span> |<span data-ttu-id="d441c-186">The number that is used to divide.</span><span class="sxs-lookup"><span data-stu-id="d441c-186">The number that is used to divide.</span></span> <span data-ttu-id="d441c-187">Cannot be 0.</span><span class="sxs-lookup"><span data-stu-id="d441c-187">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-188">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-188">Return value</span></span>

<span data-ttu-id="d441c-189">An integer representing the division.</span><span class="sxs-lookup"><span data-stu-id="d441c-189">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-190">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-190">Example</span></span>

<span data-ttu-id="d441c-191">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/div.json) divides one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="d441c-191">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/div.json) divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="d441c-192">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-192">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-193">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-193">Name</span></span> | <span data-ttu-id="d441c-194">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-194">Type</span></span> | <span data-ttu-id="d441c-195">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-195">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-196">divResult</span><span class="sxs-lookup"><span data-stu-id="d441c-196">divResult</span></span> | <span data-ttu-id="d441c-197">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-197">Int</span></span> | <span data-ttu-id="d441c-198">2</span><span class="sxs-lookup"><span data-stu-id="d441c-198">2</span></span> |

<span data-ttu-id="d441c-199">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-199">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/div.json
```

<span data-ttu-id="d441c-200">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-200">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/div.json 
```

<a id="float" />

## <a name="float"></a><span data-ttu-id="d441c-201">float</span><span class="sxs-lookup"><span data-stu-id="d441c-201">float</span></span>
`float(arg1)`

<span data-ttu-id="d441c-202">Converts the value to a floating point number.</span><span class="sxs-lookup"><span data-stu-id="d441c-202">Converts the value to a floating point number.</span></span> <span data-ttu-id="d441c-203">You only use this function when passing custom parameters to an application, such as a Logic App.</span><span class="sxs-lookup"><span data-stu-id="d441c-203">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-204">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-204">Parameters</span></span>

| <span data-ttu-id="d441c-205">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-205">Parameter</span></span> | <span data-ttu-id="d441c-206">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-206">Required</span></span> | <span data-ttu-id="d441c-207">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-207">Type</span></span> | <span data-ttu-id="d441c-208">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-208">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-209">arg1</span><span class="sxs-lookup"><span data-stu-id="d441c-209">arg1</span></span> |<span data-ttu-id="d441c-210">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-210">Yes</span></span> |<span data-ttu-id="d441c-211">string or int</span><span class="sxs-lookup"><span data-stu-id="d441c-211">string or int</span></span> |<span data-ttu-id="d441c-212">The value to convert to a floating point number.</span><span class="sxs-lookup"><span data-stu-id="d441c-212">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-213">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-213">Return value</span></span>
<span data-ttu-id="d441c-214">A floating point number.</span><span class="sxs-lookup"><span data-stu-id="d441c-214">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-215">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-215">Example</span></span>

<span data-ttu-id="d441c-216">The following example shows how to use float to pass parameters to a Logic App:</span><span class="sxs-lookup"><span data-stu-id="d441c-216">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
            "custom1": {
                "value": "[float('3.0')]"
            },
            "custom2": {
                "value": "[float(3)]"
            },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="d441c-217">int</span><span class="sxs-lookup"><span data-stu-id="d441c-217">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="d441c-218">Converts the specified value to an integer.</span><span class="sxs-lookup"><span data-stu-id="d441c-218">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-219">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-219">Parameters</span></span>

| <span data-ttu-id="d441c-220">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-220">Parameter</span></span> | <span data-ttu-id="d441c-221">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-221">Required</span></span> | <span data-ttu-id="d441c-222">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-222">Type</span></span> | <span data-ttu-id="d441c-223">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-223">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-224">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="d441c-224">valueToConvert</span></span> |<span data-ttu-id="d441c-225">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-225">Yes</span></span> |<span data-ttu-id="d441c-226">string or int</span><span class="sxs-lookup"><span data-stu-id="d441c-226">string or int</span></span> |<span data-ttu-id="d441c-227">The value to convert to an integer.</span><span class="sxs-lookup"><span data-stu-id="d441c-227">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-228">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-228">Return value</span></span>

<span data-ttu-id="d441c-229">An integer of the converted value.</span><span class="sxs-lookup"><span data-stu-id="d441c-229">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-230">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-230">Example</span></span>

<span data-ttu-id="d441c-231">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/int.json) converts the user-provided parameter value to integer.</span><span class="sxs-lookup"><span data-stu-id="d441c-231">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/int.json) converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="d441c-232">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-232">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-233">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-233">Name</span></span> | <span data-ttu-id="d441c-234">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-234">Type</span></span> | <span data-ttu-id="d441c-235">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-235">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-236">intResult</span><span class="sxs-lookup"><span data-stu-id="d441c-236">intResult</span></span> | <span data-ttu-id="d441c-237">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-237">Int</span></span> | <span data-ttu-id="d441c-238">4</span><span class="sxs-lookup"><span data-stu-id="d441c-238">4</span></span> |

<span data-ttu-id="d441c-239">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-239">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/int.json
```

<span data-ttu-id="d441c-240">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-240">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/int.json
```

<a id="max" />

## <a name="max"></a><span data-ttu-id="d441c-241">max</span><span class="sxs-lookup"><span data-stu-id="d441c-241">max</span></span>
`max (arg1)`

<span data-ttu-id="d441c-242">Returns the maximum value from an array of integers or a comma-separated list of integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-242">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-243">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-243">Parameters</span></span>

| <span data-ttu-id="d441c-244">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-244">Parameter</span></span> | <span data-ttu-id="d441c-245">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-245">Required</span></span> | <span data-ttu-id="d441c-246">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-246">Type</span></span> | <span data-ttu-id="d441c-247">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-247">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-248">arg1</span><span class="sxs-lookup"><span data-stu-id="d441c-248">arg1</span></span> |<span data-ttu-id="d441c-249">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-249">Yes</span></span> |<span data-ttu-id="d441c-250">array of integers, or comma-separated list of integers</span><span class="sxs-lookup"><span data-stu-id="d441c-250">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="d441c-251">The collection to get the maximum value.</span><span class="sxs-lookup"><span data-stu-id="d441c-251">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-252">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-252">Return value</span></span>

<span data-ttu-id="d441c-253">An integer representing the maximum value from the collection.</span><span class="sxs-lookup"><span data-stu-id="d441c-253">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-254">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-254">Example</span></span>

<span data-ttu-id="d441c-255">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/max.json) shows how to use max with an array and a list of integers:</span><span class="sxs-lookup"><span data-stu-id="d441c-255">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/max.json) shows how to use max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="d441c-256">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-257">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-257">Name</span></span> | <span data-ttu-id="d441c-258">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-258">Type</span></span> | <span data-ttu-id="d441c-259">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-260">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d441c-260">arrayOutput</span></span> | <span data-ttu-id="d441c-261">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-261">Int</span></span> | <span data-ttu-id="d441c-262">5</span><span class="sxs-lookup"><span data-stu-id="d441c-262">5</span></span> |
| <span data-ttu-id="d441c-263">intOutput</span><span class="sxs-lookup"><span data-stu-id="d441c-263">intOutput</span></span> | <span data-ttu-id="d441c-264">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-264">Int</span></span> | <span data-ttu-id="d441c-265">5</span><span class="sxs-lookup"><span data-stu-id="d441c-265">5</span></span> |

<span data-ttu-id="d441c-266">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-266">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/max.json
```

<span data-ttu-id="d441c-267">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-267">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/max.json
```

<a id="min" />

## <a name="min"></a><span data-ttu-id="d441c-268">min</span><span class="sxs-lookup"><span data-stu-id="d441c-268">min</span></span>
`min (arg1)`

<span data-ttu-id="d441c-269">Returns the minimum value from an array of integers or a comma-separated list of integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-269">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-270">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-270">Parameters</span></span>

| <span data-ttu-id="d441c-271">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-271">Parameter</span></span> | <span data-ttu-id="d441c-272">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-272">Required</span></span> | <span data-ttu-id="d441c-273">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-273">Type</span></span> | <span data-ttu-id="d441c-274">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-274">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-275">arg1</span><span class="sxs-lookup"><span data-stu-id="d441c-275">arg1</span></span> |<span data-ttu-id="d441c-276">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-276">Yes</span></span> |<span data-ttu-id="d441c-277">array of integers, or comma-separated list of integers</span><span class="sxs-lookup"><span data-stu-id="d441c-277">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="d441c-278">The collection to get the minimum value.</span><span class="sxs-lookup"><span data-stu-id="d441c-278">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-279">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-279">Return value</span></span>

<span data-ttu-id="d441c-280">An integer representing minimum value from the collection.</span><span class="sxs-lookup"><span data-stu-id="d441c-280">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-281">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-281">Example</span></span>

<span data-ttu-id="d441c-282">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/min.json) shows how to use min with an array and a list of integers:</span><span class="sxs-lookup"><span data-stu-id="d441c-282">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/min.json) shows how to use min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="d441c-283">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-283">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-284">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-284">Name</span></span> | <span data-ttu-id="d441c-285">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-285">Type</span></span> | <span data-ttu-id="d441c-286">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-286">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-287">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d441c-287">arrayOutput</span></span> | <span data-ttu-id="d441c-288">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-288">Int</span></span> | <span data-ttu-id="d441c-289">0</span><span class="sxs-lookup"><span data-stu-id="d441c-289">0</span></span> |
| <span data-ttu-id="d441c-290">intOutput</span><span class="sxs-lookup"><span data-stu-id="d441c-290">intOutput</span></span> | <span data-ttu-id="d441c-291">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-291">Int</span></span> | <span data-ttu-id="d441c-292">0</span><span class="sxs-lookup"><span data-stu-id="d441c-292">0</span></span> |

<span data-ttu-id="d441c-293">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-293">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/min.json
```

<span data-ttu-id="d441c-294">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-294">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/min.json
```

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="d441c-295">mod</span><span class="sxs-lookup"><span data-stu-id="d441c-295">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="d441c-296">Returns the remainder of the integer division using the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-296">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-297">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-297">Parameters</span></span>

| <span data-ttu-id="d441c-298">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-298">Parameter</span></span> | <span data-ttu-id="d441c-299">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-299">Required</span></span> | <span data-ttu-id="d441c-300">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-300">Type</span></span> | <span data-ttu-id="d441c-301">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-301">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-302">operand1</span><span class="sxs-lookup"><span data-stu-id="d441c-302">operand1</span></span> |<span data-ttu-id="d441c-303">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-303">Yes</span></span> |<span data-ttu-id="d441c-304">int</span><span class="sxs-lookup"><span data-stu-id="d441c-304">int</span></span> |<span data-ttu-id="d441c-305">The number being divided.</span><span class="sxs-lookup"><span data-stu-id="d441c-305">The number being divided.</span></span> |
| <span data-ttu-id="d441c-306">operand2</span><span class="sxs-lookup"><span data-stu-id="d441c-306">operand2</span></span> |<span data-ttu-id="d441c-307">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-307">Yes</span></span> |<span data-ttu-id="d441c-308">int</span><span class="sxs-lookup"><span data-stu-id="d441c-308">int</span></span> |<span data-ttu-id="d441c-309">The number that is used to divide, Cannot be 0.</span><span class="sxs-lookup"><span data-stu-id="d441c-309">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-310">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-310">Return value</span></span>
<span data-ttu-id="d441c-311">An integer representing the remainder.</span><span class="sxs-lookup"><span data-stu-id="d441c-311">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-312">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-312">Example</span></span>

<span data-ttu-id="d441c-313">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/mod.json) returns the remainder of dividing one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="d441c-313">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/mod.json) returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="d441c-314">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-314">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-315">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-315">Name</span></span> | <span data-ttu-id="d441c-316">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-316">Type</span></span> | <span data-ttu-id="d441c-317">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-317">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-318">modResult</span><span class="sxs-lookup"><span data-stu-id="d441c-318">modResult</span></span> | <span data-ttu-id="d441c-319">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-319">Int</span></span> | <span data-ttu-id="d441c-320">1</span><span class="sxs-lookup"><span data-stu-id="d441c-320">1</span></span> |

<span data-ttu-id="d441c-321">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-321">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/mod.json
```

<span data-ttu-id="d441c-322">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-322">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/mod.json
```

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="d441c-323">mul</span><span class="sxs-lookup"><span data-stu-id="d441c-323">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="d441c-324">Returns the multiplication of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-324">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-325">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-325">Parameters</span></span>

| <span data-ttu-id="d441c-326">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-326">Parameter</span></span> | <span data-ttu-id="d441c-327">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-327">Required</span></span> | <span data-ttu-id="d441c-328">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-328">Type</span></span> | <span data-ttu-id="d441c-329">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-329">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-330">operand1</span><span class="sxs-lookup"><span data-stu-id="d441c-330">operand1</span></span> |<span data-ttu-id="d441c-331">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-331">Yes</span></span> |<span data-ttu-id="d441c-332">int</span><span class="sxs-lookup"><span data-stu-id="d441c-332">int</span></span> |<span data-ttu-id="d441c-333">First number to multiply.</span><span class="sxs-lookup"><span data-stu-id="d441c-333">First number to multiply.</span></span> |
| <span data-ttu-id="d441c-334">operand2</span><span class="sxs-lookup"><span data-stu-id="d441c-334">operand2</span></span> |<span data-ttu-id="d441c-335">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-335">Yes</span></span> |<span data-ttu-id="d441c-336">int</span><span class="sxs-lookup"><span data-stu-id="d441c-336">int</span></span> |<span data-ttu-id="d441c-337">Second number to multiply.</span><span class="sxs-lookup"><span data-stu-id="d441c-337">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-338">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-338">Return value</span></span>

<span data-ttu-id="d441c-339">An integer representing the multiplication.</span><span class="sxs-lookup"><span data-stu-id="d441c-339">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-340">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-340">Example</span></span>

<span data-ttu-id="d441c-341">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/mul.json) multiplies one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="d441c-341">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/mul.json) multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="d441c-342">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-342">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-343">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-343">Name</span></span> | <span data-ttu-id="d441c-344">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-344">Type</span></span> | <span data-ttu-id="d441c-345">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-345">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-346">mulResult</span><span class="sxs-lookup"><span data-stu-id="d441c-346">mulResult</span></span> | <span data-ttu-id="d441c-347">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-347">Int</span></span> | <span data-ttu-id="d441c-348">15</span><span class="sxs-lookup"><span data-stu-id="d441c-348">15</span></span> |

<span data-ttu-id="d441c-349">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-349">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/mul.json
```

<span data-ttu-id="d441c-350">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-350">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/mul.json
```

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="d441c-351">sub</span><span class="sxs-lookup"><span data-stu-id="d441c-351">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="d441c-352">Returns the subtraction of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="d441c-352">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="d441c-353">Parameters</span><span class="sxs-lookup"><span data-stu-id="d441c-353">Parameters</span></span>

| <span data-ttu-id="d441c-354">Parameter</span><span class="sxs-lookup"><span data-stu-id="d441c-354">Parameter</span></span> | <span data-ttu-id="d441c-355">Required</span><span class="sxs-lookup"><span data-stu-id="d441c-355">Required</span></span> | <span data-ttu-id="d441c-356">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-356">Type</span></span> | <span data-ttu-id="d441c-357">Description</span><span class="sxs-lookup"><span data-stu-id="d441c-357">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d441c-358">operand1</span><span class="sxs-lookup"><span data-stu-id="d441c-358">operand1</span></span> |<span data-ttu-id="d441c-359">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-359">Yes</span></span> |<span data-ttu-id="d441c-360">int</span><span class="sxs-lookup"><span data-stu-id="d441c-360">int</span></span> |<span data-ttu-id="d441c-361">The number that is subtracted from.</span><span class="sxs-lookup"><span data-stu-id="d441c-361">The number that is subtracted from.</span></span> |
| <span data-ttu-id="d441c-362">operand2</span><span class="sxs-lookup"><span data-stu-id="d441c-362">operand2</span></span> |<span data-ttu-id="d441c-363">Yes</span><span class="sxs-lookup"><span data-stu-id="d441c-363">Yes</span></span> |<span data-ttu-id="d441c-364">int</span><span class="sxs-lookup"><span data-stu-id="d441c-364">int</span></span> |<span data-ttu-id="d441c-365">The number that is subtracted.</span><span class="sxs-lookup"><span data-stu-id="d441c-365">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d441c-366">Return value</span><span class="sxs-lookup"><span data-stu-id="d441c-366">Return value</span></span>
<span data-ttu-id="d441c-367">An integer representing the subtraction.</span><span class="sxs-lookup"><span data-stu-id="d441c-367">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="d441c-368">Example</span><span class="sxs-lookup"><span data-stu-id="d441c-368">Example</span></span>

<span data-ttu-id="d441c-369">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/sub.json) subtracts one parameter from another parameter.</span><span class="sxs-lookup"><span data-stu-id="d441c-369">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/sub.json) subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="d441c-370">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="d441c-370">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="d441c-371">Name</span><span class="sxs-lookup"><span data-stu-id="d441c-371">Name</span></span> | <span data-ttu-id="d441c-372">Type</span><span class="sxs-lookup"><span data-stu-id="d441c-372">Type</span></span> | <span data-ttu-id="d441c-373">Value</span><span class="sxs-lookup"><span data-stu-id="d441c-373">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d441c-374">subResult</span><span class="sxs-lookup"><span data-stu-id="d441c-374">subResult</span></span> | <span data-ttu-id="d441c-375">Int</span><span class="sxs-lookup"><span data-stu-id="d441c-375">Int</span></span> | <span data-ttu-id="d441c-376">4</span><span class="sxs-lookup"><span data-stu-id="d441c-376">4</span></span> |

<span data-ttu-id="d441c-377">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-377">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/sub.json
```

<span data-ttu-id="d441c-378">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="d441c-378">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/sub.json
```

## <a name="next-steps"></a><span data-ttu-id="d441c-379">Next steps</span><span class="sxs-lookup"><span data-stu-id="d441c-379">Next steps</span></span>
* <span data-ttu-id="d441c-380">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d441c-380">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d441c-381">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d441c-381">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d441c-382">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d441c-382">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="d441c-383">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d441c-383">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

