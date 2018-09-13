---
title: Azure Resource Manager template functions - resources | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to retrieve values about resources.
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
ms.date: 06/06/2018
ms.author: tomfitz
ms.openlocfilehash: 4e454030f77a22236da18c8d8a5215667784f7c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869088"
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f5c3d-103">Resource functions for Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="f5c3d-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="f5c3d-104">Resource Manager provides the following functions for getting resource values:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="f5c3d-105">listAccountSas</span><span class="sxs-lookup"><span data-stu-id="f5c3d-105">listAccountSas</span></span>](#list)
* [<span data-ttu-id="f5c3d-106">listKeys</span><span class="sxs-lookup"><span data-stu-id="f5c3d-106">listKeys</span></span>](#listkeys)
* [<span data-ttu-id="f5c3d-107">listSecrets</span><span class="sxs-lookup"><span data-stu-id="f5c3d-107">listSecrets</span></span>](#list)
* [<span data-ttu-id="f5c3d-108">list\*</span><span class="sxs-lookup"><span data-stu-id="f5c3d-108">list\*</span></span>](#list)
* [<span data-ttu-id="f5c3d-109">providers</span><span class="sxs-lookup"><span data-stu-id="f5c3d-109">providers</span></span>](#providers)
* [<span data-ttu-id="f5c3d-110">reference</span><span class="sxs-lookup"><span data-stu-id="f5c3d-110">reference</span></span>](#reference)
* [<span data-ttu-id="f5c3d-111">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="f5c3d-111">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="f5c3d-112">resourceId</span><span class="sxs-lookup"><span data-stu-id="f5c3d-112">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="f5c3d-113">subscription</span><span class="sxs-lookup"><span data-stu-id="f5c3d-113">subscription</span></span>](#subscription)

<span data-ttu-id="f5c3d-114">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-114">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listaccountsas-listkeys-listsecrets-and-list"></a><span data-ttu-id="f5c3d-115">listAccountSas, listKeys, listSecrets, and list\*</span><span class="sxs-lookup"><span data-stu-id="f5c3d-115">listAccountSas, listKeys, listSecrets, and list\*</span></span>
`listAccountSas(resourceName or resourceIdentifier, apiVersion, functionValues)`

`listKeys(resourceName or resourceIdentifier, apiVersion)`

`listSecrets(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="f5c3d-116">Returns the values for any resource type that supports the list operation.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-116">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="f5c3d-117">The most common usages are `listKeys` and `listSecrets`.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-117">The most common usages are `listKeys` and `listSecrets`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="f5c3d-118">Parameters</span><span class="sxs-lookup"><span data-stu-id="f5c3d-118">Parameters</span></span>

| <span data-ttu-id="f5c3d-119">Parameter</span><span class="sxs-lookup"><span data-stu-id="f5c3d-119">Parameter</span></span> | <span data-ttu-id="f5c3d-120">Required</span><span class="sxs-lookup"><span data-stu-id="f5c3d-120">Required</span></span> | <span data-ttu-id="f5c3d-121">Type</span><span class="sxs-lookup"><span data-stu-id="f5c3d-121">Type</span></span> | <span data-ttu-id="f5c3d-122">Description</span><span class="sxs-lookup"><span data-stu-id="f5c3d-122">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f5c3d-123">resourceName or resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="f5c3d-123">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="f5c3d-124">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-124">Yes</span></span> |<span data-ttu-id="f5c3d-125">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-125">string</span></span> |<span data-ttu-id="f5c3d-126">Unique identifier for the resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-126">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="f5c3d-127">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f5c3d-127">apiVersion</span></span> |<span data-ttu-id="f5c3d-128">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-128">Yes</span></span> |<span data-ttu-id="f5c3d-129">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-129">string</span></span> |<span data-ttu-id="f5c3d-130">API version of resource runtime state.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-130">API version of resource runtime state.</span></span> <span data-ttu-id="f5c3d-131">Typically, in the format, **yyyy-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-131">Typically, in the format, **yyyy-mm-dd**.</span></span> |
| <span data-ttu-id="f5c3d-132">functionValues</span><span class="sxs-lookup"><span data-stu-id="f5c3d-132">functionValues</span></span> |<span data-ttu-id="f5c3d-133">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-133">No</span></span> |<span data-ttu-id="f5c3d-134">object</span><span class="sxs-lookup"><span data-stu-id="f5c3d-134">object</span></span> | <span data-ttu-id="f5c3d-135">An object that has values for the function.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-135">An object that has values for the function.</span></span> <span data-ttu-id="f5c3d-136">Only provide this object for functions that support receiving an object with parameter values, such as **listAccountSas** on a storage account.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-136">Only provide this object for functions that support receiving an object with parameter values, such as **listAccountSas** on a storage account.</span></span> | 

### <a name="return-value"></a><span data-ttu-id="f5c3d-137">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-137">Return value</span></span>

<span data-ttu-id="f5c3d-138">The returned object from listKeys has the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-138">The returned object from listKeys has the following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="f5c3d-139">Other list functions have different return formats.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-139">Other list functions have different return formats.</span></span> <span data-ttu-id="f5c3d-140">To see the format of a function, include it in the outputs section as shown in the example template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-140">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="f5c3d-141">Remarks</span><span class="sxs-lookup"><span data-stu-id="f5c3d-141">Remarks</span></span>

<span data-ttu-id="f5c3d-142">Any operation that starts with **list** can be used as a function in your template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-142">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="f5c3d-143">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-143">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="f5c3d-144">The [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-144">The [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*.</span></span> <span data-ttu-id="f5c3d-145">To use this function in a template, provide an object with the body parameter values.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-145">To use this function in a template, provide an object with the body parameter values.</span></span>

<span data-ttu-id="f5c3d-146">To determine which resource types have a list operation, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-146">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="f5c3d-147">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-147">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="f5c3d-148">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-148">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="f5c3d-149">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-149">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="f5c3d-150">The following example gets all list operations for storage accounts:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-150">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="f5c3d-151">Use the following Azure CLI command to filter only the list operations:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-151">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="f5c3d-152">Specify the resource by using either the resource name or the [resourceId function](#resourceid).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-152">Specify the resource by using either the resource name or the [resourceId function](#resourceid).</span></span> <span data-ttu-id="f5c3d-153">When using this function in the same template that deploys the referenced resource, use the resource name.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-153">When using this function in the same template that deploys the referenced resource, use the resource name.</span></span>

### <a name="example"></a><span data-ttu-id="f5c3d-154">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-154">Example</span></span>

<span data-ttu-id="f5c3d-155">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/listkeys.json) shows how to return the primary and secondary keys from a storage account in the outputs section.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-155">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/listkeys.json) shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span> <span data-ttu-id="f5c3d-156">It also returns a SAS token for the storage account.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-156">It also returns a SAS token for the storage account.</span></span> <span data-ttu-id="f5c3d-157">To get that token, it passes an object to listAccountSas function.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-157">To get that token, it passes an object to listAccountSas function.</span></span> <span data-ttu-id="f5c3d-158">This example is intended to show how you use the list functions.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-158">This example is intended to show how you use the list functions.</span></span> <span data-ttu-id="f5c3d-159">Typically, you would use the SAS token in a resource value rather than return it as an output value.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-159">Typically, you would use the SAS token in a resource value rather than return it as an output value.</span></span> <span data-ttu-id="f5c3d-160">Output values are stored in the deployment history and aren't secure.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-160">Output values are stored in the deployment history and aren't secure.</span></span> <span data-ttu-id="f5c3d-161">You must specify an expiry time in the future for the deployment to succeed.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-161">You must specify an expiry time in the future for the deployment to succeed.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storagename": {
            "type": "string"
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus"
        },
        "requestContent": {
            "type": "object",
            "defaultValue": {
                "signedServices": "b",
                "signedResourceType": "c",
                "signedPermission": "r",
                "signedExpiry": "2018-08-20T11:00:00Z",
                "signedResourceTypes": "s"
            }
        }
    },
    "resources": [
        {
            "apiVersion": "2018-02-01",
            "name": "[parameters('storagename')]",
            "location": "[parameters('location')]",
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "StorageV2",
            "properties": {
                "supportsHttpsTrafficOnly": false,
                "accessTier": "Hot",
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        },
                        "file": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            },
            "dependsOn": []
        }
    ],
    "outputs": {
        "keys": {
            "type": "object",
            "value": "[listKeys(parameters('storagename'), '2018-02-01')]"
        },
        "accountSAS": {
            "type": "object",
            "value": "[listAccountSas(parameters('storagename'), '2018-02-01', parameters('requestContent'))]"
        }
    }
}
``` 

<span data-ttu-id="f5c3d-162">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-162">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/listkeys.json --parameters storagename=<your-storage-account>
```

<span data-ttu-id="f5c3d-163">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-163">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/listkeys.json -storagename <your-storage-account>
```

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="f5c3d-164">providers</span><span class="sxs-lookup"><span data-stu-id="f5c3d-164">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="f5c3d-165">Returns information about a resource provider and its supported resource types.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-165">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="f5c3d-166">If you don't provide a resource type, the function returns all the supported types for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-166">If you don't provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="f5c3d-167">Parameters</span><span class="sxs-lookup"><span data-stu-id="f5c3d-167">Parameters</span></span>

| <span data-ttu-id="f5c3d-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="f5c3d-168">Parameter</span></span> | <span data-ttu-id="f5c3d-169">Required</span><span class="sxs-lookup"><span data-stu-id="f5c3d-169">Required</span></span> | <span data-ttu-id="f5c3d-170">Type</span><span class="sxs-lookup"><span data-stu-id="f5c3d-170">Type</span></span> | <span data-ttu-id="f5c3d-171">Description</span><span class="sxs-lookup"><span data-stu-id="f5c3d-171">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f5c3d-172">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="f5c3d-172">providerNamespace</span></span> |<span data-ttu-id="f5c3d-173">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-173">Yes</span></span> |<span data-ttu-id="f5c3d-174">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-174">string</span></span> |<span data-ttu-id="f5c3d-175">Namespace of the provider</span><span class="sxs-lookup"><span data-stu-id="f5c3d-175">Namespace of the provider</span></span> |
| <span data-ttu-id="f5c3d-176">resourceType</span><span class="sxs-lookup"><span data-stu-id="f5c3d-176">resourceType</span></span> |<span data-ttu-id="f5c3d-177">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-177">No</span></span> |<span data-ttu-id="f5c3d-178">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-178">string</span></span> |<span data-ttu-id="f5c3d-179">The type of resource within the specified namespace.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-179">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f5c3d-180">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-180">Return value</span></span>

<span data-ttu-id="f5c3d-181">Each supported type is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-181">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="f5c3d-182">Array ordering of the returned values isn't guaranteed.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-182">Array ordering of the returned values isn't guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="f5c3d-183">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-183">Example</span></span>

<span data-ttu-id="f5c3d-184">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/providers.json) shows how to use the provider function:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-184">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/providers.json) shows how to use the provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "providerNamespace": {
            "type": "string"
        },
        "resourceType": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers(parameters('providerNamespace'), parameters('resourceType'))]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f5c3d-185">For the **Microsoft.Web** resource provider and **sites** resource type, the preceding example returns an object in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-185">For the **Microsoft.Web** resource provider and **sites** resource type, the preceding example returns an object in the following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<span data-ttu-id="f5c3d-186">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-186">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/providers.json --parameters providerNamespace=Microsoft.Web resourceType=sites
```

<span data-ttu-id="f5c3d-187">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-187">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/providers.json -providerNamespace Microsoft.Web -resourceType sites
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="f5c3d-188">reference</span><span class="sxs-lookup"><span data-stu-id="f5c3d-188">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion], ['Full'])`

<span data-ttu-id="f5c3d-189">Returns an object representing a resource's runtime state.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-189">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="f5c3d-190">Parameters</span><span class="sxs-lookup"><span data-stu-id="f5c3d-190">Parameters</span></span>

| <span data-ttu-id="f5c3d-191">Parameter</span><span class="sxs-lookup"><span data-stu-id="f5c3d-191">Parameter</span></span> | <span data-ttu-id="f5c3d-192">Required</span><span class="sxs-lookup"><span data-stu-id="f5c3d-192">Required</span></span> | <span data-ttu-id="f5c3d-193">Type</span><span class="sxs-lookup"><span data-stu-id="f5c3d-193">Type</span></span> | <span data-ttu-id="f5c3d-194">Description</span><span class="sxs-lookup"><span data-stu-id="f5c3d-194">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f5c3d-195">resourceName or resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="f5c3d-195">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="f5c3d-196">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-196">Yes</span></span> |<span data-ttu-id="f5c3d-197">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-197">string</span></span> |<span data-ttu-id="f5c3d-198">Name or unique identifier of a resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-198">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="f5c3d-199">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f5c3d-199">apiVersion</span></span> |<span data-ttu-id="f5c3d-200">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-200">No</span></span> |<span data-ttu-id="f5c3d-201">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-201">string</span></span> |<span data-ttu-id="f5c3d-202">API version of the specified resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-202">API version of the specified resource.</span></span> <span data-ttu-id="f5c3d-203">Include this parameter when the resource isn't provisioned within same template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-203">Include this parameter when the resource isn't provisioned within same template.</span></span> <span data-ttu-id="f5c3d-204">Typically, in the format, **yyyy-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-204">Typically, in the format, **yyyy-mm-dd**.</span></span> |
| <span data-ttu-id="f5c3d-205">'Full'</span><span class="sxs-lookup"><span data-stu-id="f5c3d-205">'Full'</span></span> |<span data-ttu-id="f5c3d-206">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-206">No</span></span> |<span data-ttu-id="f5c3d-207">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-207">string</span></span> |<span data-ttu-id="f5c3d-208">Value that specifies whether to return the full resource object.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-208">Value that specifies whether to return the full resource object.</span></span> <span data-ttu-id="f5c3d-209">If you don't specify `'Full'`, only the properties object of the resource is returned.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-209">If you don't specify `'Full'`, only the properties object of the resource is returned.</span></span> <span data-ttu-id="f5c3d-210">The full object includes values such as the resource ID and location.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-210">The full object includes values such as the resource ID and location.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f5c3d-211">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-211">Return value</span></span>

<span data-ttu-id="f5c3d-212">Every resource type returns different properties for the reference function.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-212">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="f5c3d-213">The function doesn't return a single, predefined format.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-213">The function doesn't return a single, predefined format.</span></span> <span data-ttu-id="f5c3d-214">Also, the returned value differs based on whether you specified the full object.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-214">Also, the returned value differs based on whether you specified the full object.</span></span> <span data-ttu-id="f5c3d-215">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-215">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="f5c3d-216">Remarks</span><span class="sxs-lookup"><span data-stu-id="f5c3d-216">Remarks</span></span>

<span data-ttu-id="f5c3d-217">The reference function derives its value from a runtime state, and therefore can't be used in the variables section.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-217">The reference function derives its value from a runtime state, and therefore can't be used in the variables section.</span></span> <span data-ttu-id="f5c3d-218">It can be used in outputs section of a template or [linked template](resource-group-linked-templates.md#link-or-nest-a-template).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-218">It can be used in outputs section of a template or [linked template](resource-group-linked-templates.md#link-or-nest-a-template).</span></span> <span data-ttu-id="f5c3d-219">It can't be used in the outputs section of a [nested template](resource-group-linked-templates.md#link-or-nest-a-template).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-219">It can't be used in the outputs section of a [nested template](resource-group-linked-templates.md#link-or-nest-a-template).</span></span> <span data-ttu-id="f5c3d-220">To return the values for a deployed resource in a nested template, convert your nested template to a linked template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-220">To return the values for a deployed resource in a nested template, convert your nested template to a linked template.</span></span> 

<span data-ttu-id="f5c3d-221">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template and you refer to the resource by its name (not resource ID).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-221">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template and you refer to the resource by its name (not resource ID).</span></span> <span data-ttu-id="f5c3d-222">You don't need to also use the dependsOn property.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-222">You don't need to also use the dependsOn property.</span></span> <span data-ttu-id="f5c3d-223">The function isn't evaluated until the referenced resource has completed deployment.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-223">The function isn't evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="f5c3d-224">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-224">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="f5c3d-225">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-225">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="f5c3d-226">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-226">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

<span data-ttu-id="f5c3d-227">Use `'Full'` when you need resource values that aren't part of the properties schema.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-227">Use `'Full'` when you need resource values that aren't part of the properties schema.</span></span> <span data-ttu-id="f5c3d-228">For example, to set key vault access policies, get the identity properties for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-228">For example, to set key vault access policies, get the identity properties for a virtual machine.</span></span>

```json
{
  "type": "Microsoft.KeyVault/vaults",
  "properties": {
    "tenantId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.tenantId]",
    "accessPolicies": [
      {
        "tenantId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.tenantId]",
        "objectId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.principalId]",
        "permissions": {
          "keys": [
            "all"
          ],
          "secrets": [
            "all"
          ]
        }
      }
    ],
    ...
```

<span data-ttu-id="f5c3d-229">For the complete example of the preceding template, see [Windows to Key Vault](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo08.msiWindowsToKeyvault.json).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-229">For the complete example of the preceding template, see [Windows to Key Vault](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo08.msiWindowsToKeyvault.json).</span></span> <span data-ttu-id="f5c3d-230">A similar example is available for [Linux](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo07.msiLinuxToArm.json).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-230">A similar example is available for [Linux](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo07.msiLinuxToArm.json).</span></span>

### <a name="example"></a><span data-ttu-id="f5c3d-231">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-231">Example</span></span>

<span data-ttu-id="f5c3d-232">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/referencewithstorage.json) deploys a resource, and references that resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-232">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/referencewithstorage.json) deploys a resource, and references that resource.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      },
      "fullReferenceOutput": {
        "type": "object",
        "value": "[reference(parameters('storageAccountName'), '2016-12-01', 'Full')]"
      }
    }
}
``` 

<span data-ttu-id="f5c3d-233">The preceding example returns the two objects.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-233">The preceding example returns the two objects.</span></span> <span data-ttu-id="f5c3d-234">The properties object is in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-234">The properties object is in the following format:</span></span>

```json
{
   "creationTime": "2017-10-09T18:55:40.5863736Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="f5c3d-235">The full object is in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-235">The full object is in the following format:</span></span>

```json
{
  "apiVersion":"2016-12-01",
  "location":"southcentralus",
  "sku": {
    "name":"Standard_LRS",
    "tier":"Standard"
  },
  "tags":{},
  "kind":"Storage",
  "properties": {
    "creationTime":"2017-10-09T18:55:40.5863736Z",
    "primaryEndpoints": {
      "blob":"https://examplestorage.blob.core.windows.net/",
      "file":"https://examplestorage.file.core.windows.net/",
      "queue":"https://examplestorage.queue.core.windows.net/",
      "table":"https://examplestorage.table.core.windows.net/"
    },
    "primaryLocation":"southcentralus",
    "provisioningState":"Succeeded",
    "statusOfPrimary":"available",
    "supportsHttpsTrafficOnly":false
  },
  "subscriptionId":"<subscription-id>",
  "resourceGroupName":"functionexamplegroup",
  "resourceId":"Microsoft.Storage/storageAccounts/examplestorage",
  "referenceApiVersion":"2016-12-01",
  "condition":true,
  "isConditionTrue":true,
  "isTemplateResource":false,
  "isAction":false,
  "provisioningOperation":"Read"
}
```

<span data-ttu-id="f5c3d-236">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-236">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/referencewithstorage.json --parameters storageAccountName=<your-storage-account>
```

<span data-ttu-id="f5c3d-237">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-237">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/referencewithstorage.json -storageAccountName <your-storage-account>
```

<span data-ttu-id="f5c3d-238">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/reference.json) references a storage account that isn't deployed in this template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-238">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/reference.json) references a storage account that isn't deployed in this template.</span></span> <span data-ttu-id="f5c3d-239">The storage account already exists within the same resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-239">The storage account already exists within the same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f5c3d-240">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-240">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/reference.json --parameters storageAccountName=<your-storage-account>
```

<span data-ttu-id="f5c3d-241">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-241">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/reference.json -storageAccountName <your-storage-account>
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="f5c3d-242">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="f5c3d-242">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="f5c3d-243">Returns an object that represents the current resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-243">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="f5c3d-244">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-244">Return value</span></span>

<span data-ttu-id="f5c3d-245">The returned object is in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-245">The returned object is in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="f5c3d-246">Remarks</span><span class="sxs-lookup"><span data-stu-id="f5c3d-246">Remarks</span></span>

<span data-ttu-id="f5c3d-247">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-247">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="f5c3d-248">The following example uses the resource group location to assign the location for a web site.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-248">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="f5c3d-249">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-249">Example</span></span>

<span data-ttu-id="f5c3d-250">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourcegroup.json) returns the properties of the resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-250">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourcegroup.json) returns the properties of the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "resourceGroupOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f5c3d-251">The preceding example returns an object in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-251">The preceding example returns an object in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="f5c3d-252">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-252">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourcegroup.json
```

<span data-ttu-id="f5c3d-253">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-253">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourcegroup.json 
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="f5c3d-254">resourceId</span><span class="sxs-lookup"><span data-stu-id="f5c3d-254">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="f5c3d-255">Returns the unique identifier of a resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-255">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="f5c3d-256">You use this function when the resource name is ambiguous or not provisioned within the same template.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-256">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="f5c3d-257">Parameters</span><span class="sxs-lookup"><span data-stu-id="f5c3d-257">Parameters</span></span>

| <span data-ttu-id="f5c3d-258">Parameter</span><span class="sxs-lookup"><span data-stu-id="f5c3d-258">Parameter</span></span> | <span data-ttu-id="f5c3d-259">Required</span><span class="sxs-lookup"><span data-stu-id="f5c3d-259">Required</span></span> | <span data-ttu-id="f5c3d-260">Type</span><span class="sxs-lookup"><span data-stu-id="f5c3d-260">Type</span></span> | <span data-ttu-id="f5c3d-261">Description</span><span class="sxs-lookup"><span data-stu-id="f5c3d-261">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f5c3d-262">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="f5c3d-262">subscriptionId</span></span> |<span data-ttu-id="f5c3d-263">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-263">No</span></span> |<span data-ttu-id="f5c3d-264">string (In GUID format)</span><span class="sxs-lookup"><span data-stu-id="f5c3d-264">string (In GUID format)</span></span> |<span data-ttu-id="f5c3d-265">Default value is the current subscription.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-265">Default value is the current subscription.</span></span> <span data-ttu-id="f5c3d-266">Specify this value when you need to retrieve a resource in another subscription.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-266">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="f5c3d-267">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f5c3d-267">resourceGroupName</span></span> |<span data-ttu-id="f5c3d-268">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-268">No</span></span> |<span data-ttu-id="f5c3d-269">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-269">string</span></span> |<span data-ttu-id="f5c3d-270">Default value is current resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-270">Default value is current resource group.</span></span> <span data-ttu-id="f5c3d-271">Specify this value when you need to retrieve a resource in another resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-271">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="f5c3d-272">resourceType</span><span class="sxs-lookup"><span data-stu-id="f5c3d-272">resourceType</span></span> |<span data-ttu-id="f5c3d-273">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-273">Yes</span></span> |<span data-ttu-id="f5c3d-274">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-274">string</span></span> |<span data-ttu-id="f5c3d-275">Type of resource including resource provider namespace.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-275">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="f5c3d-276">resourceName1</span><span class="sxs-lookup"><span data-stu-id="f5c3d-276">resourceName1</span></span> |<span data-ttu-id="f5c3d-277">Yes</span><span class="sxs-lookup"><span data-stu-id="f5c3d-277">Yes</span></span> |<span data-ttu-id="f5c3d-278">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-278">string</span></span> |<span data-ttu-id="f5c3d-279">Name of resource.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-279">Name of resource.</span></span> |
| <span data-ttu-id="f5c3d-280">resourceName2</span><span class="sxs-lookup"><span data-stu-id="f5c3d-280">resourceName2</span></span> |<span data-ttu-id="f5c3d-281">No</span><span class="sxs-lookup"><span data-stu-id="f5c3d-281">No</span></span> |<span data-ttu-id="f5c3d-282">string</span><span class="sxs-lookup"><span data-stu-id="f5c3d-282">string</span></span> |<span data-ttu-id="f5c3d-283">Next resource name segment if resource is nested.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-283">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f5c3d-284">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-284">Return value</span></span>

<span data-ttu-id="f5c3d-285">The identifier is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-285">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="f5c3d-286">Remarks</span><span class="sxs-lookup"><span data-stu-id="f5c3d-286">Remarks</span></span>

<span data-ttu-id="f5c3d-287">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-287">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="f5c3d-288">To get the resource ID for a storage account in the same subscription and resource group, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-288">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f5c3d-289">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-289">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f5c3d-290">To get the resource ID for a storage account in a different subscription and resource group, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-290">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="f5c3d-291">To get the resource ID for a database in a different resource group, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-291">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="f5c3d-292">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-292">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="f5c3d-293">The following example shows how a resource from an external resource group can easily be used:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-293">The following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="f5c3d-294">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-294">Example</span></span>

<span data-ttu-id="f5c3d-295">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourceid.json) returns the resource ID for a storage account in the resource group:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-295">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourceid.json) returns the resource ID for a storage account in the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('11111111-1111-1111-1111-111111111111', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="f5c3d-296">The output from the preceding example with the default values is:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-296">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f5c3d-297">Name</span><span class="sxs-lookup"><span data-stu-id="f5c3d-297">Name</span></span> | <span data-ttu-id="f5c3d-298">Type</span><span class="sxs-lookup"><span data-stu-id="f5c3d-298">Type</span></span> | <span data-ttu-id="f5c3d-299">Value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-299">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f5c3d-300">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="f5c3d-300">sameRGOutput</span></span> | <span data-ttu-id="f5c3d-301">String</span><span class="sxs-lookup"><span data-stu-id="f5c3d-301">String</span></span> | <span data-ttu-id="f5c3d-302">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f5c3d-302">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f5c3d-303">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="f5c3d-303">differentRGOutput</span></span> | <span data-ttu-id="f5c3d-304">String</span><span class="sxs-lookup"><span data-stu-id="f5c3d-304">String</span></span> | <span data-ttu-id="f5c3d-305">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f5c3d-305">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f5c3d-306">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="f5c3d-306">differentSubOutput</span></span> | <span data-ttu-id="f5c3d-307">String</span><span class="sxs-lookup"><span data-stu-id="f5c3d-307">String</span></span> | <span data-ttu-id="f5c3d-308">/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="f5c3d-308">/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="f5c3d-309">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="f5c3d-309">nestedResourceOutput</span></span> | <span data-ttu-id="f5c3d-310">String</span><span class="sxs-lookup"><span data-stu-id="f5c3d-310">String</span></span> | <span data-ttu-id="f5c3d-311">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="f5c3d-311">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<span data-ttu-id="f5c3d-312">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-312">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourceid.json
```

<span data-ttu-id="f5c3d-313">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-313">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourceid.json 
```

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="f5c3d-314">subscription</span><span class="sxs-lookup"><span data-stu-id="f5c3d-314">subscription</span></span>
`subscription()`

<span data-ttu-id="f5c3d-315">Returns details about the subscription for the current deployment.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-315">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="f5c3d-316">Return value</span><span class="sxs-lookup"><span data-stu-id="f5c3d-316">Return value</span></span>

<span data-ttu-id="f5c3d-317">The function returns the following format:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-317">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="f5c3d-318">Example</span><span class="sxs-lookup"><span data-stu-id="f5c3d-318">Example</span></span>

<span data-ttu-id="f5c3d-319">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/subscription.json) shows the subscription function called in the outputs section.</span><span class="sxs-lookup"><span data-stu-id="f5c3d-319">The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/subscription.json) shows the subscription function called in the outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="f5c3d-320">To deploy this example template with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-320">To deploy this example template with Azure CLI, use:</span></span>

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/subscription.json
```

<span data-ttu-id="f5c3d-321">To deploy this example template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f5c3d-321">To deploy this example template with PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/subscription.json 
```

## <a name="next-steps"></a><span data-ttu-id="f5c3d-322">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5c3d-322">Next steps</span></span>
* <span data-ttu-id="f5c3d-323">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-323">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f5c3d-324">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-324">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f5c3d-325">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-325">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f5c3d-326">To see how to deploy the template you've created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f5c3d-326">To see how to deploy the template you've created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

