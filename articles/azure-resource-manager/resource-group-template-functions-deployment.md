---
title: Azure Resource Manager template functions - deployment | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to retrieve deployment information.
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
ms.openlocfilehash: 725bc41f96359d4bf0d9d570f73f91dba5da2cab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864811"
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="67af0-103">Deployment functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="67af0-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="67af0-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span><span class="sxs-lookup"><span data-stu-id="67af0-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="67af0-105">deployment</span><span class="sxs-lookup"><span data-stu-id="67af0-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="67af0-106">parameters</span><span class="sxs-lookup"><span data-stu-id="67af0-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="67af0-107">variables</span><span class="sxs-lookup"><span data-stu-id="67af0-107">variables</span></span>](#variables)

<span data-ttu-id="67af0-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="67af0-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="67af0-109">deployment</span><span class="sxs-lookup"><span data-stu-id="67af0-109">deployment</span></span>
`deployment()`

<span data-ttu-id="67af0-110">Returns information about the current deployment operation.</span><span class="sxs-lookup"><span data-stu-id="67af0-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="67af0-111">Return value</span><span class="sxs-lookup"><span data-stu-id="67af0-111">Return value</span></span>

<span data-ttu-id="67af0-112">This function returns the object that is passed during deployment.</span><span class="sxs-lookup"><span data-stu-id="67af0-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="67af0-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span><span class="sxs-lookup"><span data-stu-id="67af0-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="67af0-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span><span class="sxs-lookup"><span data-stu-id="67af0-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="67af0-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="67af0-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="67af0-116">Remarks</span><span class="sxs-lookup"><span data-stu-id="67af0-116">Remarks</span></span>

<span data-ttu-id="67af0-117">You can use deployment() to link to another template based on the URI of the parent template.</span><span class="sxs-lookup"><span data-stu-id="67af0-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="67af0-118">Example</span><span class="sxs-lookup"><span data-stu-id="67af0-118">Example</span></span>

