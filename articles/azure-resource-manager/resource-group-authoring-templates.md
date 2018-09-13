---
title: Azure Resource Manager template structure and syntax | Microsoft Docs
description: Describes the structure and properties of Azure Resource Manager templates using declarative JSON syntax.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: tomfitz
ms.openlocfilehash: eb196803a458a28be69ebc0e60e9423e3606b8b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562800"
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="6ca76-103">Understand the structure and syntax of Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="6ca76-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="6ca76-104">This topic describes the structure of an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="6ca76-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="6ca76-105">It presents the different sections of a template and the properties that are available in those sections.</span><span class="sxs-lookup"><span data-stu-id="6ca76-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="6ca76-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="6ca76-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="6ca76-108">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6ca76-108">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="6ca76-109">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span><span class="sxs-lookup"><span data-stu-id="6ca76-109">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

## <a name="template-format"></a><span data-ttu-id="6ca76-110">Template format</span><span class="sxs-lookup"><span data-stu-id="6ca76-110">Template format</span></span>
<span data-ttu-id="6ca76-111">In its simplest structure, a template contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="6ca76-111">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="6ca76-112">Element name</span><span class="sxs-lookup"><span data-stu-id="6ca76-112">Element name</span></span> | <span data-ttu-id="6ca76-113">Required</span><span class="sxs-lookup"><span data-stu-id="6ca76-113">Required</span></span> | <span data-ttu-id="6ca76-114">Description</span><span class="sxs-lookup"><span data-stu-id="6ca76-114">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6ca76-115">$schema</span><span class="sxs-lookup"><span data-stu-id="6ca76-115">$schema</span></span> |<span data-ttu-id="6ca76-116">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-116">Yes</span></span> |<span data-ttu-id="6ca76-117">Location of the JSON schema file that describes the version of the template language.</span><span class="sxs-lookup"><span data-stu-id="6ca76-117">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="6ca76-118">Use the URL shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="6ca76-118">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="6ca76-119">contentVersion</span><span class="sxs-lookup"><span data-stu-id="6ca76-119">contentVersion</span></span> |<span data-ttu-id="6ca76-120">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-120">Yes</span></span> |<span data-ttu-id="6ca76-121">Version of the template (such as 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="6ca76-121">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="6ca76-122">You can provide any value for this element.</span><span class="sxs-lookup"><span data-stu-id="6ca76-122">You can provide any value for this element.</span></span> <span data-ttu-id="6ca76-123">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span><span class="sxs-lookup"><span data-stu-id="6ca76-123">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="6ca76-124">parameters</span><span class="sxs-lookup"><span data-stu-id="6ca76-124">parameters</span></span> |<span data-ttu-id="6ca76-125">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-125">No</span></span> |<span data-ttu-id="6ca76-126">Values that are provided when deployment is executed to customize resource deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-126">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="6ca76-127">variables</span><span class="sxs-lookup"><span data-stu-id="6ca76-127">variables</span></span> |<span data-ttu-id="6ca76-128">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-128">No</span></span> |<span data-ttu-id="6ca76-129">Values that are used as JSON fragments in the template to simplify template language expressions.</span><span class="sxs-lookup"><span data-stu-id="6ca76-129">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="6ca76-130">resources</span><span class="sxs-lookup"><span data-stu-id="6ca76-130">resources</span></span> |<span data-ttu-id="6ca76-131">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-131">Yes</span></span> |<span data-ttu-id="6ca76-132">Resource types that are deployed or updated in a resource group.</span><span class="sxs-lookup"><span data-stu-id="6ca76-132">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="6ca76-133">outputs</span><span class="sxs-lookup"><span data-stu-id="6ca76-133">outputs</span></span> |<span data-ttu-id="6ca76-134">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-134">No</span></span> |<span data-ttu-id="6ca76-135">Values that are returned after deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-135">Values that are returned after deployment.</span></span> |

