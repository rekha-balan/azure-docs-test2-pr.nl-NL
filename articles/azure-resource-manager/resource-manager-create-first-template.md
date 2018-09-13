---
title: Create first Azure Resource Manager template | Microsoft Docs
description: A step-by-step guide to creating your first Azure Resource Manager template. It shows you how to use the template reference for a storage account to create the template.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 04/18/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 8298ba5beebeb09360357e2586921eca838896a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551431"
---
# <a name="create-your-first-azure-resource-manager-template"></a><span data-ttu-id="c4907-104">Create your first Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="c4907-104">Create your first Azure Resource Manager template</span></span>
<span data-ttu-id="c4907-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c4907-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="c4907-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span><span class="sxs-lookup"><span data-stu-id="c4907-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="c4907-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4907-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="c4907-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="c4907-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="c4907-109">To create and revise templates, you need a JSON editor.</span><span class="sxs-lookup"><span data-stu-id="c4907-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="c4907-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span><span class="sxs-lookup"><span data-stu-id="c4907-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="c4907-111">It supports creating and editing Resource Manager templates through an extension.</span><span class="sxs-lookup"><span data-stu-id="c4907-111">It supports creating and editing Resource Manager templates through an extension.</span></span> <span data-ttu-id="c4907-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span><span class="sxs-lookup"><span data-stu-id="c4907-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="get-vs-code-and-extension"></a><span data-ttu-id="c4907-113">Get VS Code and extension</span><span class="sxs-lookup"><span data-stu-id="c4907-113">Get VS Code and extension</span></span>
1. <span data-ttu-id="c4907-114">If needed, install VS Code from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c4907-114">If needed, install VS Code from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>

2. <span data-ttu-id="c4907-115">Install the [Azure Resource Manager Tools](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) extension by accessing Quick Open (Ctrl+P) and running:</span><span class="sxs-lookup"><span data-stu-id="c4907-115">Install the [Azure Resource Manager Tools](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) extension by accessing Quick Open (Ctrl+P) and running:</span></span> 

   ```
   ext install msazurermtools.azurerm-vscode-tools
   ```

3. <span data-ttu-id="c4907-116">Restart VS Code when prompted to enable the extension.</span><span class="sxs-lookup"><span data-stu-id="c4907-116">Restart VS Code when prompted to enable the extension.</span></span>

## <a name="create-blank-template"></a><span data-ttu-id="c4907-117">Create blank template</span><span class="sxs-lookup"><span data-stu-id="c4907-117">Create blank template</span></span>

<span data-ttu-id="c4907-118">Let's start with a blank template that includes only the basic sections of a template.</span><span class="sxs-lookup"><span data-stu-id="c4907-118">Let's start with a blank template that includes only the basic sections of a template.</span></span>

1. <span data-ttu-id="c4907-119">Create a file.</span><span class="sxs-lookup"><span data-stu-id="c4907-119">Create a file.</span></span> 

