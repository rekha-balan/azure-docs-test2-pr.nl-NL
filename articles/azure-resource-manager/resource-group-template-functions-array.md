---
title: Azure Resource Manager template functions - arrays and objects | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template for working with arrays and objects.
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
ms.openlocfilehash: cdc8222675a9f0099edccb24310bcea03bf963f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866102"
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="01ac4-103">Array and object functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="01ac4-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="01ac4-104">Resource Manager provides several functions for working with arrays and objects.</span><span class="sxs-lookup"><span data-stu-id="01ac4-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="01ac4-105">array</span><span class="sxs-lookup"><span data-stu-id="01ac4-105">array</span></span>](#array)
* [<span data-ttu-id="01ac4-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="01ac4-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="01ac4-107">concat</span><span class="sxs-lookup"><span data-stu-id="01ac4-107">concat</span></span>](#concat)
* [<span data-ttu-id="01ac4-108">contains</span><span class="sxs-lookup"><span data-stu-id="01ac4-108">contains</span></span>](#contains)
* [<span data-ttu-id="01ac4-109">createArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="01ac4-110">empty</span><span class="sxs-lookup"><span data-stu-id="01ac4-110">empty</span></span>](#empty)
* [<span data-ttu-id="01ac4-111">first</span><span class="sxs-lookup"><span data-stu-id="01ac4-111">first</span></span>](#first)
* [<span data-ttu-id="01ac4-112">intersection</span><span class="sxs-lookup"><span data-stu-id="01ac4-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="01ac4-113">json</span><span class="sxs-lookup"><span data-stu-id="01ac4-113">json</span></span>](#json)
* [<span data-ttu-id="01ac4-114">last</span><span class="sxs-lookup"><span data-stu-id="01ac4-114">last</span></span>](#last)
* [<span data-ttu-id="01ac4-115">length</span><span class="sxs-lookup"><span data-stu-id="01ac4-115">length</span></span>](#length)
* [<span data-ttu-id="01ac4-116">max</span><span class="sxs-lookup"><span data-stu-id="01ac4-116">max</span></span>](#max)
* [<span data-ttu-id="01ac4-117">min</span><span class="sxs-lookup"><span data-stu-id="01ac4-117">min</span></span>](#min)
* [<span data-ttu-id="01ac4-118">range</span><span class="sxs-lookup"><span data-stu-id="01ac4-118">range</span></span>](#range)
* [<span data-ttu-id="01ac4-119">skip</span><span class="sxs-lookup"><span data-stu-id="01ac4-119">skip</span></span>](#skip)
* [<span data-ttu-id="01ac4-120">take</span><span class="sxs-lookup"><span data-stu-id="01ac4-120">take</span></span>](#take)
* [<span data-ttu-id="01ac4-121">union</span><span class="sxs-lookup"><span data-stu-id="01ac4-121">union</span></span>](#union)

<span data-ttu-id="01ac4-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="01ac4-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="01ac4-123">array</span><span class="sxs-lookup"><span data-stu-id="01ac4-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="01ac4-124">Converts the value to an array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-125">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-125">Parameters</span></span>

| <span data-ttu-id="01ac4-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-126">Parameter</span></span> | <span data-ttu-id="01ac4-127">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-127">Required</span></span> | <span data-ttu-id="01ac4-128">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-128">Type</span></span> | <span data-ttu-id="01ac4-129">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-130">convertToArray</span></span> |<span data-ttu-id="01ac4-131">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-131">Yes</span></span> |<span data-ttu-id="01ac4-132">int, string, array, or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-132">int, string, array, or object</span></span> |<span data-ttu-id="01ac4-133">The value to convert to an array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-134">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-134">Return value</span></span>

<span data-ttu-id="01ac4-135">An array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-136">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-136">Example</span></span>

<span data-ttu-id="01ac4-137">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/array.json) shows how to use the array function with different types.</span><span class="sxs-lookup"><span data-stu-id="01ac4-137">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/array.json) shows how to use the array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "efgh"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-138">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-139">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-139">Name</span></span> | <span data-ttu-id="01ac4-140">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-140">Type</span></span> | <span data-ttu-id="01ac4-141">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-142">intOutput</span></span> | <span data-ttu-id="01ac4-143">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-143">Array</span></span> | <span data-ttu-id="01ac4-144">[1]</span><span class="sxs-lookup"><span data-stu-id="01ac4-144">[1]</span></span> |
| <span data-ttu-id="01ac4-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-145">stringOutput</span></span> | <span data-ttu-id="01ac4-146">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-146">Array</span></span> | <span data-ttu-id="01ac4-147">["efgh"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-147">["efgh"]</span></span> |
| <span data-ttu-id="01ac4-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-148">objectOutput</span></span> | <span data-ttu-id="01ac4-149">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-149">Array</span></span> | <span data-ttu-id="01ac4-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="01ac4-150">[{"a": "b", "c": "d"}]</span></span> |

<span data-ttu-id="01ac4-151">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-151">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/array.json
```

<span data-ttu-id="01ac4-152">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-152">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/array.json
```

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="01ac4-153">coalesce</span><span class="sxs-lookup"><span data-stu-id="01ac4-153">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="01ac4-154">Returns first non-null value from the parameters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-154">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="01ac4-155">Empty strings, empty arrays, and empty objects are not null.</span><span class="sxs-lookup"><span data-stu-id="01ac4-155">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-156">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-156">Parameters</span></span>

| <span data-ttu-id="01ac4-157">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-157">Parameter</span></span> | <span data-ttu-id="01ac4-158">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-158">Required</span></span> | <span data-ttu-id="01ac4-159">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-159">Type</span></span> | <span data-ttu-id="01ac4-160">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-160">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-161">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-161">arg1</span></span> |<span data-ttu-id="01ac4-162">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-162">Yes</span></span> |<span data-ttu-id="01ac4-163">int, string, array, or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-163">int, string, array, or object</span></span> |<span data-ttu-id="01ac4-164">The first value to test for null.</span><span class="sxs-lookup"><span data-stu-id="01ac4-164">The first value to test for null.</span></span> |
| <span data-ttu-id="01ac4-165">additional args</span><span class="sxs-lookup"><span data-stu-id="01ac4-165">additional args</span></span> |<span data-ttu-id="01ac4-166">No</span><span class="sxs-lookup"><span data-stu-id="01ac4-166">No</span></span> |<span data-ttu-id="01ac4-167">int, string, array, or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-167">int, string, array, or object</span></span> |<span data-ttu-id="01ac4-168">Additional values to test for null.</span><span class="sxs-lookup"><span data-stu-id="01ac4-168">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-169">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-169">Return value</span></span>

<span data-ttu-id="01ac4-170">The value of the first non-null parameters, which can be a string, int, array, or object.</span><span class="sxs-lookup"><span data-stu-id="01ac4-170">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="01ac4-171">Null if all parameters are null.</span><span class="sxs-lookup"><span data-stu-id="01ac4-171">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="01ac4-172">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-172">Example</span></span>

<span data-ttu-id="01ac4-173">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/coalesce.json) shows the output from different uses of coalesce.</span><span class="sxs-lookup"><span data-stu-id="01ac4-173">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/coalesce.json) shows the output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="01ac4-174">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-174">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-175">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-175">Name</span></span> | <span data-ttu-id="01ac4-176">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-176">Type</span></span> | <span data-ttu-id="01ac4-177">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-177">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-178">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-178">stringOutput</span></span> | <span data-ttu-id="01ac4-179">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-179">String</span></span> | <span data-ttu-id="01ac4-180">default</span><span class="sxs-lookup"><span data-stu-id="01ac4-180">default</span></span> |
| <span data-ttu-id="01ac4-181">intOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-181">intOutput</span></span> | <span data-ttu-id="01ac4-182">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-182">Int</span></span> | <span data-ttu-id="01ac4-183">1</span><span class="sxs-lookup"><span data-stu-id="01ac4-183">1</span></span> |
| <span data-ttu-id="01ac4-184">objectOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-184">objectOutput</span></span> | <span data-ttu-id="01ac4-185">Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-185">Object</span></span> | <span data-ttu-id="01ac4-186">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="01ac4-186">{"first": "default"}</span></span> |
| <span data-ttu-id="01ac4-187">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-187">arrayOutput</span></span> | <span data-ttu-id="01ac4-188">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-188">Array</span></span> | <span data-ttu-id="01ac4-189">[1]</span><span class="sxs-lookup"><span data-stu-id="01ac4-189">[1]</span></span> |
| <span data-ttu-id="01ac4-190">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-190">emptyOutput</span></span> | <span data-ttu-id="01ac4-191">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-191">Bool</span></span> | <span data-ttu-id="01ac4-192">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-192">True</span></span> |

<span data-ttu-id="01ac4-193">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-193">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/coalesce.json
```

<span data-ttu-id="01ac4-194">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-194">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/coalesce.json
```

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="01ac4-195">concat</span><span class="sxs-lookup"><span data-stu-id="01ac4-195">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="01ac4-196">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-196">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="01ac4-197">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-197">Parameters</span></span>

| <span data-ttu-id="01ac4-198">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-198">Parameter</span></span> | <span data-ttu-id="01ac4-199">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-199">Required</span></span> | <span data-ttu-id="01ac4-200">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-200">Type</span></span> | <span data-ttu-id="01ac4-201">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-201">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-202">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-202">arg1</span></span> |<span data-ttu-id="01ac4-203">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-203">Yes</span></span> |<span data-ttu-id="01ac4-204">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-204">array or string</span></span> |<span data-ttu-id="01ac4-205">The first array or string for concatenation.</span><span class="sxs-lookup"><span data-stu-id="01ac4-205">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="01ac4-206">additional arguments</span><span class="sxs-lookup"><span data-stu-id="01ac4-206">additional arguments</span></span> |<span data-ttu-id="01ac4-207">No</span><span class="sxs-lookup"><span data-stu-id="01ac4-207">No</span></span> |<span data-ttu-id="01ac4-208">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-208">array or string</span></span> |<span data-ttu-id="01ac4-209">Additional arrays or strings in sequential order for concatenation.</span><span class="sxs-lookup"><span data-stu-id="01ac4-209">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="01ac4-210">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-210">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="01ac4-211">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-211">Return value</span></span>
<span data-ttu-id="01ac4-212">A string or array of concatenated values.</span><span class="sxs-lookup"><span data-stu-id="01ac4-212">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-213">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-213">Example</span></span>

<span data-ttu-id="01ac4-214">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-array.json) shows how to combine two arrays.</span><span class="sxs-lookup"><span data-stu-id="01ac4-214">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-array.json) shows how to combine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-215">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-215">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-216">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-216">Name</span></span> | <span data-ttu-id="01ac4-217">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-217">Type</span></span> | <span data-ttu-id="01ac4-218">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-218">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-219">return</span><span class="sxs-lookup"><span data-stu-id="01ac4-219">return</span></span> | <span data-ttu-id="01ac4-220">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-220">Array</span></span> | <span data-ttu-id="01ac4-221">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-221">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="01ac4-222">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-222">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-array.json
```

<span data-ttu-id="01ac4-223">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-223">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-array.json
```

<span data-ttu-id="01ac4-224">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-string.json) shows how to combine two string values and return a concatenated string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-224">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-string.json) shows how to combine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="01ac4-225">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-225">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-226">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-226">Name</span></span> | <span data-ttu-id="01ac4-227">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-227">Type</span></span> | <span data-ttu-id="01ac4-228">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-229">concatOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-229">concatOutput</span></span> | <span data-ttu-id="01ac4-230">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-230">String</span></span> | <span data-ttu-id="01ac4-231">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="01ac4-231">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="01ac4-232">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-232">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-string.json
```

<span data-ttu-id="01ac4-233">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-233">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-string.json
```

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="01ac4-234">contains</span><span class="sxs-lookup"><span data-stu-id="01ac4-234">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="01ac4-235">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span><span class="sxs-lookup"><span data-stu-id="01ac4-235">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-236">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-236">Parameters</span></span>

| <span data-ttu-id="01ac4-237">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-237">Parameter</span></span> | <span data-ttu-id="01ac4-238">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-238">Required</span></span> | <span data-ttu-id="01ac4-239">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-239">Type</span></span> | <span data-ttu-id="01ac4-240">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-240">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-241">container</span><span class="sxs-lookup"><span data-stu-id="01ac4-241">container</span></span> |<span data-ttu-id="01ac4-242">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-242">Yes</span></span> |<span data-ttu-id="01ac4-243">array, object, or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-243">array, object, or string</span></span> |<span data-ttu-id="01ac4-244">The value that contains the value to find.</span><span class="sxs-lookup"><span data-stu-id="01ac4-244">The value that contains the value to find.</span></span> |
| <span data-ttu-id="01ac4-245">itemToFind</span><span class="sxs-lookup"><span data-stu-id="01ac4-245">itemToFind</span></span> |<span data-ttu-id="01ac4-246">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-246">Yes</span></span> |<span data-ttu-id="01ac4-247">string or int</span><span class="sxs-lookup"><span data-stu-id="01ac4-247">string or int</span></span> |<span data-ttu-id="01ac4-248">The value to find.</span><span class="sxs-lookup"><span data-stu-id="01ac4-248">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-249">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-249">Return value</span></span>

<span data-ttu-id="01ac4-250">**True** if the item is found; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="01ac4-250">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-251">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-251">Example</span></span>

<span data-ttu-id="01ac4-252">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/contains.json) shows how to use contains with different types:</span><span class="sxs-lookup"><span data-stu-id="01ac4-252">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/contains.json) shows how to use contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="01ac4-253">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-253">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-254">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-254">Name</span></span> | <span data-ttu-id="01ac4-255">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-255">Type</span></span> | <span data-ttu-id="01ac4-256">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-256">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-257">stringTrue</span><span class="sxs-lookup"><span data-stu-id="01ac4-257">stringTrue</span></span> | <span data-ttu-id="01ac4-258">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-258">Bool</span></span> | <span data-ttu-id="01ac4-259">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-259">True</span></span> |
| <span data-ttu-id="01ac4-260">stringFalse</span><span class="sxs-lookup"><span data-stu-id="01ac4-260">stringFalse</span></span> | <span data-ttu-id="01ac4-261">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-261">Bool</span></span> | <span data-ttu-id="01ac4-262">False</span><span class="sxs-lookup"><span data-stu-id="01ac4-262">False</span></span> |
| <span data-ttu-id="01ac4-263">objectTrue</span><span class="sxs-lookup"><span data-stu-id="01ac4-263">objectTrue</span></span> | <span data-ttu-id="01ac4-264">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-264">Bool</span></span> | <span data-ttu-id="01ac4-265">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-265">True</span></span> |
| <span data-ttu-id="01ac4-266">objectFalse</span><span class="sxs-lookup"><span data-stu-id="01ac4-266">objectFalse</span></span> | <span data-ttu-id="01ac4-267">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-267">Bool</span></span> | <span data-ttu-id="01ac4-268">False</span><span class="sxs-lookup"><span data-stu-id="01ac4-268">False</span></span> |
| <span data-ttu-id="01ac4-269">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="01ac4-269">arrayTrue</span></span> | <span data-ttu-id="01ac4-270">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-270">Bool</span></span> | <span data-ttu-id="01ac4-271">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-271">True</span></span> |
| <span data-ttu-id="01ac4-272">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="01ac4-272">arrayFalse</span></span> | <span data-ttu-id="01ac4-273">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-273">Bool</span></span> | <span data-ttu-id="01ac4-274">False</span><span class="sxs-lookup"><span data-stu-id="01ac4-274">False</span></span> |

<span data-ttu-id="01ac4-275">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-275">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/contains.json
```

<span data-ttu-id="01ac4-276">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-276">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/contains.json
```

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="01ac4-277">createarray</span><span class="sxs-lookup"><span data-stu-id="01ac4-277">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="01ac4-278">Creates an array from the parameters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-278">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-279">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-279">Parameters</span></span>

| <span data-ttu-id="01ac4-280">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-280">Parameter</span></span> | <span data-ttu-id="01ac4-281">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-281">Required</span></span> | <span data-ttu-id="01ac4-282">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-282">Type</span></span> | <span data-ttu-id="01ac4-283">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-283">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-284">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-284">arg1</span></span> |<span data-ttu-id="01ac4-285">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-285">Yes</span></span> |<span data-ttu-id="01ac4-286">String, Integer, Array, or Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-286">String, Integer, Array, or Object</span></span> |<span data-ttu-id="01ac4-287">The first value in the array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-287">The first value in the array.</span></span> |
| <span data-ttu-id="01ac4-288">additional arguments</span><span class="sxs-lookup"><span data-stu-id="01ac4-288">additional arguments</span></span> |<span data-ttu-id="01ac4-289">No</span><span class="sxs-lookup"><span data-stu-id="01ac4-289">No</span></span> |<span data-ttu-id="01ac4-290">String, Integer, Array, or Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-290">String, Integer, Array, or Object</span></span> |<span data-ttu-id="01ac4-291">Additional values in the array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-291">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-292">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-292">Return value</span></span>

<span data-ttu-id="01ac4-293">An array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-293">An array.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-294">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-294">Example</span></span>

<span data-ttu-id="01ac4-295">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/createarray.json) shows how to use createArray with different types:</span><span class="sxs-lookup"><span data-stu-id="01ac4-295">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/createarray.json) shows how to use createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-296">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-296">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-297">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-297">Name</span></span> | <span data-ttu-id="01ac4-298">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-298">Type</span></span> | <span data-ttu-id="01ac4-299">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-299">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-300">stringArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-300">stringArray</span></span> | <span data-ttu-id="01ac4-301">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-301">Array</span></span> | <span data-ttu-id="01ac4-302">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-302">["a", "b", "c"]</span></span> |
| <span data-ttu-id="01ac4-303">intArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-303">intArray</span></span> | <span data-ttu-id="01ac4-304">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-304">Array</span></span> | <span data-ttu-id="01ac4-305">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="01ac4-305">[1, 2, 3]</span></span> |
| <span data-ttu-id="01ac4-306">objectArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-306">objectArray</span></span> | <span data-ttu-id="01ac4-307">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-307">Array</span></span> | <span data-ttu-id="01ac4-308">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="01ac4-308">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="01ac4-309">arrayArray</span><span class="sxs-lookup"><span data-stu-id="01ac4-309">arrayArray</span></span> | <span data-ttu-id="01ac4-310">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-310">Array</span></span> | <span data-ttu-id="01ac4-311">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="01ac4-311">[["one", "two", "three"]]</span></span> |

<span data-ttu-id="01ac4-312">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-312">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/createarray.json
```

<span data-ttu-id="01ac4-313">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-313">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/createarray.json
```

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="01ac4-314">empty</span><span class="sxs-lookup"><span data-stu-id="01ac4-314">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="01ac4-315">Determines if an array, object, or string is empty.</span><span class="sxs-lookup"><span data-stu-id="01ac4-315">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-316">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-316">Parameters</span></span>

| <span data-ttu-id="01ac4-317">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-317">Parameter</span></span> | <span data-ttu-id="01ac4-318">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-318">Required</span></span> | <span data-ttu-id="01ac4-319">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-319">Type</span></span> | <span data-ttu-id="01ac4-320">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-320">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-321">itemToTest</span><span class="sxs-lookup"><span data-stu-id="01ac4-321">itemToTest</span></span> |<span data-ttu-id="01ac4-322">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-322">Yes</span></span> |<span data-ttu-id="01ac4-323">array, object, or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-323">array, object, or string</span></span> |<span data-ttu-id="01ac4-324">The value to check if it is empty.</span><span class="sxs-lookup"><span data-stu-id="01ac4-324">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-325">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-325">Return value</span></span>

<span data-ttu-id="01ac4-326">Returns **True** if the value is empty; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="01ac4-326">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-327">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-327">Example</span></span>

<span data-ttu-id="01ac4-328">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/empty.json) checks whether an array, object, and string are empty.</span><span class="sxs-lookup"><span data-stu-id="01ac4-328">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/empty.json) checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-329">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-329">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-330">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-330">Name</span></span> | <span data-ttu-id="01ac4-331">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-331">Type</span></span> | <span data-ttu-id="01ac4-332">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-332">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-333">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="01ac4-333">arrayEmpty</span></span> | <span data-ttu-id="01ac4-334">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-334">Bool</span></span> | <span data-ttu-id="01ac4-335">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-335">True</span></span> |
| <span data-ttu-id="01ac4-336">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="01ac4-336">objectEmpty</span></span> | <span data-ttu-id="01ac4-337">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-337">Bool</span></span> | <span data-ttu-id="01ac4-338">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-338">True</span></span> |
| <span data-ttu-id="01ac4-339">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="01ac4-339">stringEmpty</span></span> | <span data-ttu-id="01ac4-340">Bool</span><span class="sxs-lookup"><span data-stu-id="01ac4-340">Bool</span></span> | <span data-ttu-id="01ac4-341">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-341">True</span></span> |

<span data-ttu-id="01ac4-342">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-342">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/empty.json
```

<span data-ttu-id="01ac4-343">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-343">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/empty.json
```

<a id="first" />

## <a name="first"></a><span data-ttu-id="01ac4-344">first</span><span class="sxs-lookup"><span data-stu-id="01ac4-344">first</span></span>
`first(arg1)`

<span data-ttu-id="01ac4-345">Returns the first element of the array, or first character of the string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-345">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-346">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-346">Parameters</span></span>

| <span data-ttu-id="01ac4-347">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-347">Parameter</span></span> | <span data-ttu-id="01ac4-348">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-348">Required</span></span> | <span data-ttu-id="01ac4-349">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-349">Type</span></span> | <span data-ttu-id="01ac4-350">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-350">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-351">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-351">arg1</span></span> |<span data-ttu-id="01ac4-352">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-352">Yes</span></span> |<span data-ttu-id="01ac4-353">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-353">array or string</span></span> |<span data-ttu-id="01ac4-354">The value to retrieve the first element or character.</span><span class="sxs-lookup"><span data-stu-id="01ac4-354">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-355">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-355">Return value</span></span>

<span data-ttu-id="01ac4-356">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-356">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-357">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-357">Example</span></span>

<span data-ttu-id="01ac4-358">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/first.json) shows how to use the first function with an array and string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-358">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/first.json) shows how to use the first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="01ac4-359">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-359">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-360">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-360">Name</span></span> | <span data-ttu-id="01ac4-361">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-361">Type</span></span> | <span data-ttu-id="01ac4-362">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-362">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-363">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-363">arrayOutput</span></span> | <span data-ttu-id="01ac4-364">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-364">String</span></span> | <span data-ttu-id="01ac4-365">one</span><span class="sxs-lookup"><span data-stu-id="01ac4-365">one</span></span> |
| <span data-ttu-id="01ac4-366">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-366">stringOutput</span></span> | <span data-ttu-id="01ac4-367">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-367">String</span></span> | <span data-ttu-id="01ac4-368">O</span><span class="sxs-lookup"><span data-stu-id="01ac4-368">O</span></span> |