<span data-ttu-id="6ca76-136">Each element contains properties you can set.</span><span class="sxs-lookup"><span data-stu-id="6ca76-136">Each element contains properties you can set.</span></span> <span data-ttu-id="6ca76-137">The following example contains the full syntax for a template:</span><span class="sxs-lookup"><span data-stu-id="6ca76-137">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
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
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": "<name-value-pairs-for-resource-tagging>",
          "comments": "<your-reference-notes>",
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": "<settings-for-the-resource>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>"
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="6ca76-138">We examine the sections of the template in greater detail later in this topic.</span><span class="sxs-lookup"><span data-stu-id="6ca76-138">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="6ca76-139">Expressions and functions</span><span class="sxs-lookup"><span data-stu-id="6ca76-139">Expressions and functions</span></span>
<span data-ttu-id="6ca76-140">The basic syntax of the template is JSON.</span><span class="sxs-lookup"><span data-stu-id="6ca76-140">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="6ca76-141">However, expressions and functions extend the JSON values available within the template.</span><span class="sxs-lookup"><span data-stu-id="6ca76-141">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="6ca76-142">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span><span class="sxs-lookup"><span data-stu-id="6ca76-142">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="6ca76-143">The value of the expression is evaluated when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="6ca76-143">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="6ca76-144">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span><span class="sxs-lookup"><span data-stu-id="6ca76-144">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="6ca76-145">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span><span class="sxs-lookup"><span data-stu-id="6ca76-145">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="6ca76-146">Typically, you use expressions with functions to perform operations for configuring the deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-146">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="6ca76-147">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="6ca76-147">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="6ca76-148">You reference properties by using the dot and [index] operators.</span><span class="sxs-lookup"><span data-stu-id="6ca76-148">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="6ca76-149">The following example shows how to use several functions when constructing values:</span><span class="sxs-lookup"><span data-stu-id="6ca76-149">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="6ca76-150">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-150">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="6ca76-151">Parameters</span><span class="sxs-lookup"><span data-stu-id="6ca76-151">Parameters</span></span>
<span data-ttu-id="6ca76-152">In the parameters section of the template, you specify which values you can input when deploying the resources.</span><span class="sxs-lookup"><span data-stu-id="6ca76-152">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="6ca76-153">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span><span class="sxs-lookup"><span data-stu-id="6ca76-153">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="6ca76-154">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span><span class="sxs-lookup"><span data-stu-id="6ca76-154">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="6ca76-155">You define parameters with the following structure:</span><span class="sxs-lookup"><span data-stu-id="6ca76-155">You define parameters with the following structure:</span></span>

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