2. <span data-ttu-id="c4907-120">Copy and paste the following JSON syntax into your file:</span><span class="sxs-lookup"><span data-stu-id="c4907-120">Copy and paste the following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {  },
     "variables": {  },
     "resources": [  ],
     "outputs": {  }
   }
   ```

3. <span data-ttu-id="c4907-121">Save this file as **azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="c4907-121">Save this file as **azuredeploy.json**.</span></span> 

## <a name="add-storage-account"></a><span data-ttu-id="c4907-122">Add storage account</span><span class="sxs-lookup"><span data-stu-id="c4907-122">Add storage account</span></span>
1. <span data-ttu-id="c4907-123">To define a storage account for deployment, you add that storage account to the **resources** section of your template.</span><span class="sxs-lookup"><span data-stu-id="c4907-123">To define a storage account for deployment, you add that storage account to the **resources** section of your template.</span></span> <span data-ttu-id="c4907-124">To find the values that are available for the storage account, look at the [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="c4907-124">To find the values that are available for the storage account, look at the [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span> <span data-ttu-id="c4907-125">Copy the JSON that is shown for the storage account.</span><span class="sxs-lookup"><span data-stu-id="c4907-125">Copy the JSON that is shown for the storage account.</span></span> 

3. <span data-ttu-id="c4907-126">Paste that JSON into the **resources** section of your template, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c4907-126">Paste that JSON into the **resources** section of your template, as shown in the following example:</span></span> 

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {  },
     "variables": {  },
     "resources": [
       {
         "name": "string",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-05-01",
         "sku": {
           "name": "string"
         },
         "kind": "string",
         "location": "string",
         "tags": {},
         "properties": {
           "customDomain": {
             "name": "string",
             "useSubDomain": boolean
           },
           "encryption": {
             "services": {
               "blob": {
                 "enabled": boolean
               }
             },
             "keySource": "Microsoft.Storage"
           },
           "accessTier": "string"
         }
       }
     ],
     "outputs": {  }
   }
   ```

  <span data-ttu-id="c4907-127">The preceding example includes many placeholder values and some properties that you might not need in your storage account.</span><span class="sxs-lookup"><span data-stu-id="c4907-127">The preceding example includes many placeholder values and some properties that you might not need in your storage account.</span></span>

## <a name="set-values-for-storage-account"></a><span data-ttu-id="c4907-128">Set values for storage account</span><span class="sxs-lookup"><span data-stu-id="c4907-128">Set values for storage account</span></span>

<span data-ttu-id="c4907-129">Now, you are ready to set values for your storage account.</span><span class="sxs-lookup"><span data-stu-id="c4907-129">Now, you are ready to set values for your storage account.</span></span> 

1. <span data-ttu-id="c4907-130">Look again at the [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts) where you copied the JSON.</span><span class="sxs-lookup"><span data-stu-id="c4907-130">Look again at the [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts) where you copied the JSON.</span></span> <span data-ttu-id="c4907-131">There are several tables that describe the properties and provide available values.</span><span class="sxs-lookup"><span data-stu-id="c4907-131">There are several tables that describe the properties and provide available values.</span></span> 

2. <span data-ttu-id="c4907-132">Notice that within the **properties** element, **customDomain**, **encryption**, and **accessTier** are all listed as not required.</span><span class="sxs-lookup"><span data-stu-id="c4907-132">Notice that within the **properties** element, **customDomain**, **encryption**, and **accessTier** are all listed as not required.</span></span> <span data-ttu-id="c4907-133">These values may be important for your scenarios, but to keep this example simple, let's remove them.</span><span class="sxs-lookup"><span data-stu-id="c4907-133">These values may be important for your scenarios, but to keep this example simple, let's remove them.</span></span>

   ```json
   "resources": [
     {
       "name": "string",
       "type": "Microsoft.Storage/storageAccounts",
       "apiVersion": "2016-05-01",
       "sku": {
         "name": "string"
       },
       "kind": "string",
       "location": "string",
       "tags": {},
       "properties": {
       }
     }
   ],
   ```