<span data-ttu-id="01ac4-369">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-369">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/first.json
```

<span data-ttu-id="01ac4-370">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-370">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/first.json
```

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="01ac4-371">intersection</span><span class="sxs-lookup"><span data-stu-id="01ac4-371">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="01ac4-372">Returns a single array or object with the common elements from the parameters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-372">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-373">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-373">Parameters</span></span>

| <span data-ttu-id="01ac4-374">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-374">Parameter</span></span> | <span data-ttu-id="01ac4-375">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-375">Required</span></span> | <span data-ttu-id="01ac4-376">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-376">Type</span></span> | <span data-ttu-id="01ac4-377">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-377">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-378">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-378">arg1</span></span> |<span data-ttu-id="01ac4-379">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-379">Yes</span></span> |<span data-ttu-id="01ac4-380">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-380">array or object</span></span> |<span data-ttu-id="01ac4-381">The first value to use for finding common elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-381">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="01ac4-382">arg2</span><span class="sxs-lookup"><span data-stu-id="01ac4-382">arg2</span></span> |<span data-ttu-id="01ac4-383">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-383">Yes</span></span> |<span data-ttu-id="01ac4-384">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-384">array or object</span></span> |<span data-ttu-id="01ac4-385">The second value to use for finding common elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-385">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="01ac4-386">additional arguments</span><span class="sxs-lookup"><span data-stu-id="01ac4-386">additional arguments</span></span> |<span data-ttu-id="01ac4-387">No</span><span class="sxs-lookup"><span data-stu-id="01ac4-387">No</span></span> |<span data-ttu-id="01ac4-388">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-388">array or object</span></span> |<span data-ttu-id="01ac4-389">Additional values to use for finding common elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-389">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-390">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-390">Return value</span></span>

