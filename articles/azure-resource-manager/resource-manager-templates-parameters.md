---
title: Azure Resource Manager template parameter section | Microsoft Docs
description: Describes the parameters section of Azure Resource Manager templates using declarative JSON syntax.
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
ms.date: 05/18/2018
ms.author: tomfitz
ms.openlocfilehash: 6d09a057d9b8a02c7f8313161e64aa3a42eb6db2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869153"
---
# <a name="parameters-section-of-azure-resource-manager-templates"></a><span data-ttu-id="93f43-103">Parameters section of Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="93f43-103">Parameters section of Azure Resource Manager templates</span></span>
<span data-ttu-id="93f43-104">In the parameters section of the template, you specify which values you can input when deploying the resources.</span><span class="sxs-lookup"><span data-stu-id="93f43-104">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="93f43-105">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span><span class="sxs-lookup"><span data-stu-id="93f43-105">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="93f43-106">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span><span class="sxs-lookup"><span data-stu-id="93f43-106">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="93f43-107">You are limited to 255 parameters in a template.</span><span class="sxs-lookup"><span data-stu-id="93f43-107">You are limited to 255 parameters in a template.</span></span> <span data-ttu-id="93f43-108">You can reduce the number of parameters by using objects that contain multiple properties, as shown in this article.</span><span class="sxs-lookup"><span data-stu-id="93f43-108">You can reduce the number of parameters by using objects that contain multiple properties, as shown in this article.</span></span>

## <a name="define-and-use-a-parameter"></a><span data-ttu-id="93f43-109">Define and use a parameter</span><span class="sxs-lookup"><span data-stu-id="93f43-109">Define and use a parameter</span></span>

<span data-ttu-id="93f43-110">The following example shows a simple parameter definition.</span><span class="sxs-lookup"><span data-stu-id="93f43-110">The following example shows a simple parameter definition.</span></span> <span data-ttu-id="93f43-111">It defines the name of the parameter, and specifies that it takes a string value.</span><span class="sxs-lookup"><span data-stu-id="93f43-111">It defines the name of the parameter, and specifies that it takes a string value.</span></span> <span data-ttu-id="93f43-112">The parameter only accepts values that make sense for its intended use.</span><span class="sxs-lookup"><span data-stu-id="93f43-112">The parameter only accepts values that make sense for its intended use.</span></span> <span data-ttu-id="93f43-113">It specifies a default value when no value is provided during deployment.</span><span class="sxs-lookup"><span data-stu-id="93f43-113">It specifies a default value when no value is provided during deployment.</span></span> <span data-ttu-id="93f43-114">Finally, the parameter includes a description of its use.</span><span class="sxs-lookup"><span data-stu-id="93f43-114">Finally, the parameter includes a description of its use.</span></span> 

```json
"parameters": {
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
}
```

<span data-ttu-id="93f43-115">In the template, you reference the value for the parameter with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="93f43-115">In the template, you reference the value for the parameter with the following syntax:</span></span>

```json
"resources": [
  {
    "type": "Microsoft.Storage/storageAccounts",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    ...
  }
]
```

## <a name="available-properties"></a><span data-ttu-id="93f43-116">Available properties</span><span class="sxs-lookup"><span data-stu-id="93f43-116">Available properties</span></span>

