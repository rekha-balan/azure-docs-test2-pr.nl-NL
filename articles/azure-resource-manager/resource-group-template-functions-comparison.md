---
title: Azure Resource Manager template functions - comparison | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to compare values.
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
ms.openlocfilehash: 364a271d84f9abfe99c7c674a6c504ce94318ac9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866273"
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="309fd-103">Comparison functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="309fd-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="309fd-104">Resource Manager provides several functions for making comparisons in your templates.</span><span class="sxs-lookup"><span data-stu-id="309fd-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="309fd-105">equals</span><span class="sxs-lookup"><span data-stu-id="309fd-105">equals</span></span>](#equals)
* [<span data-ttu-id="309fd-106">greater</span><span class="sxs-lookup"><span data-stu-id="309fd-106">greater</span></span>](#greater)
* [<span data-ttu-id="309fd-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="309fd-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="309fd-108">less</span><span class="sxs-lookup"><span data-stu-id="309fd-108">less</span></span>](#less)
* [<span data-ttu-id="309fd-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="309fd-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="309fd-110">equals</span><span class="sxs-lookup"><span data-stu-id="309fd-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="309fd-111">Checks whether two values equal each other.</span><span class="sxs-lookup"><span data-stu-id="309fd-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="309fd-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="309fd-112">Parameters</span></span>

| <span data-ttu-id="309fd-113">Parameter</span><span class="sxs-lookup"><span data-stu-id="309fd-113">Parameter</span></span> | <span data-ttu-id="309fd-114">Required</span><span class="sxs-lookup"><span data-stu-id="309fd-114">Required</span></span> | <span data-ttu-id="309fd-115">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-115">Type</span></span> | <span data-ttu-id="309fd-116">Description</span><span class="sxs-lookup"><span data-stu-id="309fd-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="309fd-117">arg1</span><span class="sxs-lookup"><span data-stu-id="309fd-117">arg1</span></span> |<span data-ttu-id="309fd-118">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-118">Yes</span></span> |<span data-ttu-id="309fd-119">int, string, array, or object</span><span class="sxs-lookup"><span data-stu-id="309fd-119">int, string, array, or object</span></span> |<span data-ttu-id="309fd-120">The first value to check for equality.</span><span class="sxs-lookup"><span data-stu-id="309fd-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="309fd-121">arg2</span><span class="sxs-lookup"><span data-stu-id="309fd-121">arg2</span></span> |<span data-ttu-id="309fd-122">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-122">Yes</span></span> |<span data-ttu-id="309fd-123">int, string, array, or object</span><span class="sxs-lookup"><span data-stu-id="309fd-123">int, string, array, or object</span></span> |<span data-ttu-id="309fd-124">The second value to check for equality.</span><span class="sxs-lookup"><span data-stu-id="309fd-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="309fd-125">Return value</span><span class="sxs-lookup"><span data-stu-id="309fd-125">Return value</span></span>

<span data-ttu-id="309fd-126">Returns **True** if the values are equal; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="309fd-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="309fd-127">Remarks</span><span class="sxs-lookup"><span data-stu-id="309fd-127">Remarks</span></span>

<span data-ttu-id="309fd-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span><span class="sxs-lookup"><span data-stu-id="309fd-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="309fd-129">Example</span><span class="sxs-lookup"><span data-stu-id="309fd-129">Example</span></span>

<span data-ttu-id="309fd-130">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/equals.json) checks different types of values for equality.</span><span class="sxs-lookup"><span data-stu-id="309fd-130">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/equals.json) checks different types of values for equality.</span></span> <span data-ttu-id="309fd-131">All the default values return True.</span><span class="sxs-lookup"><span data-stu-id="309fd-131">All the default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="309fd-132">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="309fd-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="309fd-133">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-133">Name</span></span> | <span data-ttu-id="309fd-134">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-134">Type</span></span> | <span data-ttu-id="309fd-135">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="309fd-136">checkInts</span></span> | <span data-ttu-id="309fd-137">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-137">Bool</span></span> | <span data-ttu-id="309fd-138">True</span><span class="sxs-lookup"><span data-stu-id="309fd-138">True</span></span> |
| <span data-ttu-id="309fd-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="309fd-139">checkStrings</span></span> | <span data-ttu-id="309fd-140">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-140">Bool</span></span> | <span data-ttu-id="309fd-141">True</span><span class="sxs-lookup"><span data-stu-id="309fd-141">True</span></span> |
| <span data-ttu-id="309fd-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="309fd-142">checkArrays</span></span> | <span data-ttu-id="309fd-143">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-143">Bool</span></span> | <span data-ttu-id="309fd-144">True</span><span class="sxs-lookup"><span data-stu-id="309fd-144">True</span></span> |
| <span data-ttu-id="309fd-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="309fd-145">checkObjects</span></span> | <span data-ttu-id="309fd-146">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-146">Bool</span></span> | <span data-ttu-id="309fd-147">True</span><span class="sxs-lookup"><span data-stu-id="309fd-147">True</span></span> |

<span data-ttu-id="309fd-148">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-148">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/equals.json
```

<span data-ttu-id="309fd-149">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-149">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/equals.json 
```

<span data-ttu-id="309fd-150">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/not-equals.json) uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span><span class="sxs-lookup"><span data-stu-id="309fd-150">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/not-equals.json) uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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
}
```

<span data-ttu-id="309fd-151">The output from the preceding example is:</span><span class="sxs-lookup"><span data-stu-id="309fd-151">The output from the preceding example is:</span></span>

| <span data-ttu-id="309fd-152">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-152">Name</span></span> | <span data-ttu-id="309fd-153">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-153">Type</span></span> | <span data-ttu-id="309fd-154">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-154">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-155">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="309fd-155">checkNotEquals</span></span> | <span data-ttu-id="309fd-156">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-156">Bool</span></span> | <span data-ttu-id="309fd-157">True</span><span class="sxs-lookup"><span data-stu-id="309fd-157">True</span></span> |

<span data-ttu-id="309fd-158">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-158">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json
```