<span data-ttu-id="01ac4-391">An array or object with the common elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-391">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-392">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-392">Example</span></span>

<span data-ttu-id="01ac4-393">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/intersection.json) shows how to use intersection with arrays and objects:</span><span class="sxs-lookup"><span data-stu-id="01ac4-393">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/intersection.json) shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-394">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-394">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-395">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-395">Name</span></span> | <span data-ttu-id="01ac4-396">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-396">Type</span></span> | <span data-ttu-id="01ac4-397">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-397">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-398">objectOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-398">objectOutput</span></span> | <span data-ttu-id="01ac4-399">Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-399">Object</span></span> | <span data-ttu-id="01ac4-400">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="01ac4-400">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="01ac4-401">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-401">arrayOutput</span></span> | <span data-ttu-id="01ac4-402">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-402">Array</span></span> | <span data-ttu-id="01ac4-403">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-403">["two", "three"]</span></span> |

<span data-ttu-id="01ac4-404">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-404">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/intersection.json
```

<span data-ttu-id="01ac4-405">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-405">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/intersection.json
```

## <a name="json"></a><span data-ttu-id="01ac4-406">json</span><span class="sxs-lookup"><span data-stu-id="01ac4-406">json</span></span>
`json(arg1)`

<span data-ttu-id="01ac4-407">Returns a JSON object.</span><span class="sxs-lookup"><span data-stu-id="01ac4-407">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-408">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-408">Parameters</span></span>