3. <span data-ttu-id="c4907-134">Currently, the **kind** element is set to a placeholder value ("string").</span><span class="sxs-lookup"><span data-stu-id="c4907-134">Currently, the **kind** element is set to a placeholder value ("string").</span></span> <span data-ttu-id="c4907-135">VS Code includes many features that help you understand the values to use in your template.</span><span class="sxs-lookup"><span data-stu-id="c4907-135">VS Code includes many features that help you understand the values to use in your template.</span></span> <span data-ttu-id="c4907-136">Notice that VS Code indicates this value is not valid.</span><span class="sxs-lookup"><span data-stu-id="c4907-136">Notice that VS Code indicates this value is not valid.</span></span> <span data-ttu-id="c4907-137">If you hover over "string", VS Code suggests that the valid values for **kind** are `Storage` or `BlobStorage`.</span><span class="sxs-lookup"><span data-stu-id="c4907-137">If you hover over "string", VS Code suggests that the valid values for **kind** are `Storage` or `BlobStorage`.</span></span> 

   ![show VS Code suggested values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-create-first-template/vs-code-show-values.png)

   <span data-ttu-id="c4907-139">To see the available values, delete the characters between the double-quotes and select **Ctrl+Space**.</span><span class="sxs-lookup"><span data-stu-id="c4907-139">To see the available values, delete the characters between the double-quotes and select **Ctrl+Space**.</span></span> <span data-ttu-id="c4907-140">Select **Storage** from the available options.</span><span class="sxs-lookup"><span data-stu-id="c4907-140">Select **Storage** from the available options.</span></span>
  
   ![show intellisense](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-create-first-template/intellisense.png)

   <span data-ttu-id="c4907-142">If you are not using VS Code, look at the storage accounts template reference page.</span><span class="sxs-lookup"><span data-stu-id="c4907-142">If you are not using VS Code, look at the storage accounts template reference page.</span></span> <span data-ttu-id="c4907-143">Notice that the description lists the same valid values.</span><span class="sxs-lookup"><span data-stu-id="c4907-143">Notice that the description lists the same valid values.</span></span> <span data-ttu-id="c4907-144">Set the element to **Storage**.</span><span class="sxs-lookup"><span data-stu-id="c4907-144">Set the element to **Storage**.</span></span>

   ```json
   "kind": "Storage",
   ```