<span data-ttu-id="309fd-159">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-159">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/not-equals.json 
```

## <a name="greater"></a><span data-ttu-id="309fd-160">greater</span><span class="sxs-lookup"><span data-stu-id="309fd-160">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="309fd-161">Checks whether the first value is greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="309fd-161">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="309fd-162">Parameters</span><span class="sxs-lookup"><span data-stu-id="309fd-162">Parameters</span></span>

| <span data-ttu-id="309fd-163">Parameter</span><span class="sxs-lookup"><span data-stu-id="309fd-163">Parameter</span></span> | <span data-ttu-id="309fd-164">Required</span><span class="sxs-lookup"><span data-stu-id="309fd-164">Required</span></span> | <span data-ttu-id="309fd-165">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-165">Type</span></span> | <span data-ttu-id="309fd-166">Description</span><span class="sxs-lookup"><span data-stu-id="309fd-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="309fd-167">arg1</span><span class="sxs-lookup"><span data-stu-id="309fd-167">arg1</span></span> |<span data-ttu-id="309fd-168">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-168">Yes</span></span> |<span data-ttu-id="309fd-169">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-169">int or string</span></span> |<span data-ttu-id="309fd-170">The first value for the greater comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-170">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="309fd-171">arg2</span><span class="sxs-lookup"><span data-stu-id="309fd-171">arg2</span></span> |<span data-ttu-id="309fd-172">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-172">Yes</span></span> |<span data-ttu-id="309fd-173">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-173">int or string</span></span> |<span data-ttu-id="309fd-174">The second value for the greater comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-174">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="309fd-175">Return value</span><span class="sxs-lookup"><span data-stu-id="309fd-175">Return value</span></span>

<span data-ttu-id="309fd-176">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="309fd-176">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="309fd-177">Example</span><span class="sxs-lookup"><span data-stu-id="309fd-177">Example</span></span>

<span data-ttu-id="309fd-178">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/greater.json) checks whether the one value is greater than the other.</span><span class="sxs-lookup"><span data-stu-id="309fd-178">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/greater.json) checks whether the one value is greater than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="309fd-179">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="309fd-179">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="309fd-180">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-180">Name</span></span> | <span data-ttu-id="309fd-181">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-181">Type</span></span> | <span data-ttu-id="309fd-182">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-182">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-183">checkInts</span><span class="sxs-lookup"><span data-stu-id="309fd-183">checkInts</span></span> | <span data-ttu-id="309fd-184">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-184">Bool</span></span> | <span data-ttu-id="309fd-185">False</span><span class="sxs-lookup"><span data-stu-id="309fd-185">False</span></span> |
| <span data-ttu-id="309fd-186">checkStrings</span><span class="sxs-lookup"><span data-stu-id="309fd-186">checkStrings</span></span> | <span data-ttu-id="309fd-187">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-187">Bool</span></span> | <span data-ttu-id="309fd-188">True</span><span class="sxs-lookup"><span data-stu-id="309fd-188">True</span></span> |

<span data-ttu-id="309fd-189">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-189">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/greater.json
```