| <span data-ttu-id="01ac4-409">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-409">Parameter</span></span> | <span data-ttu-id="01ac4-410">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-410">Required</span></span> | <span data-ttu-id="01ac4-411">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-411">Type</span></span> | <span data-ttu-id="01ac4-412">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-412">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-413">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-413">arg1</span></span> |<span data-ttu-id="01ac4-414">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-414">Yes</span></span> |<span data-ttu-id="01ac4-415">string</span><span class="sxs-lookup"><span data-stu-id="01ac4-415">string</span></span> |<span data-ttu-id="01ac4-416">The value to convert to JSON.</span><span class="sxs-lookup"><span data-stu-id="01ac4-416">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="01ac4-417">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-417">Return value</span></span>

<span data-ttu-id="01ac4-418">The JSON object from the specified string, or an empty object when **null** is specified.</span><span class="sxs-lookup"><span data-stu-id="01ac4-418">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-419">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-419">Example</span></span>

<span data-ttu-id="01ac4-420">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/json.json) shows how to use the json function with arrays and objects:</span><span class="sxs-lookup"><span data-stu-id="01ac4-420">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/json.json) shows how to use the json function with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-421">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-421">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-422">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-422">Name</span></span> | <span data-ttu-id="01ac4-423">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-423">Type</span></span> | <span data-ttu-id="01ac4-424">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-424">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-425">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-425">jsonOutput</span></span> | <span data-ttu-id="01ac4-426">Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-426">Object</span></span> | <span data-ttu-id="01ac4-427">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="01ac4-427">{"a": "b"}</span></span> |
| <span data-ttu-id="01ac4-428">nullOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-428">nullOutput</span></span> | <span data-ttu-id="01ac4-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="01ac4-429">Boolean</span></span> | <span data-ttu-id="01ac4-430">True</span><span class="sxs-lookup"><span data-stu-id="01ac4-430">True</span></span> |

