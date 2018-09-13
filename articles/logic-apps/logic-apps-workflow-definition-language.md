---
title: Schema reference for Workflow Definition Language - Azure Logic Apps | Microsoft Docs
description: Write custom workflow definitions for Azure Logic Apps with the Workflow Definition Language
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: reference
ms.date: 04/30/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: d5dadd054f95e61626942a1cab7d95ba8c9182e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783463"
---
# <a name="schema-reference-for-workflow-definition-language-in-azure-logic-apps"></a><span data-ttu-id="77fc8-103">Schema reference for Workflow Definition Language in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="77fc8-103">Schema reference for Workflow Definition Language in Azure Logic Apps</span></span>

<span data-ttu-id="77fc8-104">When you create a logic app workflow with [Azure Logic Apps](../logic-apps/logic-apps-overview.md), your workflow's underlying definition describes the actual logic that runs for your logic app.</span><span class="sxs-lookup"><span data-stu-id="77fc8-104">When you create a logic app workflow with [Azure Logic Apps](../logic-apps/logic-apps-overview.md), your workflow's underlying definition describes the actual logic that runs for your logic app.</span></span> <span data-ttu-id="77fc8-105">This description follows a structure that's defined and validated by the Workflow Definition Language schema, which uses [JavaScript Object Notation (JSON)](https://www.json.org/).</span><span class="sxs-lookup"><span data-stu-id="77fc8-105">This description follows a structure that's defined and validated by the Workflow Definition Language schema, which uses [JavaScript Object Notation (JSON)](https://www.json.org/).</span></span> 
  
## <a name="workflow-definition-structure"></a><span data-ttu-id="77fc8-106">Workflow definition structure</span><span class="sxs-lookup"><span data-stu-id="77fc8-106">Workflow definition structure</span></span>

<span data-ttu-id="77fc8-107">A workflow definition has at least one trigger that instantiates your logic app, plus one or more actions that your logic app runs.</span><span class="sxs-lookup"><span data-stu-id="77fc8-107">A workflow definition has at least one trigger that instantiates your logic app, plus one or more actions that your logic app runs.</span></span> 

<span data-ttu-id="77fc8-108">Here is the high-level structure for a workflow definition:</span><span class="sxs-lookup"><span data-stu-id="77fc8-108">Here is the high-level structure for a workflow definition:</span></span>  
  
```json
"definition": {
  "$schema": "<workflow-definition-language-schema-version>",
  "contentVersion": "<workflow-definition-version-number>",
  "parameters": { "<workflow-parameter-definitions>" },
  "triggers": { "<workflow-trigger-definitions>" },
  "actions": { "<workflow-action-definitions>" },
  "outputs": { "<workflow-output-definitions>" }
}
```
  
| <span data-ttu-id="77fc8-109">Element</span><span class="sxs-lookup"><span data-stu-id="77fc8-109">Element</span></span> | <span data-ttu-id="77fc8-110">Required</span><span class="sxs-lookup"><span data-stu-id="77fc8-110">Required</span></span> | <span data-ttu-id="77fc8-111">Description</span><span class="sxs-lookup"><span data-stu-id="77fc8-111">Description</span></span> | 
|---------|----------|-------------| 
| <span data-ttu-id="77fc8-112">definition</span><span class="sxs-lookup"><span data-stu-id="77fc8-112">definition</span></span> | <span data-ttu-id="77fc8-113">Yes</span><span class="sxs-lookup"><span data-stu-id="77fc8-113">Yes</span></span> | <span data-ttu-id="77fc8-114">The starting element for your workflow definition</span><span class="sxs-lookup"><span data-stu-id="77fc8-114">The starting element for your workflow definition</span></span> | 
| <span data-ttu-id="77fc8-115">$schema</span><span class="sxs-lookup"><span data-stu-id="77fc8-115">$schema</span></span> | <span data-ttu-id="77fc8-116">Only when externally referencing a workflow definition</span><span class="sxs-lookup"><span data-stu-id="77fc8-116">Only when externally referencing a workflow definition</span></span> | <span data-ttu-id="77fc8-117">The location for the JSON schema file that describes the Workflow Definition Language version, which you can find here:</span><span class="sxs-lookup"><span data-stu-id="77fc8-117">The location for the JSON schema file that describes the Workflow Definition Language version, which you can find here:</span></span> <p>`https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json`</p> |   
| <span data-ttu-id="77fc8-118">contentVersion</span><span class="sxs-lookup"><span data-stu-id="77fc8-118">contentVersion</span></span> | <span data-ttu-id="77fc8-119">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-119">No</span></span> | <span data-ttu-id="77fc8-120">The version number for your workflow definition, which is "1.0.0.0" by default.</span><span class="sxs-lookup"><span data-stu-id="77fc8-120">The version number for your workflow definition, which is "1.0.0.0" by default.</span></span> <span data-ttu-id="77fc8-121">To help identify and confirm the correct definition when deploying a workflow, specify a value to use.</span><span class="sxs-lookup"><span data-stu-id="77fc8-121">To help identify and confirm the correct definition when deploying a workflow, specify a value to use.</span></span> | 
| <span data-ttu-id="77fc8-122">parameters</span><span class="sxs-lookup"><span data-stu-id="77fc8-122">parameters</span></span> | <span data-ttu-id="77fc8-123">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-123">No</span></span> | <span data-ttu-id="77fc8-124">The definitions for one or more parameters that pass data into your workflow</span><span class="sxs-lookup"><span data-stu-id="77fc8-124">The definitions for one or more parameters that pass data into your workflow</span></span> <p><p><span data-ttu-id="77fc8-125">Maximum parameters: 50</span><span class="sxs-lookup"><span data-stu-id="77fc8-125">Maximum parameters: 50</span></span> | 
| <span data-ttu-id="77fc8-126">triggers</span><span class="sxs-lookup"><span data-stu-id="77fc8-126">triggers</span></span> | <span data-ttu-id="77fc8-127">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-127">No</span></span> | <span data-ttu-id="77fc8-128">The definitions for one or more triggers that instantiate your workflow.</span><span class="sxs-lookup"><span data-stu-id="77fc8-128">The definitions for one or more triggers that instantiate your workflow.</span></span> <span data-ttu-id="77fc8-129">You can define more than one trigger, but only with the Workflow Definition Language, not visually through the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="77fc8-129">You can define more than one trigger, but only with the Workflow Definition Language, not visually through the Logic Apps Designer.</span></span> <p><p><span data-ttu-id="77fc8-130">Maximum triggers: 10</span><span class="sxs-lookup"><span data-stu-id="77fc8-130">Maximum triggers: 10</span></span> | 
| <span data-ttu-id="77fc8-131">actions</span><span class="sxs-lookup"><span data-stu-id="77fc8-131">actions</span></span> | <span data-ttu-id="77fc8-132">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-132">No</span></span> | <span data-ttu-id="77fc8-133">The definitions for one or more actions to execute at workflow runtime</span><span class="sxs-lookup"><span data-stu-id="77fc8-133">The definitions for one or more actions to execute at workflow runtime</span></span> <p><p><span data-ttu-id="77fc8-134">Maximum actions: 250</span><span class="sxs-lookup"><span data-stu-id="77fc8-134">Maximum actions: 250</span></span> | 
| <span data-ttu-id="77fc8-135">outputs</span><span class="sxs-lookup"><span data-stu-id="77fc8-135">outputs</span></span> | <span data-ttu-id="77fc8-136">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-136">No</span></span> | <span data-ttu-id="77fc8-137">The definitions for the outputs that return from a workflow run</span><span class="sxs-lookup"><span data-stu-id="77fc8-137">The definitions for the outputs that return from a workflow run</span></span> <p><p><span data-ttu-id="77fc8-138">Maximum outputs: 10</span><span class="sxs-lookup"><span data-stu-id="77fc8-138">Maximum outputs: 10</span></span> |  
|||| 

## <a name="parameters"></a><span data-ttu-id="77fc8-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="77fc8-139">Parameters</span></span>

<span data-ttu-id="77fc8-140">In the `parameters` section, define all the workflow parameters that your logic app uses at deployment for accepting inputs.</span><span class="sxs-lookup"><span data-stu-id="77fc8-140">In the `parameters` section, define all the workflow parameters that your logic app uses at deployment for accepting inputs.</span></span> <span data-ttu-id="77fc8-141">Both parameter declarations and parameter values are required at deployment.</span><span class="sxs-lookup"><span data-stu-id="77fc8-141">Both parameter declarations and parameter values are required at deployment.</span></span> <span data-ttu-id="77fc8-142">Before you can use these parameters in other workflow sections, make sure that you declare all the parameters in these sections.</span><span class="sxs-lookup"><span data-stu-id="77fc8-142">Before you can use these parameters in other workflow sections, make sure that you declare all the parameters in these sections.</span></span> 

<span data-ttu-id="77fc8-143">Here is the general structure for a parameter definition:</span><span class="sxs-lookup"><span data-stu-id="77fc8-143">Here is the general structure for a parameter definition:</span></span>  

```json
"parameters": {
  "<parameter-name>": {
    "type": "<parameter-type>",
    "defaultValue": "<default-parameter-value>",
    "allowedValues": [ <array-with-permitted-parameter-values> ],
    "metadata": { 
      "key": { 
        "name": "<key-value>"
      } 
    }
  }
},
```

| <span data-ttu-id="77fc8-144">Element</span><span class="sxs-lookup"><span data-stu-id="77fc8-144">Element</span></span> | <span data-ttu-id="77fc8-145">Required</span><span class="sxs-lookup"><span data-stu-id="77fc8-145">Required</span></span> | <span data-ttu-id="77fc8-146">Type</span><span class="sxs-lookup"><span data-stu-id="77fc8-146">Type</span></span> | <span data-ttu-id="77fc8-147">Description</span><span class="sxs-lookup"><span data-stu-id="77fc8-147">Description</span></span> |  
|---------|----------|------|-------------|  
| <span data-ttu-id="77fc8-148">type</span><span class="sxs-lookup"><span data-stu-id="77fc8-148">type</span></span> | <span data-ttu-id="77fc8-149">Yes</span><span class="sxs-lookup"><span data-stu-id="77fc8-149">Yes</span></span> | <span data-ttu-id="77fc8-150">int, float, string, securestring, bool, array, JSON object, secureobject</span><span class="sxs-lookup"><span data-stu-id="77fc8-150">int, float, string, securestring, bool, array, JSON object, secureobject</span></span> <p><p><span data-ttu-id="77fc8-151">**Note**: For all passwords, keys, and secrets, use the `securestring` and `secureobject` types because the `GET` operation doesn't return these types.</span><span class="sxs-lookup"><span data-stu-id="77fc8-151">**Note**: For all passwords, keys, and secrets, use the `securestring` and `secureobject` types because the `GET` operation doesn't return these types.</span></span> | <span data-ttu-id="77fc8-152">The type for the parameter</span><span class="sxs-lookup"><span data-stu-id="77fc8-152">The type for the parameter</span></span> |
| <span data-ttu-id="77fc8-153">defaultValue</span><span class="sxs-lookup"><span data-stu-id="77fc8-153">defaultValue</span></span> | <span data-ttu-id="77fc8-154">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-154">No</span></span> | <span data-ttu-id="77fc8-155">Same as `type`</span><span class="sxs-lookup"><span data-stu-id="77fc8-155">Same as `type`</span></span> | <span data-ttu-id="77fc8-156">The default parameter value when no value is specified when the workflow instantiates</span><span class="sxs-lookup"><span data-stu-id="77fc8-156">The default parameter value when no value is specified when the workflow instantiates</span></span> | 
| <span data-ttu-id="77fc8-157">allowedValues</span><span class="sxs-lookup"><span data-stu-id="77fc8-157">allowedValues</span></span> | <span data-ttu-id="77fc8-158">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-158">No</span></span> | <span data-ttu-id="77fc8-159">Same as `type`</span><span class="sxs-lookup"><span data-stu-id="77fc8-159">Same as `type`</span></span> | <span data-ttu-id="77fc8-160">An array with values that the parameter can accept</span><span class="sxs-lookup"><span data-stu-id="77fc8-160">An array with values that the parameter can accept</span></span> |  
| <span data-ttu-id="77fc8-161">metadata</span><span class="sxs-lookup"><span data-stu-id="77fc8-161">metadata</span></span> | <span data-ttu-id="77fc8-162">No</span><span class="sxs-lookup"><span data-stu-id="77fc8-162">No</span></span> | <span data-ttu-id="77fc8-163">JSON object</span><span class="sxs-lookup"><span data-stu-id="77fc8-163">JSON object</span></span> | <span data-ttu-id="77fc8-164">Any other parameter details, for example, the name or a readable description for your logic app, or design-time data used by Visual Studio or other tools</span><span class="sxs-lookup"><span data-stu-id="77fc8-164">Any other parameter details, for example, the name or a readable description for your logic app, or design-time data used by Visual Studio or other tools</span></span> |  
||||

## <a name="triggers-and-actions"></a><span data-ttu-id="77fc8-165">Triggers and actions</span><span class="sxs-lookup"><span data-stu-id="77fc8-165">Triggers and actions</span></span>  

<span data-ttu-id="77fc8-166">In a workflow definition, the `triggers` and `actions` sections define the calls that happen during your workflow's execution.</span><span class="sxs-lookup"><span data-stu-id="77fc8-166">In a workflow definition, the `triggers` and `actions` sections define the calls that happen during your workflow's execution.</span></span> <span data-ttu-id="77fc8-167">For syntax and more information about these sections, see [Workflow triggers and actions](../logic-apps/logic-apps-workflow-actions-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="77fc8-167">For syntax and more information about these sections, see [Workflow triggers and actions](../logic-apps/logic-apps-workflow-actions-triggers.md).</span></span>
  
## <a name="outputs"></a><span data-ttu-id="77fc8-168">Outputs</span><span class="sxs-lookup"><span data-stu-id="77fc8-168">Outputs</span></span> 

<span data-ttu-id="77fc8-169">In the `outputs` section, define the data that your workflow can return when finished running.</span><span class="sxs-lookup"><span data-stu-id="77fc8-169">In the `outputs` section, define the data that your workflow can return when finished running.</span></span> <span data-ttu-id="77fc8-170">For example, to track a specific status or value from each run, specify that the workflow output returns that data.</span><span class="sxs-lookup"><span data-stu-id="77fc8-170">For example, to track a specific status or value from each run, specify that the workflow output returns that data.</span></span> 

> [!NOTE]
> <span data-ttu-id="77fc8-171">When responding to incoming requests from a service's REST API, do not use `outputs`.</span><span class="sxs-lookup"><span data-stu-id="77fc8-171">When responding to incoming requests from a service's REST API, do not use `outputs`.</span></span> <span data-ttu-id="77fc8-172">Instead, use the `Response` action type.</span><span class="sxs-lookup"><span data-stu-id="77fc8-172">Instead, use the `Response` action type.</span></span> <span data-ttu-id="77fc8-173">For more information, see [Workflow triggers and actions](../logic-apps/logic-apps-workflow-actions-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="77fc8-173">For more information, see [Workflow triggers and actions](../logic-apps/logic-apps-workflow-actions-triggers.md).</span></span>

<span data-ttu-id="77fc8-174">Here is the general structure for an output definition:</span><span class="sxs-lookup"><span data-stu-id="77fc8-174">Here is the general structure for an output definition:</span></span> 

```json
"outputs": {
  "<key-name>": {  
    "type": "<key-type>",  
    "value": "<key-value>"  
  }
} 
```

| <span data-ttu-id="77fc8-175">Element</span><span class="sxs-lookup"><span data-stu-id="77fc8-175">Element</span></span> | <span data-ttu-id="77fc8-176">Required</span><span class="sxs-lookup"><span data-stu-id="77fc8-176">Required</span></span> | <span data-ttu-id="77fc8-177">Type</span><span class="sxs-lookup"><span data-stu-id="77fc8-177">Type</span></span> | <span data-ttu-id="77fc8-178">Description</span><span class="sxs-lookup"><span data-stu-id="77fc8-178">Description</span></span> | 
|---------|----------|------|-------------| 
| <span data-ttu-id="77fc8-179"><*key-name*></span><span class="sxs-lookup"><span data-stu-id="77fc8-179"><*key-name*></span></span> | <span data-ttu-id="77fc8-180">Yes</span><span class="sxs-lookup"><span data-stu-id="77fc8-180">Yes</span></span> | <span data-ttu-id="77fc8-181">String</span><span class="sxs-lookup"><span data-stu-id="77fc8-181">String</span></span> | <span data-ttu-id="77fc8-182">The key name for the output return value</span><span class="sxs-lookup"><span data-stu-id="77fc8-182">The key name for the output return value</span></span> |  
| <span data-ttu-id="77fc8-183">type</span><span class="sxs-lookup"><span data-stu-id="77fc8-183">type</span></span> | <span data-ttu-id="77fc8-184">Yes</span><span class="sxs-lookup"><span data-stu-id="77fc8-184">Yes</span></span> | <span data-ttu-id="77fc8-185">int, float, string, securestring, bool, array, JSON object</span><span class="sxs-lookup"><span data-stu-id="77fc8-185">int, float, string, securestring, bool, array, JSON object</span></span> | <span data-ttu-id="77fc8-186">The type for the output return value</span><span class="sxs-lookup"><span data-stu-id="77fc8-186">The type for the output return value</span></span> | 
| <span data-ttu-id="77fc8-187">value</span><span class="sxs-lookup"><span data-stu-id="77fc8-187">value</span></span> | <span data-ttu-id="77fc8-188">Yes</span><span class="sxs-lookup"><span data-stu-id="77fc8-188">Yes</span></span> | <span data-ttu-id="77fc8-189">Same as `type`</span><span class="sxs-lookup"><span data-stu-id="77fc8-189">Same as `type`</span></span> | <span data-ttu-id="77fc8-190">The output return value</span><span class="sxs-lookup"><span data-stu-id="77fc8-190">The output return value</span></span> |  
||||| 

<span data-ttu-id="77fc8-191">To get the output from a workflow run, review the logic app's run history and details in the Azure portal or use the [Workflow REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="77fc8-191">To get the output from a workflow run, review the logic app's run history and details in the Azure portal or use the [Workflow REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span> <span data-ttu-id="77fc8-192">You can also pass output to external systems, for example, Power BI so that you can create dashboards.</span><span class="sxs-lookup"><span data-stu-id="77fc8-192">You can also pass output to external systems, for example, Power BI so that you can create dashboards.</span></span> 

<a name="expressions"></a>

## <a name="expressions"></a><span data-ttu-id="77fc8-193">Expressions</span><span class="sxs-lookup"><span data-stu-id="77fc8-193">Expressions</span></span>

<span data-ttu-id="77fc8-194">With JSON, you can have literal values that exist at design time, for example:</span><span class="sxs-lookup"><span data-stu-id="77fc8-194">With JSON, you can have literal values that exist at design time, for example:</span></span>

```json
"customerName": "Sophia Owen", 
"rainbowColors": ["red", "orange", "yellow", "green", "blue", "indigo", "violet"], 
"rainbowColorsCount": 7 
```

<span data-ttu-id="77fc8-195">You can also have values that don't exist until run time.</span><span class="sxs-lookup"><span data-stu-id="77fc8-195">You can also have values that don't exist until run time.</span></span> <span data-ttu-id="77fc8-196">To represent these values, you can use *expressions*, which are evaluated at run time.</span><span class="sxs-lookup"><span data-stu-id="77fc8-196">To represent these values, you can use *expressions*, which are evaluated at run time.</span></span> <span data-ttu-id="77fc8-197">An expression is a sequence that can contain one or more [functions](#functions), [operators](#operators), variables, explicit values, or constants.</span><span class="sxs-lookup"><span data-stu-id="77fc8-197">An expression is a sequence that can contain one or more [functions](#functions), [operators](#operators), variables, explicit values, or constants.</span></span> <span data-ttu-id="77fc8-198">In your workflow definition, you can use an expression anywhere in a JSON string value by prefixing the expression with the at-sign (\@).</span><span class="sxs-lookup"><span data-stu-id="77fc8-198">In your workflow definition, you can use an expression anywhere in a JSON string value by prefixing the expression with the at-sign (\@).</span></span> <span data-ttu-id="77fc8-199">When evaluating an expression that represents a JSON value, the expression body is extracted by removing the \@ character, and always results in another JSON value.</span><span class="sxs-lookup"><span data-stu-id="77fc8-199">When evaluating an expression that represents a JSON value, the expression body is extracted by removing the \@ character, and always results in another JSON value.</span></span> 

<span data-ttu-id="77fc8-200">For example, for the previously defined `customerName` property, you can get the property value by using the [parameters()](../logic-apps/workflow-definition-language-functions-reference.md#parameters) function in an expression and assign that value to the `accountName` property:</span><span class="sxs-lookup"><span data-stu-id="77fc8-200">For example, for the previously defined `customerName` property, you can get the property value by using the [parameters()](../logic-apps/workflow-definition-language-functions-reference.md#parameters) function in an expression and assign that value to the `accountName` property:</span></span>

```json
"customerName": "Sophia Owen", 
"accountName": "@parameters('customerName')"
```

<span data-ttu-id="77fc8-201">*String interpolation* also lets you use multiple expressions inside strings that are wrapped by the \@ character and curly braces ({}).</span><span class="sxs-lookup"><span data-stu-id="77fc8-201">*String interpolation* also lets you use multiple expressions inside strings that are wrapped by the \@ character and curly braces ({}).</span></span> <span data-ttu-id="77fc8-202">Here is the syntax:</span><span class="sxs-lookup"><span data-stu-id="77fc8-202">Here is the syntax:</span></span>

```json
@{ "<expression1>", "<expression2>" }
```

<span data-ttu-id="77fc8-203">The result is always a string, making this capability similar to the `concat()` function, for example:</span><span class="sxs-lookup"><span data-stu-id="77fc8-203">The result is always a string, making this capability similar to the `concat()` function, for example:</span></span> 

```json
"customerName": "First name: @{parameters('firstName')} Last name: @{parameters('lastName')}"
```

<span data-ttu-id="77fc8-204">If you have a literal string that starts with the \@ character, prefix the \@ character with another \@ character as an escape character: \@\@</span><span class="sxs-lookup"><span data-stu-id="77fc8-204">If you have a literal string that starts with the \@ character, prefix the \@ character with another \@ character as an escape character: \@\@</span></span>

<span data-ttu-id="77fc8-205">These examples show how expressions are evaluated:</span><span class="sxs-lookup"><span data-stu-id="77fc8-205">These examples show how expressions are evaluated:</span></span>

| <span data-ttu-id="77fc8-206">JSON value</span><span class="sxs-lookup"><span data-stu-id="77fc8-206">JSON value</span></span> | <span data-ttu-id="77fc8-207">Result</span><span class="sxs-lookup"><span data-stu-id="77fc8-207">Result</span></span> |
|------------|--------| 
| <span data-ttu-id="77fc8-208">"Sophia Owen"</span><span class="sxs-lookup"><span data-stu-id="77fc8-208">"Sophia Owen"</span></span> | <span data-ttu-id="77fc8-209">Return these characters: 'Sophia Owen'</span><span class="sxs-lookup"><span data-stu-id="77fc8-209">Return these characters: 'Sophia Owen'</span></span> |
| <span data-ttu-id="77fc8-210">"array[1]"</span><span class="sxs-lookup"><span data-stu-id="77fc8-210">"array[1]"</span></span> | <span data-ttu-id="77fc8-211">Return these characters: 'array[1]'</span><span class="sxs-lookup"><span data-stu-id="77fc8-211">Return these characters: 'array[1]'</span></span> |
| <span data-ttu-id="77fc8-212">"\@\@"</span><span class="sxs-lookup"><span data-stu-id="77fc8-212">"\@\@"</span></span> | <span data-ttu-id="77fc8-213">Return these characters as a one-character string: '\@'</span><span class="sxs-lookup"><span data-stu-id="77fc8-213">Return these characters as a one-character string: '\@'</span></span> |   
| <span data-ttu-id="77fc8-214">" \@"</span><span class="sxs-lookup"><span data-stu-id="77fc8-214">" \@"</span></span> | <span data-ttu-id="77fc8-215">Return these characters as a two-character string: ' \@'</span><span class="sxs-lookup"><span data-stu-id="77fc8-215">Return these characters as a two-character string: ' \@'</span></span> |
|||

<span data-ttu-id="77fc8-216">For these examples, suppose you define "myBirthMonth" equal to "January" and "myAge" equal to the number 42:</span><span class="sxs-lookup"><span data-stu-id="77fc8-216">For these examples, suppose you define "myBirthMonth" equal to "January" and "myAge" equal to the number 42:</span></span>  
  
```json
"myBirthMonth": "January",
"myAge": 42
```

<span data-ttu-id="77fc8-217">These examples show how the following expressions are evaluated:</span><span class="sxs-lookup"><span data-stu-id="77fc8-217">These examples show how the following expressions are evaluated:</span></span>

| <span data-ttu-id="77fc8-218">JSON expression</span><span class="sxs-lookup"><span data-stu-id="77fc8-218">JSON expression</span></span> | <span data-ttu-id="77fc8-219">Result</span><span class="sxs-lookup"><span data-stu-id="77fc8-219">Result</span></span> |
|-----------------|--------| 
| <span data-ttu-id="77fc8-220">"\@parameters('myBirthMonth')"</span><span class="sxs-lookup"><span data-stu-id="77fc8-220">"\@parameters('myBirthMonth')"</span></span> | <span data-ttu-id="77fc8-221">Return this string: "January"</span><span class="sxs-lookup"><span data-stu-id="77fc8-221">Return this string: "January"</span></span> |  
| <span data-ttu-id="77fc8-222">"\@{parameters('myBirthMonth')}"</span><span class="sxs-lookup"><span data-stu-id="77fc8-222">"\@{parameters('myBirthMonth')}"</span></span> | <span data-ttu-id="77fc8-223">Return this string: "January"</span><span class="sxs-lookup"><span data-stu-id="77fc8-223">Return this string: "January"</span></span> |  
| <span data-ttu-id="77fc8-224">"\@parameters('myAge')"</span><span class="sxs-lookup"><span data-stu-id="77fc8-224">"\@parameters('myAge')"</span></span> | <span data-ttu-id="77fc8-225">Return this number: 42</span><span class="sxs-lookup"><span data-stu-id="77fc8-225">Return this number: 42</span></span> |  
| <span data-ttu-id="77fc8-226">"\@{parameters('myAge')}"</span><span class="sxs-lookup"><span data-stu-id="77fc8-226">"\@{parameters('myAge')}"</span></span> | <span data-ttu-id="77fc8-227">Return this number as a string: "42"</span><span class="sxs-lookup"><span data-stu-id="77fc8-227">Return this number as a string: "42"</span></span> |  
| <span data-ttu-id="77fc8-228">"My age is \@{parameters('myAge')}"</span><span class="sxs-lookup"><span data-stu-id="77fc8-228">"My age is \@{parameters('myAge')}"</span></span> | <span data-ttu-id="77fc8-229">Return this string: "My age is 42"</span><span class="sxs-lookup"><span data-stu-id="77fc8-229">Return this string: "My age is 42"</span></span> |  
| <span data-ttu-id="77fc8-230">"\@concat('My age is ', string(parameters('myAge')))"</span><span class="sxs-lookup"><span data-stu-id="77fc8-230">"\@concat('My age is ', string(parameters('myAge')))"</span></span> | <span data-ttu-id="77fc8-231">Return this string: "My age is 42"</span><span class="sxs-lookup"><span data-stu-id="77fc8-231">Return this string: "My age is 42"</span></span> |  
| <span data-ttu-id="77fc8-232">"My age is \@\@{parameters('myAge')}"</span><span class="sxs-lookup"><span data-stu-id="77fc8-232">"My age is \@\@{parameters('myAge')}"</span></span> | <span data-ttu-id="77fc8-233">Return this string, which includes the expression: "My age is \@{parameters('myAge')}\`</span><span class="sxs-lookup"><span data-stu-id="77fc8-233">Return this string, which includes the expression: "My age is \@{parameters('myAge')}\`</span></span> | 
||| 

<span data-ttu-id="77fc8-234">When you're working visually in the Logic Apps Designer, you can create expressions through the Expression builder, for example:</span><span class="sxs-lookup"><span data-stu-id="77fc8-234">When you're working visually in the Logic Apps Designer, you can create expressions through the Expression builder, for example:</span></span> 

![Logic Apps Designer > Expression builder](./media/logic-apps-workflow-definition-language/expression-builder.png)

<span data-ttu-id="77fc8-236">When you're done, the expression appears for the corresponding property in your workflow definition, for example, the `searchQuery` property here:</span><span class="sxs-lookup"><span data-stu-id="77fc8-236">When you're done, the expression appears for the corresponding property in your workflow definition, for example, the `searchQuery` property here:</span></span>

```json
"Search_tweets": {
  "inputs": {
    "host": {
      "connection": {
       "name": "@parameters('$connections')['twitter']['connectionId']"
      }
    }
  },
  "method": "get",
  "path": "/searchtweets",
  "queries": {
    "maxResults": 20,
    "searchQuery": "Azure @{concat('firstName','', 'LastName')}"
  }
},
```

<a name="operators"></a>

## <a name="operators"></a><span data-ttu-id="77fc8-237">Operators</span><span class="sxs-lookup"><span data-stu-id="77fc8-237">Operators</span></span>

<span data-ttu-id="77fc8-238">In [expressions](#expressions) and [functions](#functions), operators perform specific tasks, such as reference a property or a value in an array.</span><span class="sxs-lookup"><span data-stu-id="77fc8-238">In [expressions](#expressions) and [functions](#functions), operators perform specific tasks, such as reference a property or a value in an array.</span></span> 

| <span data-ttu-id="77fc8-239">Operator</span><span class="sxs-lookup"><span data-stu-id="77fc8-239">Operator</span></span> | <span data-ttu-id="77fc8-240">Task</span><span class="sxs-lookup"><span data-stu-id="77fc8-240">Task</span></span> | 
|----------|------|
| <span data-ttu-id="77fc8-241">'</span><span class="sxs-lookup"><span data-stu-id="77fc8-241">'</span></span> | <span data-ttu-id="77fc8-242">To use a string literal as input or in expressions and functions, wrap the string only with single quotation marks, for example, `'<myString>'`.</span><span class="sxs-lookup"><span data-stu-id="77fc8-242">To use a string literal as input or in expressions and functions, wrap the string only with single quotation marks, for example, `'<myString>'`.</span></span> <span data-ttu-id="77fc8-243">Do not use double quotation marks (""), which conflict with the JSON formatting around an entire expression.</span><span class="sxs-lookup"><span data-stu-id="77fc8-243">Do not use double quotation marks (""), which conflict with the JSON formatting around an entire expression.</span></span> <span data-ttu-id="77fc8-244">For example:</span><span class="sxs-lookup"><span data-stu-id="77fc8-244">For example:</span></span> <p><span data-ttu-id="77fc8-245">**Yes**: length('Hello')</span><span class="sxs-lookup"><span data-stu-id="77fc8-245">**Yes**: length('Hello')</span></span> </br><span data-ttu-id="77fc8-246">**No**: length("Hello")</span><span class="sxs-lookup"><span data-stu-id="77fc8-246">**No**: length("Hello")</span></span> <p><span data-ttu-id="77fc8-247">When you pass arrays or numbers, you don't need wrapping punctuation.</span><span class="sxs-lookup"><span data-stu-id="77fc8-247">When you pass arrays or numbers, you don't need wrapping punctuation.</span></span> <span data-ttu-id="77fc8-248">For example:</span><span class="sxs-lookup"><span data-stu-id="77fc8-248">For example:</span></span> <p><span data-ttu-id="77fc8-249">**Yes**: length([1, 2, 3])</span><span class="sxs-lookup"><span data-stu-id="77fc8-249">**Yes**: length([1, 2, 3])</span></span> </br><span data-ttu-id="77fc8-250">**No**: length("[1, 2, 3]")</span><span class="sxs-lookup"><span data-stu-id="77fc8-250">**No**: length("[1, 2, 3]")</span></span> | 
| <span data-ttu-id="77fc8-251">[]</span><span class="sxs-lookup"><span data-stu-id="77fc8-251">[]</span></span> | <span data-ttu-id="77fc8-252">To reference a value at a specific position (index) in an array, use square brackets.</span><span class="sxs-lookup"><span data-stu-id="77fc8-252">To reference a value at a specific position (index) in an array, use square brackets.</span></span> <span data-ttu-id="77fc8-253">For example, to get the second item in an array:</span><span class="sxs-lookup"><span data-stu-id="77fc8-253">For example, to get the second item in an array:</span></span> <p>`myArray[1]` | 
| <span data-ttu-id="77fc8-254">.</span><span class="sxs-lookup"><span data-stu-id="77fc8-254">.</span></span> | <span data-ttu-id="77fc8-255">To reference a property in an object, use the dot operator.</span><span class="sxs-lookup"><span data-stu-id="77fc8-255">To reference a property in an object, use the dot operator.</span></span> <span data-ttu-id="77fc8-256">For example, to get the `name` property for a `customer` JSON object:</span><span class="sxs-lookup"><span data-stu-id="77fc8-256">For example, to get the `name` property for a `customer` JSON object:</span></span> <p>`"@parameters('customer').name"` | 
| <span data-ttu-id="77fc8-257">?</span><span class="sxs-lookup"><span data-stu-id="77fc8-257">?</span></span> | <span data-ttu-id="77fc8-258">To reference null properties in an object without a runtime error, use the question mark operator.</span><span class="sxs-lookup"><span data-stu-id="77fc8-258">To reference null properties in an object without a runtime error, use the question mark operator.</span></span> <span data-ttu-id="77fc8-259">For example, to handle null outputs from a trigger, you can use this expression:</span><span class="sxs-lookup"><span data-stu-id="77fc8-259">For example, to handle null outputs from a trigger, you can use this expression:</span></span> <p>`@coalesce(trigger().outputs?.body?.<someProperty>, '<property-default-value>')` | 
||| 

<a name="functions"></a>

## <a name="functions"></a><span data-ttu-id="77fc8-260">Functions</span><span class="sxs-lookup"><span data-stu-id="77fc8-260">Functions</span></span>

<span data-ttu-id="77fc8-261">Some expressions get their values from runtime actions that might not yet exist when a logic app starts to run.</span><span class="sxs-lookup"><span data-stu-id="77fc8-261">Some expressions get their values from runtime actions that might not yet exist when a logic app starts to run.</span></span> <span data-ttu-id="77fc8-262">To reference or work with these values in expressions, you can use [*functions*](../logic-apps/workflow-definition-language-functions-reference.md) that the Workflow Definition Language provides.</span><span class="sxs-lookup"><span data-stu-id="77fc8-262">To reference or work with these values in expressions, you can use [*functions*](../logic-apps/workflow-definition-language-functions-reference.md) that the Workflow Definition Language provides.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="77fc8-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="77fc8-263">Next steps</span></span>

* <span data-ttu-id="77fc8-264">Learn about [Workflow Definition Language actions and triggers](../logic-apps/logic-apps-workflow-actions-triggers.md)</span><span class="sxs-lookup"><span data-stu-id="77fc8-264">Learn about [Workflow Definition Language actions and triggers](../logic-apps/logic-apps-workflow-actions-triggers.md)</span></span>
* <span data-ttu-id="77fc8-265">Learn about programmatically creating and managing logic apps with the [Workflow REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="77fc8-265">Learn about programmatically creating and managing logic apps with the [Workflow REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>