<span data-ttu-id="93f43-117">The preceding example showed only some of the properties you can use in the parameter section.</span><span class="sxs-lookup"><span data-stu-id="93f43-117">The preceding example showed only some of the properties you can use in the parameter section.</span></span> <span data-ttu-id="93f43-118">The available properties are:</span><span class="sxs-lookup"><span data-stu-id="93f43-118">The available properties are:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="93f43-119">Element name</span><span class="sxs-lookup"><span data-stu-id="93f43-119">Element name</span></span> | <span data-ttu-id="93f43-120">Required</span><span class="sxs-lookup"><span data-stu-id="93f43-120">Required</span></span> | <span data-ttu-id="93f43-121">Description</span><span class="sxs-lookup"><span data-stu-id="93f43-121">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93f43-122">parameterName</span><span class="sxs-lookup"><span data-stu-id="93f43-122">parameterName</span></span> |<span data-ttu-id="93f43-123">Yes</span><span class="sxs-lookup"><span data-stu-id="93f43-123">Yes</span></span> |<span data-ttu-id="93f43-124">Name of the parameter.</span><span class="sxs-lookup"><span data-stu-id="93f43-124">Name of the parameter.</span></span> <span data-ttu-id="93f43-125">Must be a valid JavaScript identifier.</span><span class="sxs-lookup"><span data-stu-id="93f43-125">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="93f43-126">type</span><span class="sxs-lookup"><span data-stu-id="93f43-126">type</span></span> |<span data-ttu-id="93f43-127">Yes</span><span class="sxs-lookup"><span data-stu-id="93f43-127">Yes</span></span> |<span data-ttu-id="93f43-128">Type of the parameter value.</span><span class="sxs-lookup"><span data-stu-id="93f43-128">Type of the parameter value.</span></span> <span data-ttu-id="93f43-129">The allowed types and values are **string**, **securestring**, **int**, **bool**, **object**, **secureObject**, and **array**.</span><span class="sxs-lookup"><span data-stu-id="93f43-129">The allowed types and values are **string**, **securestring**, **int**, **bool**, **object**, **secureObject**, and **array**.</span></span> |
| <span data-ttu-id="93f43-130">defaultValue</span><span class="sxs-lookup"><span data-stu-id="93f43-130">defaultValue</span></span> |<span data-ttu-id="93f43-131">No</span><span class="sxs-lookup"><span data-stu-id="93f43-131">No</span></span> |<span data-ttu-id="93f43-132">Default value for the parameter, if no value is provided for the parameter.</span><span class="sxs-lookup"><span data-stu-id="93f43-132">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="93f43-133">allowedValues</span><span class="sxs-lookup"><span data-stu-id="93f43-133">allowedValues</span></span> |<span data-ttu-id="93f43-134">No</span><span class="sxs-lookup"><span data-stu-id="93f43-134">No</span></span> |<span data-ttu-id="93f43-135">Array of allowed values for the parameter to make sure that the right value is provided.</span><span class="sxs-lookup"><span data-stu-id="93f43-135">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="93f43-136">minValue</span><span class="sxs-lookup"><span data-stu-id="93f43-136">minValue</span></span> |<span data-ttu-id="93f43-137">No</span><span class="sxs-lookup"><span data-stu-id="93f43-137">No</span></span> |<span data-ttu-id="93f43-138">The minimum value for int type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="93f43-138">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="93f43-139">maxValue</span><span class="sxs-lookup"><span data-stu-id="93f43-139">maxValue</span></span> |<span data-ttu-id="93f43-140">No</span><span class="sxs-lookup"><span data-stu-id="93f43-140">No</span></span> |<span data-ttu-id="93f43-141">The maximum value for int type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="93f43-141">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="93f43-142">minLength</span><span class="sxs-lookup"><span data-stu-id="93f43-142">minLength</span></span> |<span data-ttu-id="93f43-143">No</span><span class="sxs-lookup"><span data-stu-id="93f43-143">No</span></span> |<span data-ttu-id="93f43-144">The minimum length for string, securestring, and array type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="93f43-144">The minimum length for string, securestring, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="93f43-145">maxLength</span><span class="sxs-lookup"><span data-stu-id="93f43-145">maxLength</span></span> |<span data-ttu-id="93f43-146">No</span><span class="sxs-lookup"><span data-stu-id="93f43-146">No</span></span> |<span data-ttu-id="93f43-147">The maximum length for string, securestring, and array type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="93f43-147">The maximum length for string, securestring, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="93f43-148">description</span><span class="sxs-lookup"><span data-stu-id="93f43-148">description</span></span> |<span data-ttu-id="93f43-149">No</span><span class="sxs-lookup"><span data-stu-id="93f43-149">No</span></span> |<span data-ttu-id="93f43-150">Description of the parameter that is displayed to users through the portal.</span><span class="sxs-lookup"><span data-stu-id="93f43-150">Description of the parameter that is displayed to users through the portal.</span></span> |

## <a name="template-functions-with-parameters"></a><span data-ttu-id="93f43-151">Template functions with parameters</span><span class="sxs-lookup"><span data-stu-id="93f43-151">Template functions with parameters</span></span>