<span data-ttu-id="01ac4-431">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-431">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/json.json
```

<span data-ttu-id="01ac4-432">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-432">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/json.json
```

<a id="last" />

## <a name="last"></a><span data-ttu-id="01ac4-433">last</span><span class="sxs-lookup"><span data-stu-id="01ac4-433">last</span></span>
`last (arg1)`

<span data-ttu-id="01ac4-434">Returns the last element of the array, or last character of the string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-434">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-435">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-435">Parameters</span></span>

| <span data-ttu-id="01ac4-436">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-436">Parameter</span></span> | <span data-ttu-id="01ac4-437">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-437">Required</span></span> | <span data-ttu-id="01ac4-438">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-438">Type</span></span> | <span data-ttu-id="01ac4-439">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-439">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-440">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-440">arg1</span></span> |<span data-ttu-id="01ac4-441">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-441">Yes</span></span> |<span data-ttu-id="01ac4-442">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-442">array or string</span></span> |<span data-ttu-id="01ac4-443">The value to retrieve the last element or character.</span><span class="sxs-lookup"><span data-stu-id="01ac4-443">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-444">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-444">Return value</span></span>

<span data-ttu-id="01ac4-445">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-445">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-446">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-446">Example</span></span>

<span data-ttu-id="01ac4-447">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/last.json) shows how to use the last function with an array and string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-447">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/last.json) shows how to use the last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="01ac4-448">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-448">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-449">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-449">Name</span></span> | <span data-ttu-id="01ac4-450">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-450">Type</span></span> | <span data-ttu-id="01ac4-451">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-451">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-452">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-452">arrayOutput</span></span> | <span data-ttu-id="01ac4-453">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-453">String</span></span> | <span data-ttu-id="01ac4-454">three</span><span class="sxs-lookup"><span data-stu-id="01ac4-454">three</span></span> |
| <span data-ttu-id="01ac4-455">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-455">stringOutput</span></span> | <span data-ttu-id="01ac4-456">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-456">String</span></span> | <span data-ttu-id="01ac4-457">e</span><span class="sxs-lookup"><span data-stu-id="01ac4-457">e</span></span> |

<span data-ttu-id="01ac4-458">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-458">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/last.json
```

<span data-ttu-id="01ac4-459">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-459">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/last.json
```

<a id="length" />

## <a name="length"></a><span data-ttu-id="01ac4-460">length</span><span class="sxs-lookup"><span data-stu-id="01ac4-460">length</span></span>
`length(arg1)`

<span data-ttu-id="01ac4-461">Returns the number of elements in an array, or characters in a string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-461">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-462">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-462">Parameters</span></span>

| <span data-ttu-id="01ac4-463">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-463">Parameter</span></span> | <span data-ttu-id="01ac4-464">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-464">Required</span></span> | <span data-ttu-id="01ac4-465">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-465">Type</span></span> | <span data-ttu-id="01ac4-466">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-466">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-467">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-467">arg1</span></span> |<span data-ttu-id="01ac4-468">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-468">Yes</span></span> |<span data-ttu-id="01ac4-469">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-469">array or string</span></span> |<span data-ttu-id="01ac4-470">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-470">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-471">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-471">Return value</span></span>

<span data-ttu-id="01ac4-472">An int.</span><span class="sxs-lookup"><span data-stu-id="01ac4-472">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="01ac4-473">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-473">Example</span></span>