<span data-ttu-id="67af0-119">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/deployment.json) returns the deployment object:</span><span class="sxs-lookup"><span data-stu-id="67af0-119">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/deployment.json) returns the deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="67af0-120">The preceding example returns the following object:</span><span class="sxs-lookup"><span data-stu-id="67af0-120">The preceding example returns the following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<span data-ttu-id="67af0-121">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-121">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/deployment.json
```

<span data-ttu-id="67af0-122">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-122">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/deployment.json
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="67af0-123">parameters</span><span class="sxs-lookup"><span data-stu-id="67af0-123">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="67af0-124">Returns a parameter value.</span><span class="sxs-lookup"><span data-stu-id="67af0-124">Returns a parameter value.</span></span> <span data-ttu-id="67af0-125">The specified parameter name must be defined in the parameters section of the template.</span><span class="sxs-lookup"><span data-stu-id="67af0-125">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="67af0-126">Parameters</span><span class="sxs-lookup"><span data-stu-id="67af0-126">Parameters</span></span>

| <span data-ttu-id="67af0-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="67af0-127">Parameter</span></span> | <span data-ttu-id="67af0-128">Required</span><span class="sxs-lookup"><span data-stu-id="67af0-128">Required</span></span> | <span data-ttu-id="67af0-129">Type</span><span class="sxs-lookup"><span data-stu-id="67af0-129">Type</span></span> | <span data-ttu-id="67af0-130">Description</span><span class="sxs-lookup"><span data-stu-id="67af0-130">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67af0-131">parameterName</span><span class="sxs-lookup"><span data-stu-id="67af0-131">parameterName</span></span> |<span data-ttu-id="67af0-132">Yes</span><span class="sxs-lookup"><span data-stu-id="67af0-132">Yes</span></span> |<span data-ttu-id="67af0-133">string</span><span class="sxs-lookup"><span data-stu-id="67af0-133">string</span></span> |<span data-ttu-id="67af0-134">The name of the parameter to return.</span><span class="sxs-lookup"><span data-stu-id="67af0-134">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67af0-135">Return value</span><span class="sxs-lookup"><span data-stu-id="67af0-135">Return value</span></span>

<span data-ttu-id="67af0-136">The value of the specified parameter.</span><span class="sxs-lookup"><span data-stu-id="67af0-136">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="67af0-137">Remarks</span><span class="sxs-lookup"><span data-stu-id="67af0-137">Remarks</span></span>

<span data-ttu-id="67af0-138">Typically, you use parameters to set resource values.</span><span class="sxs-lookup"><span data-stu-id="67af0-138">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="67af0-139">The following example sets the name of web site to the parameter value passed in during deployment.</span><span class="sxs-lookup"><span data-stu-id="67af0-139">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="67af0-140">Example</span><span class="sxs-lookup"><span data-stu-id="67af0-140">Example</span></span>

<span data-ttu-id="67af0-141">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/parameters.json) shows a simplified use of the parameters function.</span><span class="sxs-lookup"><span data-stu-id="67af0-141">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/parameters.json) shows a simplified use of the parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="67af0-142">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="67af0-142">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67af0-143">Name</span><span class="sxs-lookup"><span data-stu-id="67af0-143">Name</span></span> | <span data-ttu-id="67af0-144">Type</span><span class="sxs-lookup"><span data-stu-id="67af0-144">Type</span></span> | <span data-ttu-id="67af0-145">Value</span><span class="sxs-lookup"><span data-stu-id="67af0-145">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67af0-146">stringOutput</span><span class="sxs-lookup"><span data-stu-id="67af0-146">stringOutput</span></span> | <span data-ttu-id="67af0-147">String</span><span class="sxs-lookup"><span data-stu-id="67af0-147">String</span></span> | <span data-ttu-id="67af0-148">option 1</span><span class="sxs-lookup"><span data-stu-id="67af0-148">option 1</span></span> |
| <span data-ttu-id="67af0-149">intOutput</span><span class="sxs-lookup"><span data-stu-id="67af0-149">intOutput</span></span> | <span data-ttu-id="67af0-150">Int</span><span class="sxs-lookup"><span data-stu-id="67af0-150">Int</span></span> | <span data-ttu-id="67af0-151">1</span><span class="sxs-lookup"><span data-stu-id="67af0-151">1</span></span> |
| <span data-ttu-id="67af0-152">objectOutput</span><span class="sxs-lookup"><span data-stu-id="67af0-152">objectOutput</span></span> | <span data-ttu-id="67af0-153">Object</span><span class="sxs-lookup"><span data-stu-id="67af0-153">Object</span></span> | <span data-ttu-id="67af0-154">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="67af0-154">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="67af0-155">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="67af0-155">arrayOutput</span></span> | <span data-ttu-id="67af0-156">Array</span><span class="sxs-lookup"><span data-stu-id="67af0-156">Array</span></span> | <span data-ttu-id="67af0-157">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="67af0-157">[1, 2, 3]</span></span> |
| <span data-ttu-id="67af0-158">crossOutput</span><span class="sxs-lookup"><span data-stu-id="67af0-158">crossOutput</span></span> | <span data-ttu-id="67af0-159">String</span><span class="sxs-lookup"><span data-stu-id="67af0-159">String</span></span> | <span data-ttu-id="67af0-160">option 1</span><span class="sxs-lookup"><span data-stu-id="67af0-160">option 1</span></span> |

<span data-ttu-id="67af0-161">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-161">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/parameters.json
```