<span data-ttu-id="93f43-152">When providing the default value for a parameter, you can use most template functions.</span><span class="sxs-lookup"><span data-stu-id="93f43-152">When providing the default value for a parameter, you can use most template functions.</span></span> <span data-ttu-id="93f43-153">You can use another parameter value to build a default value.</span><span class="sxs-lookup"><span data-stu-id="93f43-153">You can use another parameter value to build a default value.</span></span> <span data-ttu-id="93f43-154">The following template demonstrates the use of functions in the default value:</span><span class="sxs-lookup"><span data-stu-id="93f43-154">The following template demonstrates the use of functions in the default value:</span></span>

```json
"parameters": {
  "siteName": {
    "type": "string",
    "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]",
    "metadata": {
      "description": "The site name. To use the default value, do not specify a new value."
    }
  },
  "hostingPlanName": {
    "type": "string",
    "defaultValue": "[concat(parameters('siteName'),'-plan')]",
    "metadata": {
      "description": "The host name. To use the default value, do not specify a new value."
    }
  }
}
```

<span data-ttu-id="93f43-155">You cannot use the `reference` function in the parameters section.</span><span class="sxs-lookup"><span data-stu-id="93f43-155">You cannot use the `reference` function in the parameters section.</span></span> <span data-ttu-id="93f43-156">Parameters are evaluated before deployment so the `reference` function cannot obtain the runtime state of a resource.</span><span class="sxs-lookup"><span data-stu-id="93f43-156">Parameters are evaluated before deployment so the `reference` function cannot obtain the runtime state of a resource.</span></span> 

## <a name="objects-as-parameters"></a><span data-ttu-id="93f43-157">Objects as parameters</span><span class="sxs-lookup"><span data-stu-id="93f43-157">Objects as parameters</span></span>

<span data-ttu-id="93f43-158">It can be easier to organize related values by passing them in as an object.</span><span class="sxs-lookup"><span data-stu-id="93f43-158">It can be easier to organize related values by passing them in as an object.</span></span> <span data-ttu-id="93f43-159">This approach also reduces the number of parameters in the template.</span><span class="sxs-lookup"><span data-stu-id="93f43-159">This approach also reduces the number of parameters in the template.</span></span>

<span data-ttu-id="93f43-160">Define the parameter in your template and specify a JSON object instead of a single value during deployment.</span><span class="sxs-lookup"><span data-stu-id="93f43-160">Define the parameter in your template and specify a JSON object instead of a single value during deployment.</span></span> 

```json
"parameters": {
  "VNetSettings": {
    "type": "object",
    "defaultValue": {
      "name": "VNet1",
      "location": "eastus",
      "addressPrefixes": [
        {
          "name": "firstPrefix",
          "addressPrefix": "10.0.0.0/22"
        }
      ],
      "subnets": [
        {
          "name": "firstSubnet",
          "addressPrefix": "10.0.0.0/24"
        },
        {
          "name": "secondSubnet",
          "addressPrefix": "10.0.1.0/24"
        }
      ]
    }
  }
},
```

<span data-ttu-id="93f43-161">Then, reference the subproperties of the parameter by using the dot operator.</span><span class="sxs-lookup"><span data-stu-id="93f43-161">Then, reference the subproperties of the parameter by using the dot operator.</span></span>

```json
"resources": [
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('VNetSettings').name]",
    "location": "[parameters('VNetSettings').location]",
    "properties": {
      "addressSpace":{
        "addressPrefixes": [
          "[parameters('VNetSettings').addressPrefixes[0].addressPrefix]"
        ]
      },
      "subnets":[
        {
          "name":"[parameters('VNetSettings').subnets[0].name]",
          "properties": {
            "addressPrefix": "[parameters('VNetSettings').subnets[0].addressPrefix]"
          }
        },
        {
          "name":"[parameters('VNetSettings').subnets[1].name]",
          "properties": {
            "addressPrefix": "[parameters('VNetSettings').subnets[1].addressPrefix]"
          }
        }
      ]
    }
  }
]
```