<span data-ttu-id="01ac4-474">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/length.json) shows how to use length with an array and string:</span><span class="sxs-lookup"><span data-stu-id="01ac4-474">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/length.json) shows how to use length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-475">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-475">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-476">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-476">Name</span></span> | <span data-ttu-id="01ac4-477">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-477">Type</span></span> | <span data-ttu-id="01ac4-478">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-478">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-479">arrayLength</span><span class="sxs-lookup"><span data-stu-id="01ac4-479">arrayLength</span></span> | <span data-ttu-id="01ac4-480">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-480">Int</span></span> | <span data-ttu-id="01ac4-481">3</span><span class="sxs-lookup"><span data-stu-id="01ac4-481">3</span></span> |
| <span data-ttu-id="01ac4-482">stringLength</span><span class="sxs-lookup"><span data-stu-id="01ac4-482">stringLength</span></span> | <span data-ttu-id="01ac4-483">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-483">Int</span></span> | <span data-ttu-id="01ac4-484">13</span><span class="sxs-lookup"><span data-stu-id="01ac4-484">13</span></span> |

<span data-ttu-id="01ac4-485">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-485">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/length.json
```

<span data-ttu-id="01ac4-486">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-486">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/length.json
```

<span data-ttu-id="01ac4-487">You can use this function with an array to specify the number of iterations when creating resources.</span><span class="sxs-lookup"><span data-stu-id="01ac4-487">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="01ac4-488">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span><span class="sxs-lookup"><span data-stu-id="01ac4-488">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="01ac4-489">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="01ac4-489">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="max" />

## <a name="max"></a><span data-ttu-id="01ac4-490">max</span><span class="sxs-lookup"><span data-stu-id="01ac4-490">max</span></span>
`max(arg1)`

<span data-ttu-id="01ac4-491">Returns the maximum value from an array of integers or a comma-separated list of integers.</span><span class="sxs-lookup"><span data-stu-id="01ac4-491">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-492">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-492">Parameters</span></span>

| <span data-ttu-id="01ac4-493">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-493">Parameter</span></span> | <span data-ttu-id="01ac4-494">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-494">Required</span></span> | <span data-ttu-id="01ac4-495">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-495">Type</span></span> | <span data-ttu-id="01ac4-496">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-496">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-497">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-497">arg1</span></span> |<span data-ttu-id="01ac4-498">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-498">Yes</span></span> |<span data-ttu-id="01ac4-499">array of integers, or comma-separated list of integers</span><span class="sxs-lookup"><span data-stu-id="01ac4-499">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="01ac4-500">The collection to get the maximum value.</span><span class="sxs-lookup"><span data-stu-id="01ac4-500">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-501">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-501">Return value</span></span>

<span data-ttu-id="01ac4-502">An int representing the maximum value.</span><span class="sxs-lookup"><span data-stu-id="01ac4-502">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-503">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-503">Example</span></span>

<span data-ttu-id="01ac4-504">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/max.json) shows how to use max with an array and a list of integers:</span><span class="sxs-lookup"><span data-stu-id="01ac4-504">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/max.json) shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="01ac4-505">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-505">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-506">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-506">Name</span></span> | <span data-ttu-id="01ac4-507">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-507">Type</span></span> | <span data-ttu-id="01ac4-508">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-508">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-509">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-509">arrayOutput</span></span> | <span data-ttu-id="01ac4-510">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-510">Int</span></span> | <span data-ttu-id="01ac4-511">5</span><span class="sxs-lookup"><span data-stu-id="01ac4-511">5</span></span> |
| <span data-ttu-id="01ac4-512">intOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-512">intOutput</span></span> | <span data-ttu-id="01ac4-513">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-513">Int</span></span> | <span data-ttu-id="01ac4-514">5</span><span class="sxs-lookup"><span data-stu-id="01ac4-514">5</span></span> |

<span data-ttu-id="01ac4-515">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-515">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/max.json
```

<span data-ttu-id="01ac4-516">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-516">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/max.json
```

<a id="min" />

## <a name="min"></a><span data-ttu-id="01ac4-517">min</span><span class="sxs-lookup"><span data-stu-id="01ac4-517">min</span></span>
`min(arg1)`

<span data-ttu-id="01ac4-518">Returns the minimum value from an array of integers or a comma-separated list of integers.</span><span class="sxs-lookup"><span data-stu-id="01ac4-518">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-519">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-519">Parameters</span></span>

| <span data-ttu-id="01ac4-520">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-520">Parameter</span></span> | <span data-ttu-id="01ac4-521">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-521">Required</span></span> | <span data-ttu-id="01ac4-522">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-522">Type</span></span> | <span data-ttu-id="01ac4-523">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-523">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-524">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-524">arg1</span></span> |<span data-ttu-id="01ac4-525">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-525">Yes</span></span> |<span data-ttu-id="01ac4-526">array of integers, or comma-separated list of integers</span><span class="sxs-lookup"><span data-stu-id="01ac4-526">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="01ac4-527">The collection to get the minimum value.</span><span class="sxs-lookup"><span data-stu-id="01ac4-527">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-528">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-528">Return value</span></span>

<span data-ttu-id="01ac4-529">An int representing the minimum value.</span><span class="sxs-lookup"><span data-stu-id="01ac4-529">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-530">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-530">Example</span></span>

<span data-ttu-id="01ac4-531">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/min.json) shows how to use min with an array and a list of integers:</span><span class="sxs-lookup"><span data-stu-id="01ac4-531">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/min.json) shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="01ac4-532">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-532">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-533">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-533">Name</span></span> | <span data-ttu-id="01ac4-534">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-534">Type</span></span> | <span data-ttu-id="01ac4-535">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-535">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-536">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-536">arrayOutput</span></span> | <span data-ttu-id="01ac4-537">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-537">Int</span></span> | <span data-ttu-id="01ac4-538">0</span><span class="sxs-lookup"><span data-stu-id="01ac4-538">0</span></span> |
| <span data-ttu-id="01ac4-539">intOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-539">intOutput</span></span> | <span data-ttu-id="01ac4-540">Int</span><span class="sxs-lookup"><span data-stu-id="01ac4-540">Int</span></span> | <span data-ttu-id="01ac4-541">0</span><span class="sxs-lookup"><span data-stu-id="01ac4-541">0</span></span> |

<span data-ttu-id="01ac4-542">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-542">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/min.json
```

<span data-ttu-id="01ac4-543">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-543">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/min.json
```

<a id="range" />

## <a name="range"></a><span data-ttu-id="01ac4-544">range</span><span class="sxs-lookup"><span data-stu-id="01ac4-544">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="01ac4-545">Creates an array of integers from a starting integer and containing a number of items.</span><span class="sxs-lookup"><span data-stu-id="01ac4-545">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-546">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-546">Parameters</span></span>

