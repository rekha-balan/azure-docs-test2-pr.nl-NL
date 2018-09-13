---
title: Azure Resource Manager template functions - logical | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to determine logical values.
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
ms.date: 09/05/2017
ms.author: tomfitz
ms.openlocfilehash: d8a7ae412fc80dff7bd91c1cdc5d4fcd985e07f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867222"
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f020d-103">Logical functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="f020d-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="f020d-104">Resource Manager provides several functions for making comparisons in your templates.</span><span class="sxs-lookup"><span data-stu-id="f020d-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="f020d-105">and</span><span class="sxs-lookup"><span data-stu-id="f020d-105">and</span></span>](#and)
* [<span data-ttu-id="f020d-106">bool</span><span class="sxs-lookup"><span data-stu-id="f020d-106">bool</span></span>](#bool)
* [<span data-ttu-id="f020d-107">if</span><span class="sxs-lookup"><span data-stu-id="f020d-107">if</span></span>](#if)
* [<span data-ttu-id="f020d-108">not</span><span class="sxs-lookup"><span data-stu-id="f020d-108">not</span></span>](#not)
* [<span data-ttu-id="f020d-109">or</span><span class="sxs-lookup"><span data-stu-id="f020d-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="f020d-110">and</span><span class="sxs-lookup"><span data-stu-id="f020d-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="f020d-111">Checks whether both parameter values are true.</span><span class="sxs-lookup"><span data-stu-id="f020d-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="f020d-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="f020d-112">Parameters</span></span>

| <span data-ttu-id="f020d-113">Parameter</span><span class="sxs-lookup"><span data-stu-id="f020d-113">Parameter</span></span> | <span data-ttu-id="f020d-114">Required</span><span class="sxs-lookup"><span data-stu-id="f020d-114">Required</span></span> | <span data-ttu-id="f020d-115">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-115">Type</span></span> | <span data-ttu-id="f020d-116">Description</span><span class="sxs-lookup"><span data-stu-id="f020d-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f020d-117">arg1</span><span class="sxs-lookup"><span data-stu-id="f020d-117">arg1</span></span> |<span data-ttu-id="f020d-118">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-118">Yes</span></span> |<span data-ttu-id="f020d-119">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-119">boolean</span></span> |<span data-ttu-id="f020d-120">The first value to check whether is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="f020d-121">arg2</span><span class="sxs-lookup"><span data-stu-id="f020d-121">arg2</span></span> |<span data-ttu-id="f020d-122">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-122">Yes</span></span> |<span data-ttu-id="f020d-123">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-123">boolean</span></span> |<span data-ttu-id="f020d-124">The second value to check whether is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f020d-125">Return value</span><span class="sxs-lookup"><span data-stu-id="f020d-125">Return value</span></span>

<span data-ttu-id="f020d-126">Returns **True** if both values are true; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="f020d-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="f020d-127">Examples</span><span class="sxs-lookup"><span data-stu-id="f020d-127">Examples</span></span>

<span data-ttu-id="f020d-128">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span><span class="sxs-lookup"><span data-stu-id="f020d-128">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="f020d-129">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="f020d-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="f020d-130">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-130">Name</span></span> | <span data-ttu-id="f020d-131">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-131">Type</span></span> | <span data-ttu-id="f020d-132">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-133">andExampleOutput</span></span> | <span data-ttu-id="f020d-134">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-134">Bool</span></span> | <span data-ttu-id="f020d-135">False</span><span class="sxs-lookup"><span data-stu-id="f020d-135">False</span></span> |
| <span data-ttu-id="f020d-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-136">orExampleOutput</span></span> | <span data-ttu-id="f020d-137">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-137">Bool</span></span> | <span data-ttu-id="f020d-138">True</span><span class="sxs-lookup"><span data-stu-id="f020d-138">True</span></span> |
| <span data-ttu-id="f020d-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-139">notExampleOutput</span></span> | <span data-ttu-id="f020d-140">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-140">Bool</span></span> | <span data-ttu-id="f020d-141">False</span><span class="sxs-lookup"><span data-stu-id="f020d-141">False</span></span> |

<span data-ttu-id="f020d-142">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-142">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

<span data-ttu-id="f020d-143">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-143">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

## <a name="bool"></a><span data-ttu-id="f020d-144">bool</span><span class="sxs-lookup"><span data-stu-id="f020d-144">bool</span></span>
`bool(arg1)`

<span data-ttu-id="f020d-145">Converts the parameter to a boolean.</span><span class="sxs-lookup"><span data-stu-id="f020d-145">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="f020d-146">Parameters</span><span class="sxs-lookup"><span data-stu-id="f020d-146">Parameters</span></span>

| <span data-ttu-id="f020d-147">Parameter</span><span class="sxs-lookup"><span data-stu-id="f020d-147">Parameter</span></span> | <span data-ttu-id="f020d-148">Required</span><span class="sxs-lookup"><span data-stu-id="f020d-148">Required</span></span> | <span data-ttu-id="f020d-149">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-149">Type</span></span> | <span data-ttu-id="f020d-150">Description</span><span class="sxs-lookup"><span data-stu-id="f020d-150">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f020d-151">arg1</span><span class="sxs-lookup"><span data-stu-id="f020d-151">arg1</span></span> |<span data-ttu-id="f020d-152">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-152">Yes</span></span> |<span data-ttu-id="f020d-153">string or int</span><span class="sxs-lookup"><span data-stu-id="f020d-153">string or int</span></span> |<span data-ttu-id="f020d-154">The value to convert to a boolean.</span><span class="sxs-lookup"><span data-stu-id="f020d-154">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f020d-155">Return value</span><span class="sxs-lookup"><span data-stu-id="f020d-155">Return value</span></span>
<span data-ttu-id="f020d-156">A boolean of the converted value.</span><span class="sxs-lookup"><span data-stu-id="f020d-156">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="f020d-157">Examples</span><span class="sxs-lookup"><span data-stu-id="f020d-157">Examples</span></span>

<span data-ttu-id="f020d-158">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/bool.json) shows how to use bool with a string or integer.</span><span class="sxs-lookup"><span data-stu-id="f020d-158">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/bool.json) shows how to use bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="f020d-159">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="f020d-159">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f020d-160">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-160">Name</span></span> | <span data-ttu-id="f020d-161">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-161">Type</span></span> | <span data-ttu-id="f020d-162">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-162">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-163">trueString</span><span class="sxs-lookup"><span data-stu-id="f020d-163">trueString</span></span> | <span data-ttu-id="f020d-164">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-164">Bool</span></span> | <span data-ttu-id="f020d-165">True</span><span class="sxs-lookup"><span data-stu-id="f020d-165">True</span></span> |
| <span data-ttu-id="f020d-166">falseString</span><span class="sxs-lookup"><span data-stu-id="f020d-166">falseString</span></span> | <span data-ttu-id="f020d-167">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-167">Bool</span></span> | <span data-ttu-id="f020d-168">False</span><span class="sxs-lookup"><span data-stu-id="f020d-168">False</span></span> |
| <span data-ttu-id="f020d-169">trueInt</span><span class="sxs-lookup"><span data-stu-id="f020d-169">trueInt</span></span> | <span data-ttu-id="f020d-170">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-170">Bool</span></span> | <span data-ttu-id="f020d-171">True</span><span class="sxs-lookup"><span data-stu-id="f020d-171">True</span></span> |
| <span data-ttu-id="f020d-172">falseInt</span><span class="sxs-lookup"><span data-stu-id="f020d-172">falseInt</span></span> | <span data-ttu-id="f020d-173">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-173">Bool</span></span> | <span data-ttu-id="f020d-174">False</span><span class="sxs-lookup"><span data-stu-id="f020d-174">False</span></span> |

<span data-ttu-id="f020d-175">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-175">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/bool.json
```

<span data-ttu-id="f020d-176">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-176">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/bool.json
```

## <a name="if"></a><span data-ttu-id="f020d-177">if</span><span class="sxs-lookup"><span data-stu-id="f020d-177">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="f020d-178">Returns a value based on whether a condition is true or false.</span><span class="sxs-lookup"><span data-stu-id="f020d-178">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="f020d-179">Parameters</span><span class="sxs-lookup"><span data-stu-id="f020d-179">Parameters</span></span>

| <span data-ttu-id="f020d-180">Parameter</span><span class="sxs-lookup"><span data-stu-id="f020d-180">Parameter</span></span> | <span data-ttu-id="f020d-181">Required</span><span class="sxs-lookup"><span data-stu-id="f020d-181">Required</span></span> | <span data-ttu-id="f020d-182">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-182">Type</span></span> | <span data-ttu-id="f020d-183">Description</span><span class="sxs-lookup"><span data-stu-id="f020d-183">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f020d-184">condition</span><span class="sxs-lookup"><span data-stu-id="f020d-184">condition</span></span> |<span data-ttu-id="f020d-185">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-185">Yes</span></span> |<span data-ttu-id="f020d-186">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-186">boolean</span></span> |<span data-ttu-id="f020d-187">The value to check whether it is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-187">The value to check whether it is true.</span></span> |
| <span data-ttu-id="f020d-188">trueValue</span><span class="sxs-lookup"><span data-stu-id="f020d-188">trueValue</span></span> |<span data-ttu-id="f020d-189">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-189">Yes</span></span> | <span data-ttu-id="f020d-190">string, int, object, or array</span><span class="sxs-lookup"><span data-stu-id="f020d-190">string, int, object, or array</span></span> |<span data-ttu-id="f020d-191">The value to return when the condition is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-191">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="f020d-192">falseValue</span><span class="sxs-lookup"><span data-stu-id="f020d-192">falseValue</span></span> |<span data-ttu-id="f020d-193">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-193">Yes</span></span> | <span data-ttu-id="f020d-194">string, int, object, or array</span><span class="sxs-lookup"><span data-stu-id="f020d-194">string, int, object, or array</span></span> |<span data-ttu-id="f020d-195">The value to return when the condition is false.</span><span class="sxs-lookup"><span data-stu-id="f020d-195">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f020d-196">Return value</span><span class="sxs-lookup"><span data-stu-id="f020d-196">Return value</span></span>

<span data-ttu-id="f020d-197">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span><span class="sxs-lookup"><span data-stu-id="f020d-197">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="f020d-198">Remarks</span><span class="sxs-lookup"><span data-stu-id="f020d-198">Remarks</span></span>

<span data-ttu-id="f020d-199">You can use this function to conditionally set a resource property.</span><span class="sxs-lookup"><span data-stu-id="f020d-199">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="f020d-200">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span><span class="sxs-lookup"><span data-stu-id="f020d-200">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="f020d-201">Examples</span><span class="sxs-lookup"><span data-stu-id="f020d-201">Examples</span></span>

<span data-ttu-id="f020d-202">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/if.json) shows how to use the `if` function.</span><span class="sxs-lookup"><span data-stu-id="f020d-202">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/if.json) shows how to use the `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="f020d-203">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="f020d-203">The output from the preceding example is:</span></span>

| <span data-ttu-id="f020d-204">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-204">Name</span></span> | <span data-ttu-id="f020d-205">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-205">Type</span></span> | <span data-ttu-id="f020d-206">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-206">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-207">yesOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-207">yesOutput</span></span> | <span data-ttu-id="f020d-208">String</span><span class="sxs-lookup"><span data-stu-id="f020d-208">String</span></span> | <span data-ttu-id="f020d-209">yes</span><span class="sxs-lookup"><span data-stu-id="f020d-209">yes</span></span> |
| <span data-ttu-id="f020d-210">noOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-210">noOutput</span></span> | <span data-ttu-id="f020d-211">String</span><span class="sxs-lookup"><span data-stu-id="f020d-211">String</span></span> | <span data-ttu-id="f020d-212">no</span><span class="sxs-lookup"><span data-stu-id="f020d-212">no</span></span> |

<span data-ttu-id="f020d-213">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-213">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/if.json
```