<span data-ttu-id="309fd-190">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-190">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/greater.json 
```

## <a name="greaterorequals"></a><span data-ttu-id="309fd-191">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="309fd-191">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="309fd-192">Checks whether the first value is greater than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="309fd-192">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="309fd-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="309fd-193">Parameters</span></span>

| <span data-ttu-id="309fd-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="309fd-194">Parameter</span></span> | <span data-ttu-id="309fd-195">Required</span><span class="sxs-lookup"><span data-stu-id="309fd-195">Required</span></span> | <span data-ttu-id="309fd-196">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-196">Type</span></span> | <span data-ttu-id="309fd-197">Description</span><span class="sxs-lookup"><span data-stu-id="309fd-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="309fd-198">arg1</span><span class="sxs-lookup"><span data-stu-id="309fd-198">arg1</span></span> |<span data-ttu-id="309fd-199">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-199">Yes</span></span> |<span data-ttu-id="309fd-200">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-200">int or string</span></span> |<span data-ttu-id="309fd-201">The first value for the greater or equal comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-201">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="309fd-202">arg2</span><span class="sxs-lookup"><span data-stu-id="309fd-202">arg2</span></span> |<span data-ttu-id="309fd-203">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-203">Yes</span></span> |<span data-ttu-id="309fd-204">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-204">int or string</span></span> |<span data-ttu-id="309fd-205">The second value for the greater or equal comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-205">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="309fd-206">Return value</span><span class="sxs-lookup"><span data-stu-id="309fd-206">Return value</span></span>

<span data-ttu-id="309fd-207">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="309fd-207">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="309fd-208">Example</span><span class="sxs-lookup"><span data-stu-id="309fd-208">Example</span></span>

<span data-ttu-id="309fd-209">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/greaterorequals.json) checks whether the one value is greater than or equal to the other.</span><span class="sxs-lookup"><span data-stu-id="309fd-209">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/greaterorequals.json) checks whether the one value is greater than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="309fd-210">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="309fd-210">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="309fd-211">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-211">Name</span></span> | <span data-ttu-id="309fd-212">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-212">Type</span></span> | <span data-ttu-id="309fd-213">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-213">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-214">checkInts</span><span class="sxs-lookup"><span data-stu-id="309fd-214">checkInts</span></span> | <span data-ttu-id="309fd-215">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-215">Bool</span></span> | <span data-ttu-id="309fd-216">False</span><span class="sxs-lookup"><span data-stu-id="309fd-216">False</span></span> |
| <span data-ttu-id="309fd-217">checkStrings</span><span class="sxs-lookup"><span data-stu-id="309fd-217">checkStrings</span></span> | <span data-ttu-id="309fd-218">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-218">Bool</span></span> | <span data-ttu-id="309fd-219">True</span><span class="sxs-lookup"><span data-stu-id="309fd-219">True</span></span> |

<span data-ttu-id="309fd-220">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-220">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/greaterorequals.json
```

<span data-ttu-id="309fd-221">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-221">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/greaterorequals.json 
```

## <a name="less"></a><span data-ttu-id="309fd-222">less</span><span class="sxs-lookup"><span data-stu-id="309fd-222">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="309fd-223">Checks whether the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="309fd-223">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="309fd-224">Parameters</span><span class="sxs-lookup"><span data-stu-id="309fd-224">Parameters</span></span>

| <span data-ttu-id="309fd-225">Parameter</span><span class="sxs-lookup"><span data-stu-id="309fd-225">Parameter</span></span> | <span data-ttu-id="309fd-226">Required</span><span class="sxs-lookup"><span data-stu-id="309fd-226">Required</span></span> | <span data-ttu-id="309fd-227">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-227">Type</span></span> | <span data-ttu-id="309fd-228">Description</span><span class="sxs-lookup"><span data-stu-id="309fd-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="309fd-229">arg1</span><span class="sxs-lookup"><span data-stu-id="309fd-229">arg1</span></span> |<span data-ttu-id="309fd-230">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-230">Yes</span></span> |<span data-ttu-id="309fd-231">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-231">int or string</span></span> |<span data-ttu-id="309fd-232">The first value for the less comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-232">The first value for the less comparison.</span></span> |
| <span data-ttu-id="309fd-233">arg2</span><span class="sxs-lookup"><span data-stu-id="309fd-233">arg2</span></span> |<span data-ttu-id="309fd-234">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-234">Yes</span></span> |<span data-ttu-id="309fd-235">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-235">int or string</span></span> |<span data-ttu-id="309fd-236">The second value for the less comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-236">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="309fd-237">Return value</span><span class="sxs-lookup"><span data-stu-id="309fd-237">Return value</span></span>

<span data-ttu-id="309fd-238">Returns **True** if the first value is less than the second value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="309fd-238">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="309fd-239">Example</span><span class="sxs-lookup"><span data-stu-id="309fd-239">Example</span></span>

<span data-ttu-id="309fd-240">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/less.json) checks whether the one value is less than the other.</span><span class="sxs-lookup"><span data-stu-id="309fd-240">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/less.json) checks whether the one value is less than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="309fd-241">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="309fd-241">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="309fd-242">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-242">Name</span></span> | <span data-ttu-id="309fd-243">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-243">Type</span></span> | <span data-ttu-id="309fd-244">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-244">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-245">checkInts</span><span class="sxs-lookup"><span data-stu-id="309fd-245">checkInts</span></span> | <span data-ttu-id="309fd-246">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-246">Bool</span></span> | <span data-ttu-id="309fd-247">True</span><span class="sxs-lookup"><span data-stu-id="309fd-247">True</span></span> |
| <span data-ttu-id="309fd-248">checkStrings</span><span class="sxs-lookup"><span data-stu-id="309fd-248">checkStrings</span></span> | <span data-ttu-id="309fd-249">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-249">Bool</span></span> | <span data-ttu-id="309fd-250">False</span><span class="sxs-lookup"><span data-stu-id="309fd-250">False</span></span> |

<span data-ttu-id="309fd-251">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-251">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/less.json
```