<span data-ttu-id="c4907-145">Your template now looks like:</span><span class="sxs-lookup"><span data-stu-id="c4907-145">Your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {  },
  "variables": {  },
  "resources": [
    {
      "name": "string",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "string"
      },
      "kind": "Storage",
      "location": "string",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="add-template-function"></a><span data-ttu-id="c4907-146">Add template function</span><span class="sxs-lookup"><span data-stu-id="c4907-146">Add template function</span></span>

<span data-ttu-id="c4907-147">You use functions within your template to simplify the syntax of the template, and to retrieve values that are only available when the template is being deployed.</span><span class="sxs-lookup"><span data-stu-id="c4907-147">You use functions within your template to simplify the syntax of the template, and to retrieve values that are only available when the template is being deployed.</span></span> <span data-ttu-id="c4907-148">For the full set of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c4907-148">For the full set of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span>

<span data-ttu-id="c4907-149">To specify that the storage account is deployed to the same location as the resource group, set the **location** property to:</span><span class="sxs-lookup"><span data-stu-id="c4907-149">To specify that the storage account is deployed to the same location as the resource group, set the **location** property to:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="c4907-150">Again, VS Code helps you by suggesting available functions.</span><span class="sxs-lookup"><span data-stu-id="c4907-150">Again, VS Code helps you by suggesting available functions.</span></span> 

![show functions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-create-first-template/show-functions.png)

<span data-ttu-id="c4907-152">Notice that the function is surrounded by square brackets.</span><span class="sxs-lookup"><span data-stu-id="c4907-152">Notice that the function is surrounded by square brackets.</span></span> <span data-ttu-id="c4907-153">The [resourceGroup](resource-group-template-functions.md#resourcegroup) function returns an object with a property called `location`.</span><span class="sxs-lookup"><span data-stu-id="c4907-153">The [resourceGroup](resource-group-template-functions.md#resourcegroup) function returns an object with a property called `location`.</span></span> <span data-ttu-id="c4907-154">The resource group holds all related resources for your solution.</span><span class="sxs-lookup"><span data-stu-id="c4907-154">The resource group holds all related resources for your solution.</span></span> <span data-ttu-id="c4907-155">You could hardcode the location property to a value like "Central US" but you would have to manually change the template to redeploy to a different location.</span><span class="sxs-lookup"><span data-stu-id="c4907-155">You could hardcode the location property to a value like "Central US" but you would have to manually change the template to redeploy to a different location.</span></span> <span data-ttu-id="c4907-156">Using the `resourceGroup` function, makes it easy to redeploy this template to a different resource group in a different location.</span><span class="sxs-lookup"><span data-stu-id="c4907-156">Using the `resourceGroup` function, makes it easy to redeploy this template to a different resource group in a different location.</span></span>

<span data-ttu-id="c4907-157">Your template now looks like:</span><span class="sxs-lookup"><span data-stu-id="c4907-157">Your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {  },
  "variables": {  },
  "resources": [
    {
      "name": "string",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "string"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="add-parameters-and-variables"></a><span data-ttu-id="c4907-158">Add parameters and variables</span><span class="sxs-lookup"><span data-stu-id="c4907-158">Add parameters and variables</span></span>
<span data-ttu-id="c4907-159">There are only two values left to set in your template - **name** and **sku.name**.</span><span class="sxs-lookup"><span data-stu-id="c4907-159">There are only two values left to set in your template - **name** and **sku.name**.</span></span> <span data-ttu-id="c4907-160">For these properties, you add parameters that enable you to customize these values during deployment.</span><span class="sxs-lookup"><span data-stu-id="c4907-160">For these properties, you add parameters that enable you to customize these values during deployment.</span></span> 

<span data-ttu-id="c4907-161">Storage account names have several restrictions that make them difficult to set.</span><span class="sxs-lookup"><span data-stu-id="c4907-161">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="c4907-162">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span><span class="sxs-lookup"><span data-stu-id="c4907-162">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="c4907-163">Rather than trying to guess a unique value that matches the restrictions, use the [uniqueString](resource-group-template-functions.md#uniquestring) function to generate a hash value.</span><span class="sxs-lookup"><span data-stu-id="c4907-163">Rather than trying to guess a unique value that matches the restrictions, use the [uniqueString](resource-group-template-functions.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="c4907-164">To give this hash value more meaning, add a prefix that helps you identify it as a storage account after deployment.</span><span class="sxs-lookup"><span data-stu-id="c4907-164">To give this hash value more meaning, add a prefix that helps you identify it as a storage account after deployment.</span></span> 

1. <span data-ttu-id="c4907-165">To pass in a prefix for the name that matches your naming conventions, go to the **parameters** section of your template.</span><span class="sxs-lookup"><span data-stu-id="c4907-165">To pass in a prefix for the name that matches your naming conventions, go to the **parameters** section of your template.</span></span> <span data-ttu-id="c4907-166">Add a parameter to the template that accepts a prefix for the storage account name:</span><span class="sxs-lookup"><span data-stu-id="c4907-166">Add a parameter to the template that accepts a prefix for the storage account name:</span></span>

   ```json
   "parameters": {
     "storageNamePrefix": {
       "type": "string",
       "maxLength": 11,
       "defaultValue": "storage",
       "metadata": {
         "description": "The value to use for starting the storage account name."
       }
     }
   },
   ```

  <span data-ttu-id="c4907-167">The prefix is limited to a maximum of 11 characters because `uniqueString` returns 13 characters, and the name cannot exceed 24 characters.</span><span class="sxs-lookup"><span data-stu-id="c4907-167">The prefix is limited to a maximum of 11 characters because `uniqueString` returns 13 characters, and the name cannot exceed 24 characters.</span></span> <span data-ttu-id="c4907-168">If you do not pass in a value for the parameter during deployment, the default value is used.</span><span class="sxs-lookup"><span data-stu-id="c4907-168">If you do not pass in a value for the parameter during deployment, the default value is used.</span></span>

2. <span data-ttu-id="c4907-169">Go to the **variables** section of the template.</span><span class="sxs-lookup"><span data-stu-id="c4907-169">Go to the **variables** section of the template.</span></span> <span data-ttu-id="c4907-170">To construct the name from the prefix and unique string, add the following variable:</span><span class="sxs-lookup"><span data-stu-id="c4907-170">To construct the name from the prefix and unique string, add the following variable:</span></span>

   ```json
   "variables": {
     "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
   },
   ```

3. <span data-ttu-id="c4907-171">In the **resources** section, set the storage account name to that variable.</span><span class="sxs-lookup"><span data-stu-id="c4907-171">In the **resources** section, set the storage account name to that variable.</span></span>

   ```json
   "name": "[variables('storageName')]",
   ```

3. <span data-ttu-id="c4907-172">To enable passing in different SKUs for the storage account, go to the **parameters** section.</span><span class="sxs-lookup"><span data-stu-id="c4907-172">To enable passing in different SKUs for the storage account, go to the **parameters** section.</span></span> <span data-ttu-id="c4907-173">After the parameter for storage name prefix, add a parameter that specifies the allowed SKU values and a default value.</span><span class="sxs-lookup"><span data-stu-id="c4907-173">After the parameter for storage name prefix, add a parameter that specifies the allowed SKU values and a default value.</span></span> <span data-ttu-id="c4907-174">You can find the allowed values from either the template reference page or VS Code.</span><span class="sxs-lookup"><span data-stu-id="c4907-174">You can find the allowed values from either the template reference page or VS Code.</span></span> <span data-ttu-id="c4907-175">In the following example, you include all valid values for SKU.</span><span class="sxs-lookup"><span data-stu-id="c4907-175">In the following example, you include all valid values for SKU.</span></span> <span data-ttu-id="c4907-176">However, you could limit the allowed values to only those types of SKUs that you want to deploy through this template.</span><span class="sxs-lookup"><span data-stu-id="c4907-176">However, you could limit the allowed values to only those types of SKUs that you want to deploy through this template.</span></span>

   ```json
   "parameters": {
     "storageNamePrefix": {
       "type": "string",
       "maxLength": 11,
       "defaultValue": "storage",
       "metadata": {
         "description": "The value to use for starting the storage account name."
       }
     },
     "storageSKU": {
       "type": "string",
       "allowedValues": [
         "Standard_LRS",
         "Standard_ZRS",
         "Standard_GRS",
         "Standard_RAGRS",
         "Premium_LRS"
       ],
       "defaultValue": "Standard_LRS",
       "metadata": {
         "description": "The type of replication to use for the storage account."
       }
     }
   },
   ```

3. <span data-ttu-id="c4907-177">Change the SKU property to use the value from the parameter:</span><span class="sxs-lookup"><span data-stu-id="c4907-177">Change the SKU property to use the value from the parameter:</span></span>

   ```json
   "sku": {
     "name": "[parameters('storageSKU')]"
   },
   ```    

4. <span data-ttu-id="c4907-178">Save your file.</span><span class="sxs-lookup"><span data-stu-id="c4907-178">Save your file.</span></span>

## <a name="final-template"></a><span data-ttu-id="c4907-179">Final template</span><span class="sxs-lookup"><span data-stu-id="c4907-179">Final template</span></span>

<span data-ttu-id="c4907-180">After completing the steps in this article, your template now looks like:</span><span class="sxs-lookup"><span data-stu-id="c4907-180">After completing the steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="c4907-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4907-181">Next steps</span></span>
* <span data-ttu-id="c4907-182">Your template is complete, and you are ready to deploy it to your subscription.</span><span class="sxs-lookup"><span data-stu-id="c4907-182">Your template is complete, and you are ready to deploy it to your subscription.</span></span> <span data-ttu-id="c4907-183">To deploy, see [Deploy resources to Azure](resource-manager-quickstart-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c4907-183">To deploy, see [Deploy resources to Azure](resource-manager-quickstart-deploy.md).</span></span>
* <span data-ttu-id="c4907-184">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c4907-184">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c4907-185">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="c4907-185">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>