## <a name="recommendations"></a><span data-ttu-id="93f43-162">Recommendations</span><span class="sxs-lookup"><span data-stu-id="93f43-162">Recommendations</span></span>
<span data-ttu-id="93f43-163">The following information can be helpful when you work with parameters:</span><span class="sxs-lookup"><span data-stu-id="93f43-163">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="93f43-164">Minimize your use of parameters.</span><span class="sxs-lookup"><span data-stu-id="93f43-164">Minimize your use of parameters.</span></span> <span data-ttu-id="93f43-165">Whenever possible, use a variable or a literal value.</span><span class="sxs-lookup"><span data-stu-id="93f43-165">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="93f43-166">Use parameters only for these scenarios:</span><span class="sxs-lookup"><span data-stu-id="93f43-166">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="93f43-167">Settings that you want to use variations of according to environment (SKU, size, capacity).</span><span class="sxs-lookup"><span data-stu-id="93f43-167">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="93f43-168">Resource names that you want to specify for easy identification.</span><span class="sxs-lookup"><span data-stu-id="93f43-168">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="93f43-169">Values that you use frequently to complete other tasks (such as an admin user name).</span><span class="sxs-lookup"><span data-stu-id="93f43-169">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="93f43-170">Secrets (such as passwords).</span><span class="sxs-lookup"><span data-stu-id="93f43-170">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="93f43-171">The number or array of values to use when you create multiple instances of a resource type.</span><span class="sxs-lookup"><span data-stu-id="93f43-171">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="93f43-172">Use camel case for parameter names.</span><span class="sxs-lookup"><span data-stu-id="93f43-172">Use camel case for parameter names.</span></span>
* <span data-ttu-id="93f43-173">Provide a description of every parameter in the metadata:</span><span class="sxs-lookup"><span data-stu-id="93f43-173">Provide a description of every parameter in the metadata:</span></span>

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

* <span data-ttu-id="93f43-174">Define default values for parameters (except for passwords and SSH keys).</span><span class="sxs-lookup"><span data-stu-id="93f43-174">Define default values for parameters (except for passwords and SSH keys).</span></span> <span data-ttu-id="93f43-175">By providing a default value, the parameter becomes optional during deployment.</span><span class="sxs-lookup"><span data-stu-id="93f43-175">By providing a default value, the parameter becomes optional during deployment.</span></span> <span data-ttu-id="93f43-176">The default value can be an empty string.</span><span class="sxs-lookup"><span data-stu-id="93f43-176">The default value can be an empty string.</span></span> 
   
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

* <span data-ttu-id="93f43-177">Use **securestring** for all passwords and secrets.</span><span class="sxs-lookup"><span data-stu-id="93f43-177">Use **securestring** for all passwords and secrets.</span></span> <span data-ttu-id="93f43-178">If you pass sensitive data in a JSON object, use the **secureObject** type.</span><span class="sxs-lookup"><span data-stu-id="93f43-178">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="93f43-179">Template parameters with securestring or secureObject types cannot be read after resource deployment.</span><span class="sxs-lookup"><span data-stu-id="93f43-179">Template parameters with securestring or secureObject types cannot be read after resource deployment.</span></span> 
   
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