<span data-ttu-id="309fd-252">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-252">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/less.json 
```

## <a name="lessorequals"></a><span data-ttu-id="309fd-253">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="309fd-253">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="309fd-254">Checks whether the first value is less than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="309fd-254">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="309fd-255">Parameters</span><span class="sxs-lookup"><span data-stu-id="309fd-255">Parameters</span></span>

| <span data-ttu-id="309fd-256">Parameter</span><span class="sxs-lookup"><span data-stu-id="309fd-256">Parameter</span></span> | <span data-ttu-id="309fd-257">Required</span><span class="sxs-lookup"><span data-stu-id="309fd-257">Required</span></span> | <span data-ttu-id="309fd-258">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-258">Type</span></span> | <span data-ttu-id="309fd-259">Description</span><span class="sxs-lookup"><span data-stu-id="309fd-259">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="309fd-260">arg1</span><span class="sxs-lookup"><span data-stu-id="309fd-260">arg1</span></span> |<span data-ttu-id="309fd-261">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-261">Yes</span></span> |<span data-ttu-id="309fd-262">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-262">int or string</span></span> |<span data-ttu-id="309fd-263">The first value for the less or equals comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-263">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="309fd-264">arg2</span><span class="sxs-lookup"><span data-stu-id="309fd-264">arg2</span></span> |<span data-ttu-id="309fd-265">Yes</span><span class="sxs-lookup"><span data-stu-id="309fd-265">Yes</span></span> |<span data-ttu-id="309fd-266">int or string</span><span class="sxs-lookup"><span data-stu-id="309fd-266">int or string</span></span> |<span data-ttu-id="309fd-267">The second value for the less or equals comparison.</span><span class="sxs-lookup"><span data-stu-id="309fd-267">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="309fd-268">Return value</span><span class="sxs-lookup"><span data-stu-id="309fd-268">Return value</span></span>

<span data-ttu-id="309fd-269">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="309fd-269">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="309fd-270">Example</span><span class="sxs-lookup"><span data-stu-id="309fd-270">Example</span></span>

<span data-ttu-id="309fd-271">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/lessorequals.json) checks whether the one value is less than or equal to the other.</span><span class="sxs-lookup"><span data-stu-id="309fd-271">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/lessorequals.json) checks whether the one value is less than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="309fd-272">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="309fd-272">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="309fd-273">Name</span><span class="sxs-lookup"><span data-stu-id="309fd-273">Name</span></span> | <span data-ttu-id="309fd-274">Type</span><span class="sxs-lookup"><span data-stu-id="309fd-274">Type</span></span> | <span data-ttu-id="309fd-275">Value</span><span class="sxs-lookup"><span data-stu-id="309fd-275">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="309fd-276">checkInts</span><span class="sxs-lookup"><span data-stu-id="309fd-276">checkInts</span></span> | <span data-ttu-id="309fd-277">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-277">Bool</span></span> | <span data-ttu-id="309fd-278">True</span><span class="sxs-lookup"><span data-stu-id="309fd-278">True</span></span> |
| <span data-ttu-id="309fd-279">checkStrings</span><span class="sxs-lookup"><span data-stu-id="309fd-279">checkStrings</span></span> | <span data-ttu-id="309fd-280">Bool</span><span class="sxs-lookup"><span data-stu-id="309fd-280">Bool</span></span> | <span data-ttu-id="309fd-281">False</span><span class="sxs-lookup"><span data-stu-id="309fd-281">False</span></span> |

<span data-ttu-id="309fd-282">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-282">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/lessorequals.json
```

<span data-ttu-id="309fd-283">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="309fd-283">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/lessorequals.json 
```

## <a name="next-steps"></a><span data-ttu-id="309fd-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="309fd-284">Next steps</span></span>
* <span data-ttu-id="309fd-285">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="309fd-285">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="309fd-286">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="309fd-286">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="309fd-287">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="309fd-287">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="309fd-288">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="309fd-288">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