<span data-ttu-id="f020d-214">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-214">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/if.json
```

## <a name="not"></a><span data-ttu-id="f020d-215">not</span><span class="sxs-lookup"><span data-stu-id="f020d-215">not</span></span>
`not(arg1)`

<span data-ttu-id="f020d-216">Converts boolean value to its opposite value.</span><span class="sxs-lookup"><span data-stu-id="f020d-216">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="f020d-217">Parameters</span><span class="sxs-lookup"><span data-stu-id="f020d-217">Parameters</span></span>

| <span data-ttu-id="f020d-218">Parameter</span><span class="sxs-lookup"><span data-stu-id="f020d-218">Parameter</span></span> | <span data-ttu-id="f020d-219">Required</span><span class="sxs-lookup"><span data-stu-id="f020d-219">Required</span></span> | <span data-ttu-id="f020d-220">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-220">Type</span></span> | <span data-ttu-id="f020d-221">Description</span><span class="sxs-lookup"><span data-stu-id="f020d-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f020d-222">arg1</span><span class="sxs-lookup"><span data-stu-id="f020d-222">arg1</span></span> |<span data-ttu-id="f020d-223">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-223">Yes</span></span> |<span data-ttu-id="f020d-224">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-224">boolean</span></span> |<span data-ttu-id="f020d-225">The value to convert.</span><span class="sxs-lookup"><span data-stu-id="f020d-225">The value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f020d-226">Return value</span><span class="sxs-lookup"><span data-stu-id="f020d-226">Return value</span></span>

<span data-ttu-id="f020d-227">Returns **True** when parameter is **False**.</span><span class="sxs-lookup"><span data-stu-id="f020d-227">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="f020d-228">Returns **False** when parameter is **True**.</span><span class="sxs-lookup"><span data-stu-id="f020d-228">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="f020d-229">Examples</span><span class="sxs-lookup"><span data-stu-id="f020d-229">Examples</span></span>

<span data-ttu-id="f020d-230">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span><span class="sxs-lookup"><span data-stu-id="f020d-230">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="f020d-231">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="f020d-231">The output from the preceding example is:</span></span>

| <span data-ttu-id="f020d-232">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-232">Name</span></span> | <span data-ttu-id="f020d-233">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-233">Type</span></span> | <span data-ttu-id="f020d-234">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-234">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-235">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-235">andExampleOutput</span></span> | <span data-ttu-id="f020d-236">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-236">Bool</span></span> | <span data-ttu-id="f020d-237">False</span><span class="sxs-lookup"><span data-stu-id="f020d-237">False</span></span> |
| <span data-ttu-id="f020d-238">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-238">orExampleOutput</span></span> | <span data-ttu-id="f020d-239">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-239">Bool</span></span> | <span data-ttu-id="f020d-240">True</span><span class="sxs-lookup"><span data-stu-id="f020d-240">True</span></span> |
| <span data-ttu-id="f020d-241">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-241">notExampleOutput</span></span> | <span data-ttu-id="f020d-242">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-242">Bool</span></span> | <span data-ttu-id="f020d-243">False</span><span class="sxs-lookup"><span data-stu-id="f020d-243">False</span></span> |

<span data-ttu-id="f020d-244">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-244">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

<span data-ttu-id="f020d-245">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-245">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

<span data-ttu-id="f020d-246">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/not-equals.json) uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="f020d-246">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/not-equals.json) uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="f020d-247">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="f020d-247">The output from the preceding example is:</span></span>

| <span data-ttu-id="f020d-248">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-248">Name</span></span> | <span data-ttu-id="f020d-249">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-249">Type</span></span> | <span data-ttu-id="f020d-250">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-250">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-251">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="f020d-251">checkNotEquals</span></span> | <span data-ttu-id="f020d-252">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-252">Bool</span></span> | <span data-ttu-id="f020d-253">True</span><span class="sxs-lookup"><span data-stu-id="f020d-253">True</span></span> |

<span data-ttu-id="f020d-254">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-254">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json
```

<span data-ttu-id="f020d-255">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-255">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json
```

## <a name="or"></a><span data-ttu-id="f020d-256">or</span><span class="sxs-lookup"><span data-stu-id="f020d-256">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="f020d-257">Checks whether either parameter value is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-257">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="f020d-258">Parameters</span><span class="sxs-lookup"><span data-stu-id="f020d-258">Parameters</span></span>

| <span data-ttu-id="f020d-259">Parameter</span><span class="sxs-lookup"><span data-stu-id="f020d-259">Parameter</span></span> | <span data-ttu-id="f020d-260">Required</span><span class="sxs-lookup"><span data-stu-id="f020d-260">Required</span></span> | <span data-ttu-id="f020d-261">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-261">Type</span></span> | <span data-ttu-id="f020d-262">Description</span><span class="sxs-lookup"><span data-stu-id="f020d-262">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f020d-263">arg1</span><span class="sxs-lookup"><span data-stu-id="f020d-263">arg1</span></span> |<span data-ttu-id="f020d-264">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-264">Yes</span></span> |<span data-ttu-id="f020d-265">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-265">boolean</span></span> |<span data-ttu-id="f020d-266">The first value to check whether is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-266">The first value to check whether is true.</span></span> |
| <span data-ttu-id="f020d-267">arg2</span><span class="sxs-lookup"><span data-stu-id="f020d-267">arg2</span></span> |<span data-ttu-id="f020d-268">Yes</span><span class="sxs-lookup"><span data-stu-id="f020d-268">Yes</span></span> |<span data-ttu-id="f020d-269">boolean</span><span class="sxs-lookup"><span data-stu-id="f020d-269">boolean</span></span> |<span data-ttu-id="f020d-270">The second value to check whether is true.</span><span class="sxs-lookup"><span data-stu-id="f020d-270">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f020d-271">Return value</span><span class="sxs-lookup"><span data-stu-id="f020d-271">Return value</span></span>

<span data-ttu-id="f020d-272">Returns **True** if either value is true; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="f020d-272">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="f020d-273">Examples</span><span class="sxs-lookup"><span data-stu-id="f020d-273">Examples</span></span>

<span data-ttu-id="f020d-274">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span><span class="sxs-lookup"><span data-stu-id="f020d-274">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/andornot.json) shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="f020d-275">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="f020d-275">The output from the preceding example is:</span></span>

| <span data-ttu-id="f020d-276">Name</span><span class="sxs-lookup"><span data-stu-id="f020d-276">Name</span></span> | <span data-ttu-id="f020d-277">Type</span><span class="sxs-lookup"><span data-stu-id="f020d-277">Type</span></span> | <span data-ttu-id="f020d-278">Value</span><span class="sxs-lookup"><span data-stu-id="f020d-278">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f020d-279">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-279">andExampleOutput</span></span> | <span data-ttu-id="f020d-280">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-280">Bool</span></span> | <span data-ttu-id="f020d-281">False</span><span class="sxs-lookup"><span data-stu-id="f020d-281">False</span></span> |
| <span data-ttu-id="f020d-282">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-282">orExampleOutput</span></span> | <span data-ttu-id="f020d-283">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-283">Bool</span></span> | <span data-ttu-id="f020d-284">True</span><span class="sxs-lookup"><span data-stu-id="f020d-284">True</span></span> |
| <span data-ttu-id="f020d-285">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="f020d-285">notExampleOutput</span></span> | <span data-ttu-id="f020d-286">Bool</span><span class="sxs-lookup"><span data-stu-id="f020d-286">Bool</span></span> | <span data-ttu-id="f020d-287">False</span><span class="sxs-lookup"><span data-stu-id="f020d-287">False</span></span> |

<span data-ttu-id="f020d-288">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-288">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

<span data-ttu-id="f020d-289">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f020d-289">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/andornot.json
```

## <a name="next-steps"></a><span data-ttu-id="f020d-290">Next steps</span><span class="sxs-lookup"><span data-stu-id="f020d-290">Next steps</span></span>
* <span data-ttu-id="f020d-291">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f020d-291">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f020d-292">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f020d-292">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f020d-293">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f020d-293">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f020d-294">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f020d-294">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