| <span data-ttu-id="01ac4-547">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-547">Parameter</span></span> | <span data-ttu-id="01ac4-548">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-548">Required</span></span> | <span data-ttu-id="01ac4-549">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-549">Type</span></span> | <span data-ttu-id="01ac4-550">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-550">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-551">startingInteger</span><span class="sxs-lookup"><span data-stu-id="01ac4-551">startingInteger</span></span> |<span data-ttu-id="01ac4-552">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-552">Yes</span></span> |<span data-ttu-id="01ac4-553">int</span><span class="sxs-lookup"><span data-stu-id="01ac4-553">int</span></span> |<span data-ttu-id="01ac4-554">The first integer in the array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-554">The first integer in the array.</span></span> |
| <span data-ttu-id="01ac4-555">numberofElements</span><span class="sxs-lookup"><span data-stu-id="01ac4-555">numberofElements</span></span> |<span data-ttu-id="01ac4-556">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-556">Yes</span></span> |<span data-ttu-id="01ac4-557">int</span><span class="sxs-lookup"><span data-stu-id="01ac4-557">int</span></span> |<span data-ttu-id="01ac4-558">The number of integers in the array.</span><span class="sxs-lookup"><span data-stu-id="01ac4-558">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-559">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-559">Return value</span></span>

<span data-ttu-id="01ac4-560">An array of integers.</span><span class="sxs-lookup"><span data-stu-id="01ac4-560">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-561">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-561">Example</span></span>

<span data-ttu-id="01ac4-562">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/range.json) shows how to use the range function:</span><span class="sxs-lookup"><span data-stu-id="01ac4-562">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/range.json) shows how to use the range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-563">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-564">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-564">Name</span></span> | <span data-ttu-id="01ac4-565">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-565">Type</span></span> | <span data-ttu-id="01ac4-566">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-567">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-567">rangeOutput</span></span> | <span data-ttu-id="01ac4-568">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-568">Array</span></span> | <span data-ttu-id="01ac4-569">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="01ac4-569">[5, 6, 7]</span></span> |

<span data-ttu-id="01ac4-570">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-570">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/range.json
```

<span data-ttu-id="01ac4-571">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-571">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/range.json
```

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="01ac4-572">skip</span><span class="sxs-lookup"><span data-stu-id="01ac4-572">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="01ac4-573">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-573">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-574">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-574">Parameters</span></span>

| <span data-ttu-id="01ac4-575">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-575">Parameter</span></span> | <span data-ttu-id="01ac4-576">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-576">Required</span></span> | <span data-ttu-id="01ac4-577">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-577">Type</span></span> | <span data-ttu-id="01ac4-578">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-578">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-579">originalValue</span><span class="sxs-lookup"><span data-stu-id="01ac4-579">originalValue</span></span> |<span data-ttu-id="01ac4-580">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-580">Yes</span></span> |<span data-ttu-id="01ac4-581">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-581">array or string</span></span> |<span data-ttu-id="01ac4-582">The array or string to use for skipping.</span><span class="sxs-lookup"><span data-stu-id="01ac4-582">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="01ac4-583">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="01ac4-583">numberToSkip</span></span> |<span data-ttu-id="01ac4-584">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-584">Yes</span></span> |<span data-ttu-id="01ac4-585">int</span><span class="sxs-lookup"><span data-stu-id="01ac4-585">int</span></span> |<span data-ttu-id="01ac4-586">The number of elements or characters to skip.</span><span class="sxs-lookup"><span data-stu-id="01ac4-586">The number of elements or characters to skip.</span></span> <span data-ttu-id="01ac4-587">If this value is 0 or less, all the elements or characters in the value are returned.</span><span class="sxs-lookup"><span data-stu-id="01ac4-587">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="01ac4-588">If it is larger than the length of the array or string, an empty array or string is returned.</span><span class="sxs-lookup"><span data-stu-id="01ac4-588">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-589">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-589">Return value</span></span>

<span data-ttu-id="01ac4-590">An array or string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-590">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-591">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-591">Example</span></span>

<span data-ttu-id="01ac4-592">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/skip.json) skips the specified number of elements in the array, and the specified number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-592">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/skip.json) skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-593">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-593">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-594">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-594">Name</span></span> | <span data-ttu-id="01ac4-595">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-595">Type</span></span> | <span data-ttu-id="01ac4-596">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-596">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-597">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-597">arrayOutput</span></span> | <span data-ttu-id="01ac4-598">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-598">Array</span></span> | <span data-ttu-id="01ac4-599">["three"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-599">["three"]</span></span> |
| <span data-ttu-id="01ac4-600">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-600">stringOutput</span></span> | <span data-ttu-id="01ac4-601">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-601">String</span></span> | <span data-ttu-id="01ac4-602">two three</span><span class="sxs-lookup"><span data-stu-id="01ac4-602">two three</span></span> |

<span data-ttu-id="01ac4-603">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-603">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/skip.json
```

<span data-ttu-id="01ac4-604">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-604">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/skip.json
```

<a id="take" />

## <a name="take"></a><span data-ttu-id="01ac4-605">take</span><span class="sxs-lookup"><span data-stu-id="01ac4-605">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="01ac4-606">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-606">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-607">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-607">Parameters</span></span>

| <span data-ttu-id="01ac4-608">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-608">Parameter</span></span> | <span data-ttu-id="01ac4-609">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-609">Required</span></span> | <span data-ttu-id="01ac4-610">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-610">Type</span></span> | <span data-ttu-id="01ac4-611">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-612">originalValue</span><span class="sxs-lookup"><span data-stu-id="01ac4-612">originalValue</span></span> |<span data-ttu-id="01ac4-613">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-613">Yes</span></span> |<span data-ttu-id="01ac4-614">array or string</span><span class="sxs-lookup"><span data-stu-id="01ac4-614">array or string</span></span> |<span data-ttu-id="01ac4-615">The array or string to take the elements from.</span><span class="sxs-lookup"><span data-stu-id="01ac4-615">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="01ac4-616">numberToTake</span><span class="sxs-lookup"><span data-stu-id="01ac4-616">numberToTake</span></span> |<span data-ttu-id="01ac4-617">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-617">Yes</span></span> |<span data-ttu-id="01ac4-618">int</span><span class="sxs-lookup"><span data-stu-id="01ac4-618">int</span></span> |<span data-ttu-id="01ac4-619">The number of elements or characters to take.</span><span class="sxs-lookup"><span data-stu-id="01ac4-619">The number of elements or characters to take.</span></span> <span data-ttu-id="01ac4-620">If this value is 0 or less, an empty array or string is returned.</span><span class="sxs-lookup"><span data-stu-id="01ac4-620">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="01ac4-621">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span><span class="sxs-lookup"><span data-stu-id="01ac4-621">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-622">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-622">Return value</span></span>

<span data-ttu-id="01ac4-623">An array or string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-623">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-624">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-624">Example</span></span>

<span data-ttu-id="01ac4-625">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/take.json) takes the specified number of elements from the array, and characters from a string.</span><span class="sxs-lookup"><span data-stu-id="01ac4-625">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/take.json) takes the specified number of elements from the array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-626">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-626">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-627">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-627">Name</span></span> | <span data-ttu-id="01ac4-628">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-628">Type</span></span> | <span data-ttu-id="01ac4-629">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-629">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-630">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-630">arrayOutput</span></span> | <span data-ttu-id="01ac4-631">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-631">Array</span></span> | <span data-ttu-id="01ac4-632">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-632">["one", "two"]</span></span> |
| <span data-ttu-id="01ac4-633">stringOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-633">stringOutput</span></span> | <span data-ttu-id="01ac4-634">String</span><span class="sxs-lookup"><span data-stu-id="01ac4-634">String</span></span> | <span data-ttu-id="01ac4-635">on</span><span class="sxs-lookup"><span data-stu-id="01ac4-635">on</span></span> |