| <span data-ttu-id="6ca76-156">Element name</span><span class="sxs-lookup"><span data-stu-id="6ca76-156">Element name</span></span> | <span data-ttu-id="6ca76-157">Required</span><span class="sxs-lookup"><span data-stu-id="6ca76-157">Required</span></span> | <span data-ttu-id="6ca76-158">Description</span><span class="sxs-lookup"><span data-stu-id="6ca76-158">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6ca76-159">parameterName</span><span class="sxs-lookup"><span data-stu-id="6ca76-159">parameterName</span></span> |<span data-ttu-id="6ca76-160">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-160">Yes</span></span> |<span data-ttu-id="6ca76-161">Name of the parameter.</span><span class="sxs-lookup"><span data-stu-id="6ca76-161">Name of the parameter.</span></span> <span data-ttu-id="6ca76-162">Must be a valid JavaScript identifier.</span><span class="sxs-lookup"><span data-stu-id="6ca76-162">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="6ca76-163">type</span><span class="sxs-lookup"><span data-stu-id="6ca76-163">type</span></span> |<span data-ttu-id="6ca76-164">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-164">Yes</span></span> |<span data-ttu-id="6ca76-165">Type of the parameter value.</span><span class="sxs-lookup"><span data-stu-id="6ca76-165">Type of the parameter value.</span></span> <span data-ttu-id="6ca76-166">See the list of allowed types after this table.</span><span class="sxs-lookup"><span data-stu-id="6ca76-166">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="6ca76-167">defaultValue</span><span class="sxs-lookup"><span data-stu-id="6ca76-167">defaultValue</span></span> |<span data-ttu-id="6ca76-168">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-168">No</span></span> |<span data-ttu-id="6ca76-169">Default value for the parameter, if no value is provided for the parameter.</span><span class="sxs-lookup"><span data-stu-id="6ca76-169">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="6ca76-170">allowedValues</span><span class="sxs-lookup"><span data-stu-id="6ca76-170">allowedValues</span></span> |<span data-ttu-id="6ca76-171">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-171">No</span></span> |<span data-ttu-id="6ca76-172">Array of allowed values for the parameter to make sure that the right value is provided.</span><span class="sxs-lookup"><span data-stu-id="6ca76-172">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="6ca76-173">minValue</span><span class="sxs-lookup"><span data-stu-id="6ca76-173">minValue</span></span> |<span data-ttu-id="6ca76-174">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-174">No</span></span> |<span data-ttu-id="6ca76-175">The minimum value for int type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="6ca76-175">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6ca76-176">maxValue</span><span class="sxs-lookup"><span data-stu-id="6ca76-176">maxValue</span></span> |<span data-ttu-id="6ca76-177">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-177">No</span></span> |<span data-ttu-id="6ca76-178">The maximum value for int type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="6ca76-178">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6ca76-179">minLength</span><span class="sxs-lookup"><span data-stu-id="6ca76-179">minLength</span></span> |<span data-ttu-id="6ca76-180">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-180">No</span></span> |<span data-ttu-id="6ca76-181">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="6ca76-181">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6ca76-182">maxLength</span><span class="sxs-lookup"><span data-stu-id="6ca76-182">maxLength</span></span> |<span data-ttu-id="6ca76-183">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-183">No</span></span> |<span data-ttu-id="6ca76-184">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span><span class="sxs-lookup"><span data-stu-id="6ca76-184">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="6ca76-185">description</span><span class="sxs-lookup"><span data-stu-id="6ca76-185">description</span></span> |<span data-ttu-id="6ca76-186">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-186">No</span></span> |<span data-ttu-id="6ca76-187">Description of the parameter that is displayed to users through the portal.</span><span class="sxs-lookup"><span data-stu-id="6ca76-187">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="6ca76-188">The allowed types and values are:</span><span class="sxs-lookup"><span data-stu-id="6ca76-188">The allowed types and values are:</span></span>

* <span data-ttu-id="6ca76-189">**string**</span><span class="sxs-lookup"><span data-stu-id="6ca76-189">**string**</span></span>
* <span data-ttu-id="6ca76-190">**secureString**</span><span class="sxs-lookup"><span data-stu-id="6ca76-190">**secureString**</span></span>
* <span data-ttu-id="6ca76-191">**int**</span><span class="sxs-lookup"><span data-stu-id="6ca76-191">**int**</span></span>
* <span data-ttu-id="6ca76-192">**bool**</span><span class="sxs-lookup"><span data-stu-id="6ca76-192">**bool**</span></span>
* <span data-ttu-id="6ca76-193">**object**</span><span class="sxs-lookup"><span data-stu-id="6ca76-193">**object**</span></span> 
* <span data-ttu-id="6ca76-194">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="6ca76-194">**secureObject**</span></span>
* <span data-ttu-id="6ca76-195">**array**</span><span class="sxs-lookup"><span data-stu-id="6ca76-195">**array**</span></span>

