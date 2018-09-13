---
title: Azure Resource Manager template functions - string | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to work with strings.
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
ms.openlocfilehash: 33a49a9fb66240382b0bb4e0bedbb07b8d78a763
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868159"
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="df661-103">String functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="df661-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="df661-104">Resource Manager provides the following functions for working with strings:</span><span class="sxs-lookup"><span data-stu-id="df661-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="df661-105">base64</span><span class="sxs-lookup"><span data-stu-id="df661-105">base64</span></span>](#base64)
* [<span data-ttu-id="df661-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="df661-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="df661-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="df661-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="df661-108">concat</span><span class="sxs-lookup"><span data-stu-id="df661-108">concat</span></span>](#concat)
* [<span data-ttu-id="df661-109">contains</span><span class="sxs-lookup"><span data-stu-id="df661-109">contains</span></span>](#contains)
* [<span data-ttu-id="df661-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="df661-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="df661-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="df661-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="df661-112">empty</span><span class="sxs-lookup"><span data-stu-id="df661-112">empty</span></span>](#empty)
* [<span data-ttu-id="df661-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="df661-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="df661-114">first</span><span class="sxs-lookup"><span data-stu-id="df661-114">first</span></span>](#first)
* [<span data-ttu-id="df661-115">guid</span><span class="sxs-lookup"><span data-stu-id="df661-115">guid</span></span>](#guid)
* [<span data-ttu-id="df661-116">indexOf</span><span class="sxs-lookup"><span data-stu-id="df661-116">indexOf</span></span>](#indexof)
* [<span data-ttu-id="df661-117">last</span><span class="sxs-lookup"><span data-stu-id="df661-117">last</span></span>](#last)
* [<span data-ttu-id="df661-118">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="df661-118">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="df661-119">length</span><span class="sxs-lookup"><span data-stu-id="df661-119">length</span></span>](#length)
* [<span data-ttu-id="df661-120">padLeft</span><span class="sxs-lookup"><span data-stu-id="df661-120">padLeft</span></span>](#padleft)
* [<span data-ttu-id="df661-121">replace</span><span class="sxs-lookup"><span data-stu-id="df661-121">replace</span></span>](#replace)
* [<span data-ttu-id="df661-122">skip</span><span class="sxs-lookup"><span data-stu-id="df661-122">skip</span></span>](#skip)
* [<span data-ttu-id="df661-123">split</span><span class="sxs-lookup"><span data-stu-id="df661-123">split</span></span>](#split)
* [<span data-ttu-id="df661-124">startsWith</span><span class="sxs-lookup"><span data-stu-id="df661-124">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="df661-125">string</span><span class="sxs-lookup"><span data-stu-id="df661-125">string</span></span>](#string)
* [<span data-ttu-id="df661-126">substring</span><span class="sxs-lookup"><span data-stu-id="df661-126">substring</span></span>](#substring)
* [<span data-ttu-id="df661-127">take</span><span class="sxs-lookup"><span data-stu-id="df661-127">take</span></span>](#take)
* [<span data-ttu-id="df661-128">toLower</span><span class="sxs-lookup"><span data-stu-id="df661-128">toLower</span></span>](#tolower)
* [<span data-ttu-id="df661-129">toUpper</span><span class="sxs-lookup"><span data-stu-id="df661-129">toUpper</span></span>](#toupper)
* [<span data-ttu-id="df661-130">trim</span><span class="sxs-lookup"><span data-stu-id="df661-130">trim</span></span>](#trim)
* [<span data-ttu-id="df661-131">uniqueString</span><span class="sxs-lookup"><span data-stu-id="df661-131">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="df661-132">uri</span><span class="sxs-lookup"><span data-stu-id="df661-132">uri</span></span>](#uri)
* [<span data-ttu-id="df661-133">uriComponent</span><span class="sxs-lookup"><span data-stu-id="df661-133">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="df661-134">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="df661-134">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="df661-135">base64</span><span class="sxs-lookup"><span data-stu-id="df661-135">base64</span></span>
`base64(inputString)`

<span data-ttu-id="df661-136">Returns the base64 representation of the input string.</span><span class="sxs-lookup"><span data-stu-id="df661-136">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-137">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-137">Parameters</span></span>

| <span data-ttu-id="df661-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-138">Parameter</span></span> | <span data-ttu-id="df661-139">Required</span><span class="sxs-lookup"><span data-stu-id="df661-139">Required</span></span> | <span data-ttu-id="df661-140">Type</span><span class="sxs-lookup"><span data-stu-id="df661-140">Type</span></span> | <span data-ttu-id="df661-141">Description</span><span class="sxs-lookup"><span data-stu-id="df661-141">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-142">inputString</span><span class="sxs-lookup"><span data-stu-id="df661-142">inputString</span></span> |<span data-ttu-id="df661-143">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-143">Yes</span></span> |<span data-ttu-id="df661-144">string</span><span class="sxs-lookup"><span data-stu-id="df661-144">string</span></span> |<span data-ttu-id="df661-145">The value to return as a base64 representation.</span><span class="sxs-lookup"><span data-stu-id="df661-145">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-146">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-146">Return value</span></span>

<span data-ttu-id="df661-147">A string containing the base64 representation.</span><span class="sxs-lookup"><span data-stu-id="df661-147">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-148">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-148">Examples</span></span>

<span data-ttu-id="df661-149">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) shows how to use the base64 function.</span><span class="sxs-lookup"><span data-stu-id="df661-149">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="df661-150">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-150">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-151">Name</span><span class="sxs-lookup"><span data-stu-id="df661-151">Name</span></span> | <span data-ttu-id="df661-152">Type</span><span class="sxs-lookup"><span data-stu-id="df661-152">Type</span></span> | <span data-ttu-id="df661-153">Value</span><span class="sxs-lookup"><span data-stu-id="df661-153">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-154">base64Output</span><span class="sxs-lookup"><span data-stu-id="df661-154">base64Output</span></span> | <span data-ttu-id="df661-155">String</span><span class="sxs-lookup"><span data-stu-id="df661-155">String</span></span> | <span data-ttu-id="df661-156">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="df661-156">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="df661-157">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-157">toStringOutput</span></span> | <span data-ttu-id="df661-158">String</span><span class="sxs-lookup"><span data-stu-id="df661-158">String</span></span> | <span data-ttu-id="df661-159">one, two, three</span><span class="sxs-lookup"><span data-stu-id="df661-159">one, two, three</span></span> |
| <span data-ttu-id="df661-160">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="df661-160">toJsonOutput</span></span> | <span data-ttu-id="df661-161">Object</span><span class="sxs-lookup"><span data-stu-id="df661-161">Object</span></span> | <span data-ttu-id="df661-162">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="df661-162">{"one": "a", "two": "b"}</span></span> |

<span data-ttu-id="df661-163">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-163">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<span data-ttu-id="df661-164">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-164">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="df661-165">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="df661-165">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="df661-166">Converts a base64 representation to a JSON object.</span><span class="sxs-lookup"><span data-stu-id="df661-166">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-167">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-167">Parameters</span></span>

| <span data-ttu-id="df661-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-168">Parameter</span></span> | <span data-ttu-id="df661-169">Required</span><span class="sxs-lookup"><span data-stu-id="df661-169">Required</span></span> | <span data-ttu-id="df661-170">Type</span><span class="sxs-lookup"><span data-stu-id="df661-170">Type</span></span> | <span data-ttu-id="df661-171">Description</span><span class="sxs-lookup"><span data-stu-id="df661-171">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="df661-172">base64Value</span></span> |<span data-ttu-id="df661-173">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-173">Yes</span></span> |<span data-ttu-id="df661-174">string</span><span class="sxs-lookup"><span data-stu-id="df661-174">string</span></span> |<span data-ttu-id="df661-175">The base64 representation to convert to a JSON object.</span><span class="sxs-lookup"><span data-stu-id="df661-175">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-176">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-176">Return value</span></span>

<span data-ttu-id="df661-177">A JSON object.</span><span class="sxs-lookup"><span data-stu-id="df661-177">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-178">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-178">Examples</span></span>

<span data-ttu-id="df661-179">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) uses the base64ToJson function to convert a base64 value:</span><span class="sxs-lookup"><span data-stu-id="df661-179">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="df661-180">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-180">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-181">Name</span><span class="sxs-lookup"><span data-stu-id="df661-181">Name</span></span> | <span data-ttu-id="df661-182">Type</span><span class="sxs-lookup"><span data-stu-id="df661-182">Type</span></span> | <span data-ttu-id="df661-183">Value</span><span class="sxs-lookup"><span data-stu-id="df661-183">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-184">base64Output</span><span class="sxs-lookup"><span data-stu-id="df661-184">base64Output</span></span> | <span data-ttu-id="df661-185">String</span><span class="sxs-lookup"><span data-stu-id="df661-185">String</span></span> | <span data-ttu-id="df661-186">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="df661-186">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="df661-187">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-187">toStringOutput</span></span> | <span data-ttu-id="df661-188">String</span><span class="sxs-lookup"><span data-stu-id="df661-188">String</span></span> | <span data-ttu-id="df661-189">one, two, three</span><span class="sxs-lookup"><span data-stu-id="df661-189">one, two, three</span></span> |
| <span data-ttu-id="df661-190">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="df661-190">toJsonOutput</span></span> | <span data-ttu-id="df661-191">Object</span><span class="sxs-lookup"><span data-stu-id="df661-191">Object</span></span> | <span data-ttu-id="df661-192">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="df661-192">{"one": "a", "two": "b"}</span></span> |

<span data-ttu-id="df661-193">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-193">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<span data-ttu-id="df661-194">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-194">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="df661-195">base64ToString</span><span class="sxs-lookup"><span data-stu-id="df661-195">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="df661-196">Converts a base64 representation to a string.</span><span class="sxs-lookup"><span data-stu-id="df661-196">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-197">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-197">Parameters</span></span>

| <span data-ttu-id="df661-198">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-198">Parameter</span></span> | <span data-ttu-id="df661-199">Required</span><span class="sxs-lookup"><span data-stu-id="df661-199">Required</span></span> | <span data-ttu-id="df661-200">Type</span><span class="sxs-lookup"><span data-stu-id="df661-200">Type</span></span> | <span data-ttu-id="df661-201">Description</span><span class="sxs-lookup"><span data-stu-id="df661-201">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-202">base64Value</span><span class="sxs-lookup"><span data-stu-id="df661-202">base64Value</span></span> |<span data-ttu-id="df661-203">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-203">Yes</span></span> |<span data-ttu-id="df661-204">string</span><span class="sxs-lookup"><span data-stu-id="df661-204">string</span></span> |<span data-ttu-id="df661-205">The base64 representation to convert to a string.</span><span class="sxs-lookup"><span data-stu-id="df661-205">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-206">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-206">Return value</span></span>

<span data-ttu-id="df661-207">A string of the converted base64 value.</span><span class="sxs-lookup"><span data-stu-id="df661-207">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-208">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-208">Examples</span></span>

<span data-ttu-id="df661-209">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) uses the base64ToString function to convert a base64 value:</span><span class="sxs-lookup"><span data-stu-id="df661-209">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/base64.json) uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="df661-210">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-210">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-211">Name</span><span class="sxs-lookup"><span data-stu-id="df661-211">Name</span></span> | <span data-ttu-id="df661-212">Type</span><span class="sxs-lookup"><span data-stu-id="df661-212">Type</span></span> | <span data-ttu-id="df661-213">Value</span><span class="sxs-lookup"><span data-stu-id="df661-213">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-214">base64Output</span><span class="sxs-lookup"><span data-stu-id="df661-214">base64Output</span></span> | <span data-ttu-id="df661-215">String</span><span class="sxs-lookup"><span data-stu-id="df661-215">String</span></span> | <span data-ttu-id="df661-216">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="df661-216">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="df661-217">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-217">toStringOutput</span></span> | <span data-ttu-id="df661-218">String</span><span class="sxs-lookup"><span data-stu-id="df661-218">String</span></span> | <span data-ttu-id="df661-219">one, two, three</span><span class="sxs-lookup"><span data-stu-id="df661-219">one, two, three</span></span> |
| <span data-ttu-id="df661-220">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="df661-220">toJsonOutput</span></span> | <span data-ttu-id="df661-221">Object</span><span class="sxs-lookup"><span data-stu-id="df661-221">Object</span></span> | <span data-ttu-id="df661-222">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="df661-222">{"one": "a", "two": "b"}</span></span> |

<span data-ttu-id="df661-223">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-223">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<span data-ttu-id="df661-224">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-224">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/base64.json
```

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="df661-225">concat</span><span class="sxs-lookup"><span data-stu-id="df661-225">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="df661-226">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span><span class="sxs-lookup"><span data-stu-id="df661-226">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-227">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-227">Parameters</span></span>

| <span data-ttu-id="df661-228">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-228">Parameter</span></span> | <span data-ttu-id="df661-229">Required</span><span class="sxs-lookup"><span data-stu-id="df661-229">Required</span></span> | <span data-ttu-id="df661-230">Type</span><span class="sxs-lookup"><span data-stu-id="df661-230">Type</span></span> | <span data-ttu-id="df661-231">Description</span><span class="sxs-lookup"><span data-stu-id="df661-231">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-232">arg1</span><span class="sxs-lookup"><span data-stu-id="df661-232">arg1</span></span> |<span data-ttu-id="df661-233">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-233">Yes</span></span> |<span data-ttu-id="df661-234">string or array</span><span class="sxs-lookup"><span data-stu-id="df661-234">string or array</span></span> |<span data-ttu-id="df661-235">The first value for concatenation.</span><span class="sxs-lookup"><span data-stu-id="df661-235">The first value for concatenation.</span></span> |
| <span data-ttu-id="df661-236">additional arguments</span><span class="sxs-lookup"><span data-stu-id="df661-236">additional arguments</span></span> |<span data-ttu-id="df661-237">No</span><span class="sxs-lookup"><span data-stu-id="df661-237">No</span></span> |<span data-ttu-id="df661-238">string</span><span class="sxs-lookup"><span data-stu-id="df661-238">string</span></span> |<span data-ttu-id="df661-239">Additional values in sequential order for concatenation.</span><span class="sxs-lookup"><span data-stu-id="df661-239">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-240">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-240">Return value</span></span>
<span data-ttu-id="df661-241">A string or array of concatenated values.</span><span class="sxs-lookup"><span data-stu-id="df661-241">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-242">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-242">Examples</span></span>

<span data-ttu-id="df661-243">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-string.json) shows how to combine two string values and return a concatenated string.</span><span class="sxs-lookup"><span data-stu-id="df661-243">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-string.json) shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="df661-244">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-244">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-245">Name</span><span class="sxs-lookup"><span data-stu-id="df661-245">Name</span></span> | <span data-ttu-id="df661-246">Type</span><span class="sxs-lookup"><span data-stu-id="df661-246">Type</span></span> | <span data-ttu-id="df661-247">Value</span><span class="sxs-lookup"><span data-stu-id="df661-247">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-248">concatOutput</span><span class="sxs-lookup"><span data-stu-id="df661-248">concatOutput</span></span> | <span data-ttu-id="df661-249">String</span><span class="sxs-lookup"><span data-stu-id="df661-249">String</span></span> | <span data-ttu-id="df661-250">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="df661-250">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="df661-251">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-251">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-string.json
```

<span data-ttu-id="df661-252">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-252">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-string.json
```

<span data-ttu-id="df661-253">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-array.json) shows how to combine two arrays.</span><span class="sxs-lookup"><span data-stu-id="df661-253">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/concat-array.json) shows how to combine two arrays.</span></span>

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

<span data-ttu-id="df661-254">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-254">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-255">Name</span><span class="sxs-lookup"><span data-stu-id="df661-255">Name</span></span> | <span data-ttu-id="df661-256">Type</span><span class="sxs-lookup"><span data-stu-id="df661-256">Type</span></span> | <span data-ttu-id="df661-257">Value</span><span class="sxs-lookup"><span data-stu-id="df661-257">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-258">return</span><span class="sxs-lookup"><span data-stu-id="df661-258">return</span></span> | <span data-ttu-id="df661-259">Array</span><span class="sxs-lookup"><span data-stu-id="df661-259">Array</span></span> | <span data-ttu-id="df661-260">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="df661-260">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="df661-261">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-261">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-array.json
```

<span data-ttu-id="df661-262">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-262">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/concat-array.json
```

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="df661-263">contains</span><span class="sxs-lookup"><span data-stu-id="df661-263">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="df661-264">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span><span class="sxs-lookup"><span data-stu-id="df661-264">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-265">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-265">Parameters</span></span>

| <span data-ttu-id="df661-266">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-266">Parameter</span></span> | <span data-ttu-id="df661-267">Required</span><span class="sxs-lookup"><span data-stu-id="df661-267">Required</span></span> | <span data-ttu-id="df661-268">Type</span><span class="sxs-lookup"><span data-stu-id="df661-268">Type</span></span> | <span data-ttu-id="df661-269">Description</span><span class="sxs-lookup"><span data-stu-id="df661-269">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-270">container</span><span class="sxs-lookup"><span data-stu-id="df661-270">container</span></span> |<span data-ttu-id="df661-271">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-271">Yes</span></span> |<span data-ttu-id="df661-272">array, object, or string</span><span class="sxs-lookup"><span data-stu-id="df661-272">array, object, or string</span></span> |<span data-ttu-id="df661-273">The value that contains the value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-273">The value that contains the value to find.</span></span> |
| <span data-ttu-id="df661-274">itemToFind</span><span class="sxs-lookup"><span data-stu-id="df661-274">itemToFind</span></span> |<span data-ttu-id="df661-275">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-275">Yes</span></span> |<span data-ttu-id="df661-276">string or int</span><span class="sxs-lookup"><span data-stu-id="df661-276">string or int</span></span> |<span data-ttu-id="df661-277">The value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-277">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-278">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-278">Return value</span></span>

<span data-ttu-id="df661-279">**True** if the item is found; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="df661-279">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-280">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-280">Examples</span></span>

<span data-ttu-id="df661-281">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/contains.json) shows how to use contains with different types:</span><span class="sxs-lookup"><span data-stu-id="df661-281">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/contains.json) shows how to use contains with different types:</span></span>

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

<span data-ttu-id="df661-282">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-282">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-283">Name</span><span class="sxs-lookup"><span data-stu-id="df661-283">Name</span></span> | <span data-ttu-id="df661-284">Type</span><span class="sxs-lookup"><span data-stu-id="df661-284">Type</span></span> | <span data-ttu-id="df661-285">Value</span><span class="sxs-lookup"><span data-stu-id="df661-285">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-286">stringTrue</span><span class="sxs-lookup"><span data-stu-id="df661-286">stringTrue</span></span> | <span data-ttu-id="df661-287">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-287">Bool</span></span> | <span data-ttu-id="df661-288">True</span><span class="sxs-lookup"><span data-stu-id="df661-288">True</span></span> |
| <span data-ttu-id="df661-289">stringFalse</span><span class="sxs-lookup"><span data-stu-id="df661-289">stringFalse</span></span> | <span data-ttu-id="df661-290">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-290">Bool</span></span> | <span data-ttu-id="df661-291">False</span><span class="sxs-lookup"><span data-stu-id="df661-291">False</span></span> |
| <span data-ttu-id="df661-292">objectTrue</span><span class="sxs-lookup"><span data-stu-id="df661-292">objectTrue</span></span> | <span data-ttu-id="df661-293">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-293">Bool</span></span> | <span data-ttu-id="df661-294">True</span><span class="sxs-lookup"><span data-stu-id="df661-294">True</span></span> |
| <span data-ttu-id="df661-295">objectFalse</span><span class="sxs-lookup"><span data-stu-id="df661-295">objectFalse</span></span> | <span data-ttu-id="df661-296">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-296">Bool</span></span> | <span data-ttu-id="df661-297">False</span><span class="sxs-lookup"><span data-stu-id="df661-297">False</span></span> |
| <span data-ttu-id="df661-298">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="df661-298">arrayTrue</span></span> | <span data-ttu-id="df661-299">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-299">Bool</span></span> | <span data-ttu-id="df661-300">True</span><span class="sxs-lookup"><span data-stu-id="df661-300">True</span></span> |
| <span data-ttu-id="df661-301">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="df661-301">arrayFalse</span></span> | <span data-ttu-id="df661-302">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-302">Bool</span></span> | <span data-ttu-id="df661-303">False</span><span class="sxs-lookup"><span data-stu-id="df661-303">False</span></span> |

<span data-ttu-id="df661-304">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-304">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/contains.json
```

<span data-ttu-id="df661-305">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-305">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/contains.json
```

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="df661-306">dataUri</span><span class="sxs-lookup"><span data-stu-id="df661-306">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="df661-307">Converts a value to a data URI.</span><span class="sxs-lookup"><span data-stu-id="df661-307">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-308">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-308">Parameters</span></span>

| <span data-ttu-id="df661-309">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-309">Parameter</span></span> | <span data-ttu-id="df661-310">Required</span><span class="sxs-lookup"><span data-stu-id="df661-310">Required</span></span> | <span data-ttu-id="df661-311">Type</span><span class="sxs-lookup"><span data-stu-id="df661-311">Type</span></span> | <span data-ttu-id="df661-312">Description</span><span class="sxs-lookup"><span data-stu-id="df661-312">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-313">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="df661-313">stringToConvert</span></span> |<span data-ttu-id="df661-314">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-314">Yes</span></span> |<span data-ttu-id="df661-315">string</span><span class="sxs-lookup"><span data-stu-id="df661-315">string</span></span> |<span data-ttu-id="df661-316">The value to convert to a data URI.</span><span class="sxs-lookup"><span data-stu-id="df661-316">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-317">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-317">Return value</span></span>

<span data-ttu-id="df661-318">A string formatted as a data URI.</span><span class="sxs-lookup"><span data-stu-id="df661-318">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-319">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-319">Examples</span></span>

<span data-ttu-id="df661-320">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json) converts a value to a data URI, and converts a data URI to a string:</span><span class="sxs-lookup"><span data-stu-id="df661-320">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json) converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="df661-321">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-321">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-322">Name</span><span class="sxs-lookup"><span data-stu-id="df661-322">Name</span></span> | <span data-ttu-id="df661-323">Type</span><span class="sxs-lookup"><span data-stu-id="df661-323">Type</span></span> | <span data-ttu-id="df661-324">Value</span><span class="sxs-lookup"><span data-stu-id="df661-324">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-325">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="df661-325">dataUriOutput</span></span> | <span data-ttu-id="df661-326">String</span><span class="sxs-lookup"><span data-stu-id="df661-326">String</span></span> | <span data-ttu-id="df661-327">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="df661-327">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="df661-328">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-328">toStringOutput</span></span> | <span data-ttu-id="df661-329">String</span><span class="sxs-lookup"><span data-stu-id="df661-329">String</span></span> | <span data-ttu-id="df661-330">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="df661-330">Hello, World!</span></span> |

<span data-ttu-id="df661-331">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-331">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/datauri.json
```

<span data-ttu-id="df661-332">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-332">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/datauri.json
```

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="df661-333">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="df661-333">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="df661-334">Converts a data URI formatted value to a string.</span><span class="sxs-lookup"><span data-stu-id="df661-334">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-335">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-335">Parameters</span></span>

| <span data-ttu-id="df661-336">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-336">Parameter</span></span> | <span data-ttu-id="df661-337">Required</span><span class="sxs-lookup"><span data-stu-id="df661-337">Required</span></span> | <span data-ttu-id="df661-338">Type</span><span class="sxs-lookup"><span data-stu-id="df661-338">Type</span></span> | <span data-ttu-id="df661-339">Description</span><span class="sxs-lookup"><span data-stu-id="df661-339">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-340">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="df661-340">dataUriToConvert</span></span> |<span data-ttu-id="df661-341">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-341">Yes</span></span> |<span data-ttu-id="df661-342">string</span><span class="sxs-lookup"><span data-stu-id="df661-342">string</span></span> |<span data-ttu-id="df661-343">The data URI value to convert.</span><span class="sxs-lookup"><span data-stu-id="df661-343">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-344">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-344">Return value</span></span>

<span data-ttu-id="df661-345">A string containing the converted value.</span><span class="sxs-lookup"><span data-stu-id="df661-345">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-346">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-346">Examples</span></span>

<span data-ttu-id="df661-347">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json) converts a value to a data URI, and converts a data URI to a string:</span><span class="sxs-lookup"><span data-stu-id="df661-347">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/datauri.json) converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="df661-348">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-348">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-349">Name</span><span class="sxs-lookup"><span data-stu-id="df661-349">Name</span></span> | <span data-ttu-id="df661-350">Type</span><span class="sxs-lookup"><span data-stu-id="df661-350">Type</span></span> | <span data-ttu-id="df661-351">Value</span><span class="sxs-lookup"><span data-stu-id="df661-351">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-352">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="df661-352">dataUriOutput</span></span> | <span data-ttu-id="df661-353">String</span><span class="sxs-lookup"><span data-stu-id="df661-353">String</span></span> | <span data-ttu-id="df661-354">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="df661-354">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="df661-355">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-355">toStringOutput</span></span> | <span data-ttu-id="df661-356">String</span><span class="sxs-lookup"><span data-stu-id="df661-356">String</span></span> | <span data-ttu-id="df661-357">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="df661-357">Hello, World!</span></span> |

<span data-ttu-id="df661-358">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-358">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/datauri.json
```

<span data-ttu-id="df661-359">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-359">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/datauri.json
```

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="df661-360">empty</span><span class="sxs-lookup"><span data-stu-id="df661-360">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="df661-361">Determines if an array, object, or string is empty.</span><span class="sxs-lookup"><span data-stu-id="df661-361">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-362">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-362">Parameters</span></span>

| <span data-ttu-id="df661-363">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-363">Parameter</span></span> | <span data-ttu-id="df661-364">Required</span><span class="sxs-lookup"><span data-stu-id="df661-364">Required</span></span> | <span data-ttu-id="df661-365">Type</span><span class="sxs-lookup"><span data-stu-id="df661-365">Type</span></span> | <span data-ttu-id="df661-366">Description</span><span class="sxs-lookup"><span data-stu-id="df661-366">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-367">itemToTest</span><span class="sxs-lookup"><span data-stu-id="df661-367">itemToTest</span></span> |<span data-ttu-id="df661-368">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-368">Yes</span></span> |<span data-ttu-id="df661-369">array, object, or string</span><span class="sxs-lookup"><span data-stu-id="df661-369">array, object, or string</span></span> |<span data-ttu-id="df661-370">The value to check if it is empty.</span><span class="sxs-lookup"><span data-stu-id="df661-370">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-371">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-371">Return value</span></span>

<span data-ttu-id="df661-372">Returns **True** if the value is empty; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="df661-372">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-373">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-373">Examples</span></span>

<span data-ttu-id="df661-374">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/empty.json) checks whether an array, object, and string are empty.</span><span class="sxs-lookup"><span data-stu-id="df661-374">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/empty.json) checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="df661-375">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-375">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-376">Name</span><span class="sxs-lookup"><span data-stu-id="df661-376">Name</span></span> | <span data-ttu-id="df661-377">Type</span><span class="sxs-lookup"><span data-stu-id="df661-377">Type</span></span> | <span data-ttu-id="df661-378">Value</span><span class="sxs-lookup"><span data-stu-id="df661-378">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-379">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="df661-379">arrayEmpty</span></span> | <span data-ttu-id="df661-380">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-380">Bool</span></span> | <span data-ttu-id="df661-381">True</span><span class="sxs-lookup"><span data-stu-id="df661-381">True</span></span> |
| <span data-ttu-id="df661-382">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="df661-382">objectEmpty</span></span> | <span data-ttu-id="df661-383">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-383">Bool</span></span> | <span data-ttu-id="df661-384">True</span><span class="sxs-lookup"><span data-stu-id="df661-384">True</span></span> |
| <span data-ttu-id="df661-385">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="df661-385">stringEmpty</span></span> | <span data-ttu-id="df661-386">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-386">Bool</span></span> | <span data-ttu-id="df661-387">True</span><span class="sxs-lookup"><span data-stu-id="df661-387">True</span></span> |

<span data-ttu-id="df661-388">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-388">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/empty.json
```

<span data-ttu-id="df661-389">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-389">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/empty.json
```

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="df661-390">endsWith</span><span class="sxs-lookup"><span data-stu-id="df661-390">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="df661-391">Determines whether a string ends with a value.</span><span class="sxs-lookup"><span data-stu-id="df661-391">Determines whether a string ends with a value.</span></span> <span data-ttu-id="df661-392">The comparison is case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="df661-392">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-393">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-393">Parameters</span></span>

| <span data-ttu-id="df661-394">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-394">Parameter</span></span> | <span data-ttu-id="df661-395">Required</span><span class="sxs-lookup"><span data-stu-id="df661-395">Required</span></span> | <span data-ttu-id="df661-396">Type</span><span class="sxs-lookup"><span data-stu-id="df661-396">Type</span></span> | <span data-ttu-id="df661-397">Description</span><span class="sxs-lookup"><span data-stu-id="df661-397">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-398">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="df661-398">stringToSearch</span></span> |<span data-ttu-id="df661-399">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-399">Yes</span></span> |<span data-ttu-id="df661-400">string</span><span class="sxs-lookup"><span data-stu-id="df661-400">string</span></span> |<span data-ttu-id="df661-401">The value that contains the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-401">The value that contains the item to find.</span></span> |
| <span data-ttu-id="df661-402">stringToFind</span><span class="sxs-lookup"><span data-stu-id="df661-402">stringToFind</span></span> |<span data-ttu-id="df661-403">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-403">Yes</span></span> |<span data-ttu-id="df661-404">string</span><span class="sxs-lookup"><span data-stu-id="df661-404">string</span></span> |<span data-ttu-id="df661-405">The value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-405">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-406">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-406">Return value</span></span>

<span data-ttu-id="df661-407">**True** if the last character or characters of the string match the value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="df661-407">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-408">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-408">Examples</span></span>

<span data-ttu-id="df661-409">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json) shows how to use the startsWith and endsWith functions:</span><span class="sxs-lookup"><span data-stu-id="df661-409">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json) shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="df661-410">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-410">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-411">Name</span><span class="sxs-lookup"><span data-stu-id="df661-411">Name</span></span> | <span data-ttu-id="df661-412">Type</span><span class="sxs-lookup"><span data-stu-id="df661-412">Type</span></span> | <span data-ttu-id="df661-413">Value</span><span class="sxs-lookup"><span data-stu-id="df661-413">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-414">startsTrue</span><span class="sxs-lookup"><span data-stu-id="df661-414">startsTrue</span></span> | <span data-ttu-id="df661-415">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-415">Bool</span></span> | <span data-ttu-id="df661-416">True</span><span class="sxs-lookup"><span data-stu-id="df661-416">True</span></span> |
| <span data-ttu-id="df661-417">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="df661-417">startsCapTrue</span></span> | <span data-ttu-id="df661-418">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-418">Bool</span></span> | <span data-ttu-id="df661-419">True</span><span class="sxs-lookup"><span data-stu-id="df661-419">True</span></span> |
| <span data-ttu-id="df661-420">startsFalse</span><span class="sxs-lookup"><span data-stu-id="df661-420">startsFalse</span></span> | <span data-ttu-id="df661-421">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-421">Bool</span></span> | <span data-ttu-id="df661-422">False</span><span class="sxs-lookup"><span data-stu-id="df661-422">False</span></span> |
| <span data-ttu-id="df661-423">endsTrue</span><span class="sxs-lookup"><span data-stu-id="df661-423">endsTrue</span></span> | <span data-ttu-id="df661-424">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-424">Bool</span></span> | <span data-ttu-id="df661-425">True</span><span class="sxs-lookup"><span data-stu-id="df661-425">True</span></span> |
| <span data-ttu-id="df661-426">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="df661-426">endsCapTrue</span></span> | <span data-ttu-id="df661-427">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-427">Bool</span></span> | <span data-ttu-id="df661-428">True</span><span class="sxs-lookup"><span data-stu-id="df661-428">True</span></span> |
| <span data-ttu-id="df661-429">endsFalse</span><span class="sxs-lookup"><span data-stu-id="df661-429">endsFalse</span></span> | <span data-ttu-id="df661-430">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-430">Bool</span></span> | <span data-ttu-id="df661-431">False</span><span class="sxs-lookup"><span data-stu-id="df661-431">False</span></span> |

<span data-ttu-id="df661-432">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-432">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/startsendswith.json
```

<span data-ttu-id="df661-433">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-433">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/startsendswith.json
```

<a id="first" />

## <a name="first"></a><span data-ttu-id="df661-434">first</span><span class="sxs-lookup"><span data-stu-id="df661-434">first</span></span>
`first(arg1)`

<span data-ttu-id="df661-435">Returns the first character of the string, or first element of the array.</span><span class="sxs-lookup"><span data-stu-id="df661-435">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-436">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-436">Parameters</span></span>

| <span data-ttu-id="df661-437">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-437">Parameter</span></span> | <span data-ttu-id="df661-438">Required</span><span class="sxs-lookup"><span data-stu-id="df661-438">Required</span></span> | <span data-ttu-id="df661-439">Type</span><span class="sxs-lookup"><span data-stu-id="df661-439">Type</span></span> | <span data-ttu-id="df661-440">Description</span><span class="sxs-lookup"><span data-stu-id="df661-440">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-441">arg1</span><span class="sxs-lookup"><span data-stu-id="df661-441">arg1</span></span> |<span data-ttu-id="df661-442">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-442">Yes</span></span> |<span data-ttu-id="df661-443">array or string</span><span class="sxs-lookup"><span data-stu-id="df661-443">array or string</span></span> |<span data-ttu-id="df661-444">The value to retrieve the first element or character.</span><span class="sxs-lookup"><span data-stu-id="df661-444">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-445">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-445">Return value</span></span>

<span data-ttu-id="df661-446">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span><span class="sxs-lookup"><span data-stu-id="df661-446">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-447">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-447">Examples</span></span>

<span data-ttu-id="df661-448">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/first.json) shows how to use the first function with an array and string.</span><span class="sxs-lookup"><span data-stu-id="df661-448">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/first.json) shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="df661-449">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-449">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-450">Name</span><span class="sxs-lookup"><span data-stu-id="df661-450">Name</span></span> | <span data-ttu-id="df661-451">Type</span><span class="sxs-lookup"><span data-stu-id="df661-451">Type</span></span> | <span data-ttu-id="df661-452">Value</span><span class="sxs-lookup"><span data-stu-id="df661-452">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-453">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="df661-453">arrayOutput</span></span> | <span data-ttu-id="df661-454">String</span><span class="sxs-lookup"><span data-stu-id="df661-454">String</span></span> | <span data-ttu-id="df661-455">one</span><span class="sxs-lookup"><span data-stu-id="df661-455">one</span></span> |
| <span data-ttu-id="df661-456">stringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-456">stringOutput</span></span> | <span data-ttu-id="df661-457">String</span><span class="sxs-lookup"><span data-stu-id="df661-457">String</span></span> | <span data-ttu-id="df661-458">O</span><span class="sxs-lookup"><span data-stu-id="df661-458">O</span></span> |

<span data-ttu-id="df661-459">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-459">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/first.json
```

<span data-ttu-id="df661-460">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-460">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/first.json
```

## <a name="guid"></a><span data-ttu-id="df661-461">guid</span><span class="sxs-lookup"><span data-stu-id="df661-461">guid</span></span>

`guid (baseString, ...)`

<span data-ttu-id="df661-462">Creates a value in the format of a globally unique identifier based on the values provided as parameters.</span><span class="sxs-lookup"><span data-stu-id="df661-462">Creates a value in the format of a globally unique identifier based on the values provided as parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-463">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-463">Parameters</span></span>

| <span data-ttu-id="df661-464">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-464">Parameter</span></span> | <span data-ttu-id="df661-465">Required</span><span class="sxs-lookup"><span data-stu-id="df661-465">Required</span></span> | <span data-ttu-id="df661-466">Type</span><span class="sxs-lookup"><span data-stu-id="df661-466">Type</span></span> | <span data-ttu-id="df661-467">Description</span><span class="sxs-lookup"><span data-stu-id="df661-467">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-468">baseString</span><span class="sxs-lookup"><span data-stu-id="df661-468">baseString</span></span> |<span data-ttu-id="df661-469">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-469">Yes</span></span> |<span data-ttu-id="df661-470">string</span><span class="sxs-lookup"><span data-stu-id="df661-470">string</span></span> |<span data-ttu-id="df661-471">The value used in the hash function to create the GUID.</span><span class="sxs-lookup"><span data-stu-id="df661-471">The value used in the hash function to create the GUID.</span></span> |
| <span data-ttu-id="df661-472">additional parameters as needed</span><span class="sxs-lookup"><span data-stu-id="df661-472">additional parameters as needed</span></span> |<span data-ttu-id="df661-473">No</span><span class="sxs-lookup"><span data-stu-id="df661-473">No</span></span> |<span data-ttu-id="df661-474">string</span><span class="sxs-lookup"><span data-stu-id="df661-474">string</span></span> |<span data-ttu-id="df661-475">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span><span class="sxs-lookup"><span data-stu-id="df661-475">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="df661-476">Remarks</span><span class="sxs-lookup"><span data-stu-id="df661-476">Remarks</span></span>

<span data-ttu-id="df661-477">This function is helpful when you need to create a value in the format of a globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="df661-477">This function is helpful when you need to create a value in the format of a globally unique identifier.</span></span> <span data-ttu-id="df661-478">You provide parameter values that limit the scope of uniqueness for the result.</span><span class="sxs-lookup"><span data-stu-id="df661-478">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="df661-479">You can specify whether the name is unique down to subscription, resource group, or deployment.</span><span class="sxs-lookup"><span data-stu-id="df661-479">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span>

<span data-ttu-id="df661-480">The returned value is not a random string, but rather the result of a hash function.</span><span class="sxs-lookup"><span data-stu-id="df661-480">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="df661-481">The returned value is 36 characters long.</span><span class="sxs-lookup"><span data-stu-id="df661-481">The returned value is 36 characters long.</span></span> <span data-ttu-id="df661-482">It is not globally unique.</span><span class="sxs-lookup"><span data-stu-id="df661-482">It is not globally unique.</span></span>

<span data-ttu-id="df661-483">The following examples show how to use guid to create a unique value for commonly used levels.</span><span class="sxs-lookup"><span data-stu-id="df661-483">The following examples show how to use guid to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="df661-484">Unique scoped to subscription</span><span class="sxs-lookup"><span data-stu-id="df661-484">Unique scoped to subscription</span></span>

```json
"[guid(subscription().subscriptionId)]"
```

<span data-ttu-id="df661-485">Unique scoped to resource group</span><span class="sxs-lookup"><span data-stu-id="df661-485">Unique scoped to resource group</span></span>

```json
"[guid(resourceGroup().id)]"
```

<span data-ttu-id="df661-486">Unique scoped to deployment for a resource group</span><span class="sxs-lookup"><span data-stu-id="df661-486">Unique scoped to deployment for a resource group</span></span>

```json
"[guid(resourceGroup().id, deployment().name)]"
```

### <a name="return-value"></a><span data-ttu-id="df661-487">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-487">Return value</span></span>

<span data-ttu-id="df661-488">A string containing 36 characters in the format of a globally unique identifier.</span><span class="sxs-lookup"><span data-stu-id="df661-488">A string containing 36 characters in the format of a globally unique identifier.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-489">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-489">Examples</span></span>

<span data-ttu-id="df661-490">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/guid.json) returns results from guid:</span><span class="sxs-lookup"><span data-stu-id="df661-490">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/guid.json) returns results from guid:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {},
    "resources": [],
    "outputs": {
        "guidPerSubscription": {
            "value": "[guid(subscription().subscriptionId)]",
            "type": "string"
        },
        "guidPerResourceGroup": {
            "value": "[guid(resourceGroup().id)]",
            "type": "string"
        },
        "guidPerDeployment": {
            "value": "[guid(resourceGroup().id, deployment().name)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="df661-491">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-491">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/guid.json
```

<span data-ttu-id="df661-492">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-492">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/guid.json
```

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="df661-493">indexOf</span><span class="sxs-lookup"><span data-stu-id="df661-493">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="df661-494">Returns the first position of a value within a string.</span><span class="sxs-lookup"><span data-stu-id="df661-494">Returns the first position of a value within a string.</span></span> <span data-ttu-id="df661-495">The comparison is case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="df661-495">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-496">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-496">Parameters</span></span>

| <span data-ttu-id="df661-497">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-497">Parameter</span></span> | <span data-ttu-id="df661-498">Required</span><span class="sxs-lookup"><span data-stu-id="df661-498">Required</span></span> | <span data-ttu-id="df661-499">Type</span><span class="sxs-lookup"><span data-stu-id="df661-499">Type</span></span> | <span data-ttu-id="df661-500">Description</span><span class="sxs-lookup"><span data-stu-id="df661-500">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-501">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="df661-501">stringToSearch</span></span> |<span data-ttu-id="df661-502">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-502">Yes</span></span> |<span data-ttu-id="df661-503">string</span><span class="sxs-lookup"><span data-stu-id="df661-503">string</span></span> |<span data-ttu-id="df661-504">The value that contains the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-504">The value that contains the item to find.</span></span> |
| <span data-ttu-id="df661-505">stringToFind</span><span class="sxs-lookup"><span data-stu-id="df661-505">stringToFind</span></span> |<span data-ttu-id="df661-506">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-506">Yes</span></span> |<span data-ttu-id="df661-507">string</span><span class="sxs-lookup"><span data-stu-id="df661-507">string</span></span> |<span data-ttu-id="df661-508">The value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-508">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-509">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-509">Return value</span></span>

<span data-ttu-id="df661-510">An integer that represents the position of the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-510">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="df661-511">The value is zero-based.</span><span class="sxs-lookup"><span data-stu-id="df661-511">The value is zero-based.</span></span> <span data-ttu-id="df661-512">If the item is not found, -1 is returned.</span><span class="sxs-lookup"><span data-stu-id="df661-512">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-513">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-513">Examples</span></span>

<span data-ttu-id="df661-514">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json) shows how to use the indexOf and lastIndexOf functions:</span><span class="sxs-lookup"><span data-stu-id="df661-514">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json) shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="df661-515">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-515">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-516">Name</span><span class="sxs-lookup"><span data-stu-id="df661-516">Name</span></span> | <span data-ttu-id="df661-517">Type</span><span class="sxs-lookup"><span data-stu-id="df661-517">Type</span></span> | <span data-ttu-id="df661-518">Value</span><span class="sxs-lookup"><span data-stu-id="df661-518">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-519">firstT</span><span class="sxs-lookup"><span data-stu-id="df661-519">firstT</span></span> | <span data-ttu-id="df661-520">Int</span><span class="sxs-lookup"><span data-stu-id="df661-520">Int</span></span> | <span data-ttu-id="df661-521">0</span><span class="sxs-lookup"><span data-stu-id="df661-521">0</span></span> |
| <span data-ttu-id="df661-522">lastT</span><span class="sxs-lookup"><span data-stu-id="df661-522">lastT</span></span> | <span data-ttu-id="df661-523">Int</span><span class="sxs-lookup"><span data-stu-id="df661-523">Int</span></span> | <span data-ttu-id="df661-524">3</span><span class="sxs-lookup"><span data-stu-id="df661-524">3</span></span> |
| <span data-ttu-id="df661-525">firstString</span><span class="sxs-lookup"><span data-stu-id="df661-525">firstString</span></span> | <span data-ttu-id="df661-526">Int</span><span class="sxs-lookup"><span data-stu-id="df661-526">Int</span></span> | <span data-ttu-id="df661-527">2</span><span class="sxs-lookup"><span data-stu-id="df661-527">2</span></span> |
| <span data-ttu-id="df661-528">lastString</span><span class="sxs-lookup"><span data-stu-id="df661-528">lastString</span></span> | <span data-ttu-id="df661-529">Int</span><span class="sxs-lookup"><span data-stu-id="df661-529">Int</span></span> | <span data-ttu-id="df661-530">0</span><span class="sxs-lookup"><span data-stu-id="df661-530">0</span></span> |
| <span data-ttu-id="df661-531">notFound</span><span class="sxs-lookup"><span data-stu-id="df661-531">notFound</span></span> | <span data-ttu-id="df661-532">Int</span><span class="sxs-lookup"><span data-stu-id="df661-532">Int</span></span> | <span data-ttu-id="df661-533">-1</span><span class="sxs-lookup"><span data-stu-id="df661-533">-1</span></span> |

<span data-ttu-id="df661-534">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-534">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/indexof.json
```

<span data-ttu-id="df661-535">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-535">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/indexof.json
```

<a id="last" />

## <a name="last"></a><span data-ttu-id="df661-536">last</span><span class="sxs-lookup"><span data-stu-id="df661-536">last</span></span>
`last (arg1)`

<span data-ttu-id="df661-537">Returns last character of the string, or the last element of the array.</span><span class="sxs-lookup"><span data-stu-id="df661-537">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-538">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-538">Parameters</span></span>

| <span data-ttu-id="df661-539">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-539">Parameter</span></span> | <span data-ttu-id="df661-540">Required</span><span class="sxs-lookup"><span data-stu-id="df661-540">Required</span></span> | <span data-ttu-id="df661-541">Type</span><span class="sxs-lookup"><span data-stu-id="df661-541">Type</span></span> | <span data-ttu-id="df661-542">Description</span><span class="sxs-lookup"><span data-stu-id="df661-542">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-543">arg1</span><span class="sxs-lookup"><span data-stu-id="df661-543">arg1</span></span> |<span data-ttu-id="df661-544">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-544">Yes</span></span> |<span data-ttu-id="df661-545">array or string</span><span class="sxs-lookup"><span data-stu-id="df661-545">array or string</span></span> |<span data-ttu-id="df661-546">The value to retrieve the last element or character.</span><span class="sxs-lookup"><span data-stu-id="df661-546">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-547">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-547">Return value</span></span>

<span data-ttu-id="df661-548">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span><span class="sxs-lookup"><span data-stu-id="df661-548">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-549">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-549">Examples</span></span>

<span data-ttu-id="df661-550">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/last.json) shows how to use the last function with an array and string.</span><span class="sxs-lookup"><span data-stu-id="df661-550">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/last.json) shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="df661-551">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-551">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-552">Name</span><span class="sxs-lookup"><span data-stu-id="df661-552">Name</span></span> | <span data-ttu-id="df661-553">Type</span><span class="sxs-lookup"><span data-stu-id="df661-553">Type</span></span> | <span data-ttu-id="df661-554">Value</span><span class="sxs-lookup"><span data-stu-id="df661-554">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-555">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="df661-555">arrayOutput</span></span> | <span data-ttu-id="df661-556">String</span><span class="sxs-lookup"><span data-stu-id="df661-556">String</span></span> | <span data-ttu-id="df661-557">three</span><span class="sxs-lookup"><span data-stu-id="df661-557">three</span></span> |
| <span data-ttu-id="df661-558">stringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-558">stringOutput</span></span> | <span data-ttu-id="df661-559">String</span><span class="sxs-lookup"><span data-stu-id="df661-559">String</span></span> | <span data-ttu-id="df661-560">e</span><span class="sxs-lookup"><span data-stu-id="df661-560">e</span></span> |

<span data-ttu-id="df661-561">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-561">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/last.json
```

<span data-ttu-id="df661-562">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-562">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/last.json
```

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="df661-563">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="df661-563">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="df661-564">Returns the last position of a value within a string.</span><span class="sxs-lookup"><span data-stu-id="df661-564">Returns the last position of a value within a string.</span></span> <span data-ttu-id="df661-565">The comparison is case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="df661-565">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-566">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-566">Parameters</span></span>

| <span data-ttu-id="df661-567">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-567">Parameter</span></span> | <span data-ttu-id="df661-568">Required</span><span class="sxs-lookup"><span data-stu-id="df661-568">Required</span></span> | <span data-ttu-id="df661-569">Type</span><span class="sxs-lookup"><span data-stu-id="df661-569">Type</span></span> | <span data-ttu-id="df661-570">Description</span><span class="sxs-lookup"><span data-stu-id="df661-570">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-571">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="df661-571">stringToSearch</span></span> |<span data-ttu-id="df661-572">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-572">Yes</span></span> |<span data-ttu-id="df661-573">string</span><span class="sxs-lookup"><span data-stu-id="df661-573">string</span></span> |<span data-ttu-id="df661-574">The value that contains the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-574">The value that contains the item to find.</span></span> |
| <span data-ttu-id="df661-575">stringToFind</span><span class="sxs-lookup"><span data-stu-id="df661-575">stringToFind</span></span> |<span data-ttu-id="df661-576">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-576">Yes</span></span> |<span data-ttu-id="df661-577">string</span><span class="sxs-lookup"><span data-stu-id="df661-577">string</span></span> |<span data-ttu-id="df661-578">The value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-578">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-579">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-579">Return value</span></span>

<span data-ttu-id="df661-580">An integer that represents the last position of the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-580">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="df661-581">The value is zero-based.</span><span class="sxs-lookup"><span data-stu-id="df661-581">The value is zero-based.</span></span> <span data-ttu-id="df661-582">If the item is not found, -1 is returned.</span><span class="sxs-lookup"><span data-stu-id="df661-582">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-583">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-583">Examples</span></span>

<span data-ttu-id="df661-584">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json) shows how to use the indexOf and lastIndexOf functions:</span><span class="sxs-lookup"><span data-stu-id="df661-584">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/indexof.json) shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="df661-585">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-585">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-586">Name</span><span class="sxs-lookup"><span data-stu-id="df661-586">Name</span></span> | <span data-ttu-id="df661-587">Type</span><span class="sxs-lookup"><span data-stu-id="df661-587">Type</span></span> | <span data-ttu-id="df661-588">Value</span><span class="sxs-lookup"><span data-stu-id="df661-588">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-589">firstT</span><span class="sxs-lookup"><span data-stu-id="df661-589">firstT</span></span> | <span data-ttu-id="df661-590">Int</span><span class="sxs-lookup"><span data-stu-id="df661-590">Int</span></span> | <span data-ttu-id="df661-591">0</span><span class="sxs-lookup"><span data-stu-id="df661-591">0</span></span> |
| <span data-ttu-id="df661-592">lastT</span><span class="sxs-lookup"><span data-stu-id="df661-592">lastT</span></span> | <span data-ttu-id="df661-593">Int</span><span class="sxs-lookup"><span data-stu-id="df661-593">Int</span></span> | <span data-ttu-id="df661-594">3</span><span class="sxs-lookup"><span data-stu-id="df661-594">3</span></span> |
| <span data-ttu-id="df661-595">firstString</span><span class="sxs-lookup"><span data-stu-id="df661-595">firstString</span></span> | <span data-ttu-id="df661-596">Int</span><span class="sxs-lookup"><span data-stu-id="df661-596">Int</span></span> | <span data-ttu-id="df661-597">2</span><span class="sxs-lookup"><span data-stu-id="df661-597">2</span></span> |
| <span data-ttu-id="df661-598">lastString</span><span class="sxs-lookup"><span data-stu-id="df661-598">lastString</span></span> | <span data-ttu-id="df661-599">Int</span><span class="sxs-lookup"><span data-stu-id="df661-599">Int</span></span> | <span data-ttu-id="df661-600">0</span><span class="sxs-lookup"><span data-stu-id="df661-600">0</span></span> |
| <span data-ttu-id="df661-601">notFound</span><span class="sxs-lookup"><span data-stu-id="df661-601">notFound</span></span> | <span data-ttu-id="df661-602">Int</span><span class="sxs-lookup"><span data-stu-id="df661-602">Int</span></span> | <span data-ttu-id="df661-603">-1</span><span class="sxs-lookup"><span data-stu-id="df661-603">-1</span></span> |

<span data-ttu-id="df661-604">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-604">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/indexof.json
```

<span data-ttu-id="df661-605">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-605">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/indexof.json
```

<a id="length" />

## <a name="length"></a><span data-ttu-id="df661-606">length</span><span class="sxs-lookup"><span data-stu-id="df661-606">length</span></span>
`length(string)`

<span data-ttu-id="df661-607">Returns the number of characters in a string, or elements in an array.</span><span class="sxs-lookup"><span data-stu-id="df661-607">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-608">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-608">Parameters</span></span>

| <span data-ttu-id="df661-609">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-609">Parameter</span></span> | <span data-ttu-id="df661-610">Required</span><span class="sxs-lookup"><span data-stu-id="df661-610">Required</span></span> | <span data-ttu-id="df661-611">Type</span><span class="sxs-lookup"><span data-stu-id="df661-611">Type</span></span> | <span data-ttu-id="df661-612">Description</span><span class="sxs-lookup"><span data-stu-id="df661-612">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-613">arg1</span><span class="sxs-lookup"><span data-stu-id="df661-613">arg1</span></span> |<span data-ttu-id="df661-614">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-614">Yes</span></span> |<span data-ttu-id="df661-615">array or string</span><span class="sxs-lookup"><span data-stu-id="df661-615">array or string</span></span> |<span data-ttu-id="df661-616">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span><span class="sxs-lookup"><span data-stu-id="df661-616">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-617">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-617">Return value</span></span>

<span data-ttu-id="df661-618">An int.</span><span class="sxs-lookup"><span data-stu-id="df661-618">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="df661-619">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-619">Examples</span></span>

<span data-ttu-id="df661-620">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/length.json) shows how to use length with an array and string:</span><span class="sxs-lookup"><span data-stu-id="df661-620">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/length.json) shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="df661-621">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-621">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-622">Name</span><span class="sxs-lookup"><span data-stu-id="df661-622">Name</span></span> | <span data-ttu-id="df661-623">Type</span><span class="sxs-lookup"><span data-stu-id="df661-623">Type</span></span> | <span data-ttu-id="df661-624">Value</span><span class="sxs-lookup"><span data-stu-id="df661-624">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-625">arrayLength</span><span class="sxs-lookup"><span data-stu-id="df661-625">arrayLength</span></span> | <span data-ttu-id="df661-626">Int</span><span class="sxs-lookup"><span data-stu-id="df661-626">Int</span></span> | <span data-ttu-id="df661-627">3</span><span class="sxs-lookup"><span data-stu-id="df661-627">3</span></span> |
| <span data-ttu-id="df661-628">stringLength</span><span class="sxs-lookup"><span data-stu-id="df661-628">stringLength</span></span> | <span data-ttu-id="df661-629">Int</span><span class="sxs-lookup"><span data-stu-id="df661-629">Int</span></span> | <span data-ttu-id="df661-630">13</span><span class="sxs-lookup"><span data-stu-id="df661-630">13</span></span> |

<span data-ttu-id="df661-631">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-631">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/length.json
```

<span data-ttu-id="df661-632">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-632">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/length.json
```

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="df661-633">padLeft</span><span class="sxs-lookup"><span data-stu-id="df661-633">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="df661-634">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span><span class="sxs-lookup"><span data-stu-id="df661-634">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-635">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-635">Parameters</span></span>

| <span data-ttu-id="df661-636">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-636">Parameter</span></span> | <span data-ttu-id="df661-637">Required</span><span class="sxs-lookup"><span data-stu-id="df661-637">Required</span></span> | <span data-ttu-id="df661-638">Type</span><span class="sxs-lookup"><span data-stu-id="df661-638">Type</span></span> | <span data-ttu-id="df661-639">Description</span><span class="sxs-lookup"><span data-stu-id="df661-639">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-640">valueToPad</span><span class="sxs-lookup"><span data-stu-id="df661-640">valueToPad</span></span> |<span data-ttu-id="df661-641">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-641">Yes</span></span> |<span data-ttu-id="df661-642">string or int</span><span class="sxs-lookup"><span data-stu-id="df661-642">string or int</span></span> |<span data-ttu-id="df661-643">The value to right-align.</span><span class="sxs-lookup"><span data-stu-id="df661-643">The value to right-align.</span></span> |
| <span data-ttu-id="df661-644">totalLength</span><span class="sxs-lookup"><span data-stu-id="df661-644">totalLength</span></span> |<span data-ttu-id="df661-645">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-645">Yes</span></span> |<span data-ttu-id="df661-646">int</span><span class="sxs-lookup"><span data-stu-id="df661-646">int</span></span> |<span data-ttu-id="df661-647">The total number of characters in the returned string.</span><span class="sxs-lookup"><span data-stu-id="df661-647">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="df661-648">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="df661-648">paddingCharacter</span></span> |<span data-ttu-id="df661-649">No</span><span class="sxs-lookup"><span data-stu-id="df661-649">No</span></span> |<span data-ttu-id="df661-650">single character</span><span class="sxs-lookup"><span data-stu-id="df661-650">single character</span></span> |<span data-ttu-id="df661-651">The character to use for left-padding until the total length is reached.</span><span class="sxs-lookup"><span data-stu-id="df661-651">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="df661-652">The default value is a space.</span><span class="sxs-lookup"><span data-stu-id="df661-652">The default value is a space.</span></span> |

<span data-ttu-id="df661-653">If the original string is longer than the number of characters to pad, no characters are added.</span><span class="sxs-lookup"><span data-stu-id="df661-653">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="df661-654">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-654">Return value</span></span>

<span data-ttu-id="df661-655">A string with at least the number of specified characters.</span><span class="sxs-lookup"><span data-stu-id="df661-655">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-656">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-656">Examples</span></span>

<span data-ttu-id="df661-657">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/padleft.json) shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span><span class="sxs-lookup"><span data-stu-id="df661-657">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/padleft.json) shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="df661-658">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-658">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-659">Name</span><span class="sxs-lookup"><span data-stu-id="df661-659">Name</span></span> | <span data-ttu-id="df661-660">Type</span><span class="sxs-lookup"><span data-stu-id="df661-660">Type</span></span> | <span data-ttu-id="df661-661">Value</span><span class="sxs-lookup"><span data-stu-id="df661-661">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-662">stringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-662">stringOutput</span></span> | <span data-ttu-id="df661-663">String</span><span class="sxs-lookup"><span data-stu-id="df661-663">String</span></span> | <span data-ttu-id="df661-664">0000000123</span><span class="sxs-lookup"><span data-stu-id="df661-664">0000000123</span></span> |

<span data-ttu-id="df661-665">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-665">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/padleft.json
```

<span data-ttu-id="df661-666">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-666">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/padleft.json
```

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="df661-667">replace</span><span class="sxs-lookup"><span data-stu-id="df661-667">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="df661-668">Returns a new string with all instances of one string replaced by another string.</span><span class="sxs-lookup"><span data-stu-id="df661-668">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-669">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-669">Parameters</span></span>

| <span data-ttu-id="df661-670">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-670">Parameter</span></span> | <span data-ttu-id="df661-671">Required</span><span class="sxs-lookup"><span data-stu-id="df661-671">Required</span></span> | <span data-ttu-id="df661-672">Type</span><span class="sxs-lookup"><span data-stu-id="df661-672">Type</span></span> | <span data-ttu-id="df661-673">Description</span><span class="sxs-lookup"><span data-stu-id="df661-673">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-674">originalString</span><span class="sxs-lookup"><span data-stu-id="df661-674">originalString</span></span> |<span data-ttu-id="df661-675">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-675">Yes</span></span> |<span data-ttu-id="df661-676">string</span><span class="sxs-lookup"><span data-stu-id="df661-676">string</span></span> |<span data-ttu-id="df661-677">The value that has all instances of one string replaced by another string.</span><span class="sxs-lookup"><span data-stu-id="df661-677">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="df661-678">oldString</span><span class="sxs-lookup"><span data-stu-id="df661-678">oldString</span></span> |<span data-ttu-id="df661-679">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-679">Yes</span></span> |<span data-ttu-id="df661-680">string</span><span class="sxs-lookup"><span data-stu-id="df661-680">string</span></span> |<span data-ttu-id="df661-681">The string to be removed from the original string.</span><span class="sxs-lookup"><span data-stu-id="df661-681">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="df661-682">newString</span><span class="sxs-lookup"><span data-stu-id="df661-682">newString</span></span> |<span data-ttu-id="df661-683">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-683">Yes</span></span> |<span data-ttu-id="df661-684">string</span><span class="sxs-lookup"><span data-stu-id="df661-684">string</span></span> |<span data-ttu-id="df661-685">The string to add in place of the removed string.</span><span class="sxs-lookup"><span data-stu-id="df661-685">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-686">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-686">Return value</span></span>

<span data-ttu-id="df661-687">A string with the replaced characters.</span><span class="sxs-lookup"><span data-stu-id="df661-687">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-688">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-688">Examples</span></span>

<span data-ttu-id="df661-689">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/replace.json) shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span><span class="sxs-lookup"><span data-stu-id="df661-689">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/replace.json) shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="df661-690">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-690">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-691">Name</span><span class="sxs-lookup"><span data-stu-id="df661-691">Name</span></span> | <span data-ttu-id="df661-692">Type</span><span class="sxs-lookup"><span data-stu-id="df661-692">Type</span></span> | <span data-ttu-id="df661-693">Value</span><span class="sxs-lookup"><span data-stu-id="df661-693">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-694">firstOutput</span><span class="sxs-lookup"><span data-stu-id="df661-694">firstOutput</span></span> | <span data-ttu-id="df661-695">String</span><span class="sxs-lookup"><span data-stu-id="df661-695">String</span></span> | <span data-ttu-id="df661-696">1231231234</span><span class="sxs-lookup"><span data-stu-id="df661-696">1231231234</span></span> |
| <span data-ttu-id="df661-697">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="df661-697">secodeOutput</span></span> | <span data-ttu-id="df661-698">String</span><span class="sxs-lookup"><span data-stu-id="df661-698">String</span></span> | <span data-ttu-id="df661-699">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="df661-699">123-123-xxxx</span></span> |

<span data-ttu-id="df661-700">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-700">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/replace.json
```

<span data-ttu-id="df661-701">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-701">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/replace.json
```

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="df661-702">skip</span><span class="sxs-lookup"><span data-stu-id="df661-702">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="df661-703">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span><span class="sxs-lookup"><span data-stu-id="df661-703">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-704">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-704">Parameters</span></span>

| <span data-ttu-id="df661-705">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-705">Parameter</span></span> | <span data-ttu-id="df661-706">Required</span><span class="sxs-lookup"><span data-stu-id="df661-706">Required</span></span> | <span data-ttu-id="df661-707">Type</span><span class="sxs-lookup"><span data-stu-id="df661-707">Type</span></span> | <span data-ttu-id="df661-708">Description</span><span class="sxs-lookup"><span data-stu-id="df661-708">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-709">originalValue</span><span class="sxs-lookup"><span data-stu-id="df661-709">originalValue</span></span> |<span data-ttu-id="df661-710">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-710">Yes</span></span> |<span data-ttu-id="df661-711">array or string</span><span class="sxs-lookup"><span data-stu-id="df661-711">array or string</span></span> |<span data-ttu-id="df661-712">The array or string to use for skipping.</span><span class="sxs-lookup"><span data-stu-id="df661-712">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="df661-713">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="df661-713">numberToSkip</span></span> |<span data-ttu-id="df661-714">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-714">Yes</span></span> |<span data-ttu-id="df661-715">int</span><span class="sxs-lookup"><span data-stu-id="df661-715">int</span></span> |<span data-ttu-id="df661-716">The number of elements or characters to skip.</span><span class="sxs-lookup"><span data-stu-id="df661-716">The number of elements or characters to skip.</span></span> <span data-ttu-id="df661-717">If this value is 0 or less, all the elements or characters in the value are returned.</span><span class="sxs-lookup"><span data-stu-id="df661-717">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="df661-718">If it is larger than the length of the array or string, an empty array or string is returned.</span><span class="sxs-lookup"><span data-stu-id="df661-718">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-719">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-719">Return value</span></span>

<span data-ttu-id="df661-720">An array or string.</span><span class="sxs-lookup"><span data-stu-id="df661-720">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-721">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-721">Examples</span></span>

<span data-ttu-id="df661-722">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/skip.json) skips the specified number of elements in the array, and the specified number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="df661-722">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/skip.json) skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="df661-723">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-723">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-724">Name</span><span class="sxs-lookup"><span data-stu-id="df661-724">Name</span></span> | <span data-ttu-id="df661-725">Type</span><span class="sxs-lookup"><span data-stu-id="df661-725">Type</span></span> | <span data-ttu-id="df661-726">Value</span><span class="sxs-lookup"><span data-stu-id="df661-726">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-727">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="df661-727">arrayOutput</span></span> | <span data-ttu-id="df661-728">Array</span><span class="sxs-lookup"><span data-stu-id="df661-728">Array</span></span> | <span data-ttu-id="df661-729">["three"]</span><span class="sxs-lookup"><span data-stu-id="df661-729">["three"]</span></span> |
| <span data-ttu-id="df661-730">stringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-730">stringOutput</span></span> | <span data-ttu-id="df661-731">String</span><span class="sxs-lookup"><span data-stu-id="df661-731">String</span></span> | <span data-ttu-id="df661-732">two three</span><span class="sxs-lookup"><span data-stu-id="df661-732">two three</span></span> |

<span data-ttu-id="df661-733">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-733">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/skip.json
```

<span data-ttu-id="df661-734">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-734">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/skip.json
```

<a id="split" />

## <a name="split"></a><span data-ttu-id="df661-735">split</span><span class="sxs-lookup"><span data-stu-id="df661-735">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="df661-736">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span><span class="sxs-lookup"><span data-stu-id="df661-736">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-737">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-737">Parameters</span></span>

| <span data-ttu-id="df661-738">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-738">Parameter</span></span> | <span data-ttu-id="df661-739">Required</span><span class="sxs-lookup"><span data-stu-id="df661-739">Required</span></span> | <span data-ttu-id="df661-740">Type</span><span class="sxs-lookup"><span data-stu-id="df661-740">Type</span></span> | <span data-ttu-id="df661-741">Description</span><span class="sxs-lookup"><span data-stu-id="df661-741">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-742">inputString</span><span class="sxs-lookup"><span data-stu-id="df661-742">inputString</span></span> |<span data-ttu-id="df661-743">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-743">Yes</span></span> |<span data-ttu-id="df661-744">string</span><span class="sxs-lookup"><span data-stu-id="df661-744">string</span></span> |<span data-ttu-id="df661-745">The string to split.</span><span class="sxs-lookup"><span data-stu-id="df661-745">The string to split.</span></span> |
| <span data-ttu-id="df661-746">delimiter</span><span class="sxs-lookup"><span data-stu-id="df661-746">delimiter</span></span> |<span data-ttu-id="df661-747">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-747">Yes</span></span> |<span data-ttu-id="df661-748">string or array of strings</span><span class="sxs-lookup"><span data-stu-id="df661-748">string or array of strings</span></span> |<span data-ttu-id="df661-749">The delimiter to use for splitting the string.</span><span class="sxs-lookup"><span data-stu-id="df661-749">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-750">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-750">Return value</span></span>

<span data-ttu-id="df661-751">An array of strings.</span><span class="sxs-lookup"><span data-stu-id="df661-751">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-752">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-752">Examples</span></span>

<span data-ttu-id="df661-753">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/split.json) splits the input string with a comma, and with either a comma or a semi-colon.</span><span class="sxs-lookup"><span data-stu-id="df661-753">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/split.json) splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="df661-754">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-754">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-755">Name</span><span class="sxs-lookup"><span data-stu-id="df661-755">Name</span></span> | <span data-ttu-id="df661-756">Type</span><span class="sxs-lookup"><span data-stu-id="df661-756">Type</span></span> | <span data-ttu-id="df661-757">Value</span><span class="sxs-lookup"><span data-stu-id="df661-757">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-758">firstOutput</span><span class="sxs-lookup"><span data-stu-id="df661-758">firstOutput</span></span> | <span data-ttu-id="df661-759">Array</span><span class="sxs-lookup"><span data-stu-id="df661-759">Array</span></span> | <span data-ttu-id="df661-760">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="df661-760">["one", "two", "three"]</span></span> |
| <span data-ttu-id="df661-761">secondOutput</span><span class="sxs-lookup"><span data-stu-id="df661-761">secondOutput</span></span> | <span data-ttu-id="df661-762">Array</span><span class="sxs-lookup"><span data-stu-id="df661-762">Array</span></span> | <span data-ttu-id="df661-763">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="df661-763">["one", "two", "three"]</span></span> |

<span data-ttu-id="df661-764">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-764">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/split.json
```

<span data-ttu-id="df661-765">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-765">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/split.json
```

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="df661-766">startsWith</span><span class="sxs-lookup"><span data-stu-id="df661-766">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="df661-767">Determines whether a string starts with a value.</span><span class="sxs-lookup"><span data-stu-id="df661-767">Determines whether a string starts with a value.</span></span> <span data-ttu-id="df661-768">The comparison is case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="df661-768">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-769">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-769">Parameters</span></span>

| <span data-ttu-id="df661-770">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-770">Parameter</span></span> | <span data-ttu-id="df661-771">Required</span><span class="sxs-lookup"><span data-stu-id="df661-771">Required</span></span> | <span data-ttu-id="df661-772">Type</span><span class="sxs-lookup"><span data-stu-id="df661-772">Type</span></span> | <span data-ttu-id="df661-773">Description</span><span class="sxs-lookup"><span data-stu-id="df661-773">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-774">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="df661-774">stringToSearch</span></span> |<span data-ttu-id="df661-775">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-775">Yes</span></span> |<span data-ttu-id="df661-776">string</span><span class="sxs-lookup"><span data-stu-id="df661-776">string</span></span> |<span data-ttu-id="df661-777">The value that contains the item to find.</span><span class="sxs-lookup"><span data-stu-id="df661-777">The value that contains the item to find.</span></span> |
| <span data-ttu-id="df661-778">stringToFind</span><span class="sxs-lookup"><span data-stu-id="df661-778">stringToFind</span></span> |<span data-ttu-id="df661-779">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-779">Yes</span></span> |<span data-ttu-id="df661-780">string</span><span class="sxs-lookup"><span data-stu-id="df661-780">string</span></span> |<span data-ttu-id="df661-781">The value to find.</span><span class="sxs-lookup"><span data-stu-id="df661-781">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-782">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-782">Return value</span></span>

<span data-ttu-id="df661-783">**True** if the first character or characters of the string match the value; otherwise, **False**.</span><span class="sxs-lookup"><span data-stu-id="df661-783">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-784">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-784">Examples</span></span>

<span data-ttu-id="df661-785">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json) shows how to use the startsWith and endsWith functions:</span><span class="sxs-lookup"><span data-stu-id="df661-785">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/startsendswith.json) shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="df661-786">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-786">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-787">Name</span><span class="sxs-lookup"><span data-stu-id="df661-787">Name</span></span> | <span data-ttu-id="df661-788">Type</span><span class="sxs-lookup"><span data-stu-id="df661-788">Type</span></span> | <span data-ttu-id="df661-789">Value</span><span class="sxs-lookup"><span data-stu-id="df661-789">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-790">startsTrue</span><span class="sxs-lookup"><span data-stu-id="df661-790">startsTrue</span></span> | <span data-ttu-id="df661-791">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-791">Bool</span></span> | <span data-ttu-id="df661-792">True</span><span class="sxs-lookup"><span data-stu-id="df661-792">True</span></span> |
| <span data-ttu-id="df661-793">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="df661-793">startsCapTrue</span></span> | <span data-ttu-id="df661-794">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-794">Bool</span></span> | <span data-ttu-id="df661-795">True</span><span class="sxs-lookup"><span data-stu-id="df661-795">True</span></span> |
| <span data-ttu-id="df661-796">startsFalse</span><span class="sxs-lookup"><span data-stu-id="df661-796">startsFalse</span></span> | <span data-ttu-id="df661-797">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-797">Bool</span></span> | <span data-ttu-id="df661-798">False</span><span class="sxs-lookup"><span data-stu-id="df661-798">False</span></span> |
| <span data-ttu-id="df661-799">endsTrue</span><span class="sxs-lookup"><span data-stu-id="df661-799">endsTrue</span></span> | <span data-ttu-id="df661-800">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-800">Bool</span></span> | <span data-ttu-id="df661-801">True</span><span class="sxs-lookup"><span data-stu-id="df661-801">True</span></span> |
| <span data-ttu-id="df661-802">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="df661-802">endsCapTrue</span></span> | <span data-ttu-id="df661-803">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-803">Bool</span></span> | <span data-ttu-id="df661-804">True</span><span class="sxs-lookup"><span data-stu-id="df661-804">True</span></span> |
| <span data-ttu-id="df661-805">endsFalse</span><span class="sxs-lookup"><span data-stu-id="df661-805">endsFalse</span></span> | <span data-ttu-id="df661-806">Bool</span><span class="sxs-lookup"><span data-stu-id="df661-806">Bool</span></span> | <span data-ttu-id="df661-807">False</span><span class="sxs-lookup"><span data-stu-id="df661-807">False</span></span> |

<span data-ttu-id="df661-808">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-808">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/startsendswith.json
```

<span data-ttu-id="df661-809">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-809">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/startsendswith.json
```

<a id="string" />

## <a name="string"></a><span data-ttu-id="df661-810">string</span><span class="sxs-lookup"><span data-stu-id="df661-810">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="df661-811">Converts the specified value to a string.</span><span class="sxs-lookup"><span data-stu-id="df661-811">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-812">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-812">Parameters</span></span>

| <span data-ttu-id="df661-813">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-813">Parameter</span></span> | <span data-ttu-id="df661-814">Required</span><span class="sxs-lookup"><span data-stu-id="df661-814">Required</span></span> | <span data-ttu-id="df661-815">Type</span><span class="sxs-lookup"><span data-stu-id="df661-815">Type</span></span> | <span data-ttu-id="df661-816">Description</span><span class="sxs-lookup"><span data-stu-id="df661-816">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-817">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="df661-817">valueToConvert</span></span> |<span data-ttu-id="df661-818">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-818">Yes</span></span> | <span data-ttu-id="df661-819">Any</span><span class="sxs-lookup"><span data-stu-id="df661-819">Any</span></span> |<span data-ttu-id="df661-820">The value to convert to string.</span><span class="sxs-lookup"><span data-stu-id="df661-820">The value to convert to string.</span></span> <span data-ttu-id="df661-821">Any type of value can be converted, including objects and arrays.</span><span class="sxs-lookup"><span data-stu-id="df661-821">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-822">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-822">Return value</span></span>

<span data-ttu-id="df661-823">A string of the converted value.</span><span class="sxs-lookup"><span data-stu-id="df661-823">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-824">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-824">Examples</span></span>

<span data-ttu-id="df661-825">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/string.json) shows how to convert different types of values to strings:</span><span class="sxs-lookup"><span data-stu-id="df661-825">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/string.json) shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="df661-826">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-826">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-827">Name</span><span class="sxs-lookup"><span data-stu-id="df661-827">Name</span></span> | <span data-ttu-id="df661-828">Type</span><span class="sxs-lookup"><span data-stu-id="df661-828">Type</span></span> | <span data-ttu-id="df661-829">Value</span><span class="sxs-lookup"><span data-stu-id="df661-829">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-830">objectOutput</span><span class="sxs-lookup"><span data-stu-id="df661-830">objectOutput</span></span> | <span data-ttu-id="df661-831">String</span><span class="sxs-lookup"><span data-stu-id="df661-831">String</span></span> | <span data-ttu-id="df661-832">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="df661-832">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="df661-833">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="df661-833">arrayOutput</span></span> | <span data-ttu-id="df661-834">String</span><span class="sxs-lookup"><span data-stu-id="df661-834">String</span></span> | <span data-ttu-id="df661-835">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="df661-835">["a","b","c"]</span></span> |
| <span data-ttu-id="df661-836">intOutput</span><span class="sxs-lookup"><span data-stu-id="df661-836">intOutput</span></span> | <span data-ttu-id="df661-837">String</span><span class="sxs-lookup"><span data-stu-id="df661-837">String</span></span> | <span data-ttu-id="df661-838">5</span><span class="sxs-lookup"><span data-stu-id="df661-838">5</span></span> |

<span data-ttu-id="df661-839">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-839">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/string.json
```

<span data-ttu-id="df661-840">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-840">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/string.json
```

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="df661-841">substring</span><span class="sxs-lookup"><span data-stu-id="df661-841">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="df661-842">Returns a substring that starts at the specified character position and contains the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="df661-842">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-843">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-843">Parameters</span></span>

| <span data-ttu-id="df661-844">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-844">Parameter</span></span> | <span data-ttu-id="df661-845">Required</span><span class="sxs-lookup"><span data-stu-id="df661-845">Required</span></span> | <span data-ttu-id="df661-846">Type</span><span class="sxs-lookup"><span data-stu-id="df661-846">Type</span></span> | <span data-ttu-id="df661-847">Description</span><span class="sxs-lookup"><span data-stu-id="df661-847">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-848">stringToParse</span><span class="sxs-lookup"><span data-stu-id="df661-848">stringToParse</span></span> |<span data-ttu-id="df661-849">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-849">Yes</span></span> |<span data-ttu-id="df661-850">string</span><span class="sxs-lookup"><span data-stu-id="df661-850">string</span></span> |<span data-ttu-id="df661-851">The original string from which the substring is extracted.</span><span class="sxs-lookup"><span data-stu-id="df661-851">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="df661-852">startIndex</span><span class="sxs-lookup"><span data-stu-id="df661-852">startIndex</span></span> |<span data-ttu-id="df661-853">No</span><span class="sxs-lookup"><span data-stu-id="df661-853">No</span></span> |<span data-ttu-id="df661-854">int</span><span class="sxs-lookup"><span data-stu-id="df661-854">int</span></span> |<span data-ttu-id="df661-855">The zero-based starting character position for the substring.</span><span class="sxs-lookup"><span data-stu-id="df661-855">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="df661-856">length</span><span class="sxs-lookup"><span data-stu-id="df661-856">length</span></span> |<span data-ttu-id="df661-857">No</span><span class="sxs-lookup"><span data-stu-id="df661-857">No</span></span> |<span data-ttu-id="df661-858">int</span><span class="sxs-lookup"><span data-stu-id="df661-858">int</span></span> |<span data-ttu-id="df661-859">The number of characters for the substring.</span><span class="sxs-lookup"><span data-stu-id="df661-859">The number of characters for the substring.</span></span> <span data-ttu-id="df661-860">Must refer to a location within the string.</span><span class="sxs-lookup"><span data-stu-id="df661-860">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-861">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-861">Return value</span></span>

<span data-ttu-id="df661-862">The substring.</span><span class="sxs-lookup"><span data-stu-id="df661-862">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="df661-863">Remarks</span><span class="sxs-lookup"><span data-stu-id="df661-863">Remarks</span></span>

<span data-ttu-id="df661-864">The function fails when the substring extends beyond the end of the string.</span><span class="sxs-lookup"><span data-stu-id="df661-864">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="df661-865">The following example fails with the error "The index and length parameters must refer to a location within the string.</span><span class="sxs-lookup"><span data-stu-id="df661-865">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="df661-866">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span><span class="sxs-lookup"><span data-stu-id="df661-866">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="df661-867">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-867">Examples</span></span>

<span data-ttu-id="df661-868">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/substring.json) extracts a substring from a parameter.</span><span class="sxs-lookup"><span data-stu-id="df661-868">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/substring.json) extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="df661-869">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-869">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-870">Name</span><span class="sxs-lookup"><span data-stu-id="df661-870">Name</span></span> | <span data-ttu-id="df661-871">Type</span><span class="sxs-lookup"><span data-stu-id="df661-871">Type</span></span> | <span data-ttu-id="df661-872">Value</span><span class="sxs-lookup"><span data-stu-id="df661-872">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-873">substringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-873">substringOutput</span></span> | <span data-ttu-id="df661-874">String</span><span class="sxs-lookup"><span data-stu-id="df661-874">String</span></span> | <span data-ttu-id="df661-875">two</span><span class="sxs-lookup"><span data-stu-id="df661-875">two</span></span> |

<span data-ttu-id="df661-876">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-876">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/substring.json
```

<span data-ttu-id="df661-877">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-877">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/substring.json
```

<a id="take" />

## <a name="take"></a><span data-ttu-id="df661-878">take</span><span class="sxs-lookup"><span data-stu-id="df661-878">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="df661-879">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span><span class="sxs-lookup"><span data-stu-id="df661-879">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-880">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-880">Parameters</span></span>

| <span data-ttu-id="df661-881">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-881">Parameter</span></span> | <span data-ttu-id="df661-882">Required</span><span class="sxs-lookup"><span data-stu-id="df661-882">Required</span></span> | <span data-ttu-id="df661-883">Type</span><span class="sxs-lookup"><span data-stu-id="df661-883">Type</span></span> | <span data-ttu-id="df661-884">Description</span><span class="sxs-lookup"><span data-stu-id="df661-884">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-885">originalValue</span><span class="sxs-lookup"><span data-stu-id="df661-885">originalValue</span></span> |<span data-ttu-id="df661-886">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-886">Yes</span></span> |<span data-ttu-id="df661-887">array or string</span><span class="sxs-lookup"><span data-stu-id="df661-887">array or string</span></span> |<span data-ttu-id="df661-888">The array or string to take the elements from.</span><span class="sxs-lookup"><span data-stu-id="df661-888">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="df661-889">numberToTake</span><span class="sxs-lookup"><span data-stu-id="df661-889">numberToTake</span></span> |<span data-ttu-id="df661-890">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-890">Yes</span></span> |<span data-ttu-id="df661-891">int</span><span class="sxs-lookup"><span data-stu-id="df661-891">int</span></span> |<span data-ttu-id="df661-892">The number of elements or characters to take.</span><span class="sxs-lookup"><span data-stu-id="df661-892">The number of elements or characters to take.</span></span> <span data-ttu-id="df661-893">If this value is 0 or less, an empty array or string is returned.</span><span class="sxs-lookup"><span data-stu-id="df661-893">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="df661-894">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span><span class="sxs-lookup"><span data-stu-id="df661-894">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-895">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-895">Return value</span></span>

<span data-ttu-id="df661-896">An array or string.</span><span class="sxs-lookup"><span data-stu-id="df661-896">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-897">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-897">Examples</span></span>

<span data-ttu-id="df661-898">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/take.json) takes the specified number of elements from the array, and characters from a string.</span><span class="sxs-lookup"><span data-stu-id="df661-898">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/take.json) takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="df661-899">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-899">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-900">Name</span><span class="sxs-lookup"><span data-stu-id="df661-900">Name</span></span> | <span data-ttu-id="df661-901">Type</span><span class="sxs-lookup"><span data-stu-id="df661-901">Type</span></span> | <span data-ttu-id="df661-902">Value</span><span class="sxs-lookup"><span data-stu-id="df661-902">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-903">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="df661-903">arrayOutput</span></span> | <span data-ttu-id="df661-904">Array</span><span class="sxs-lookup"><span data-stu-id="df661-904">Array</span></span> | <span data-ttu-id="df661-905">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="df661-905">["one", "two"]</span></span> |
| <span data-ttu-id="df661-906">stringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-906">stringOutput</span></span> | <span data-ttu-id="df661-907">String</span><span class="sxs-lookup"><span data-stu-id="df661-907">String</span></span> | <span data-ttu-id="df661-908">on</span><span class="sxs-lookup"><span data-stu-id="df661-908">on</span></span> |

<span data-ttu-id="df661-909">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-909">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/take.json
```

<span data-ttu-id="df661-910">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-910">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/take.json
```

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="df661-911">toLower</span><span class="sxs-lookup"><span data-stu-id="df661-911">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="df661-912">Converts the specified string to lower case.</span><span class="sxs-lookup"><span data-stu-id="df661-912">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-913">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-913">Parameters</span></span>

| <span data-ttu-id="df661-914">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-914">Parameter</span></span> | <span data-ttu-id="df661-915">Required</span><span class="sxs-lookup"><span data-stu-id="df661-915">Required</span></span> | <span data-ttu-id="df661-916">Type</span><span class="sxs-lookup"><span data-stu-id="df661-916">Type</span></span> | <span data-ttu-id="df661-917">Description</span><span class="sxs-lookup"><span data-stu-id="df661-917">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-918">stringToChange</span><span class="sxs-lookup"><span data-stu-id="df661-918">stringToChange</span></span> |<span data-ttu-id="df661-919">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-919">Yes</span></span> |<span data-ttu-id="df661-920">string</span><span class="sxs-lookup"><span data-stu-id="df661-920">string</span></span> |<span data-ttu-id="df661-921">The value to convert to lower case.</span><span class="sxs-lookup"><span data-stu-id="df661-921">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-922">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-922">Return value</span></span>

<span data-ttu-id="df661-923">The string converted to lower case.</span><span class="sxs-lookup"><span data-stu-id="df661-923">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-924">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-924">Examples</span></span>

<span data-ttu-id="df661-925">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json) converts a parameter value to lower case and to upper case.</span><span class="sxs-lookup"><span data-stu-id="df661-925">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json) converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="df661-926">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-926">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-927">Name</span><span class="sxs-lookup"><span data-stu-id="df661-927">Name</span></span> | <span data-ttu-id="df661-928">Type</span><span class="sxs-lookup"><span data-stu-id="df661-928">Type</span></span> | <span data-ttu-id="df661-929">Value</span><span class="sxs-lookup"><span data-stu-id="df661-929">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-930">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="df661-930">toLowerOutput</span></span> | <span data-ttu-id="df661-931">String</span><span class="sxs-lookup"><span data-stu-id="df661-931">String</span></span> | <span data-ttu-id="df661-932">one two three</span><span class="sxs-lookup"><span data-stu-id="df661-932">one two three</span></span> |
| <span data-ttu-id="df661-933">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="df661-933">toUpperOutput</span></span> | <span data-ttu-id="df661-934">String</span><span class="sxs-lookup"><span data-stu-id="df661-934">String</span></span> | <span data-ttu-id="df661-935">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="df661-935">ONE TWO THREE</span></span> |

<span data-ttu-id="df661-936">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-936">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/tolower.json
```

<span data-ttu-id="df661-937">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-937">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/tolower.json
```

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="df661-938">toUpper</span><span class="sxs-lookup"><span data-stu-id="df661-938">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="df661-939">Converts the specified string to upper case.</span><span class="sxs-lookup"><span data-stu-id="df661-939">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-940">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-940">Parameters</span></span>

| <span data-ttu-id="df661-941">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-941">Parameter</span></span> | <span data-ttu-id="df661-942">Required</span><span class="sxs-lookup"><span data-stu-id="df661-942">Required</span></span> | <span data-ttu-id="df661-943">Type</span><span class="sxs-lookup"><span data-stu-id="df661-943">Type</span></span> | <span data-ttu-id="df661-944">Description</span><span class="sxs-lookup"><span data-stu-id="df661-944">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-945">stringToChange</span><span class="sxs-lookup"><span data-stu-id="df661-945">stringToChange</span></span> |<span data-ttu-id="df661-946">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-946">Yes</span></span> |<span data-ttu-id="df661-947">string</span><span class="sxs-lookup"><span data-stu-id="df661-947">string</span></span> |<span data-ttu-id="df661-948">The value to convert to upper case.</span><span class="sxs-lookup"><span data-stu-id="df661-948">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-949">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-949">Return value</span></span>

<span data-ttu-id="df661-950">The string converted to upper case.</span><span class="sxs-lookup"><span data-stu-id="df661-950">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-951">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-951">Examples</span></span>

<span data-ttu-id="df661-952">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json) converts a parameter value to lower case and to upper case.</span><span class="sxs-lookup"><span data-stu-id="df661-952">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/tolower.json) converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="df661-953">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-953">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-954">Name</span><span class="sxs-lookup"><span data-stu-id="df661-954">Name</span></span> | <span data-ttu-id="df661-955">Type</span><span class="sxs-lookup"><span data-stu-id="df661-955">Type</span></span> | <span data-ttu-id="df661-956">Value</span><span class="sxs-lookup"><span data-stu-id="df661-956">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-957">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="df661-957">toLowerOutput</span></span> | <span data-ttu-id="df661-958">String</span><span class="sxs-lookup"><span data-stu-id="df661-958">String</span></span> | <span data-ttu-id="df661-959">one two three</span><span class="sxs-lookup"><span data-stu-id="df661-959">one two three</span></span> |
| <span data-ttu-id="df661-960">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="df661-960">toUpperOutput</span></span> | <span data-ttu-id="df661-961">String</span><span class="sxs-lookup"><span data-stu-id="df661-961">String</span></span> | <span data-ttu-id="df661-962">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="df661-962">ONE TWO THREE</span></span> |

<span data-ttu-id="df661-963">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-963">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/tolower.json
```

<span data-ttu-id="df661-964">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-964">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/tolower.json
```

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="df661-965">trim</span><span class="sxs-lookup"><span data-stu-id="df661-965">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="df661-966">Removes all leading and trailing white-space characters from the specified string.</span><span class="sxs-lookup"><span data-stu-id="df661-966">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-967">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-967">Parameters</span></span>

| <span data-ttu-id="df661-968">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-968">Parameter</span></span> | <span data-ttu-id="df661-969">Required</span><span class="sxs-lookup"><span data-stu-id="df661-969">Required</span></span> | <span data-ttu-id="df661-970">Type</span><span class="sxs-lookup"><span data-stu-id="df661-970">Type</span></span> | <span data-ttu-id="df661-971">Description</span><span class="sxs-lookup"><span data-stu-id="df661-971">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-972">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="df661-972">stringToTrim</span></span> |<span data-ttu-id="df661-973">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-973">Yes</span></span> |<span data-ttu-id="df661-974">string</span><span class="sxs-lookup"><span data-stu-id="df661-974">string</span></span> |<span data-ttu-id="df661-975">The value to trim.</span><span class="sxs-lookup"><span data-stu-id="df661-975">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-976">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-976">Return value</span></span>

<span data-ttu-id="df661-977">The string without leading and trailing white-space characters.</span><span class="sxs-lookup"><span data-stu-id="df661-977">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-978">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-978">Examples</span></span>

<span data-ttu-id="df661-979">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/trim.json) trims the white-space characters from the parameter.</span><span class="sxs-lookup"><span data-stu-id="df661-979">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/trim.json) trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="df661-980">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-980">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-981">Name</span><span class="sxs-lookup"><span data-stu-id="df661-981">Name</span></span> | <span data-ttu-id="df661-982">Type</span><span class="sxs-lookup"><span data-stu-id="df661-982">Type</span></span> | <span data-ttu-id="df661-983">Value</span><span class="sxs-lookup"><span data-stu-id="df661-983">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-984">return</span><span class="sxs-lookup"><span data-stu-id="df661-984">return</span></span> | <span data-ttu-id="df661-985">String</span><span class="sxs-lookup"><span data-stu-id="df661-985">String</span></span> | <span data-ttu-id="df661-986">one two three</span><span class="sxs-lookup"><span data-stu-id="df661-986">one two three</span></span> |

<span data-ttu-id="df661-987">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-987">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/trim.json
```

<span data-ttu-id="df661-988">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-988">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/trim.json
```

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="df661-989">uniqueString</span><span class="sxs-lookup"><span data-stu-id="df661-989">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="df661-990">Creates a deterministic hash string based on the values provided as parameters.</span><span class="sxs-lookup"><span data-stu-id="df661-990">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="df661-991">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-991">Parameters</span></span>

| <span data-ttu-id="df661-992">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-992">Parameter</span></span> | <span data-ttu-id="df661-993">Required</span><span class="sxs-lookup"><span data-stu-id="df661-993">Required</span></span> | <span data-ttu-id="df661-994">Type</span><span class="sxs-lookup"><span data-stu-id="df661-994">Type</span></span> | <span data-ttu-id="df661-995">Description</span><span class="sxs-lookup"><span data-stu-id="df661-995">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-996">baseString</span><span class="sxs-lookup"><span data-stu-id="df661-996">baseString</span></span> |<span data-ttu-id="df661-997">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-997">Yes</span></span> |<span data-ttu-id="df661-998">string</span><span class="sxs-lookup"><span data-stu-id="df661-998">string</span></span> |<span data-ttu-id="df661-999">The value used in the hash function to create a unique string.</span><span class="sxs-lookup"><span data-stu-id="df661-999">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="df661-1000">additional parameters as needed</span><span class="sxs-lookup"><span data-stu-id="df661-1000">additional parameters as needed</span></span> |<span data-ttu-id="df661-1001">No</span><span class="sxs-lookup"><span data-stu-id="df661-1001">No</span></span> |<span data-ttu-id="df661-1002">string</span><span class="sxs-lookup"><span data-stu-id="df661-1002">string</span></span> |<span data-ttu-id="df661-1003">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span><span class="sxs-lookup"><span data-stu-id="df661-1003">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="df661-1004">Remarks</span><span class="sxs-lookup"><span data-stu-id="df661-1004">Remarks</span></span>

<span data-ttu-id="df661-1005">This function is helpful when you need to create a unique name for a resource.</span><span class="sxs-lookup"><span data-stu-id="df661-1005">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="df661-1006">You provide parameter values that limit the scope of uniqueness for the result.</span><span class="sxs-lookup"><span data-stu-id="df661-1006">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="df661-1007">You can specify whether the name is unique down to subscription, resource group, or deployment.</span><span class="sxs-lookup"><span data-stu-id="df661-1007">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="df661-1008">The returned value is not a random string, but rather the result of a hash function.</span><span class="sxs-lookup"><span data-stu-id="df661-1008">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="df661-1009">The returned value is 13 characters long.</span><span class="sxs-lookup"><span data-stu-id="df661-1009">The returned value is 13 characters long.</span></span> <span data-ttu-id="df661-1010">It is not globally unique.</span><span class="sxs-lookup"><span data-stu-id="df661-1010">It is not globally unique.</span></span> <span data-ttu-id="df661-1011">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span><span class="sxs-lookup"><span data-stu-id="df661-1011">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="df661-1012">The following example shows the format of the returned value.</span><span class="sxs-lookup"><span data-stu-id="df661-1012">The following example shows the format of the returned value.</span></span> <span data-ttu-id="df661-1013">The actual value varies by the provided parameters.</span><span class="sxs-lookup"><span data-stu-id="df661-1013">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="df661-1014">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span><span class="sxs-lookup"><span data-stu-id="df661-1014">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="df661-1015">Unique scoped to subscription</span><span class="sxs-lookup"><span data-stu-id="df661-1015">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="df661-1016">Unique scoped to resource group</span><span class="sxs-lookup"><span data-stu-id="df661-1016">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="df661-1017">Unique scoped to deployment for a resource group</span><span class="sxs-lookup"><span data-stu-id="df661-1017">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="df661-1018">The following example shows how to create a unique name for a storage account based on your resource group.</span><span class="sxs-lookup"><span data-stu-id="df661-1018">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="df661-1019">Inside the resource group, the name is not unique if constructed the same way.</span><span class="sxs-lookup"><span data-stu-id="df661-1019">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="df661-1020">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-1020">Return value</span></span>

<span data-ttu-id="df661-1021">A string containing 13 characters.</span><span class="sxs-lookup"><span data-stu-id="df661-1021">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-1022">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-1022">Examples</span></span>

<span data-ttu-id="df661-1023">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uniquestring.json) returns results from uniquestring:</span><span class="sxs-lookup"><span data-stu-id="df661-1023">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uniquestring.json) returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="df661-1024">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1024">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uniquestring.json
```

<span data-ttu-id="df661-1025">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1025">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uniquestring.json
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="df661-1026">uri</span><span class="sxs-lookup"><span data-stu-id="df661-1026">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="df661-1027">Creates an absolute URI by combining the baseUri and the relativeUri string.</span><span class="sxs-lookup"><span data-stu-id="df661-1027">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-1028">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-1028">Parameters</span></span>

| <span data-ttu-id="df661-1029">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-1029">Parameter</span></span> | <span data-ttu-id="df661-1030">Required</span><span class="sxs-lookup"><span data-stu-id="df661-1030">Required</span></span> | <span data-ttu-id="df661-1031">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1031">Type</span></span> | <span data-ttu-id="df661-1032">Description</span><span class="sxs-lookup"><span data-stu-id="df661-1032">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-1033">baseUri</span><span class="sxs-lookup"><span data-stu-id="df661-1033">baseUri</span></span> |<span data-ttu-id="df661-1034">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-1034">Yes</span></span> |<span data-ttu-id="df661-1035">string</span><span class="sxs-lookup"><span data-stu-id="df661-1035">string</span></span> |<span data-ttu-id="df661-1036">The base uri string.</span><span class="sxs-lookup"><span data-stu-id="df661-1036">The base uri string.</span></span> |
| <span data-ttu-id="df661-1037">relativeUri</span><span class="sxs-lookup"><span data-stu-id="df661-1037">relativeUri</span></span> |<span data-ttu-id="df661-1038">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-1038">Yes</span></span> |<span data-ttu-id="df661-1039">string</span><span class="sxs-lookup"><span data-stu-id="df661-1039">string</span></span> |<span data-ttu-id="df661-1040">The relative uri string to add to the base uri string.</span><span class="sxs-lookup"><span data-stu-id="df661-1040">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="df661-1041">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span><span class="sxs-lookup"><span data-stu-id="df661-1041">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="df661-1042">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="df661-1042">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="df661-1043">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-1043">Return value</span></span>

<span data-ttu-id="df661-1044">A string representing the absolute URI for the base and relative values.</span><span class="sxs-lookup"><span data-stu-id="df661-1044">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-1045">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-1045">Examples</span></span>

<span data-ttu-id="df661-1046">The following example shows how to construct a link to a nested template based on the value of the parent template.</span><span class="sxs-lookup"><span data-stu-id="df661-1046">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="df661-1047">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="df661-1047">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="df661-1048">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-1048">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-1049">Name</span><span class="sxs-lookup"><span data-stu-id="df661-1049">Name</span></span> | <span data-ttu-id="df661-1050">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1050">Type</span></span> | <span data-ttu-id="df661-1051">Value</span><span class="sxs-lookup"><span data-stu-id="df661-1051">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-1052">uriOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1052">uriOutput</span></span> | <span data-ttu-id="df661-1053">String</span><span class="sxs-lookup"><span data-stu-id="df661-1053">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |
| <span data-ttu-id="df661-1054">componentOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1054">componentOutput</span></span> | <span data-ttu-id="df661-1055">String</span><span class="sxs-lookup"><span data-stu-id="df661-1055">String</span></span> | <span data-ttu-id="df661-1056">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="df661-1056">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="df661-1057">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1057">toStringOutput</span></span> | <span data-ttu-id="df661-1058">String</span><span class="sxs-lookup"><span data-stu-id="df661-1058">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |

<span data-ttu-id="df661-1059">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1059">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

<span data-ttu-id="df661-1060">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1060">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="df661-1061">uriComponent</span><span class="sxs-lookup"><span data-stu-id="df661-1061">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="df661-1062">Encodes a URI.</span><span class="sxs-lookup"><span data-stu-id="df661-1062">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-1063">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-1063">Parameters</span></span>

| <span data-ttu-id="df661-1064">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-1064">Parameter</span></span> | <span data-ttu-id="df661-1065">Required</span><span class="sxs-lookup"><span data-stu-id="df661-1065">Required</span></span> | <span data-ttu-id="df661-1066">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1066">Type</span></span> | <span data-ttu-id="df661-1067">Description</span><span class="sxs-lookup"><span data-stu-id="df661-1067">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-1068">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="df661-1068">stringToEncode</span></span> |<span data-ttu-id="df661-1069">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-1069">Yes</span></span> |<span data-ttu-id="df661-1070">string</span><span class="sxs-lookup"><span data-stu-id="df661-1070">string</span></span> |<span data-ttu-id="df661-1071">The value to encode.</span><span class="sxs-lookup"><span data-stu-id="df661-1071">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-1072">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-1072">Return value</span></span>

<span data-ttu-id="df661-1073">A string of the URI encoded value.</span><span class="sxs-lookup"><span data-stu-id="df661-1073">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-1074">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-1074">Examples</span></span>

<span data-ttu-id="df661-1075">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="df661-1075">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="df661-1076">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-1076">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-1077">Name</span><span class="sxs-lookup"><span data-stu-id="df661-1077">Name</span></span> | <span data-ttu-id="df661-1078">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1078">Type</span></span> | <span data-ttu-id="df661-1079">Value</span><span class="sxs-lookup"><span data-stu-id="df661-1079">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-1080">uriOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1080">uriOutput</span></span> | <span data-ttu-id="df661-1081">String</span><span class="sxs-lookup"><span data-stu-id="df661-1081">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |
| <span data-ttu-id="df661-1082">componentOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1082">componentOutput</span></span> | <span data-ttu-id="df661-1083">String</span><span class="sxs-lookup"><span data-stu-id="df661-1083">String</span></span> | <span data-ttu-id="df661-1084">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="df661-1084">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="df661-1085">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1085">toStringOutput</span></span> | <span data-ttu-id="df661-1086">String</span><span class="sxs-lookup"><span data-stu-id="df661-1086">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |

<span data-ttu-id="df661-1087">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1087">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

<span data-ttu-id="df661-1088">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1088">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="df661-1089">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="df661-1089">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="df661-1090">Returns a string of a URI encoded value.</span><span class="sxs-lookup"><span data-stu-id="df661-1090">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="df661-1091">Parameters</span><span class="sxs-lookup"><span data-stu-id="df661-1091">Parameters</span></span>

| <span data-ttu-id="df661-1092">Parameter</span><span class="sxs-lookup"><span data-stu-id="df661-1092">Parameter</span></span> | <span data-ttu-id="df661-1093">Required</span><span class="sxs-lookup"><span data-stu-id="df661-1093">Required</span></span> | <span data-ttu-id="df661-1094">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1094">Type</span></span> | <span data-ttu-id="df661-1095">Description</span><span class="sxs-lookup"><span data-stu-id="df661-1095">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="df661-1096">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="df661-1096">uriEncodedString</span></span> |<span data-ttu-id="df661-1097">Yes</span><span class="sxs-lookup"><span data-stu-id="df661-1097">Yes</span></span> |<span data-ttu-id="df661-1098">string</span><span class="sxs-lookup"><span data-stu-id="df661-1098">string</span></span> |<span data-ttu-id="df661-1099">The URI encoded value to convert to a string.</span><span class="sxs-lookup"><span data-stu-id="df661-1099">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="df661-1100">Return value</span><span class="sxs-lookup"><span data-stu-id="df661-1100">Return value</span></span>

<span data-ttu-id="df661-1101">A decoded string of URI encoded value.</span><span class="sxs-lookup"><span data-stu-id="df661-1101">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="df661-1102">Examples</span><span class="sxs-lookup"><span data-stu-id="df661-1102">Examples</span></span>

<span data-ttu-id="df661-1103">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="df661-1103">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/uri.json) shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="df661-1104">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="df661-1104">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="df661-1105">Name</span><span class="sxs-lookup"><span data-stu-id="df661-1105">Name</span></span> | <span data-ttu-id="df661-1106">Type</span><span class="sxs-lookup"><span data-stu-id="df661-1106">Type</span></span> | <span data-ttu-id="df661-1107">Value</span><span class="sxs-lookup"><span data-stu-id="df661-1107">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="df661-1108">uriOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1108">uriOutput</span></span> | <span data-ttu-id="df661-1109">String</span><span class="sxs-lookup"><span data-stu-id="df661-1109">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |
| <span data-ttu-id="df661-1110">componentOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1110">componentOutput</span></span> | <span data-ttu-id="df661-1111">String</span><span class="sxs-lookup"><span data-stu-id="df661-1111">String</span></span> | <span data-ttu-id="df661-1112">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="df661-1112">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="df661-1113">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="df661-1113">toStringOutput</span></span> | <span data-ttu-id="df661-1114">String</span><span class="sxs-lookup"><span data-stu-id="df661-1114">String</span></span> | http://contoso.com/resources/nested/azuredeploy.json |

<span data-ttu-id="df661-1115">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1115">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

<span data-ttu-id="df661-1116">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="df661-1116">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/uri.json
```

## <a name="next-steps"></a><span data-ttu-id="df661-1117">Next steps</span><span class="sxs-lookup"><span data-stu-id="df661-1117">Next steps</span></span>
* <span data-ttu-id="df661-1118">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="df661-1118">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="df661-1119">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="df661-1119">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="df661-1120">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="df661-1120">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="df661-1121">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="df661-1121">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

