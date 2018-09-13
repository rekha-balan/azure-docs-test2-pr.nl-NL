---
title: Resource Manager Template Functions | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to retrieve values, work with strings and numerics, and retrieve deployment information.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: tomfitz
ms.openlocfilehash: 591749e2a91f8dcc080b5fa697c1f9bf953d836f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564093"
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="3293f-103">Azure Resource Manager template functions</span><span class="sxs-lookup"><span data-stu-id="3293f-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="3293f-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="3293f-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="3293f-105">Template functions and their parameters are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="3293f-105">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="3293f-106">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span><span class="sxs-lookup"><span data-stu-id="3293f-106">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="3293f-107">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span><span class="sxs-lookup"><span data-stu-id="3293f-107">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="3293f-108">Certain resource types may have case requirements irrespective of how functions are evaluated.</span><span class="sxs-lookup"><span data-stu-id="3293f-108">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

## <a name="numeric-functions"></a><span data-ttu-id="3293f-109">Numeric functions</span><span class="sxs-lookup"><span data-stu-id="3293f-109">Numeric functions</span></span>
<span data-ttu-id="3293f-110">Resource Manager provides the following functions for working with integers:</span><span class="sxs-lookup"><span data-stu-id="3293f-110">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="3293f-111">add</span><span class="sxs-lookup"><span data-stu-id="3293f-111">add</span></span>](#add)
* [<span data-ttu-id="3293f-112">copyIndex</span><span class="sxs-lookup"><span data-stu-id="3293f-112">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="3293f-113">div</span><span class="sxs-lookup"><span data-stu-id="3293f-113">div</span></span>](#div)
* [<span data-ttu-id="3293f-114">int</span><span class="sxs-lookup"><span data-stu-id="3293f-114">int</span></span>](#int)
* [<span data-ttu-id="3293f-115">mod</span><span class="sxs-lookup"><span data-stu-id="3293f-115">mod</span></span>](#mod)
* [<span data-ttu-id="3293f-116">mul</span><span class="sxs-lookup"><span data-stu-id="3293f-116">mul</span></span>](#mul)
* [<span data-ttu-id="3293f-117">sub</span><span class="sxs-lookup"><span data-stu-id="3293f-117">sub</span></span>](#sub)

<a id="add" />

### <a name="add"></a><span data-ttu-id="3293f-118">add</span><span class="sxs-lookup"><span data-stu-id="3293f-118">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="3293f-119">Returns the sum of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="3293f-119">Returns the sum of the two provided integers.</span></span>

| <span data-ttu-id="3293f-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-120">Parameter</span></span> | <span data-ttu-id="3293f-121">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-121">Required</span></span> | <span data-ttu-id="3293f-122">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-122">Type</span></span> | <span data-ttu-id="3293f-123">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-123">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="3293f-124">operand1</span><span class="sxs-lookup"><span data-stu-id="3293f-124">operand1</span></span> |<span data-ttu-id="3293f-125">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-125">Yes</span></span> |<span data-ttu-id="3293f-126">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-126">Integer</span></span> |<span data-ttu-id="3293f-127">First number to add.</span><span class="sxs-lookup"><span data-stu-id="3293f-127">First number to add.</span></span> |
|<span data-ttu-id="3293f-128">operand2</span><span class="sxs-lookup"><span data-stu-id="3293f-128">operand2</span></span> |<span data-ttu-id="3293f-129">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-129">Yes</span></span> |<span data-ttu-id="3293f-130">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-130">Integer</span></span> |<span data-ttu-id="3293f-131">Second number to add.</span><span class="sxs-lookup"><span data-stu-id="3293f-131">Second number to add.</span></span> |

<span data-ttu-id="3293f-132">The following example adds two parameters.</span><span class="sxs-lookup"><span data-stu-id="3293f-132">The following example adds two parameters.</span></span>

```json
"parameters": {
  "first": {
    "type": "int",
    "metadata": {
      "description": "First integer to add"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Second integer to add"
    }
  }
},
...
"outputs": {
  "addResult": {
    "type": "int",
    "value": "[add(parameters('first'), parameters('second'))]"
  }
}
```

<a id="copyindex" />

### <a name="copyindex"></a><span data-ttu-id="3293f-133">copyIndex</span><span class="sxs-lookup"><span data-stu-id="3293f-133">copyIndex</span></span>
`copyIndex(offset)`

<span data-ttu-id="3293f-134">Returns the index of an iteration loop.</span><span class="sxs-lookup"><span data-stu-id="3293f-134">Returns the index of an iteration loop.</span></span> 

| <span data-ttu-id="3293f-135">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-135">Parameter</span></span> | <span data-ttu-id="3293f-136">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-136">Required</span></span> | <span data-ttu-id="3293f-137">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-137">Type</span></span> | <span data-ttu-id="3293f-138">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-138">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-139">offset</span><span class="sxs-lookup"><span data-stu-id="3293f-139">offset</span></span> |<span data-ttu-id="3293f-140">No</span><span class="sxs-lookup"><span data-stu-id="3293f-140">No</span></span> |<span data-ttu-id="3293f-141">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-141">Integer</span></span> |<span data-ttu-id="3293f-142">The number to add to the zero-based iteration value.</span><span class="sxs-lookup"><span data-stu-id="3293f-142">The number to add to the zero-based iteration value.</span></span> |

<span data-ttu-id="3293f-143">This function is always used with a **copy** object.</span><span class="sxs-lookup"><span data-stu-id="3293f-143">This function is always used with a **copy** object.</span></span> <span data-ttu-id="3293f-144">If no value is provided for **offset**, the current iteration value is returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-144">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="3293f-145">The iteration value starts at zero.</span><span class="sxs-lookup"><span data-stu-id="3293f-145">The iteration value starts at zero.</span></span> <span data-ttu-id="3293f-146">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3293f-146">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="3293f-147">The following example shows a copy loop and the index value included in the name.</span><span class="sxs-lookup"><span data-stu-id="3293f-147">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

<a id="div" />

### <a name="div"></a><span data-ttu-id="3293f-148">div</span><span class="sxs-lookup"><span data-stu-id="3293f-148">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="3293f-149">Returns the integer division of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="3293f-149">Returns the integer division of the two provided integers.</span></span>

| <span data-ttu-id="3293f-150">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-150">Parameter</span></span> | <span data-ttu-id="3293f-151">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-151">Required</span></span> | <span data-ttu-id="3293f-152">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-152">Type</span></span> | <span data-ttu-id="3293f-153">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-153">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-154">operand1</span><span class="sxs-lookup"><span data-stu-id="3293f-154">operand1</span></span> |<span data-ttu-id="3293f-155">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-155">Yes</span></span> |<span data-ttu-id="3293f-156">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-156">Integer</span></span> |<span data-ttu-id="3293f-157">The number being divided.</span><span class="sxs-lookup"><span data-stu-id="3293f-157">The number being divided.</span></span> |
| <span data-ttu-id="3293f-158">operand2</span><span class="sxs-lookup"><span data-stu-id="3293f-158">operand2</span></span> |<span data-ttu-id="3293f-159">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-159">Yes</span></span> |<span data-ttu-id="3293f-160">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-160">Integer</span></span> |<span data-ttu-id="3293f-161">The number that is used to divide.</span><span class="sxs-lookup"><span data-stu-id="3293f-161">The number that is used to divide.</span></span> <span data-ttu-id="3293f-162">Cannot be 0.</span><span class="sxs-lookup"><span data-stu-id="3293f-162">Cannot be 0.</span></span> |

<span data-ttu-id="3293f-163">The following example divides one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="3293f-163">The following example divides one parameter by another parameter.</span></span>

```json
"parameters": {
  "first": {
    "type": "int",
    "metadata": {
      "description": "Integer being divided"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Integer used to divide"
    }
  }
},
...
"outputs": {
  "divResult": {
    "type": "int",
    "value": "[div(parameters('first'), parameters('second'))]"
  }
}
```

<a id="int" />

### <a name="int"></a><span data-ttu-id="3293f-164">int</span><span class="sxs-lookup"><span data-stu-id="3293f-164">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="3293f-165">Converts the specified value to an integer.</span><span class="sxs-lookup"><span data-stu-id="3293f-165">Converts the specified value to an integer.</span></span>

| <span data-ttu-id="3293f-166">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-166">Parameter</span></span> | <span data-ttu-id="3293f-167">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-167">Required</span></span> | <span data-ttu-id="3293f-168">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-168">Type</span></span> | <span data-ttu-id="3293f-169">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-169">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-170">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="3293f-170">valueToConvert</span></span> |<span data-ttu-id="3293f-171">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-171">Yes</span></span> |<span data-ttu-id="3293f-172">String or Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-172">String or Integer</span></span> |<span data-ttu-id="3293f-173">The value to convert to an integer.</span><span class="sxs-lookup"><span data-stu-id="3293f-173">The value to convert to an integer.</span></span> |

<span data-ttu-id="3293f-174">The following example converts the user-provided parameter value to Integer.</span><span class="sxs-lookup"><span data-stu-id="3293f-174">The following example converts the user-provided parameter value to Integer.</span></span>

```json
"parameters": {
    "appId": { "type": "string" }
},
"variables": { 
    "intValue": "[int(parameters('appId'))]"
}
```

<a id="mod" />

### <a name="mod"></a><span data-ttu-id="3293f-175">mod</span><span class="sxs-lookup"><span data-stu-id="3293f-175">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="3293f-176">Returns the remainder of the integer division using the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="3293f-176">Returns the remainder of the integer division using the two provided integers.</span></span>

| <span data-ttu-id="3293f-177">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-177">Parameter</span></span> | <span data-ttu-id="3293f-178">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-178">Required</span></span> | <span data-ttu-id="3293f-179">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-179">Type</span></span> | <span data-ttu-id="3293f-180">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-180">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-181">operand1</span><span class="sxs-lookup"><span data-stu-id="3293f-181">operand1</span></span> |<span data-ttu-id="3293f-182">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-182">Yes</span></span> |<span data-ttu-id="3293f-183">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-183">Integer</span></span> |<span data-ttu-id="3293f-184">The number being divided.</span><span class="sxs-lookup"><span data-stu-id="3293f-184">The number being divided.</span></span> |
| <span data-ttu-id="3293f-185">operand2</span><span class="sxs-lookup"><span data-stu-id="3293f-185">operand2</span></span> |<span data-ttu-id="3293f-186">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-186">Yes</span></span> |<span data-ttu-id="3293f-187">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-187">Integer</span></span> |<span data-ttu-id="3293f-188">The number that is used to divide, Cannot be 0.</span><span class="sxs-lookup"><span data-stu-id="3293f-188">The number that is used to divide, Cannot be 0.</span></span> |

<span data-ttu-id="3293f-189">The following example returns the remainder of dividing one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="3293f-189">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
"parameters": {
  "first": {
    "type": "int",
    "metadata": {
      "description": "Integer being divided"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Integer used to divide"
    }
  }
},
...
"outputs": {
  "modResult": {
    "type": "int",
    "value": "[mod(parameters('first'), parameters('second'))]"
  }
}
```

<a id="mul" />

### <a name="mul"></a><span data-ttu-id="3293f-190">mul</span><span class="sxs-lookup"><span data-stu-id="3293f-190">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="3293f-191">Returns the multiplication of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="3293f-191">Returns the multiplication of the two provided integers.</span></span>

| <span data-ttu-id="3293f-192">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-192">Parameter</span></span> | <span data-ttu-id="3293f-193">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-193">Required</span></span> | <span data-ttu-id="3293f-194">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-194">Type</span></span> | <span data-ttu-id="3293f-195">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-195">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-196">operand1</span><span class="sxs-lookup"><span data-stu-id="3293f-196">operand1</span></span> |<span data-ttu-id="3293f-197">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-197">Yes</span></span> |<span data-ttu-id="3293f-198">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-198">Integer</span></span> |<span data-ttu-id="3293f-199">First number to multiply.</span><span class="sxs-lookup"><span data-stu-id="3293f-199">First number to multiply.</span></span> |
| <span data-ttu-id="3293f-200">operand2</span><span class="sxs-lookup"><span data-stu-id="3293f-200">operand2</span></span> |<span data-ttu-id="3293f-201">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-201">Yes</span></span> |<span data-ttu-id="3293f-202">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-202">Integer</span></span> |<span data-ttu-id="3293f-203">Second number to multiply.</span><span class="sxs-lookup"><span data-stu-id="3293f-203">Second number to multiply.</span></span> |

<span data-ttu-id="3293f-204">The following example multiplies one parameter by another parameter.</span><span class="sxs-lookup"><span data-stu-id="3293f-204">The following example multiplies one parameter by another parameter.</span></span>

```json
"parameters": {
  "first": {
    "type": "int",
    "metadata": {
      "description": "First integer to multiply"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Second integer to multiply"
    }
  }
},
...
"outputs": {
  "mulResult": {
    "type": "int",
    "value": "[mul(parameters('first'), parameters('second'))]"
  }
}
```

<a id="sub" />

### <a name="sub"></a><span data-ttu-id="3293f-205">sub</span><span class="sxs-lookup"><span data-stu-id="3293f-205">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="3293f-206">Returns the subtraction of the two provided integers.</span><span class="sxs-lookup"><span data-stu-id="3293f-206">Returns the subtraction of the two provided integers.</span></span>

| <span data-ttu-id="3293f-207">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-207">Parameter</span></span> | <span data-ttu-id="3293f-208">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-208">Required</span></span> | <span data-ttu-id="3293f-209">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-209">Type</span></span> | <span data-ttu-id="3293f-210">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-210">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-211">operand1</span><span class="sxs-lookup"><span data-stu-id="3293f-211">operand1</span></span> |<span data-ttu-id="3293f-212">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-212">Yes</span></span> |<span data-ttu-id="3293f-213">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-213">Integer</span></span> |<span data-ttu-id="3293f-214">The number that is subtracted from.</span><span class="sxs-lookup"><span data-stu-id="3293f-214">The number that is subtracted from.</span></span> |
| <span data-ttu-id="3293f-215">operand2</span><span class="sxs-lookup"><span data-stu-id="3293f-215">operand2</span></span> |<span data-ttu-id="3293f-216">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-216">Yes</span></span> |<span data-ttu-id="3293f-217">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-217">Integer</span></span> |<span data-ttu-id="3293f-218">The number that is subtracted.</span><span class="sxs-lookup"><span data-stu-id="3293f-218">The number that is subtracted.</span></span> |

<span data-ttu-id="3293f-219">The following example subtracts one parameter from another parameter.</span><span class="sxs-lookup"><span data-stu-id="3293f-219">The following example subtracts one parameter from another parameter.</span></span>

```json
"parameters": {
  "first": {
    "type": "int",
    "metadata": {
      "description": "Integer subtracted from"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Integer to subtract"
    }
  }
},
...
"outputs": {
  "subResult": {
    "type": "int",
    "value": "[sub(parameters('first'), parameters('second'))]"
  }
}
```

## <a name="string-functions"></a><span data-ttu-id="3293f-220">String functions</span><span class="sxs-lookup"><span data-stu-id="3293f-220">String functions</span></span>
<span data-ttu-id="3293f-221">Resource Manager provides the following functions for working with strings:</span><span class="sxs-lookup"><span data-stu-id="3293f-221">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="3293f-222">base64</span><span class="sxs-lookup"><span data-stu-id="3293f-222">base64</span></span>](#base64)
* [<span data-ttu-id="3293f-223">concat</span><span class="sxs-lookup"><span data-stu-id="3293f-223">concat</span></span>](#concat)
* [<span data-ttu-id="3293f-224">length</span><span class="sxs-lookup"><span data-stu-id="3293f-224">length</span></span>](#lengthstring)
* [<span data-ttu-id="3293f-225">padLeft</span><span class="sxs-lookup"><span data-stu-id="3293f-225">padLeft</span></span>](#padleft)
* [<span data-ttu-id="3293f-226">replace</span><span class="sxs-lookup"><span data-stu-id="3293f-226">replace</span></span>](#replace)
* [<span data-ttu-id="3293f-227">skip</span><span class="sxs-lookup"><span data-stu-id="3293f-227">skip</span></span>](#skipstring)
* [<span data-ttu-id="3293f-228">split</span><span class="sxs-lookup"><span data-stu-id="3293f-228">split</span></span>](#split)
* [<span data-ttu-id="3293f-229">string</span><span class="sxs-lookup"><span data-stu-id="3293f-229">string</span></span>](#string)
* [<span data-ttu-id="3293f-230">substring</span><span class="sxs-lookup"><span data-stu-id="3293f-230">substring</span></span>](#substring)
* [<span data-ttu-id="3293f-231">take</span><span class="sxs-lookup"><span data-stu-id="3293f-231">take</span></span>](#takestring)
* [<span data-ttu-id="3293f-232">toLower</span><span class="sxs-lookup"><span data-stu-id="3293f-232">toLower</span></span>](#tolower)
* [<span data-ttu-id="3293f-233">toUpper</span><span class="sxs-lookup"><span data-stu-id="3293f-233">toUpper</span></span>](#toupper)
* [<span data-ttu-id="3293f-234">trim</span><span class="sxs-lookup"><span data-stu-id="3293f-234">trim</span></span>](#trim)
* [<span data-ttu-id="3293f-235">uniqueString</span><span class="sxs-lookup"><span data-stu-id="3293f-235">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="3293f-236">uri</span><span class="sxs-lookup"><span data-stu-id="3293f-236">uri</span></span>](#uri)

<a id="base64" />

### <a name="base64"></a><span data-ttu-id="3293f-237">base64</span><span class="sxs-lookup"><span data-stu-id="3293f-237">base64</span></span>
`base64 (inputString)`

<span data-ttu-id="3293f-238">Returns the base64 representation of the input string.</span><span class="sxs-lookup"><span data-stu-id="3293f-238">Returns the base64 representation of the input string.</span></span>

| <span data-ttu-id="3293f-239">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-239">Parameter</span></span> | <span data-ttu-id="3293f-240">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-240">Required</span></span> | <span data-ttu-id="3293f-241">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-241">Type</span></span> | <span data-ttu-id="3293f-242">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-242">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-243">inputString</span><span class="sxs-lookup"><span data-stu-id="3293f-243">inputString</span></span> |<span data-ttu-id="3293f-244">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-244">Yes</span></span> |<span data-ttu-id="3293f-245">String</span><span class="sxs-lookup"><span data-stu-id="3293f-245">String</span></span> |<span data-ttu-id="3293f-246">The value to return as a base64 representation.</span><span class="sxs-lookup"><span data-stu-id="3293f-246">The value to return as a base64 representation.</span></span> |

<span data-ttu-id="3293f-247">The following example shows how to use the base64 function.</span><span class="sxs-lookup"><span data-stu-id="3293f-247">The following example shows how to use the base64 function.</span></span>

```json
"variables": {
  "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
  "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<a id="concat" />

### <a name="concat---string"></a><span data-ttu-id="3293f-248">concat - string</span><span class="sxs-lookup"><span data-stu-id="3293f-248">concat - string</span></span>
`concat (string1, string2, string3, ...)`

<span data-ttu-id="3293f-249">Combines multiple string values and returns the concatenated string.</span><span class="sxs-lookup"><span data-stu-id="3293f-249">Combines multiple string values and returns the concatenated string.</span></span> 

| <span data-ttu-id="3293f-250">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-250">Parameter</span></span> | <span data-ttu-id="3293f-251">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-251">Required</span></span> | <span data-ttu-id="3293f-252">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-252">Type</span></span> | <span data-ttu-id="3293f-253">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-253">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-254">string1</span><span class="sxs-lookup"><span data-stu-id="3293f-254">string1</span></span> |<span data-ttu-id="3293f-255">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-255">Yes</span></span> |<span data-ttu-id="3293f-256">String</span><span class="sxs-lookup"><span data-stu-id="3293f-256">String</span></span> |<span data-ttu-id="3293f-257">The first value for concatenation.</span><span class="sxs-lookup"><span data-stu-id="3293f-257">The first value for concatenation.</span></span> |
| <span data-ttu-id="3293f-258">additional strings</span><span class="sxs-lookup"><span data-stu-id="3293f-258">additional strings</span></span> |<span data-ttu-id="3293f-259">No</span><span class="sxs-lookup"><span data-stu-id="3293f-259">No</span></span> |<span data-ttu-id="3293f-260">String</span><span class="sxs-lookup"><span data-stu-id="3293f-260">String</span></span> |<span data-ttu-id="3293f-261">Additional values in sequential order for concatenation.</span><span class="sxs-lookup"><span data-stu-id="3293f-261">Additional values in sequential order for concatenation.</span></span> |

<span data-ttu-id="3293f-262">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span><span class="sxs-lookup"><span data-stu-id="3293f-262">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span> <span data-ttu-id="3293f-263">For an example of concatenating arrays, see [concat - array](#concatarray).</span><span class="sxs-lookup"><span data-stu-id="3293f-263">For an example of concatenating arrays, see [concat - array](#concatarray).</span></span>

<span data-ttu-id="3293f-264">The following example shows how to combine multiple string values to return a concatenated string.</span><span class="sxs-lookup"><span data-stu-id="3293f-264">The following example shows how to combine multiple string values to return a concatenated string.</span></span>

```json
"outputs": {
    "siteUri": {
      "type": "string",
      "value": "[concat('http://', reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<a id="lengthstring" />

### <a name="length---string"></a><span data-ttu-id="3293f-265">length - string</span><span class="sxs-lookup"><span data-stu-id="3293f-265">length - string</span></span>
`length(string)`

<span data-ttu-id="3293f-266">Returns the number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="3293f-266">Returns the number of characters in a string.</span></span>

| <span data-ttu-id="3293f-267">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-267">Parameter</span></span> | <span data-ttu-id="3293f-268">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-268">Required</span></span> | <span data-ttu-id="3293f-269">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-269">Type</span></span> | <span data-ttu-id="3293f-270">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-270">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-271">string</span><span class="sxs-lookup"><span data-stu-id="3293f-271">string</span></span> |<span data-ttu-id="3293f-272">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-272">Yes</span></span> |<span data-ttu-id="3293f-273">String</span><span class="sxs-lookup"><span data-stu-id="3293f-273">String</span></span> |<span data-ttu-id="3293f-274">The value to use for getting the number of characters.</span><span class="sxs-lookup"><span data-stu-id="3293f-274">The value to use for getting the number of characters.</span></span> |

<span data-ttu-id="3293f-275">For an example of using length with an array, see [length - array](#length).</span><span class="sxs-lookup"><span data-stu-id="3293f-275">For an example of using length with an array, see [length - array](#length).</span></span>

<span data-ttu-id="3293f-276">The following example returns the number of characters in a string.</span><span class="sxs-lookup"><span data-stu-id="3293f-276">The following example returns the number of characters in a string.</span></span> 

```json
"parameters": {
    "appName": { "type": "string" }
},
"variables": { 
    "nameLength": "[length(parameters('appName'))]"
}
```

<a id="padleft" />

### <a name="padleft"></a><span data-ttu-id="3293f-277">padLeft</span><span class="sxs-lookup"><span data-stu-id="3293f-277">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="3293f-278">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span><span class="sxs-lookup"><span data-stu-id="3293f-278">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

| <span data-ttu-id="3293f-279">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-279">Parameter</span></span> | <span data-ttu-id="3293f-280">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-280">Required</span></span> | <span data-ttu-id="3293f-281">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-281">Type</span></span> | <span data-ttu-id="3293f-282">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-282">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-283">valueToPad</span><span class="sxs-lookup"><span data-stu-id="3293f-283">valueToPad</span></span> |<span data-ttu-id="3293f-284">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-284">Yes</span></span> |<span data-ttu-id="3293f-285">String or Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-285">String or Integer</span></span> |<span data-ttu-id="3293f-286">The value to right-align.</span><span class="sxs-lookup"><span data-stu-id="3293f-286">The value to right-align.</span></span> |
| <span data-ttu-id="3293f-287">totalLength</span><span class="sxs-lookup"><span data-stu-id="3293f-287">totalLength</span></span> |<span data-ttu-id="3293f-288">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-288">Yes</span></span> |<span data-ttu-id="3293f-289">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-289">Integer</span></span> |<span data-ttu-id="3293f-290">The total number of characters in the returned string.</span><span class="sxs-lookup"><span data-stu-id="3293f-290">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="3293f-291">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="3293f-291">paddingCharacter</span></span> |<span data-ttu-id="3293f-292">No</span><span class="sxs-lookup"><span data-stu-id="3293f-292">No</span></span> |<span data-ttu-id="3293f-293">Single character</span><span class="sxs-lookup"><span data-stu-id="3293f-293">Single character</span></span> |<span data-ttu-id="3293f-294">The character to use for left-padding until the total length is reached.</span><span class="sxs-lookup"><span data-stu-id="3293f-294">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="3293f-295">The default value is a space.</span><span class="sxs-lookup"><span data-stu-id="3293f-295">The default value is a space.</span></span> |

<span data-ttu-id="3293f-296">The following example shows how to pad the user-provided parameter value by adding the zero character until the string reaches 10 characters.</span><span class="sxs-lookup"><span data-stu-id="3293f-296">The following example shows how to pad the user-provided parameter value by adding the zero character until the string reaches 10 characters.</span></span> <span data-ttu-id="3293f-297">If the original parameter value is longer than 10 characters, no characters are added.</span><span class="sxs-lookup"><span data-stu-id="3293f-297">If the original parameter value is longer than 10 characters, no characters are added.</span></span>

```json
"parameters": {
    "appName": { "type": "string" }
},
"variables": { 
    "paddedAppName": "[padLeft(parameters('appName'),10,'0')]"
}
```

<a id="replace" />

### <a name="replace"></a><span data-ttu-id="3293f-298">replace</span><span class="sxs-lookup"><span data-stu-id="3293f-298">replace</span></span>
`replace(originalString, oldCharacter, newCharacter)`

<span data-ttu-id="3293f-299">Returns a new string with all instances of one character in the specified string replaced by another character.</span><span class="sxs-lookup"><span data-stu-id="3293f-299">Returns a new string with all instances of one character in the specified string replaced by another character.</span></span>

| <span data-ttu-id="3293f-300">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-300">Parameter</span></span> | <span data-ttu-id="3293f-301">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-301">Required</span></span> | <span data-ttu-id="3293f-302">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-302">Type</span></span> | <span data-ttu-id="3293f-303">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-303">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-304">originalString</span><span class="sxs-lookup"><span data-stu-id="3293f-304">originalString</span></span> |<span data-ttu-id="3293f-305">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-305">Yes</span></span> |<span data-ttu-id="3293f-306">String</span><span class="sxs-lookup"><span data-stu-id="3293f-306">String</span></span> |<span data-ttu-id="3293f-307">The value that has all instances of one character replaced by another character.</span><span class="sxs-lookup"><span data-stu-id="3293f-307">The value that has all instances of one character replaced by another character.</span></span> |
| <span data-ttu-id="3293f-308">oldCharacter</span><span class="sxs-lookup"><span data-stu-id="3293f-308">oldCharacter</span></span> |<span data-ttu-id="3293f-309">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-309">Yes</span></span> |<span data-ttu-id="3293f-310">String</span><span class="sxs-lookup"><span data-stu-id="3293f-310">String</span></span> |<span data-ttu-id="3293f-311">The character to be removed from the original string.</span><span class="sxs-lookup"><span data-stu-id="3293f-311">The character to be removed from the original string.</span></span> |
| <span data-ttu-id="3293f-312">newCharacter</span><span class="sxs-lookup"><span data-stu-id="3293f-312">newCharacter</span></span> |<span data-ttu-id="3293f-313">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-313">Yes</span></span> |<span data-ttu-id="3293f-314">String</span><span class="sxs-lookup"><span data-stu-id="3293f-314">String</span></span> |<span data-ttu-id="3293f-315">The character to add in place of the removed character.</span><span class="sxs-lookup"><span data-stu-id="3293f-315">The character to add in place of the removed character.</span></span> |

<span data-ttu-id="3293f-316">The following example shows how to remove all dashes from the user-provided string.</span><span class="sxs-lookup"><span data-stu-id="3293f-316">The following example shows how to remove all dashes from the user-provided string.</span></span>

```json
"parameters": {
    "identifier": { "type": "string" }
},
"variables": { 
    "newidentifier": "[replace(parameters('identifier'),'-','')]"
}
```

<a id="skipstring" />

### <a name="skip---string"></a><span data-ttu-id="3293f-317">skip - string</span><span class="sxs-lookup"><span data-stu-id="3293f-317">skip - string</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="3293f-318">Returns a string with all the characters after the specified number in the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-318">Returns a string with all the characters after the specified number in the string.</span></span>

| <span data-ttu-id="3293f-319">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-319">Parameter</span></span> | <span data-ttu-id="3293f-320">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-320">Required</span></span> | <span data-ttu-id="3293f-321">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-321">Type</span></span> | <span data-ttu-id="3293f-322">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-322">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-323">originalValue</span><span class="sxs-lookup"><span data-stu-id="3293f-323">originalValue</span></span> |<span data-ttu-id="3293f-324">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-324">Yes</span></span> |<span data-ttu-id="3293f-325">String</span><span class="sxs-lookup"><span data-stu-id="3293f-325">String</span></span> |<span data-ttu-id="3293f-326">The string to use for skipping.</span><span class="sxs-lookup"><span data-stu-id="3293f-326">The string to use for skipping.</span></span> |
| <span data-ttu-id="3293f-327">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="3293f-327">numberToSkip</span></span> |<span data-ttu-id="3293f-328">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-328">Yes</span></span> |<span data-ttu-id="3293f-329">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-329">Integer</span></span> |<span data-ttu-id="3293f-330">The number of characters to skip.</span><span class="sxs-lookup"><span data-stu-id="3293f-330">The number of characters to skip.</span></span> <span data-ttu-id="3293f-331">If this value is 0 or less, all the characters in the string are returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-331">If this value is 0 or less, all the characters in the string are returned.</span></span> <span data-ttu-id="3293f-332">If it is larger than the length of the string, an empty string is returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-332">If it is larger than the length of the string, an empty string is returned.</span></span> |

<span data-ttu-id="3293f-333">For an example of using skip with an array, see [skip - array](#skip).</span><span class="sxs-lookup"><span data-stu-id="3293f-333">For an example of using skip with an array, see [skip - array](#skip).</span></span>

<span data-ttu-id="3293f-334">The following example skips the specified number of characters in the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-334">The following example skips the specified number of characters in the string.</span></span>

```json
"parameters": {
  "first": {
    "type": "string",
    "metadata": {
      "description": "Value to use for skipping"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Number of characters to skip"
    }
  }
},
"resources": [
],
"outputs": {
  "return": {
    "type": "string",
    "value": "[skip(parameters('first'),parameters('second'))]"
  }
}
```

<a id="split" />

### <a name="split"></a><span data-ttu-id="3293f-335">split</span><span class="sxs-lookup"><span data-stu-id="3293f-335">split</span></span>
`split(inputString, delimiterString)`

`split(inputString, delimiterArray)`

<span data-ttu-id="3293f-336">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span><span class="sxs-lookup"><span data-stu-id="3293f-336">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

| <span data-ttu-id="3293f-337">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-337">Parameter</span></span> | <span data-ttu-id="3293f-338">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-338">Required</span></span> | <span data-ttu-id="3293f-339">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-339">Type</span></span> | <span data-ttu-id="3293f-340">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-340">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-341">inputString</span><span class="sxs-lookup"><span data-stu-id="3293f-341">inputString</span></span> |<span data-ttu-id="3293f-342">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-342">Yes</span></span> |<span data-ttu-id="3293f-343">String</span><span class="sxs-lookup"><span data-stu-id="3293f-343">String</span></span> |<span data-ttu-id="3293f-344">The string to split.</span><span class="sxs-lookup"><span data-stu-id="3293f-344">The string to split.</span></span> |
| <span data-ttu-id="3293f-345">delimiter</span><span class="sxs-lookup"><span data-stu-id="3293f-345">delimiter</span></span> |<span data-ttu-id="3293f-346">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-346">Yes</span></span> |<span data-ttu-id="3293f-347">String or Array of strings</span><span class="sxs-lookup"><span data-stu-id="3293f-347">String or Array of strings</span></span> |<span data-ttu-id="3293f-348">The delimiter to use for splitting the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-348">The delimiter to use for splitting the string.</span></span> |

<span data-ttu-id="3293f-349">The following example splits the input string with a comma.</span><span class="sxs-lookup"><span data-stu-id="3293f-349">The following example splits the input string with a comma.</span></span>

```json
"parameters": {
    "inputString": { "type": "string" }
},
"variables": { 
    "stringPieces": "[split(parameters('inputString'), ',')]"
}
```

<span data-ttu-id="3293f-350">The next example splits the input string with either a comma or a semi-colon.</span><span class="sxs-lookup"><span data-stu-id="3293f-350">The next example splits the input string with either a comma or a semi-colon.</span></span>

```json
"variables": {
  "stringToSplit": "test1,test2;test3",
  "delimiters": [ ",", ";" ]
},
"resources": [ ],
"outputs": {
  "exampleOutput": {
    "value": "[split(variables('stringToSplit'), variables('delimiters'))]",
    "type": "array"
  }
}
```

<a id="string" />

### <a name="string"></a><span data-ttu-id="3293f-351">string</span><span class="sxs-lookup"><span data-stu-id="3293f-351">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="3293f-352">Converts the specified value to a string.</span><span class="sxs-lookup"><span data-stu-id="3293f-352">Converts the specified value to a string.</span></span>

| <span data-ttu-id="3293f-353">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-353">Parameter</span></span> | <span data-ttu-id="3293f-354">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-354">Required</span></span> | <span data-ttu-id="3293f-355">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-355">Type</span></span> | <span data-ttu-id="3293f-356">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-356">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-357">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="3293f-357">valueToConvert</span></span> |<span data-ttu-id="3293f-358">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-358">Yes</span></span> | <span data-ttu-id="3293f-359">Any</span><span class="sxs-lookup"><span data-stu-id="3293f-359">Any</span></span> |<span data-ttu-id="3293f-360">The value to convert to string.</span><span class="sxs-lookup"><span data-stu-id="3293f-360">The value to convert to string.</span></span> <span data-ttu-id="3293f-361">Any type of value can be converted, including objects and arrays.</span><span class="sxs-lookup"><span data-stu-id="3293f-361">Any type of value can be converted, including objects and arrays.</span></span> |

<span data-ttu-id="3293f-362">The following example converts the user-provided parameter values to strings.</span><span class="sxs-lookup"><span data-stu-id="3293f-362">The following example converts the user-provided parameter values to strings.</span></span>

```json
"parameters": {
  "jsonObject": {
    "type": "object",
    "defaultValue": {
      "valueA": 10,
      "valueB": "Example Text"
    }
  },
  "jsonArray": {
    "type": "array",
    "defaultValue": [ "a", "b", "c" ]
  },
  "jsonInt": {
    "type": "int",
    "defaultValue": 5
  }
},
"variables": { 
  "objectString": "[string(parameters('jsonObject'))]",
  "arrayString": "[string(parameters('jsonArray'))]",
  "intString": "[string(parameters('jsonInt'))]"
}
```

<a id="substring" />

### <a name="substring"></a><span data-ttu-id="3293f-363">substring</span><span class="sxs-lookup"><span data-stu-id="3293f-363">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="3293f-364">Returns a substring that starts at the specified character position and contains the specified number of characters.</span><span class="sxs-lookup"><span data-stu-id="3293f-364">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

| <span data-ttu-id="3293f-365">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-365">Parameter</span></span> | <span data-ttu-id="3293f-366">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-366">Required</span></span> | <span data-ttu-id="3293f-367">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-367">Type</span></span> | <span data-ttu-id="3293f-368">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-368">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-369">stringToParse</span><span class="sxs-lookup"><span data-stu-id="3293f-369">stringToParse</span></span> |<span data-ttu-id="3293f-370">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-370">Yes</span></span> |<span data-ttu-id="3293f-371">String</span><span class="sxs-lookup"><span data-stu-id="3293f-371">String</span></span> |<span data-ttu-id="3293f-372">The original string from which the substring is extracted.</span><span class="sxs-lookup"><span data-stu-id="3293f-372">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="3293f-373">startIndex</span><span class="sxs-lookup"><span data-stu-id="3293f-373">startIndex</span></span> |<span data-ttu-id="3293f-374">No</span><span class="sxs-lookup"><span data-stu-id="3293f-374">No</span></span> |<span data-ttu-id="3293f-375">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-375">Integer</span></span> |<span data-ttu-id="3293f-376">The zero-based starting character position for the substring.</span><span class="sxs-lookup"><span data-stu-id="3293f-376">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="3293f-377">length</span><span class="sxs-lookup"><span data-stu-id="3293f-377">length</span></span> |<span data-ttu-id="3293f-378">No</span><span class="sxs-lookup"><span data-stu-id="3293f-378">No</span></span> |<span data-ttu-id="3293f-379">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-379">Integer</span></span> |<span data-ttu-id="3293f-380">The number of characters for the substring.</span><span class="sxs-lookup"><span data-stu-id="3293f-380">The number of characters for the substring.</span></span> <span data-ttu-id="3293f-381">Must refer to a location within the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-381">Must refer to a location within the string.</span></span> |

<span data-ttu-id="3293f-382">The following example extracts the first three characters from a parameter.</span><span class="sxs-lookup"><span data-stu-id="3293f-382">The following example extracts the first three characters from a parameter.</span></span>

```json
"parameters": {
    "inputString": { "type": "string" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 3)]"
}
```

<span data-ttu-id="3293f-383">The following example will fail with the error "The index and length parameters must refer to a location within the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-383">The following example will fail with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="3293f-384">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span><span class="sxs-lookup"><span data-stu-id="3293f-384">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

<a id="takestring" />

### <a name="take---string"></a><span data-ttu-id="3293f-385">take - string</span><span class="sxs-lookup"><span data-stu-id="3293f-385">take - string</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="3293f-386">Returns a string with the specified number of characters from the start of the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-386">Returns a string with the specified number of characters from the start of the string.</span></span>

| <span data-ttu-id="3293f-387">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-387">Parameter</span></span> | <span data-ttu-id="3293f-388">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-388">Required</span></span> | <span data-ttu-id="3293f-389">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-389">Type</span></span> | <span data-ttu-id="3293f-390">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-390">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-391">originalValue</span><span class="sxs-lookup"><span data-stu-id="3293f-391">originalValue</span></span> |<span data-ttu-id="3293f-392">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-392">Yes</span></span> |<span data-ttu-id="3293f-393">String</span><span class="sxs-lookup"><span data-stu-id="3293f-393">String</span></span> |<span data-ttu-id="3293f-394">The value to take the characters from.</span><span class="sxs-lookup"><span data-stu-id="3293f-394">The value to take the characters from.</span></span> |
| <span data-ttu-id="3293f-395">numberToTake</span><span class="sxs-lookup"><span data-stu-id="3293f-395">numberToTake</span></span> |<span data-ttu-id="3293f-396">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-396">Yes</span></span> |<span data-ttu-id="3293f-397">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-397">Integer</span></span> |<span data-ttu-id="3293f-398">The number of characters to take.</span><span class="sxs-lookup"><span data-stu-id="3293f-398">The number of characters to take.</span></span> <span data-ttu-id="3293f-399">If this value is 0 or less, an empty string is returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-399">If this value is 0 or less, an empty string is returned.</span></span> <span data-ttu-id="3293f-400">If it is larger than the length of the given string, all the characters in the string are returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-400">If it is larger than the length of the given string, all the characters in the string are returned.</span></span> |

<span data-ttu-id="3293f-401">For an example of using take with an array, see [take - array](#take).</span><span class="sxs-lookup"><span data-stu-id="3293f-401">For an example of using take with an array, see [take - array](#take).</span></span>

<span data-ttu-id="3293f-402">The following example takes the specified number of characters from the string.</span><span class="sxs-lookup"><span data-stu-id="3293f-402">The following example takes the specified number of characters from the string.</span></span>

```json
"parameters": {
  "first": {
    "type": "string",
    "metadata": {
      "description": "Value to use for taking"
    }
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Number of characters to take"
    }
  }
},
"resources": [
],
"outputs": {
  "return": {
    "type": "string",
    "value": "[take(parameters('first'), parameters('second'))]"
  }
}
```

<a id="tolower" />

### <a name="tolower"></a><span data-ttu-id="3293f-403">toLower</span><span class="sxs-lookup"><span data-stu-id="3293f-403">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="3293f-404">Converts the specified string to lower case.</span><span class="sxs-lookup"><span data-stu-id="3293f-404">Converts the specified string to lower case.</span></span>

| <span data-ttu-id="3293f-405">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-405">Parameter</span></span> | <span data-ttu-id="3293f-406">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-406">Required</span></span> | <span data-ttu-id="3293f-407">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-407">Type</span></span> | <span data-ttu-id="3293f-408">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-408">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-409">stringToChange</span><span class="sxs-lookup"><span data-stu-id="3293f-409">stringToChange</span></span> |<span data-ttu-id="3293f-410">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-410">Yes</span></span> |<span data-ttu-id="3293f-411">String</span><span class="sxs-lookup"><span data-stu-id="3293f-411">String</span></span> |<span data-ttu-id="3293f-412">The value to convert to lower case.</span><span class="sxs-lookup"><span data-stu-id="3293f-412">The value to convert to lower case.</span></span> |

<span data-ttu-id="3293f-413">The following example converts the user-provided parameter value to lower case.</span><span class="sxs-lookup"><span data-stu-id="3293f-413">The following example converts the user-provided parameter value to lower case.</span></span>

```json
"parameters": {
    "appName": { "type": "string" }
},
"variables": { 
    "lowerCaseAppName": "[toLower(parameters('appName'))]"
}
```

<a id="toupper" />

### <a name="toupper"></a><span data-ttu-id="3293f-414">toUpper</span><span class="sxs-lookup"><span data-stu-id="3293f-414">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="3293f-415">Converts the specified string to upper case.</span><span class="sxs-lookup"><span data-stu-id="3293f-415">Converts the specified string to upper case.</span></span>

| <span data-ttu-id="3293f-416">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-416">Parameter</span></span> | <span data-ttu-id="3293f-417">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-417">Required</span></span> | <span data-ttu-id="3293f-418">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-418">Type</span></span> | <span data-ttu-id="3293f-419">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-420">stringToChange</span><span class="sxs-lookup"><span data-stu-id="3293f-420">stringToChange</span></span> |<span data-ttu-id="3293f-421">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-421">Yes</span></span> |<span data-ttu-id="3293f-422">String</span><span class="sxs-lookup"><span data-stu-id="3293f-422">String</span></span> |<span data-ttu-id="3293f-423">The value to convert to upper case.</span><span class="sxs-lookup"><span data-stu-id="3293f-423">The value to convert to upper case.</span></span> |

<span data-ttu-id="3293f-424">The following example converts the user-provided parameter value to upper case.</span><span class="sxs-lookup"><span data-stu-id="3293f-424">The following example converts the user-provided parameter value to upper case.</span></span>

```json
"parameters": {
    "appName": { "type": "string" }
},
"variables": { 
    "upperCaseAppName": "[toUpper(parameters('appName'))]"
}
```

<a id="trim" />

### <a name="trim"></a><span data-ttu-id="3293f-425">trim</span><span class="sxs-lookup"><span data-stu-id="3293f-425">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="3293f-426">Removes all leading and trailing white-space characters from the specified string.</span><span class="sxs-lookup"><span data-stu-id="3293f-426">Removes all leading and trailing white-space characters from the specified string.</span></span>

| <span data-ttu-id="3293f-427">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-427">Parameter</span></span> | <span data-ttu-id="3293f-428">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-428">Required</span></span> | <span data-ttu-id="3293f-429">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-429">Type</span></span> | <span data-ttu-id="3293f-430">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-430">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-431">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="3293f-431">stringToTrim</span></span> |<span data-ttu-id="3293f-432">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-432">Yes</span></span> |<span data-ttu-id="3293f-433">String</span><span class="sxs-lookup"><span data-stu-id="3293f-433">String</span></span> |<span data-ttu-id="3293f-434">The value to trim.</span><span class="sxs-lookup"><span data-stu-id="3293f-434">The value to trim.</span></span> |

<span data-ttu-id="3293f-435">The following example trims the white-space characters from the user-provided parameter value.</span><span class="sxs-lookup"><span data-stu-id="3293f-435">The following example trims the white-space characters from the user-provided parameter value.</span></span>

```json
"parameters": {
    "appName": { "type": "string" }
},
"variables": { 
    "trimAppName": "[trim(parameters('appName'))]"
}
```

<a id="uniquestring" />

### <a name="uniquestring"></a><span data-ttu-id="3293f-436">uniqueString</span><span class="sxs-lookup"><span data-stu-id="3293f-436">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="3293f-437">Creates a deterministic hash string based on the values provided as parameters.</span><span class="sxs-lookup"><span data-stu-id="3293f-437">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

| <span data-ttu-id="3293f-438">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-438">Parameter</span></span> | <span data-ttu-id="3293f-439">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-439">Required</span></span> | <span data-ttu-id="3293f-440">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-440">Type</span></span> | <span data-ttu-id="3293f-441">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-441">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-442">baseString</span><span class="sxs-lookup"><span data-stu-id="3293f-442">baseString</span></span> |<span data-ttu-id="3293f-443">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-443">Yes</span></span> |<span data-ttu-id="3293f-444">String</span><span class="sxs-lookup"><span data-stu-id="3293f-444">String</span></span> |<span data-ttu-id="3293f-445">The value used in the hash function to create a unique string.</span><span class="sxs-lookup"><span data-stu-id="3293f-445">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="3293f-446">additional parameters as needed</span><span class="sxs-lookup"><span data-stu-id="3293f-446">additional parameters as needed</span></span> |<span data-ttu-id="3293f-447">No</span><span class="sxs-lookup"><span data-stu-id="3293f-447">No</span></span> |<span data-ttu-id="3293f-448">String</span><span class="sxs-lookup"><span data-stu-id="3293f-448">String</span></span> |<span data-ttu-id="3293f-449">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span><span class="sxs-lookup"><span data-stu-id="3293f-449">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

<span data-ttu-id="3293f-450">This function is helpful when you need to create a unique name for a resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-450">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="3293f-451">You provide parameter values that limit the scope of uniqueness for the result.</span><span class="sxs-lookup"><span data-stu-id="3293f-451">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="3293f-452">You can specify whether the name is unique down to subscription, resource group, or deployment.</span><span class="sxs-lookup"><span data-stu-id="3293f-452">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="3293f-453">The returned value is not a random string, but rather the result of a hash function.</span><span class="sxs-lookup"><span data-stu-id="3293f-453">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="3293f-454">The returned value is 13 characters long.</span><span class="sxs-lookup"><span data-stu-id="3293f-454">The returned value is 13 characters long.</span></span> <span data-ttu-id="3293f-455">It is not globally unique.</span><span class="sxs-lookup"><span data-stu-id="3293f-455">It is not globally unique.</span></span> <span data-ttu-id="3293f-456">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span><span class="sxs-lookup"><span data-stu-id="3293f-456">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="3293f-457">The following example shows the format of the returned value.</span><span class="sxs-lookup"><span data-stu-id="3293f-457">The following example shows the format of the returned value.</span></span> <span data-ttu-id="3293f-458">The actual value varies by the provided parameters.</span><span class="sxs-lookup"><span data-stu-id="3293f-458">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="3293f-459">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span><span class="sxs-lookup"><span data-stu-id="3293f-459">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="3293f-460">Unique scoped to subscription</span><span class="sxs-lookup"><span data-stu-id="3293f-460">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="3293f-461">Unique scoped to resource group</span><span class="sxs-lookup"><span data-stu-id="3293f-461">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="3293f-462">Unique scoped to deployment for a resource group</span><span class="sxs-lookup"><span data-stu-id="3293f-462">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="3293f-463">The following example shows how to create a unique name for a storage account based on your resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-463">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="3293f-464">Inside the resource group, the name is not unique if constructed the same way.</span><span class="sxs-lookup"><span data-stu-id="3293f-464">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```


<a id="uri" />

### <a name="uri"></a><span data-ttu-id="3293f-465">uri</span><span class="sxs-lookup"><span data-stu-id="3293f-465">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="3293f-466">Creates an absolute URI by combining the baseUri and the relativeUri string.</span><span class="sxs-lookup"><span data-stu-id="3293f-466">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

| <span data-ttu-id="3293f-467">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-467">Parameter</span></span> | <span data-ttu-id="3293f-468">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-468">Required</span></span> | <span data-ttu-id="3293f-469">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-469">Type</span></span> | <span data-ttu-id="3293f-470">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-470">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-471">baseUri</span><span class="sxs-lookup"><span data-stu-id="3293f-471">baseUri</span></span> |<span data-ttu-id="3293f-472">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-472">Yes</span></span> |<span data-ttu-id="3293f-473">String</span><span class="sxs-lookup"><span data-stu-id="3293f-473">String</span></span> |<span data-ttu-id="3293f-474">The base uri string.</span><span class="sxs-lookup"><span data-stu-id="3293f-474">The base uri string.</span></span> |
| <span data-ttu-id="3293f-475">relativeUri</span><span class="sxs-lookup"><span data-stu-id="3293f-475">relativeUri</span></span> |<span data-ttu-id="3293f-476">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-476">Yes</span></span> |<span data-ttu-id="3293f-477">String</span><span class="sxs-lookup"><span data-stu-id="3293f-477">String</span></span> |<span data-ttu-id="3293f-478">The relative uri string to add to the base uri string.</span><span class="sxs-lookup"><span data-stu-id="3293f-478">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="3293f-479">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span><span class="sxs-lookup"><span data-stu-id="3293f-479">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="3293f-480">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="3293f-480">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

<span data-ttu-id="3293f-481">The following example shows how to construct a link to a nested template based on the value of the parent template.</span><span class="sxs-lookup"><span data-stu-id="3293f-481">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

## <a name="array-functions"></a><span data-ttu-id="3293f-482">Array functions</span><span class="sxs-lookup"><span data-stu-id="3293f-482">Array functions</span></span>
<span data-ttu-id="3293f-483">Resource Manager provides several functions for working with array values.</span><span class="sxs-lookup"><span data-stu-id="3293f-483">Resource Manager provides several functions for working with array values.</span></span>

* [<span data-ttu-id="3293f-484">concat</span><span class="sxs-lookup"><span data-stu-id="3293f-484">concat</span></span>](#concatarray)
* [<span data-ttu-id="3293f-485">length</span><span class="sxs-lookup"><span data-stu-id="3293f-485">length</span></span>](#length)
* [<span data-ttu-id="3293f-486">skip</span><span class="sxs-lookup"><span data-stu-id="3293f-486">skip</span></span>](#skip)
* [<span data-ttu-id="3293f-487">take</span><span class="sxs-lookup"><span data-stu-id="3293f-487">take</span></span>](#take)

<span data-ttu-id="3293f-488">To get an array of string values delimited by a value, see [split](#split).</span><span class="sxs-lookup"><span data-stu-id="3293f-488">To get an array of string values delimited by a value, see [split](#split).</span></span>

<a id="concatarray" />

### <a name="concat---array"></a><span data-ttu-id="3293f-489">concat - array</span><span class="sxs-lookup"><span data-stu-id="3293f-489">concat - array</span></span>
`concat (array1, array2, array3, ...)`

<span data-ttu-id="3293f-490">Combines multiple arrays and returns the concatenated array.</span><span class="sxs-lookup"><span data-stu-id="3293f-490">Combines multiple arrays and returns the concatenated array.</span></span> 

| <span data-ttu-id="3293f-491">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-491">Parameter</span></span> | <span data-ttu-id="3293f-492">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-492">Required</span></span> | <span data-ttu-id="3293f-493">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-493">Type</span></span> | <span data-ttu-id="3293f-494">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-494">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-495">array1</span><span class="sxs-lookup"><span data-stu-id="3293f-495">array1</span></span> |<span data-ttu-id="3293f-496">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-496">Yes</span></span> |<span data-ttu-id="3293f-497">Array</span><span class="sxs-lookup"><span data-stu-id="3293f-497">Array</span></span> |<span data-ttu-id="3293f-498">The first array for concatenation.</span><span class="sxs-lookup"><span data-stu-id="3293f-498">The first array for concatenation.</span></span> |
| <span data-ttu-id="3293f-499">additional arrays</span><span class="sxs-lookup"><span data-stu-id="3293f-499">additional arrays</span></span> |<span data-ttu-id="3293f-500">No</span><span class="sxs-lookup"><span data-stu-id="3293f-500">No</span></span> |<span data-ttu-id="3293f-501">Array</span><span class="sxs-lookup"><span data-stu-id="3293f-501">Array</span></span> |<span data-ttu-id="3293f-502">Additional arrays in sequential order for concatenation.</span><span class="sxs-lookup"><span data-stu-id="3293f-502">Additional arrays in sequential order for concatenation.</span></span> |

<span data-ttu-id="3293f-503">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span><span class="sxs-lookup"><span data-stu-id="3293f-503">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span> <span data-ttu-id="3293f-504">For an example of concatenating string values, see [concat - string](#concat).</span><span class="sxs-lookup"><span data-stu-id="3293f-504">For an example of concatenating string values, see [concat - string](#concat).</span></span>

<span data-ttu-id="3293f-505">The following example shows how to combine two arrays.</span><span class="sxs-lookup"><span data-stu-id="3293f-505">The following example shows how to combine two arrays.</span></span>

```json
"parameters": {
    "firstarray": {
      "type": "array"
    }
    "secondarray": {
      "type": "array"
    }
},
"variables": {
    "combinedarray": "[concat(parameters('firstarray'), parameters('secondarray'))]"
}
```

<a id="length" />

### <a name="length---array"></a><span data-ttu-id="3293f-506">length - array</span><span class="sxs-lookup"><span data-stu-id="3293f-506">length - array</span></span>
`length(array)`

<span data-ttu-id="3293f-507">Returns the number of elements in an array.</span><span class="sxs-lookup"><span data-stu-id="3293f-507">Returns the number of elements in an array.</span></span>

| <span data-ttu-id="3293f-508">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-508">Parameter</span></span> | <span data-ttu-id="3293f-509">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-509">Required</span></span> | <span data-ttu-id="3293f-510">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-510">Type</span></span> | <span data-ttu-id="3293f-511">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-512">array</span><span class="sxs-lookup"><span data-stu-id="3293f-512">array</span></span> |<span data-ttu-id="3293f-513">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-513">Yes</span></span> |<span data-ttu-id="3293f-514">Array</span><span class="sxs-lookup"><span data-stu-id="3293f-514">Array</span></span> |<span data-ttu-id="3293f-515">The array to use for getting the number of elements.</span><span class="sxs-lookup"><span data-stu-id="3293f-515">The array to use for getting the number of elements.</span></span> |

<span data-ttu-id="3293f-516">You can use this function with an array to specify the number of iterations when creating resources.</span><span class="sxs-lookup"><span data-stu-id="3293f-516">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="3293f-517">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span><span class="sxs-lookup"><span data-stu-id="3293f-517">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="3293f-518">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3293f-518">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="3293f-519">For an example of using length with a string value, see [length - string](#lengthstring).</span><span class="sxs-lookup"><span data-stu-id="3293f-519">For an example of using length with a string value, see [length - string](#lengthstring).</span></span>

<a id="skip" />

### <a name="skip---array"></a><span data-ttu-id="3293f-520">skip - array</span><span class="sxs-lookup"><span data-stu-id="3293f-520">skip - array</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="3293f-521">Returns an array with all the elements after the specified number in the array.</span><span class="sxs-lookup"><span data-stu-id="3293f-521">Returns an array with all the elements after the specified number in the array.</span></span>

| <span data-ttu-id="3293f-522">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-522">Parameter</span></span> | <span data-ttu-id="3293f-523">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-523">Required</span></span> | <span data-ttu-id="3293f-524">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-524">Type</span></span> | <span data-ttu-id="3293f-525">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-525">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-526">originalValue</span><span class="sxs-lookup"><span data-stu-id="3293f-526">originalValue</span></span> |<span data-ttu-id="3293f-527">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-527">Yes</span></span> |<span data-ttu-id="3293f-528">Array</span><span class="sxs-lookup"><span data-stu-id="3293f-528">Array</span></span> |<span data-ttu-id="3293f-529">The array to use for skipping.</span><span class="sxs-lookup"><span data-stu-id="3293f-529">The array to use for skipping.</span></span> |
| <span data-ttu-id="3293f-530">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="3293f-530">numberToSkip</span></span> |<span data-ttu-id="3293f-531">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-531">Yes</span></span> |<span data-ttu-id="3293f-532">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-532">Integer</span></span> |<span data-ttu-id="3293f-533">The number of elements to skip.</span><span class="sxs-lookup"><span data-stu-id="3293f-533">The number of elements to skip.</span></span> <span data-ttu-id="3293f-534">If this value is 0 or less, all the elements in the array are returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-534">If this value is 0 or less, all the elements in the array are returned.</span></span> <span data-ttu-id="3293f-535">If it is larger than the length of the array, an empty array is returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-535">If it is larger than the length of the array, an empty array is returned.</span></span> |

<span data-ttu-id="3293f-536">For an example of using skip with a string, see [skip - string](#skipstring).</span><span class="sxs-lookup"><span data-stu-id="3293f-536">For an example of using skip with a string, see [skip - string](#skipstring).</span></span>

<span data-ttu-id="3293f-537">The following example skips the specified number of elements in the array.</span><span class="sxs-lookup"><span data-stu-id="3293f-537">The following example skips the specified number of elements in the array.</span></span>

```json
"parameters": {
  "first": {
    "type": "array",
    "metadata": {
      "description": "Values to use for skipping"
    },
    "defaultValue": [ "one", "two", "three" ]
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Number of elements to skip"
    }
  }
},
"resources": [
],
"outputs": {
  "return": {
    "type": "array",
    "value": "[skip(parameters('first'), parameters('second'))]"
  }
}
```

<a id="take" />

### <a name="take---array"></a><span data-ttu-id="3293f-538">take - array</span><span class="sxs-lookup"><span data-stu-id="3293f-538">take - array</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="3293f-539">Returns an array with the specified number of elements from the start of the array.</span><span class="sxs-lookup"><span data-stu-id="3293f-539">Returns an array with the specified number of elements from the start of the array.</span></span>

| <span data-ttu-id="3293f-540">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-540">Parameter</span></span> | <span data-ttu-id="3293f-541">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-541">Required</span></span> | <span data-ttu-id="3293f-542">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-542">Type</span></span> | <span data-ttu-id="3293f-543">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-543">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-544">originalValue</span><span class="sxs-lookup"><span data-stu-id="3293f-544">originalValue</span></span> |<span data-ttu-id="3293f-545">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-545">Yes</span></span> |<span data-ttu-id="3293f-546">Array</span><span class="sxs-lookup"><span data-stu-id="3293f-546">Array</span></span> |<span data-ttu-id="3293f-547">The array to take the elements from.</span><span class="sxs-lookup"><span data-stu-id="3293f-547">The array to take the elements from.</span></span> |
| <span data-ttu-id="3293f-548">numberToTake</span><span class="sxs-lookup"><span data-stu-id="3293f-548">numberToTake</span></span> |<span data-ttu-id="3293f-549">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-549">Yes</span></span> |<span data-ttu-id="3293f-550">Integer</span><span class="sxs-lookup"><span data-stu-id="3293f-550">Integer</span></span> |<span data-ttu-id="3293f-551">The number of elements to take.</span><span class="sxs-lookup"><span data-stu-id="3293f-551">The number of elements to take.</span></span> <span data-ttu-id="3293f-552">If this value is 0 or less, an empty array is returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-552">If this value is 0 or less, an empty array is returned.</span></span> <span data-ttu-id="3293f-553">If it is larger than the length of the given array, all the elements in the array are returned.</span><span class="sxs-lookup"><span data-stu-id="3293f-553">If it is larger than the length of the given array, all the elements in the array are returned.</span></span> |

<span data-ttu-id="3293f-554">For an example of using take with a string, see [take - string](#takestring).</span><span class="sxs-lookup"><span data-stu-id="3293f-554">For an example of using take with a string, see [take - string](#takestring).</span></span>

<span data-ttu-id="3293f-555">The following example takes the specified number of elements from the array.</span><span class="sxs-lookup"><span data-stu-id="3293f-555">The following example takes the specified number of elements from the array.</span></span>

```json
"parameters": {
  "first": {
    "type": "array",
    "metadata": {
      "description": "Values to use for taking"
    },
    "defaultValue": [ "one", "two", "three" ]
  },
  "second": {
    "type": "int",
    "metadata": {
      "description": "Number of elements to take"
    }
  }
},
"resources": [
],
"outputs": {
  "return": {
    "type": "array",
    "value": "[take(parameters('first'),parameters('second'))]"
  }
}
```

## <a name="deployment-value-functions"></a><span data-ttu-id="3293f-556">Deployment value functions</span><span class="sxs-lookup"><span data-stu-id="3293f-556">Deployment value functions</span></span>
<span data-ttu-id="3293f-557">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span><span class="sxs-lookup"><span data-stu-id="3293f-557">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="3293f-558">deployment</span><span class="sxs-lookup"><span data-stu-id="3293f-558">deployment</span></span>](#deployment)
* [<span data-ttu-id="3293f-559">parameters</span><span class="sxs-lookup"><span data-stu-id="3293f-559">parameters</span></span>](#parameters)
* [<span data-ttu-id="3293f-560">variables</span><span class="sxs-lookup"><span data-stu-id="3293f-560">variables</span></span>](#variables)

<span data-ttu-id="3293f-561">To get values from resources, resource groups, or subscriptions, see [Resource functions](#resource-functions).</span><span class="sxs-lookup"><span data-stu-id="3293f-561">To get values from resources, resource groups, or subscriptions, see [Resource functions](#resource-functions).</span></span>

<a id="deployment" />

### <a name="deployment"></a><span data-ttu-id="3293f-562">deployment</span><span class="sxs-lookup"><span data-stu-id="3293f-562">deployment</span></span>
`deployment()`

<span data-ttu-id="3293f-563">Returns information about the current deployment operation.</span><span class="sxs-lookup"><span data-stu-id="3293f-563">Returns information about the current deployment operation.</span></span>

<span data-ttu-id="3293f-564">This function returns the object that is passed during deployment.</span><span class="sxs-lookup"><span data-stu-id="3293f-564">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="3293f-565">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span><span class="sxs-lookup"><span data-stu-id="3293f-565">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> 

<span data-ttu-id="3293f-566">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-566">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

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

<span data-ttu-id="3293f-567">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-567">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

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

<span data-ttu-id="3293f-568">The following example shows how to use deployment() to link to another template based on the URI of the parent template.</span><span class="sxs-lookup"><span data-stu-id="3293f-568">The following example shows how to use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

<a id="parameters" />

### <a name="parameters"></a><span data-ttu-id="3293f-569">parameters</span><span class="sxs-lookup"><span data-stu-id="3293f-569">parameters</span></span>
`parameters (parameterName)`

<span data-ttu-id="3293f-570">Returns a parameter value.</span><span class="sxs-lookup"><span data-stu-id="3293f-570">Returns a parameter value.</span></span> <span data-ttu-id="3293f-571">The specified parameter name must be defined in the parameters section of the template.</span><span class="sxs-lookup"><span data-stu-id="3293f-571">The specified parameter name must be defined in the parameters section of the template.</span></span>

| <span data-ttu-id="3293f-572">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-572">Parameter</span></span> | <span data-ttu-id="3293f-573">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-573">Required</span></span> | <span data-ttu-id="3293f-574">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-574">Type</span></span> | <span data-ttu-id="3293f-575">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-575">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-576">parameterName</span><span class="sxs-lookup"><span data-stu-id="3293f-576">parameterName</span></span> |<span data-ttu-id="3293f-577">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-577">Yes</span></span> |<span data-ttu-id="3293f-578">String</span><span class="sxs-lookup"><span data-stu-id="3293f-578">String</span></span> |<span data-ttu-id="3293f-579">The name of the parameter to return.</span><span class="sxs-lookup"><span data-stu-id="3293f-579">The name of the parameter to return.</span></span> |

<span data-ttu-id="3293f-580">The following example shows a simplified use of the parameters function.</span><span class="sxs-lookup"><span data-stu-id="3293f-580">The following example shows a simplified use of the parameters function.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2014-06-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

<a id="variables" />

### <a name="variables"></a><span data-ttu-id="3293f-581">variables</span><span class="sxs-lookup"><span data-stu-id="3293f-581">variables</span></span>
`variables (variableName)`

<span data-ttu-id="3293f-582">Returns the value of variable.</span><span class="sxs-lookup"><span data-stu-id="3293f-582">Returns the value of variable.</span></span> <span data-ttu-id="3293f-583">The specified variable name must be defined in the variables section of the template.</span><span class="sxs-lookup"><span data-stu-id="3293f-583">The specified variable name must be defined in the variables section of the template.</span></span>

| <span data-ttu-id="3293f-584">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-584">Parameter</span></span> | <span data-ttu-id="3293f-585">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-585">Required</span></span> | <span data-ttu-id="3293f-586">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-586">Type</span></span> | <span data-ttu-id="3293f-587">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-587">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-588">variableName</span><span class="sxs-lookup"><span data-stu-id="3293f-588">variableName</span></span> |<span data-ttu-id="3293f-589">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-589">Yes</span></span> |<span data-ttu-id="3293f-590">String</span><span class="sxs-lookup"><span data-stu-id="3293f-590">String</span></span> |<span data-ttu-id="3293f-591">The name of the variable to return.</span><span class="sxs-lookup"><span data-stu-id="3293f-591">The name of the variable to return.</span></span> |

<span data-ttu-id="3293f-592">The following example uses a variable value.</span><span class="sxs-lookup"><span data-stu-id="3293f-592">The following example uses a variable value.</span></span>

```json
"variables": {
  "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
  {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageName')]",
    ...
  }
],
```

## <a name="resource-functions"></a><span data-ttu-id="3293f-593">Resource functions</span><span class="sxs-lookup"><span data-stu-id="3293f-593">Resource functions</span></span>
<span data-ttu-id="3293f-594">Resource Manager provides the following functions for getting resource values:</span><span class="sxs-lookup"><span data-stu-id="3293f-594">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="3293f-595">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="3293f-595">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="3293f-596">providers</span><span class="sxs-lookup"><span data-stu-id="3293f-596">providers</span></span>](#providers)
* [<span data-ttu-id="3293f-597">reference</span><span class="sxs-lookup"><span data-stu-id="3293f-597">reference</span></span>](#reference)
* [<span data-ttu-id="3293f-598">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="3293f-598">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="3293f-599">resourceId</span><span class="sxs-lookup"><span data-stu-id="3293f-599">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="3293f-600">subscription</span><span class="sxs-lookup"><span data-stu-id="3293f-600">subscription</span></span>](#subscription)

<span data-ttu-id="3293f-601">To get values from parameters, variables, or the current deployment, see [Deployment value functions](#deployment-value-functions).</span><span class="sxs-lookup"><span data-stu-id="3293f-601">To get values from parameters, variables, or the current deployment, see [Deployment value functions](#deployment-value-functions).</span></span>

<a id="listkeys" />
<a id="list" />

### <a name="listkeys-and-listvalue"></a><span data-ttu-id="3293f-602">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="3293f-602">listKeys and list{Value}</span></span>
`listKeys (resourceName or resourceIdentifier, apiVersion)`

`list{Value} (resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="3293f-603">Returns the values for any resource type that supports the list operation.</span><span class="sxs-lookup"><span data-stu-id="3293f-603">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="3293f-604">The most common usage is **listKeys**.</span><span class="sxs-lookup"><span data-stu-id="3293f-604">The most common usage is **listKeys**.</span></span> 

| <span data-ttu-id="3293f-605">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-605">Parameter</span></span> | <span data-ttu-id="3293f-606">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-606">Required</span></span> | <span data-ttu-id="3293f-607">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-607">Type</span></span> | <span data-ttu-id="3293f-608">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-609">resourceName or resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="3293f-609">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="3293f-610">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-610">Yes</span></span> |<span data-ttu-id="3293f-611">String</span><span class="sxs-lookup"><span data-stu-id="3293f-611">String</span></span> |<span data-ttu-id="3293f-612">Unique identifier for the resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-612">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="3293f-613">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3293f-613">apiVersion</span></span> |<span data-ttu-id="3293f-614">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-614">Yes</span></span> |<span data-ttu-id="3293f-615">String</span><span class="sxs-lookup"><span data-stu-id="3293f-615">String</span></span> |<span data-ttu-id="3293f-616">API version of resource runtime state.</span><span class="sxs-lookup"><span data-stu-id="3293f-616">API version of resource runtime state.</span></span> <span data-ttu-id="3293f-617">Typically, in the format, **yyyy-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="3293f-617">Typically, in the format, **yyyy-mm-dd**.</span></span> |

<span data-ttu-id="3293f-618">Any operation that starts with **list** can be used as a function in your template.</span><span class="sxs-lookup"><span data-stu-id="3293f-618">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="3293f-619">The available operations include not only **listKeys**, but also operations like **list**, **listAdminKeys**, and **listStatus**.</span><span class="sxs-lookup"><span data-stu-id="3293f-619">The available operations include not only **listKeys**, but also operations like **list**, **listAdminKeys**, and **listStatus**.</span></span> <span data-ttu-id="3293f-620">To determine which resource types have a list operation, see the [REST API operations](/rest/api/) for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3293f-620">To determine which resource types have a list operation, see the [REST API operations](/rest/api/) for the resource provider.</span></span>

<span data-ttu-id="3293f-621">To find the list operations for a resource provider, use the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3293f-621">To find the list operations for a resource provider, use the following PowerShell cmdlet:</span></span>

```powershell
Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
```

<span data-ttu-id="3293f-622">To find the list operations for a resource provider, use the following Azure CLI command, and the JSON utility [jq](http://stedolan.github.io/jq/download/) to filter only the list operations:</span><span class="sxs-lookup"><span data-stu-id="3293f-622">To find the list operations for a resource provider, use the following Azure CLI command, and the JSON utility [jq](http://stedolan.github.io/jq/download/) to filter only the list operations:</span></span>

```azurecli
azure provider operations show --operationSearchString */apiapps/* --json | jq ".[] | select (.operation | contains(\"list\"))"
```

<span data-ttu-id="3293f-623">The resourceId can be specified by using the [resourceId function](#resourceid) or by using the format **{providerNamespace}/{resourceType}/{resourceName}**.</span><span class="sxs-lookup"><span data-stu-id="3293f-623">The resourceId can be specified by using the [resourceId function](#resourceid) or by using the format **{providerNamespace}/{resourceType}/{resourceName}**.</span></span>

<span data-ttu-id="3293f-624">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span><span class="sxs-lookup"><span data-stu-id="3293f-624">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

```json
"outputs": { 
  "listKeysOutput": { 
    "value": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2016-01-01')]", 
    "type" : "object" 
  } 
}
``` 

<span data-ttu-id="3293f-625">The returned object from listKeys has the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-625">The returned object from listKeys has the following format:</span></span>

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

<a id="providers" />

### <a name="providers"></a><span data-ttu-id="3293f-626">providers</span><span class="sxs-lookup"><span data-stu-id="3293f-626">providers</span></span>
`providers (providerNamespace, [resourceType])`

<span data-ttu-id="3293f-627">Returns information about a resource provider and its supported resource types.</span><span class="sxs-lookup"><span data-stu-id="3293f-627">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="3293f-628">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="3293f-628">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

| <span data-ttu-id="3293f-629">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-629">Parameter</span></span> | <span data-ttu-id="3293f-630">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-630">Required</span></span> | <span data-ttu-id="3293f-631">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-631">Type</span></span> | <span data-ttu-id="3293f-632">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-632">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-633">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="3293f-633">providerNamespace</span></span> |<span data-ttu-id="3293f-634">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-634">Yes</span></span> |<span data-ttu-id="3293f-635">String</span><span class="sxs-lookup"><span data-stu-id="3293f-635">String</span></span> |<span data-ttu-id="3293f-636">Namespace of the provider</span><span class="sxs-lookup"><span data-stu-id="3293f-636">Namespace of the provider</span></span> |
| <span data-ttu-id="3293f-637">resourceType</span><span class="sxs-lookup"><span data-stu-id="3293f-637">resourceType</span></span> |<span data-ttu-id="3293f-638">No</span><span class="sxs-lookup"><span data-stu-id="3293f-638">No</span></span> |<span data-ttu-id="3293f-639">String</span><span class="sxs-lookup"><span data-stu-id="3293f-639">String</span></span> |<span data-ttu-id="3293f-640">The type of resource within the specified namespace.</span><span class="sxs-lookup"><span data-stu-id="3293f-640">The type of resource within the specified namespace.</span></span> |

<span data-ttu-id="3293f-641">Each supported type is returned in the following format.</span><span class="sxs-lookup"><span data-stu-id="3293f-641">Each supported type is returned in the following format.</span></span> <span data-ttu-id="3293f-642">Array ordering is not guaranteed.</span><span class="sxs-lookup"><span data-stu-id="3293f-642">Array ordering is not guaranteed.</span></span>

```json
{
    "resourceType": "",
    "locations": [ ],
    "apiVersions": [ ]
}
```

<span data-ttu-id="3293f-643">The following example shows how to use the provider function:</span><span class="sxs-lookup"><span data-stu-id="3293f-643">The following example shows how to use the provider function:</span></span>

```json
"outputs": {
    "exampleOutput": {
        "value": "[providers('Microsoft.Storage', 'storageAccounts')]",
        "type" : "object"
    }
}
```

<a id="reference" />

### <a name="reference"></a><span data-ttu-id="3293f-644">reference</span><span class="sxs-lookup"><span data-stu-id="3293f-644">reference</span></span>
`reference (resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="3293f-645">Returns an object representing another resource's runtime state.</span><span class="sxs-lookup"><span data-stu-id="3293f-645">Returns an object representing another resource's runtime state.</span></span>

| <span data-ttu-id="3293f-646">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-646">Parameter</span></span> | <span data-ttu-id="3293f-647">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-647">Required</span></span> | <span data-ttu-id="3293f-648">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-648">Type</span></span> | <span data-ttu-id="3293f-649">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-649">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-650">resourceName or resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="3293f-650">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="3293f-651">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-651">Yes</span></span> |<span data-ttu-id="3293f-652">String</span><span class="sxs-lookup"><span data-stu-id="3293f-652">String</span></span> |<span data-ttu-id="3293f-653">Name or unique identifier of a resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-653">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="3293f-654">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3293f-654">apiVersion</span></span> |<span data-ttu-id="3293f-655">No</span><span class="sxs-lookup"><span data-stu-id="3293f-655">No</span></span> |<span data-ttu-id="3293f-656">String</span><span class="sxs-lookup"><span data-stu-id="3293f-656">String</span></span> |<span data-ttu-id="3293f-657">API version of the specified resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-657">API version of the specified resource.</span></span> <span data-ttu-id="3293f-658">Include this parameter when the resource is not provisioned within same template.</span><span class="sxs-lookup"><span data-stu-id="3293f-658">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="3293f-659">Typically, in the format, **yyyy-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="3293f-659">Typically, in the format, **yyyy-mm-dd**.</span></span> |

<span data-ttu-id="3293f-660">The **reference** function derives its value from a runtime state, and therefore cannot be used in the variables section.</span><span class="sxs-lookup"><span data-stu-id="3293f-660">The **reference** function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="3293f-661">It can be used in outputs section of a template.</span><span class="sxs-lookup"><span data-stu-id="3293f-661">It can be used in outputs section of a template.</span></span>

<span data-ttu-id="3293f-662">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span><span class="sxs-lookup"><span data-stu-id="3293f-662">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="3293f-663">You do not need to also use the **dependsOn** property.</span><span class="sxs-lookup"><span data-stu-id="3293f-663">You do not need to also use the **dependsOn** property.</span></span> <span data-ttu-id="3293f-664">The function is not evaluated until the referenced resource has completed deployment.</span><span class="sxs-lookup"><span data-stu-id="3293f-664">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="3293f-665">The following example references a storage account that is deployed in the same template.</span><span class="sxs-lookup"><span data-stu-id="3293f-665">The following example references a storage account that is deployed in the same template.</span></span>

```json
"outputs": {
    "NewStorage": {
        "value": "[reference(parameters('storageAccountName'))]",
        "type" : "object"
    }
}
```

<span data-ttu-id="3293f-666">The following example references a storage account that is not deployed in this template, but exists within the same resource group as the resources being deployed.</span><span class="sxs-lookup"><span data-stu-id="3293f-666">The following example references a storage account that is not deployed in this template, but exists within the same resource group as the resources being deployed.</span></span>

```json
"outputs": {
    "ExistingStorage": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
        "type" : "object"
    }
}
```

<span data-ttu-id="3293f-667">You can retrieve a particular value from the returned object, such as the blob endpoint URI, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3293f-667">You can retrieve a particular value from the returned object, such as the blob endpoint URI, as shown in the following example:</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    }
}
```

<span data-ttu-id="3293f-668">The following example references a storage account in a different resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-668">The following example references a storage account in a different resource group.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(resourceId(parameters('relatedGroup'), 'Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    }
}
```

<span data-ttu-id="3293f-669">The properties on the object returned from the **reference** function vary by resource type.</span><span class="sxs-lookup"><span data-stu-id="3293f-669">The properties on the object returned from the **reference** function vary by resource type.</span></span> <span data-ttu-id="3293f-670">To see the property names and values for a resource type, create a simple template that returns the object in the **outputs** section.</span><span class="sxs-lookup"><span data-stu-id="3293f-670">To see the property names and values for a resource type, create a simple template that returns the object in the **outputs** section.</span></span> <span data-ttu-id="3293f-671">If you have an existing resource of that type, your template just returns the object without deploying any new resources.</span><span class="sxs-lookup"><span data-stu-id="3293f-671">If you have an existing resource of that type, your template just returns the object without deploying any new resources.</span></span> <span data-ttu-id="3293f-672">If you do not have an existing resource of that type, your template deploys only that type and returns the object.</span><span class="sxs-lookup"><span data-stu-id="3293f-672">If you do not have an existing resource of that type, your template deploys only that type and returns the object.</span></span> <span data-ttu-id="3293f-673">Then, add those properties to other templates that need to dynamically retrieve the values during deployment.</span><span class="sxs-lookup"><span data-stu-id="3293f-673">Then, add those properties to other templates that need to dynamically retrieve the values during deployment.</span></span> 

<a id="resourcegroup" />

### <a name="resourcegroup"></a><span data-ttu-id="3293f-674">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="3293f-674">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="3293f-675">Returns an object that represents the current resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-675">Returns an object that represents the current resource group.</span></span> 

<span data-ttu-id="3293f-676">The returned object is in the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-676">The returned object is in the following format:</span></span>

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

<span data-ttu-id="3293f-677">The following example uses the resource group location to assign the location for a web site.</span><span class="sxs-lookup"><span data-stu-id="3293f-677">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2014-06-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

<a id="resourceid" />

### <a name="resourceid"></a><span data-ttu-id="3293f-678">resourceId</span><span class="sxs-lookup"><span data-stu-id="3293f-678">resourceId</span></span>
`resourceId ([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="3293f-679">Returns the unique identifier of a resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-679">Returns the unique identifier of a resource.</span></span> 

| <span data-ttu-id="3293f-680">Parameter</span><span class="sxs-lookup"><span data-stu-id="3293f-680">Parameter</span></span> | <span data-ttu-id="3293f-681">Required</span><span class="sxs-lookup"><span data-stu-id="3293f-681">Required</span></span> | <span data-ttu-id="3293f-682">Type</span><span class="sxs-lookup"><span data-stu-id="3293f-682">Type</span></span> | <span data-ttu-id="3293f-683">Description</span><span class="sxs-lookup"><span data-stu-id="3293f-683">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3293f-684">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3293f-684">subscriptionId</span></span> |<span data-ttu-id="3293f-685">No</span><span class="sxs-lookup"><span data-stu-id="3293f-685">No</span></span> |<span data-ttu-id="3293f-686">String (In GUID format)</span><span class="sxs-lookup"><span data-stu-id="3293f-686">String (In GUID format)</span></span> |<span data-ttu-id="3293f-687">Default value is the current subscription.</span><span class="sxs-lookup"><span data-stu-id="3293f-687">Default value is the current subscription.</span></span> <span data-ttu-id="3293f-688">Specify this value when you need to retrieve a resource in another subscription.</span><span class="sxs-lookup"><span data-stu-id="3293f-688">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="3293f-689">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3293f-689">resourceGroupName</span></span> |<span data-ttu-id="3293f-690">No</span><span class="sxs-lookup"><span data-stu-id="3293f-690">No</span></span> |<span data-ttu-id="3293f-691">String</span><span class="sxs-lookup"><span data-stu-id="3293f-691">String</span></span> |<span data-ttu-id="3293f-692">Default value is current resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-692">Default value is current resource group.</span></span> <span data-ttu-id="3293f-693">Specify this value when you need to retrieve a resource in another resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-693">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="3293f-694">resourceType</span><span class="sxs-lookup"><span data-stu-id="3293f-694">resourceType</span></span> |<span data-ttu-id="3293f-695">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-695">Yes</span></span> |<span data-ttu-id="3293f-696">String</span><span class="sxs-lookup"><span data-stu-id="3293f-696">String</span></span> |<span data-ttu-id="3293f-697">Type of resource including resource provider namespace.</span><span class="sxs-lookup"><span data-stu-id="3293f-697">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="3293f-698">resourceName1</span><span class="sxs-lookup"><span data-stu-id="3293f-698">resourceName1</span></span> |<span data-ttu-id="3293f-699">Yes</span><span class="sxs-lookup"><span data-stu-id="3293f-699">Yes</span></span> |<span data-ttu-id="3293f-700">String</span><span class="sxs-lookup"><span data-stu-id="3293f-700">String</span></span> |<span data-ttu-id="3293f-701">Name of resource.</span><span class="sxs-lookup"><span data-stu-id="3293f-701">Name of resource.</span></span> |
| <span data-ttu-id="3293f-702">resourceName2</span><span class="sxs-lookup"><span data-stu-id="3293f-702">resourceName2</span></span> |<span data-ttu-id="3293f-703">No</span><span class="sxs-lookup"><span data-stu-id="3293f-703">No</span></span> |<span data-ttu-id="3293f-704">String</span><span class="sxs-lookup"><span data-stu-id="3293f-704">String</span></span> |<span data-ttu-id="3293f-705">Next resource name segment if resource is nested.</span><span class="sxs-lookup"><span data-stu-id="3293f-705">Next resource name segment if resource is nested.</span></span> |

<span data-ttu-id="3293f-706">You use this function when the resource name is ambiguous or not provisioned within the same template.</span><span class="sxs-lookup"><span data-stu-id="3293f-706">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> <span data-ttu-id="3293f-707">The identifier is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-707">The identifier is returned in the following format:</span></span>

    /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/{resourceProviderNamespace}/{resourceType}/{resourceName}

<span data-ttu-id="3293f-708">The following example shows how to retrieve the resource ids for a web site and a database.</span><span class="sxs-lookup"><span data-stu-id="3293f-708">The following example shows how to retrieve the resource ids for a web site and a database.</span></span> <span data-ttu-id="3293f-709">The web site exists in a resource group named **myWebsitesGroup** and the database exists in the current resource group for this template.</span><span class="sxs-lookup"><span data-stu-id="3293f-709">The web site exists in a resource group named **myWebsitesGroup** and the database exists in the current resource group for this template.</span></span>

```json
[resourceId('myWebsitesGroup', 'Microsoft.Web/sites', parameters('siteName'))]
[resourceId('Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]
```

<span data-ttu-id="3293f-710">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-710">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="3293f-711">The storage account or virtual network may be used across multiple resource groups; therefore, you do not want to delete them when deleting a single resource group.</span><span class="sxs-lookup"><span data-stu-id="3293f-711">The storage account or virtual network may be used across multiple resource groups; therefore, you do not want to delete them when deleting a single resource group.</span></span> <span data-ttu-id="3293f-712">The following example shows how a resource from an external resource group can easily be used:</span><span class="sxs-lookup"><span data-stu-id="3293f-712">The following example shows how a resource from an external resource group can easily be used:</span></span>

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

<a id="subscription" />

### <a name="subscription"></a><span data-ttu-id="3293f-713">subscription</span><span class="sxs-lookup"><span data-stu-id="3293f-713">subscription</span></span>
`subscription()`

<span data-ttu-id="3293f-714">Returns details about the subscription in the following format:</span><span class="sxs-lookup"><span data-stu-id="3293f-714">Returns details about the subscription in the following format:</span></span>

```json
{
    "id": "/subscriptions/#####",
    "subscriptionId": "#####",
    "tenantId": "#####"
}
```

<span data-ttu-id="3293f-715">The following example shows the subscription function called in the outputs section.</span><span class="sxs-lookup"><span data-stu-id="3293f-715">The following example shows the subscription function called in the outputs section.</span></span> 

```json
"outputs": { 
  "exampleOutput": { 
      "value": "[subscription()]", 
      "type" : "object" 
  } 
} 
```

## <a name="next-steps"></a><span data-ttu-id="3293f-716">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3293f-716">Next Steps</span></span>
* <span data-ttu-id="3293f-717">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3293f-717">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="3293f-718">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3293f-718">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="3293f-719">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="3293f-719">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="3293f-720">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="3293f-720">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