<span data-ttu-id="67af0-162">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-162">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/parameters.json
```

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="67af0-163">variables</span><span class="sxs-lookup"><span data-stu-id="67af0-163">variables</span></span>
`variables(variableName)`

<span data-ttu-id="67af0-164">Returns the value of variable.</span><span class="sxs-lookup"><span data-stu-id="67af0-164">Returns the value of variable.</span></span> <span data-ttu-id="67af0-165">The specified variable name must be defined in the variables section of the template.</span><span class="sxs-lookup"><span data-stu-id="67af0-165">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="67af0-166">Parameters</span><span class="sxs-lookup"><span data-stu-id="67af0-166">Parameters</span></span>

| <span data-ttu-id="67af0-167">Parameter</span><span class="sxs-lookup"><span data-stu-id="67af0-167">Parameter</span></span> | <span data-ttu-id="67af0-168">Required</span><span class="sxs-lookup"><span data-stu-id="67af0-168">Required</span></span> | <span data-ttu-id="67af0-169">Type</span><span class="sxs-lookup"><span data-stu-id="67af0-169">Type</span></span> | <span data-ttu-id="67af0-170">Description</span><span class="sxs-lookup"><span data-stu-id="67af0-170">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="67af0-171">variableName</span><span class="sxs-lookup"><span data-stu-id="67af0-171">variableName</span></span> |<span data-ttu-id="67af0-172">Yes</span><span class="sxs-lookup"><span data-stu-id="67af0-172">Yes</span></span> |<span data-ttu-id="67af0-173">String</span><span class="sxs-lookup"><span data-stu-id="67af0-173">String</span></span> |<span data-ttu-id="67af0-174">The name of the variable to return.</span><span class="sxs-lookup"><span data-stu-id="67af0-174">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="67af0-175">Return value</span><span class="sxs-lookup"><span data-stu-id="67af0-175">Return value</span></span>

<span data-ttu-id="67af0-176">The value of the specified variable.</span><span class="sxs-lookup"><span data-stu-id="67af0-176">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="67af0-177">Remarks</span><span class="sxs-lookup"><span data-stu-id="67af0-177">Remarks</span></span>

<span data-ttu-id="67af0-178">Typically, you use variables to simplify your template by constructing complex values only once.</span><span class="sxs-lookup"><span data-stu-id="67af0-178">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="67af0-179">The following example constructs a unique name for a storage account.</span><span class="sxs-lookup"><span data-stu-id="67af0-179">The following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="67af0-180">Example</span><span class="sxs-lookup"><span data-stu-id="67af0-180">Example</span></span>

<span data-ttu-id="67af0-181">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/variables.json) returns different variable values.</span><span class="sxs-lookup"><span data-stu-id="67af0-181">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/variables.json) returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="67af0-182">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="67af0-182">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="67af0-183">Name</span><span class="sxs-lookup"><span data-stu-id="67af0-183">Name</span></span> | <span data-ttu-id="67af0-184">Type</span><span class="sxs-lookup"><span data-stu-id="67af0-184">Type</span></span> | <span data-ttu-id="67af0-185">Value</span><span class="sxs-lookup"><span data-stu-id="67af0-185">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="67af0-186">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="67af0-186">exampleOutput1</span></span> | <span data-ttu-id="67af0-187">String</span><span class="sxs-lookup"><span data-stu-id="67af0-187">String</span></span> | <span data-ttu-id="67af0-188">myVariable</span><span class="sxs-lookup"><span data-stu-id="67af0-188">myVariable</span></span> |
| <span data-ttu-id="67af0-189">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="67af0-189">exampleOutput2</span></span> | <span data-ttu-id="67af0-190">Array</span><span class="sxs-lookup"><span data-stu-id="67af0-190">Array</span></span> | <span data-ttu-id="67af0-191">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="67af0-191">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="67af0-192">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="67af0-192">exampleOutput3</span></span> | <span data-ttu-id="67af0-193">String</span><span class="sxs-lookup"><span data-stu-id="67af0-193">String</span></span> | <span data-ttu-id="67af0-194">myVariable</span><span class="sxs-lookup"><span data-stu-id="67af0-194">myVariable</span></span> |
| <span data-ttu-id="67af0-195">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="67af0-195">exampleOutput4</span></span> |  <span data-ttu-id="67af0-196">Object</span><span class="sxs-lookup"><span data-stu-id="67af0-196">Object</span></span> | <span data-ttu-id="67af0-197">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="67af0-197">{"property1": "value1", "property2": "value2"}</span></span> |

<span data-ttu-id="67af0-198">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-198">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/variables.json
```

<span data-ttu-id="67af0-199">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="67af0-199">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/variables.json
```

## <a name="next-steps"></a><span data-ttu-id="67af0-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="67af0-200">Next steps</span></span>
* <span data-ttu-id="67af0-201">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67af0-201">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67af0-202">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67af0-202">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="67af0-203">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="67af0-203">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="67af0-204">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="67af0-204">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