* <span data-ttu-id="93f43-180">Use a parameter to specify location, and share that parameter value as much as possible with resources that are likely to be in the same location.</span><span class="sxs-lookup"><span data-stu-id="93f43-180">Use a parameter to specify location, and share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="93f43-181">This approach minimizes the number of times users are asked to provide location information.</span><span class="sxs-lookup"><span data-stu-id="93f43-181">This approach minimizes the number of times users are asked to provide location information.</span></span> <span data-ttu-id="93f43-182">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template, or add another location parameter.</span><span class="sxs-lookup"><span data-stu-id="93f43-182">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template, or add another location parameter.</span></span> <span data-ttu-id="93f43-183">When an organization limits the allowed regions for its users, the **resourceGroup().location** expression might prevent a user from being able to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="93f43-183">When an organization limits the allowed regions for its users, the **resourceGroup().location** expression might prevent a user from being able to deploy the template.</span></span> <span data-ttu-id="93f43-184">For example, one user creates a resource group in a region.</span><span class="sxs-lookup"><span data-stu-id="93f43-184">For example, one user creates a resource group in a region.</span></span> <span data-ttu-id="93f43-185">A second user must deploy to that resource group but does not have access to the region.</span><span class="sxs-lookup"><span data-stu-id="93f43-185">A second user must deploy to that resource group but does not have access to the region.</span></span> 
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[parameters('location')]",
         ...
     }
   ]
   ```
    
* <span data-ttu-id="93f43-186">Avoid using a parameter or variable for the API version for a resource type.</span><span class="sxs-lookup"><span data-stu-id="93f43-186">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="93f43-187">Resource properties and values can vary by version number.</span><span class="sxs-lookup"><span data-stu-id="93f43-187">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="93f43-188">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span><span class="sxs-lookup"><span data-stu-id="93f43-188">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="93f43-189">Instead, hard-code the API version in the template.</span><span class="sxs-lookup"><span data-stu-id="93f43-189">Instead, hard-code the API version in the template.</span></span>
* <span data-ttu-id="93f43-190">Avoid specifying a parameter name in your template that matches a parameter in the deployment command.</span><span class="sxs-lookup"><span data-stu-id="93f43-190">Avoid specifying a parameter name in your template that matches a parameter in the deployment command.</span></span> <span data-ttu-id="93f43-191">Resource Manager resolves this naming conflict by adding the postfix **FromTemplate** to the template parameter.</span><span class="sxs-lookup"><span data-stu-id="93f43-191">Resource Manager resolves this naming conflict by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="93f43-192">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="93f43-192">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="93f43-193">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="93f43-193">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span>

## <a name="example-templates"></a><span data-ttu-id="93f43-194">Example templates</span><span class="sxs-lookup"><span data-stu-id="93f43-194">Example templates</span></span>

<span data-ttu-id="93f43-195">These example templates demonstrate some scenarios for using parameters.</span><span class="sxs-lookup"><span data-stu-id="93f43-195">These example templates demonstrate some scenarios for using parameters.</span></span> <span data-ttu-id="93f43-196">Deploy them to test how parameters are handled in different scenarios.</span><span class="sxs-lookup"><span data-stu-id="93f43-196">Deploy them to test how parameters are handled in different scenarios.</span></span>

|<span data-ttu-id="93f43-197">Template</span><span class="sxs-lookup"><span data-stu-id="93f43-197">Template</span></span>  |<span data-ttu-id="93f43-198">Description</span><span class="sxs-lookup"><span data-stu-id="93f43-198">Description</span></span>  |
|---------|---------|
|[<span data-ttu-id="93f43-199">parameters with functions for default values</span><span class="sxs-lookup"><span data-stu-id="93f43-199">parameters with functions for default values</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/parameterswithfunctions.json) | <span data-ttu-id="93f43-200">Demonstrates how to use template functions when defining default values for parameters.</span><span class="sxs-lookup"><span data-stu-id="93f43-200">Demonstrates how to use template functions when defining default values for parameters.</span></span> <span data-ttu-id="93f43-201">The template does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="93f43-201">The template does not deploy any resources.</span></span> <span data-ttu-id="93f43-202">It constructs parameter values and returns those values.</span><span class="sxs-lookup"><span data-stu-id="93f43-202">It constructs parameter values and returns those values.</span></span> |
|[<span data-ttu-id="93f43-203">parameter object</span><span class="sxs-lookup"><span data-stu-id="93f43-203">parameter object</span></span>](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/parameterobject.json) | <span data-ttu-id="93f43-204">Demonstrates using an object for a parameter.</span><span class="sxs-lookup"><span data-stu-id="93f43-204">Demonstrates using an object for a parameter.</span></span> <span data-ttu-id="93f43-205">The template does not deploy any resources.</span><span class="sxs-lookup"><span data-stu-id="93f43-205">The template does not deploy any resources.</span></span> <span data-ttu-id="93f43-206">It constructs parameter values and returns those values.</span><span class="sxs-lookup"><span data-stu-id="93f43-206">It constructs parameter values and returns those values.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="93f43-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="93f43-207">Next steps</span></span>

* <span data-ttu-id="93f43-208">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="93f43-208">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="93f43-209">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="93f43-209">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 
* <span data-ttu-id="93f43-210">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="93f43-210">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="93f43-211">For information about using a parameter object, see [Use an object as a parameter in an Azure Resource Manager template](/azure/architecture/building-blocks/extending-templates/objects-as-parameters).</span><span class="sxs-lookup"><span data-stu-id="93f43-211">For information about using a parameter object, see [Use an object as a parameter in an Azure Resource Manager template](/azure/architecture/building-blocks/extending-templates/objects-as-parameters).</span></span>
