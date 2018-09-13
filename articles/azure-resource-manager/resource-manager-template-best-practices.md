---
title: Best practices for creating Resource Manager templates | Microsoft Docs
description: Guidelines for simplifying your Azure Resource Manager templates.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: 610400830b281a4771578a4f3f75e3d7907f155e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554418"
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="c4312-103">Best practices for creating Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="c4312-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="c4312-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span><span class="sxs-lookup"><span data-stu-id="c4312-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="c4312-105">The guidelines are only suggestions.</span><span class="sxs-lookup"><span data-stu-id="c4312-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="c4312-106">They are not requirements, except where noted.</span><span class="sxs-lookup"><span data-stu-id="c4312-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="c4312-107">Your scenario might require a variation of one of the following approaches or examples.</span><span class="sxs-lookup"><span data-stu-id="c4312-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="c4312-108">Resource names</span><span class="sxs-lookup"><span data-stu-id="c4312-108">Resource names</span></span>
<span data-ttu-id="c4312-109">Generally, you work with three types of resource names in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c4312-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="c4312-110">Resource names that must be unique.</span><span class="sxs-lookup"><span data-stu-id="c4312-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="c4312-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span><span class="sxs-lookup"><span data-stu-id="c4312-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="c4312-112">Resource names that can be generic.</span><span class="sxs-lookup"><span data-stu-id="c4312-112">Resource names that can be generic.</span></span>

<span data-ttu-id="c4312-113">For help establishing a naming convention, see the [Azure infrastructure naming guidelines](../virtual-machines/windows/infrastructure-naming-guidelines.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-113">For help establishing a naming convention, see the [Azure infrastructure naming guidelines](../virtual-machines/windows/infrastructure-naming-guidelines.md).</span></span> <span data-ttu-id="c4312-114">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-114">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="c4312-115">Unique resource names</span><span class="sxs-lookup"><span data-stu-id="c4312-115">Unique resource names</span></span>
<span data-ttu-id="c4312-116">You must provide a unique resource name for any resource type that has a data access endpoint.</span><span class="sxs-lookup"><span data-stu-id="c4312-116">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="c4312-117">Some common resource types that require a unique name include:</span><span class="sxs-lookup"><span data-stu-id="c4312-117">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="c4312-118">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="c4312-118">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="c4312-119">Web Apps feature of Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c4312-119">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="c4312-120">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c4312-120">SQL Server</span></span>
* <span data-ttu-id="c4312-121">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c4312-121">Azure Key Vault</span></span>
* <span data-ttu-id="c4312-122">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="c4312-122">Azure Redis Cache</span></span>
* <span data-ttu-id="c4312-123">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c4312-123">Azure Batch</span></span>
* <span data-ttu-id="c4312-124">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c4312-124">Azure Traffic Manager</span></span>
* <span data-ttu-id="c4312-125">Azure Search</span><span class="sxs-lookup"><span data-stu-id="c4312-125">Azure Search</span></span>
* <span data-ttu-id="c4312-126">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4312-126">Azure HDInsight</span></span>

<span data-ttu-id="c4312-127"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span><span class="sxs-lookup"><span data-stu-id="c4312-127"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="c4312-128">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span><span class="sxs-lookup"><span data-stu-id="c4312-128">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="c4312-129">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions.md#uniquestring) function to generate a name.</span><span class="sxs-lookup"><span data-stu-id="c4312-129">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="c4312-130">You also might want to add a prefix or suffix to the **uniqueString** result.</span><span class="sxs-lookup"><span data-stu-id="c4312-130">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="c4312-131">Modifying the unique name can help you more easily identify the resource type from the name.</span><span class="sxs-lookup"><span data-stu-id="c4312-131">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="c4312-132">For example, you can generate a unique name for a storage account by using the following variable:</span><span class="sxs-lookup"><span data-stu-id="c4312-132">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="c4312-133">Resource names for identification</span><span class="sxs-lookup"><span data-stu-id="c4312-133">Resource names for identification</span></span>
<span data-ttu-id="c4312-134">Some resource types you might want to name, but their names do not have to be unique.</span><span class="sxs-lookup"><span data-stu-id="c4312-134">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="c4312-135">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span><span class="sxs-lookup"><span data-stu-id="c4312-135">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="c4312-136">Provide a descriptive name that helps you identify the resource in a list of resources.</span><span class="sxs-lookup"><span data-stu-id="c4312-136">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="c4312-137">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span><span class="sxs-lookup"><span data-stu-id="c4312-137">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="c4312-138">If you do not need to pass in a name during deployment, you can use a variable:</span><span class="sxs-lookup"><span data-stu-id="c4312-138">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="c4312-139">You also can use a hard-coded value:</span><span class="sxs-lookup"><span data-stu-id="c4312-139">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="c4312-140">Generic resource names</span><span class="sxs-lookup"><span data-stu-id="c4312-140">Generic resource names</span></span>
<span data-ttu-id="c4312-141">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-141">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="c4312-142">For example, you can set a standard, generic name for firewall rules on a SQL server:</span><span class="sxs-lookup"><span data-stu-id="c4312-142">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="c4312-143">Parameters</span><span class="sxs-lookup"><span data-stu-id="c4312-143">Parameters</span></span>
<span data-ttu-id="c4312-144">The following information can be helpful when you work with parameters:</span><span class="sxs-lookup"><span data-stu-id="c4312-144">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="c4312-145">Minimize your use of parameters.</span><span class="sxs-lookup"><span data-stu-id="c4312-145">Minimize your use of parameters.</span></span> <span data-ttu-id="c4312-146">Whenever possible, use a variable or a literal value.</span><span class="sxs-lookup"><span data-stu-id="c4312-146">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="c4312-147">Use parameters only for these scenarios:</span><span class="sxs-lookup"><span data-stu-id="c4312-147">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="c4312-148">Settings that you want to use variations of according to environment (SKU, size, capacity).</span><span class="sxs-lookup"><span data-stu-id="c4312-148">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="c4312-149">Resource names that you want to specify for easy identification.</span><span class="sxs-lookup"><span data-stu-id="c4312-149">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="c4312-150">Values that you use frequently to complete other tasks (such as an admin user name).</span><span class="sxs-lookup"><span data-stu-id="c4312-150">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="c4312-151">Secrets (such as passwords).</span><span class="sxs-lookup"><span data-stu-id="c4312-151">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="c4312-152">The number or array of values to use when you create multiple instances of a resource type.</span><span class="sxs-lookup"><span data-stu-id="c4312-152">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="c4312-153">Use camel case for parameter names.</span><span class="sxs-lookup"><span data-stu-id="c4312-153">Use camel case for parameter names.</span></span>
* <span data-ttu-id="c4312-154">Provide a description of every parameter in the metadata:</span><span class="sxs-lookup"><span data-stu-id="c4312-154">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="c4312-155">Define default values for parameters (except for passwords and SSH keys):</span><span class="sxs-lookup"><span data-stu-id="c4312-155">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="c4312-156">Use **SecureString** for all passwords and secrets:</span><span class="sxs-lookup"><span data-stu-id="c4312-156">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="c4312-157">Whenever possible, don't use a parameter to specify location.</span><span class="sxs-lookup"><span data-stu-id="c4312-157">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="c4312-158">Instead, use the **location** property of the resource group.</span><span class="sxs-lookup"><span data-stu-id="c4312-158">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="c4312-159">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span><span class="sxs-lookup"><span data-stu-id="c4312-159">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="c4312-160">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-160">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="c4312-161">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span><span class="sxs-lookup"><span data-stu-id="c4312-161">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="c4312-162">This minimizes the number of times users are asked to provide location information.</span><span class="sxs-lookup"><span data-stu-id="c4312-162">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="c4312-163">Avoid using a parameter or variable for the API version for a resource type.</span><span class="sxs-lookup"><span data-stu-id="c4312-163">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="c4312-164">Resource properties and values can vary by version number.</span><span class="sxs-lookup"><span data-stu-id="c4312-164">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="c4312-165">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span><span class="sxs-lookup"><span data-stu-id="c4312-165">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="c4312-166">Instead, hard-code the API version in the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-166">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="c4312-167">Variables</span><span class="sxs-lookup"><span data-stu-id="c4312-167">Variables</span></span>
<span data-ttu-id="c4312-168">The following information can be helpful when you work with variables:</span><span class="sxs-lookup"><span data-stu-id="c4312-168">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="c4312-169">Use variables for values that you need to use more than once in a template.</span><span class="sxs-lookup"><span data-stu-id="c4312-169">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="c4312-170">If a value is used only once, a hard-coded value makes your template easier to read.</span><span class="sxs-lookup"><span data-stu-id="c4312-170">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="c4312-171">You cannot use the [reference](resource-group-template-functions.md#reference) function in the **variables** section of the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-171">You cannot use the [reference](resource-group-template-functions.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="c4312-172">The **reference** function derives its value from the resource's runtime state.</span><span class="sxs-lookup"><span data-stu-id="c4312-172">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="c4312-173">However, variables are resolved during the initial parsing of the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-173">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="c4312-174">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-174">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="c4312-175">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="c4312-175">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="c4312-176">You can group variables into complex objects.</span><span class="sxs-lookup"><span data-stu-id="c4312-176">You can group variables into complex objects.</span></span> <span data-ttu-id="c4312-177">Use the **variable.subentry** format to reference a value from a complex object.</span><span class="sxs-lookup"><span data-stu-id="c4312-177">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="c4312-178">Grouping variables can help you track related variables.</span><span class="sxs-lookup"><span data-stu-id="c4312-178">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="c4312-179">It also improves readability of the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-179">It also improves readability of the template.</span></span> <span data-ttu-id="c4312-180">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="c4312-180">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="c4312-181">A complex object cannot contain an expression that references a value from a complex object.</span><span class="sxs-lookup"><span data-stu-id="c4312-181">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="c4312-182">Define a separate variable for this purpose.</span><span class="sxs-lookup"><span data-stu-id="c4312-182">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="c4312-183">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-183">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="c4312-184">Resources</span><span class="sxs-lookup"><span data-stu-id="c4312-184">Resources</span></span>
<span data-ttu-id="c4312-185">The following information can be helpful when you work with resources:</span><span class="sxs-lookup"><span data-stu-id="c4312-185">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="c4312-186">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span><span class="sxs-lookup"><span data-stu-id="c4312-186">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="c4312-187">You can use tags to add metadata to resources.</span><span class="sxs-lookup"><span data-stu-id="c4312-187">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="c4312-188">Use metadata to add information about your resources.</span><span class="sxs-lookup"><span data-stu-id="c4312-188">Use metadata to add information about your resources.</span></span> <span data-ttu-id="c4312-189">For example, you can add metadata to record billing details for a resource.</span><span class="sxs-lookup"><span data-stu-id="c4312-189">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="c4312-190">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-190">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="c4312-191">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span><span class="sxs-lookup"><span data-stu-id="c4312-191">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="c4312-192">Use the **reference** function to dynamically retrieve the namespace.</span><span class="sxs-lookup"><span data-stu-id="c4312-192">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="c4312-193">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span><span class="sxs-lookup"><span data-stu-id="c4312-193">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="c4312-194">Set the API version to the same version that you are using for the storage account in your template:</span><span class="sxs-lookup"><span data-stu-id="c4312-194">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="c4312-195">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span><span class="sxs-lookup"><span data-stu-id="c4312-195">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="c4312-196">This is the simplified syntax:</span><span class="sxs-lookup"><span data-stu-id="c4312-196">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="c4312-197">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span><span class="sxs-lookup"><span data-stu-id="c4312-197">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="c4312-198">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span><span class="sxs-lookup"><span data-stu-id="c4312-198">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="c4312-199">You also can reference an existing storage account that is in a different resource group:</span><span class="sxs-lookup"><span data-stu-id="c4312-199">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="c4312-200">Assign public IP addresses to a virtual machine only when an application requires it.</span><span class="sxs-lookup"><span data-stu-id="c4312-200">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="c4312-201">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span><span class="sxs-lookup"><span data-stu-id="c4312-201">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="c4312-202">For more information about connecting to virtual machines, see:</span><span class="sxs-lookup"><span data-stu-id="c4312-202">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="c4312-203">Run VMs for an N-tier architecture in Azure</span><span class="sxs-lookup"><span data-stu-id="c4312-203">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="c4312-204">Set up WinRM access for VMs in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4312-204">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="c4312-205">Allow external access to your VM by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c4312-205">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="c4312-206">Allow external access to your VM by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4312-206">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="c4312-207">Allow external access to your Linux VM by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4312-207">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="c4312-208">The **domainNameLabel** property for public IP addresses must be unique.</span><span class="sxs-lookup"><span data-stu-id="c4312-208">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="c4312-209">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="c4312-209">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="c4312-210">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span><span class="sxs-lookup"><span data-stu-id="c4312-210">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="c4312-211">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span><span class="sxs-lookup"><span data-stu-id="c4312-211">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="c4312-212">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span><span class="sxs-lookup"><span data-stu-id="c4312-212">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="c4312-213">Outputs</span><span class="sxs-lookup"><span data-stu-id="c4312-213">Outputs</span></span>
<span data-ttu-id="c4312-214">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="c4312-214">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="c4312-215">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span><span class="sxs-lookup"><span data-stu-id="c4312-215">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="c4312-216">When you reference the resource, use the API version that you used to create it:</span><span class="sxs-lookup"><span data-stu-id="c4312-216">When you reference the resource, use the API version that you used to create it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="c4312-217">Single template vs. nested templates</span><span class="sxs-lookup"><span data-stu-id="c4312-217">Single template vs. nested templates</span></span>
<span data-ttu-id="c4312-218">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span><span class="sxs-lookup"><span data-stu-id="c4312-218">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="c4312-219">Nested templates are common for more advanced scenarios.</span><span class="sxs-lookup"><span data-stu-id="c4312-219">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="c4312-220">Using a nested template gives you the following advantages:</span><span class="sxs-lookup"><span data-stu-id="c4312-220">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="c4312-221">You can break down a solution into targeted components.</span><span class="sxs-lookup"><span data-stu-id="c4312-221">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="c4312-222">You can reuse nested templates with different main templates.</span><span class="sxs-lookup"><span data-stu-id="c4312-222">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="c4312-223">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span><span class="sxs-lookup"><span data-stu-id="c4312-223">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="c4312-224">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-224">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="c4312-225">We recommend a design that has the following templates:</span><span class="sxs-lookup"><span data-stu-id="c4312-225">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="c4312-226">**Main template** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c4312-226">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="c4312-227">Use for the input parameters.</span><span class="sxs-lookup"><span data-stu-id="c4312-227">Use for the input parameters.</span></span>
* <span data-ttu-id="c4312-228">**Shared resources template**.</span><span class="sxs-lookup"><span data-stu-id="c4312-228">**Shared resources template**.</span></span> <span data-ttu-id="c4312-229">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span><span class="sxs-lookup"><span data-stu-id="c4312-229">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="c4312-230">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span><span class="sxs-lookup"><span data-stu-id="c4312-230">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="c4312-231">**Optional resources template**.</span><span class="sxs-lookup"><span data-stu-id="c4312-231">**Optional resources template**.</span></span> <span data-ttu-id="c4312-232">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span><span class="sxs-lookup"><span data-stu-id="c4312-232">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="c4312-233">**Member resources template**.</span><span class="sxs-lookup"><span data-stu-id="c4312-233">**Member resources template**.</span></span> <span data-ttu-id="c4312-234">Each instance type within an application tier has its own configuration.</span><span class="sxs-lookup"><span data-stu-id="c4312-234">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="c4312-235">Within a tier, you can define different instance types.</span><span class="sxs-lookup"><span data-stu-id="c4312-235">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="c4312-236">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span><span class="sxs-lookup"><span data-stu-id="c4312-236">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="c4312-237">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="c4312-237">**Scripts**.</span></span> <span data-ttu-id="c4312-238">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span><span class="sxs-lookup"><span data-stu-id="c4312-238">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="c4312-239">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span><span class="sxs-lookup"><span data-stu-id="c4312-239">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Nested template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="c4312-241">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-241">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="c4312-242">Conditionally link to nested templates</span><span class="sxs-lookup"><span data-stu-id="c4312-242">Conditionally link to nested templates</span></span>
<span data-ttu-id="c4312-243">You can use a parameter to conditionally link to nested templates.</span><span class="sxs-lookup"><span data-stu-id="c4312-243">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="c4312-244">The parameter becomes part of the URI for the template:</span><span class="sxs-lookup"><span data-stu-id="c4312-244">The parameter becomes part of the URI for the template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="c4312-245">Template format</span><span class="sxs-lookup"><span data-stu-id="c4312-245">Template format</span></span>
<span data-ttu-id="c4312-246">It's a good practice to pass your template through a JSON validator.</span><span class="sxs-lookup"><span data-stu-id="c4312-246">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="c4312-247">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span><span class="sxs-lookup"><span data-stu-id="c4312-247">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="c4312-248">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="c4312-248">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="c4312-249">It's also a good idea to format your JSON for better readability.</span><span class="sxs-lookup"><span data-stu-id="c4312-249">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="c4312-250">You can use a JSON formatter package for your local editor.</span><span class="sxs-lookup"><span data-stu-id="c4312-250">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="c4312-251">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span><span class="sxs-lookup"><span data-stu-id="c4312-251">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="c4312-252">In Visual Studio Code, press **Alt+Shift+F**.</span><span class="sxs-lookup"><span data-stu-id="c4312-252">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="c4312-253">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="c4312-253">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4312-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4312-254">Next steps</span></span>
* <span data-ttu-id="c4312-255">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-255">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="c4312-256">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-256">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="c4312-257">For help with virtual networks, see the [networking infrastructure guidelines](../virtual-machines/windows/infrastructure-networking-guidelines.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-257">For help with virtual networks, see the [networking infrastructure guidelines](../virtual-machines/windows/infrastructure-networking-guidelines.md).</span></span>
* <span data-ttu-id="c4312-258">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c4312-258">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>