<span data-ttu-id="01ac4-636">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-636">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/take.json
```

<span data-ttu-id="01ac4-637">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-637">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/take.json
```

<a id="union" />

## <a name="union"></a><span data-ttu-id="01ac4-638">union</span><span class="sxs-lookup"><span data-stu-id="01ac4-638">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="01ac4-639">Returns a single array or object with all elements from the parameters.</span><span class="sxs-lookup"><span data-stu-id="01ac4-639">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="01ac4-640">Duplicate values or keys are only included once.</span><span class="sxs-lookup"><span data-stu-id="01ac4-640">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="01ac4-641">Parameters</span><span class="sxs-lookup"><span data-stu-id="01ac4-641">Parameters</span></span>

| <span data-ttu-id="01ac4-642">Parameter</span><span class="sxs-lookup"><span data-stu-id="01ac4-642">Parameter</span></span> | <span data-ttu-id="01ac4-643">Required</span><span class="sxs-lookup"><span data-stu-id="01ac4-643">Required</span></span> | <span data-ttu-id="01ac4-644">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-644">Type</span></span> | <span data-ttu-id="01ac4-645">Description</span><span class="sxs-lookup"><span data-stu-id="01ac4-645">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01ac4-646">arg1</span><span class="sxs-lookup"><span data-stu-id="01ac4-646">arg1</span></span> |<span data-ttu-id="01ac4-647">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-647">Yes</span></span> |<span data-ttu-id="01ac4-648">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-648">array or object</span></span> |<span data-ttu-id="01ac4-649">The first value to use for joining elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-649">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="01ac4-650">arg2</span><span class="sxs-lookup"><span data-stu-id="01ac4-650">arg2</span></span> |<span data-ttu-id="01ac4-651">Yes</span><span class="sxs-lookup"><span data-stu-id="01ac4-651">Yes</span></span> |<span data-ttu-id="01ac4-652">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-652">array or object</span></span> |<span data-ttu-id="01ac4-653">The second value to use for joining elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-653">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="01ac4-654">additional arguments</span><span class="sxs-lookup"><span data-stu-id="01ac4-654">additional arguments</span></span> |<span data-ttu-id="01ac4-655">No</span><span class="sxs-lookup"><span data-stu-id="01ac4-655">No</span></span> |<span data-ttu-id="01ac4-656">array or object</span><span class="sxs-lookup"><span data-stu-id="01ac4-656">array or object</span></span> |<span data-ttu-id="01ac4-657">Additional values to use for joining elements.</span><span class="sxs-lookup"><span data-stu-id="01ac4-657">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="01ac4-658">Return value</span><span class="sxs-lookup"><span data-stu-id="01ac4-658">Return value</span></span>

<span data-ttu-id="01ac4-659">An array or object.</span><span class="sxs-lookup"><span data-stu-id="01ac4-659">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="01ac4-660">Example</span><span class="sxs-lookup"><span data-stu-id="01ac4-660">Example</span></span>

<span data-ttu-id="01ac4-661">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/union.json) shows how to use union with arrays and objects:</span><span class="sxs-lookup"><span data-stu-id="01ac4-661">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/union.json) shows how to use union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c1"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c2", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="01ac4-662">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="01ac4-662">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="01ac4-663">Name</span><span class="sxs-lookup"><span data-stu-id="01ac4-663">Name</span></span> | <span data-ttu-id="01ac4-664">Type</span><span class="sxs-lookup"><span data-stu-id="01ac4-664">Type</span></span> | <span data-ttu-id="01ac4-665">Value</span><span class="sxs-lookup"><span data-stu-id="01ac4-665">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="01ac4-666">objectOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-666">objectOutput</span></span> | <span data-ttu-id="01ac4-667">Object</span><span class="sxs-lookup"><span data-stu-id="01ac4-667">Object</span></span> | <span data-ttu-id="01ac4-668">{"one": "a", "two": "b", "three": "c2", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="01ac4-668">{"one": "a", "two": "b", "three": "c2", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="01ac4-669">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="01ac4-669">arrayOutput</span></span> | <span data-ttu-id="01ac4-670">Array</span><span class="sxs-lookup"><span data-stu-id="01ac4-670">Array</span></span> | <span data-ttu-id="01ac4-671">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="01ac4-671">["one", "two", "three", "four"]</span></span> |

<span data-ttu-id="01ac4-672">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-672">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/union.json
```

<span data-ttu-id="01ac4-673">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="01ac4-673">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/union.json
```

## <a name="next-steps"></a><span data-ttu-id="01ac4-674">Next steps</span><span class="sxs-lookup"><span data-stu-id="01ac4-674">Next steps</span></span>
* <span data-ttu-id="01ac4-675">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01ac4-675">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="01ac4-676">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="01ac4-676">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="01ac4-677">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="01ac4-677">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="01ac4-678">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="01ac4-678">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