<span data-ttu-id="6ca76-196">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span><span class="sxs-lookup"><span data-stu-id="6ca76-196">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="6ca76-197">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span><span class="sxs-lookup"><span data-stu-id="6ca76-197">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="6ca76-198">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span><span class="sxs-lookup"><span data-stu-id="6ca76-198">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="6ca76-199">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment][deployment2cmdlet] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6ca76-199">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment][deployment2cmdlet] cmdlet.</span></span> <span data-ttu-id="6ca76-200">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="6ca76-200">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="6ca76-201">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span><span class="sxs-lookup"><span data-stu-id="6ca76-201">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="6ca76-202">All passwords, keys, and other secrets should use the **secureString** type.</span><span class="sxs-lookup"><span data-stu-id="6ca76-202">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="6ca76-203">If you pass sensitive data in a JSON object, use the **secureObject** type.</span><span class="sxs-lookup"><span data-stu-id="6ca76-203">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="6ca76-204">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-204">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="6ca76-205">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span><span class="sxs-lookup"><span data-stu-id="6ca76-205">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![show deployment values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="6ca76-207">The following example shows how to define parameters:</span><span class="sxs-lookup"><span data-stu-id="6ca76-207">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="6ca76-208">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-208">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="6ca76-209">Variables</span><span class="sxs-lookup"><span data-stu-id="6ca76-209">Variables</span></span>
<span data-ttu-id="6ca76-210">In the variables section, you construct values that can be used throughout your template.</span><span class="sxs-lookup"><span data-stu-id="6ca76-210">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="6ca76-211">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span><span class="sxs-lookup"><span data-stu-id="6ca76-211">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="6ca76-212">You define variables with the following structure:</span><span class="sxs-lookup"><span data-stu-id="6ca76-212">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="6ca76-213">The following example shows how to define a variable that is constructed from two parameter values:</span><span class="sxs-lookup"><span data-stu-id="6ca76-213">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="6ca76-214">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span><span class="sxs-lookup"><span data-stu-id="6ca76-214">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="6ca76-215">Resources</span><span class="sxs-lookup"><span data-stu-id="6ca76-215">Resources</span></span>
<span data-ttu-id="6ca76-216">In the resources section, you define the resources that are deployed or updated.</span><span class="sxs-lookup"><span data-stu-id="6ca76-216">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="6ca76-217">This section can get complicated because you must understand the types you are deploying to provide the right values.</span><span class="sxs-lookup"><span data-stu-id="6ca76-217">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="6ca76-218">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="6ca76-218">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="6ca76-219">You define resources with the following structure:</span><span class="sxs-lookup"><span data-stu-id="6ca76-219">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": "<name-value-pairs-for-resource-tagging>",
      "comments": "<your-reference-notes>",
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": "<settings-for-the-resource>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>"
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="6ca76-220">Element name</span><span class="sxs-lookup"><span data-stu-id="6ca76-220">Element name</span></span> | <span data-ttu-id="6ca76-221">Required</span><span class="sxs-lookup"><span data-stu-id="6ca76-221">Required</span></span> | <span data-ttu-id="6ca76-222">Description</span><span class="sxs-lookup"><span data-stu-id="6ca76-222">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6ca76-223">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6ca76-223">apiVersion</span></span> |<span data-ttu-id="6ca76-224">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-224">Yes</span></span> |<span data-ttu-id="6ca76-225">Version of the REST API to use for creating the resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-225">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="6ca76-226">type</span><span class="sxs-lookup"><span data-stu-id="6ca76-226">type</span></span> |<span data-ttu-id="6ca76-227">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-227">Yes</span></span> |<span data-ttu-id="6ca76-228">Type of the resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-228">Type of the resource.</span></span> <span data-ttu-id="6ca76-229">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="6ca76-229">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="6ca76-230">name</span><span class="sxs-lookup"><span data-stu-id="6ca76-230">name</span></span> |<span data-ttu-id="6ca76-231">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-231">Yes</span></span> |<span data-ttu-id="6ca76-232">Name of the resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-232">Name of the resource.</span></span> <span data-ttu-id="6ca76-233">The name must follow URI component restrictions defined in RFC3986.</span><span class="sxs-lookup"><span data-stu-id="6ca76-233">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="6ca76-234">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span><span class="sxs-lookup"><span data-stu-id="6ca76-234">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="6ca76-235">location</span><span class="sxs-lookup"><span data-stu-id="6ca76-235">location</span></span> |<span data-ttu-id="6ca76-236">Varies</span><span class="sxs-lookup"><span data-stu-id="6ca76-236">Varies</span></span> |<span data-ttu-id="6ca76-237">Supported geo-locations of the provided resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-237">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="6ca76-238">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span><span class="sxs-lookup"><span data-stu-id="6ca76-238">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="6ca76-239">Usually, it also makes sense to place resources that interact with each other in the same region.</span><span class="sxs-lookup"><span data-stu-id="6ca76-239">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="6ca76-240">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span><span class="sxs-lookup"><span data-stu-id="6ca76-240">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="6ca76-241">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-241">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="6ca76-242">tags</span><span class="sxs-lookup"><span data-stu-id="6ca76-242">tags</span></span> |<span data-ttu-id="6ca76-243">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-243">No</span></span> |<span data-ttu-id="6ca76-244">Tags that are associated with the resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-244">Tags that are associated with the resource.</span></span> <span data-ttu-id="6ca76-245">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-245">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="6ca76-246">comments</span><span class="sxs-lookup"><span data-stu-id="6ca76-246">comments</span></span> |<span data-ttu-id="6ca76-247">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-247">No</span></span> |<span data-ttu-id="6ca76-248">Your notes for documenting the resources in your template</span><span class="sxs-lookup"><span data-stu-id="6ca76-248">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="6ca76-249">dependsOn</span><span class="sxs-lookup"><span data-stu-id="6ca76-249">dependsOn</span></span> |<span data-ttu-id="6ca76-250">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-250">No</span></span> |<span data-ttu-id="6ca76-251">Resources that must be deployed before this resource is deployed.</span><span class="sxs-lookup"><span data-stu-id="6ca76-251">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="6ca76-252">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span><span class="sxs-lookup"><span data-stu-id="6ca76-252">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="6ca76-253">When resources are not dependent on each other, they are deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="6ca76-253">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="6ca76-254">The value can be a comma-separated list of a resource names or resource unique identifiers.</span><span class="sxs-lookup"><span data-stu-id="6ca76-254">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="6ca76-255">Only list resources that are deployed in this template.</span><span class="sxs-lookup"><span data-stu-id="6ca76-255">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="6ca76-256">Resources that are not defined in this template must already exist.</span><span class="sxs-lookup"><span data-stu-id="6ca76-256">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="6ca76-257">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span><span class="sxs-lookup"><span data-stu-id="6ca76-257">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="6ca76-258">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-258">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="6ca76-259">properties</span><span class="sxs-lookup"><span data-stu-id="6ca76-259">properties</span></span> |<span data-ttu-id="6ca76-260">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-260">No</span></span> |<span data-ttu-id="6ca76-261">Resource-specific configuration settings.</span><span class="sxs-lookup"><span data-stu-id="6ca76-261">Resource-specific configuration settings.</span></span> <span data-ttu-id="6ca76-262">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-262">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> |
| <span data-ttu-id="6ca76-263">copy</span><span class="sxs-lookup"><span data-stu-id="6ca76-263">copy</span></span> |<span data-ttu-id="6ca76-264">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-264">No</span></span> |<span data-ttu-id="6ca76-265">If more than one instance is needed, the number of resources to create.</span><span class="sxs-lookup"><span data-stu-id="6ca76-265">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="6ca76-266">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-266">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="6ca76-267">resources</span><span class="sxs-lookup"><span data-stu-id="6ca76-267">resources</span></span> |<span data-ttu-id="6ca76-268">No</span><span class="sxs-lookup"><span data-stu-id="6ca76-268">No</span></span> |<span data-ttu-id="6ca76-269">Child resources that depend on the resource being defined.</span><span class="sxs-lookup"><span data-stu-id="6ca76-269">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="6ca76-270">Only provide resource types that are permitted by the schema of the parent resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-270">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="6ca76-271">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="6ca76-271">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="6ca76-272">Dependency on the parent resource is not implied.</span><span class="sxs-lookup"><span data-stu-id="6ca76-272">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="6ca76-273">You must explicitly define that dependency.</span><span class="sxs-lookup"><span data-stu-id="6ca76-273">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="6ca76-274">The resources section contains an array of the resources to deploy.</span><span class="sxs-lookup"><span data-stu-id="6ca76-274">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="6ca76-275">Within each resource, you can also define an array of child resources.</span><span class="sxs-lookup"><span data-stu-id="6ca76-275">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="6ca76-276">Therefore, your resources section could have a structure like:</span><span class="sxs-lookup"><span data-stu-id="6ca76-276">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="6ca76-277">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-277">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

## <a name="outputs"></a><span data-ttu-id="6ca76-278">Outputs</span><span class="sxs-lookup"><span data-stu-id="6ca76-278">Outputs</span></span>
<span data-ttu-id="6ca76-279">In the Outputs section, you specify values that are returned from deployment.</span><span class="sxs-lookup"><span data-stu-id="6ca76-279">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="6ca76-280">For example, you could return the URI to access a deployed resource.</span><span class="sxs-lookup"><span data-stu-id="6ca76-280">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="6ca76-281">The following example shows the structure of an output definition:</span><span class="sxs-lookup"><span data-stu-id="6ca76-281">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="6ca76-282">Element name</span><span class="sxs-lookup"><span data-stu-id="6ca76-282">Element name</span></span> | <span data-ttu-id="6ca76-283">Required</span><span class="sxs-lookup"><span data-stu-id="6ca76-283">Required</span></span> | <span data-ttu-id="6ca76-284">Description</span><span class="sxs-lookup"><span data-stu-id="6ca76-284">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6ca76-285">outputName</span><span class="sxs-lookup"><span data-stu-id="6ca76-285">outputName</span></span> |<span data-ttu-id="6ca76-286">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-286">Yes</span></span> |<span data-ttu-id="6ca76-287">Name of the output value.</span><span class="sxs-lookup"><span data-stu-id="6ca76-287">Name of the output value.</span></span> <span data-ttu-id="6ca76-288">Must be a valid JavaScript identifier.</span><span class="sxs-lookup"><span data-stu-id="6ca76-288">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="6ca76-289">type</span><span class="sxs-lookup"><span data-stu-id="6ca76-289">type</span></span> |<span data-ttu-id="6ca76-290">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-290">Yes</span></span> |<span data-ttu-id="6ca76-291">Type of the output value.</span><span class="sxs-lookup"><span data-stu-id="6ca76-291">Type of the output value.</span></span> <span data-ttu-id="6ca76-292">Output values support the same types as template input parameters.</span><span class="sxs-lookup"><span data-stu-id="6ca76-292">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="6ca76-293">value</span><span class="sxs-lookup"><span data-stu-id="6ca76-293">value</span></span> |<span data-ttu-id="6ca76-294">Yes</span><span class="sxs-lookup"><span data-stu-id="6ca76-294">Yes</span></span> |<span data-ttu-id="6ca76-295">Template language expression that is evaluated and returned as output value.</span><span class="sxs-lookup"><span data-stu-id="6ca76-295">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="6ca76-296">The following example shows a value that is returned in the Outputs section.</span><span class="sxs-lookup"><span data-stu-id="6ca76-296">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="6ca76-297">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-297">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ca76-298">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6ca76-298">Next Steps</span></span>
* <span data-ttu-id="6ca76-299">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="6ca76-299">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="6ca76-300">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-300">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="6ca76-301">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6ca76-301">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6ca76-302">You may need to use resources that exist within a different resource group.</span><span class="sxs-lookup"><span data-stu-id="6ca76-302">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="6ca76-303">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span><span class="sxs-lookup"><span data-stu-id="6ca76-303">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="6ca76-304">For more information, see the [resourceId function](resource-group-template-functions.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="6ca76-304">For more information, see the [resourceId function](resource-group-template-functions.md#resourceid).</span></span>

[deployment2cmdlet]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroupdeployment

