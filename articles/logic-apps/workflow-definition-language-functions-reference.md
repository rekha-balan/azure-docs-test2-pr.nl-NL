---
title: Functions reference for Workflow Definition Language - Azure Logic Apps | Microsoft Docs
description: Learn about Workflow Definition Language functions for Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: reference
ms.date: 08/15/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 8a2e06d2e6cf3e470d4e0909e5559ac0411292fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866909"
---
# <a name="functions-reference-for-workflow-definition-language-in-azure-logic-apps"></a><span data-ttu-id="457d1-103">Functions reference for Workflow Definition Language in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="457d1-103">Functions reference for Workflow Definition Language in Azure Logic Apps</span></span>

<span data-ttu-id="457d1-104">Some [expressions](../logic-apps/logic-apps-workflow-definition-language.md#expressions) in [Azure Logic Apps](../logic-apps/logic-apps-overview.md) get their values from runtime actions that might not yet exist when your logic app workflow definition starts to run.</span><span class="sxs-lookup"><span data-stu-id="457d1-104">Some [expressions](../logic-apps/logic-apps-workflow-definition-language.md#expressions) in [Azure Logic Apps](../logic-apps/logic-apps-overview.md) get their values from runtime actions that might not yet exist when your logic app workflow definition starts to run.</span></span> <span data-ttu-id="457d1-105">To reference or work with these values in expressions, you can use *functions* provided by the [Workflow Definition Language](../logic-apps/logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="457d1-105">To reference or work with these values in expressions, you can use *functions* provided by the [Workflow Definition Language](../logic-apps/logic-apps-workflow-definition-language.md).</span></span> <span data-ttu-id="457d1-106">For example, you can use math functions for calculations, such as the [add()](../logic-apps/workflow-definition-language-functions-reference.md#add) function, which returns the sum from integers or floats.</span><span class="sxs-lookup"><span data-stu-id="457d1-106">For example, you can use math functions for calculations, such as the [add()](../logic-apps/workflow-definition-language-functions-reference.md#add) function, which returns the sum from integers or floats.</span></span> <span data-ttu-id="457d1-107">Here are a couple more example tasks you can perform with functions:</span><span class="sxs-lookup"><span data-stu-id="457d1-107">Here are a couple more example tasks you can perform with functions:</span></span>

| <span data-ttu-id="457d1-108">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-108">Task</span></span> | <span data-ttu-id="457d1-109">Function syntax</span><span class="sxs-lookup"><span data-stu-id="457d1-109">Function syntax</span></span> | <span data-ttu-id="457d1-110">Result</span><span class="sxs-lookup"><span data-stu-id="457d1-110">Result</span></span> | 
| ---- | --------------- | ------ | 
| <span data-ttu-id="457d1-111">Return a string in lowercase format.</span><span class="sxs-lookup"><span data-stu-id="457d1-111">Return a string in lowercase format.</span></span> | <span data-ttu-id="457d1-112">toLower('<*text*>')</span><span class="sxs-lookup"><span data-stu-id="457d1-112">toLower('<*text*>')</span></span> <p><span data-ttu-id="457d1-113">For example: toLower('Hello')</span><span class="sxs-lookup"><span data-stu-id="457d1-113">For example: toLower('Hello')</span></span> | <span data-ttu-id="457d1-114">"hello"</span><span class="sxs-lookup"><span data-stu-id="457d1-114">"hello"</span></span> | 
| <span data-ttu-id="457d1-115">Return a globally unique identifier (GUID).</span><span class="sxs-lookup"><span data-stu-id="457d1-115">Return a globally unique identifier (GUID).</span></span> | <span data-ttu-id="457d1-116">guid()</span><span class="sxs-lookup"><span data-stu-id="457d1-116">guid()</span></span> |<span data-ttu-id="457d1-117">"c2ecc88d-88c8-4096-912c-d6f2e2b138ce"</span><span class="sxs-lookup"><span data-stu-id="457d1-117">"c2ecc88d-88c8-4096-912c-d6f2e2b138ce"</span></span> | 
|||| 

<span data-ttu-id="457d1-118">This article describes the functions you can use when creating your logic app definitions.</span><span class="sxs-lookup"><span data-stu-id="457d1-118">This article describes the functions you can use when creating your logic app definitions.</span></span>
<span data-ttu-id="457d1-119">To find functions [based on their general purpose](#ordered-by-purpose), continue with the following tables.</span><span class="sxs-lookup"><span data-stu-id="457d1-119">To find functions [based on their general purpose](#ordered-by-purpose), continue with the following tables.</span></span> <span data-ttu-id="457d1-120">Or, for detailed information about each function, see the [alphabetical list](#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-120">Or, for detailed information about each function, see the [alphabetical list](#alphabetical-list).</span></span> 

> [!NOTE]
> <span data-ttu-id="457d1-121">In the syntax for parameter definitions, a question mark (?) that appears after a parameter means the parameter is optional.</span><span class="sxs-lookup"><span data-stu-id="457d1-121">In the syntax for parameter definitions, a question mark (?) that appears after a parameter means the parameter is optional.</span></span> <span data-ttu-id="457d1-122">For example, see [getFutureTime()](#getFutureTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-122">For example, see [getFutureTime()](#getFutureTime).</span></span>

## <a name="functions-in-expressions"></a><span data-ttu-id="457d1-123">Functions in expressions</span><span class="sxs-lookup"><span data-stu-id="457d1-123">Functions in expressions</span></span>

<span data-ttu-id="457d1-124">To show how to use a function in an expression, this example shows how you can get the value from the `customerName` parameter and assign that value to the `accountName` property by using the [parameters()](#parameters) function in an expression:</span><span class="sxs-lookup"><span data-stu-id="457d1-124">To show how to use a function in an expression, this example shows how you can get the value from the `customerName` parameter and assign that value to the `accountName` property by using the [parameters()](#parameters) function in an expression:</span></span>

```json
"accountName": "@parameters('customerName')"
```

<span data-ttu-id="457d1-125">Here are some other general ways that you can use functions in expressions:</span><span class="sxs-lookup"><span data-stu-id="457d1-125">Here are some other general ways that you can use functions in expressions:</span></span>

| <span data-ttu-id="457d1-126">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-126">Task</span></span> | <span data-ttu-id="457d1-127">Function syntax in an expression</span><span class="sxs-lookup"><span data-stu-id="457d1-127">Function syntax in an expression</span></span> | 
| ---- | -------------------------------- | 
| <span data-ttu-id="457d1-128">Perform work with an item by passing that item to a function.</span><span class="sxs-lookup"><span data-stu-id="457d1-128">Perform work with an item by passing that item to a function.</span></span> | <span data-ttu-id="457d1-129">"\@<*functionName*>(<*item*>)"</span><span class="sxs-lookup"><span data-stu-id="457d1-129">"\@<*functionName*>(<*item*>)"</span></span> | 
| <span data-ttu-id="457d1-130">1. Get the *parameterName*'s value by using the nested `parameters()` function.</span><span class="sxs-lookup"><span data-stu-id="457d1-130">1. Get the *parameterName*'s value by using the nested `parameters()` function.</span></span> </br><span data-ttu-id="457d1-131">2. Perform work with the result by passing that value to *functionName*.</span><span class="sxs-lookup"><span data-stu-id="457d1-131">2. Perform work with the result by passing that value to *functionName*.</span></span> | <span data-ttu-id="457d1-132">"\@<*functionName*>(parameters('<*parameterName*>'))"</span><span class="sxs-lookup"><span data-stu-id="457d1-132">"\@<*functionName*>(parameters('<*parameterName*>'))"</span></span> | 
| <span data-ttu-id="457d1-133">1. Get the result from the nested inner function *functionName*.</span><span class="sxs-lookup"><span data-stu-id="457d1-133">1. Get the result from the nested inner function *functionName*.</span></span> </br><span data-ttu-id="457d1-134">2. Pass the result to the outer function *functionName2*.</span><span class="sxs-lookup"><span data-stu-id="457d1-134">2. Pass the result to the outer function *functionName2*.</span></span> | <span data-ttu-id="457d1-135">"\@<*functionName2*>(<*functionName*>(<*item*>))"</span><span class="sxs-lookup"><span data-stu-id="457d1-135">"\@<*functionName2*>(<*functionName*>(<*item*>))"</span></span> | 
| <span data-ttu-id="457d1-136">1. Get the result from *functionName*.</span><span class="sxs-lookup"><span data-stu-id="457d1-136">1. Get the result from *functionName*.</span></span> </br><span data-ttu-id="457d1-137">2. Given that the result is an object with property *propertyName*, get that property's value.</span><span class="sxs-lookup"><span data-stu-id="457d1-137">2. Given that the result is an object with property *propertyName*, get that property's value.</span></span> | <span data-ttu-id="457d1-138">"\@<*functionName*>(<*item*>).<*propertyName*>"</span><span class="sxs-lookup"><span data-stu-id="457d1-138">"\@<*functionName*>(<*item*>).<*propertyName*>"</span></span> | 
||| 

<span data-ttu-id="457d1-139">For example, the `concat()` function can take two or more string values as parameters.</span><span class="sxs-lookup"><span data-stu-id="457d1-139">For example, the `concat()` function can take two or more string values as parameters.</span></span> <span data-ttu-id="457d1-140">This function combines those strings into one string.</span><span class="sxs-lookup"><span data-stu-id="457d1-140">This function combines those strings into one string.</span></span> <span data-ttu-id="457d1-141">You can either pass in string literals, for example, "Sophia" and "Owen" so that you get a combined string, "SophiaOwen":</span><span class="sxs-lookup"><span data-stu-id="457d1-141">You can either pass in string literals, for example, "Sophia" and "Owen" so that you get a combined string, "SophiaOwen":</span></span>

```json
"customerName": "@concat('Sophia', 'Owen')"
```

<span data-ttu-id="457d1-142">Or, you can get string values from parameters.</span><span class="sxs-lookup"><span data-stu-id="457d1-142">Or, you can get string values from parameters.</span></span> <span data-ttu-id="457d1-143">This example uses the `parameters()` function in each `concat()` parameter and the `firstName` and `lastName` parameters.</span><span class="sxs-lookup"><span data-stu-id="457d1-143">This example uses the `parameters()` function in each `concat()` parameter and the `firstName` and `lastName` parameters.</span></span> <span data-ttu-id="457d1-144">You then pass the resulting strings to the `concat()` function so that you get a combined string, for example, "SophiaOwen":</span><span class="sxs-lookup"><span data-stu-id="457d1-144">You then pass the resulting strings to the `concat()` function so that you get a combined string, for example, "SophiaOwen":</span></span>

```json
"customerName": "@concat(parameters('firstName'), parameters('lastName'))"
```

<span data-ttu-id="457d1-145">Either way, both examples assign the result to the `customerName` property.</span><span class="sxs-lookup"><span data-stu-id="457d1-145">Either way, both examples assign the result to the `customerName` property.</span></span> 

<span data-ttu-id="457d1-146">Here are the available functions ordered by their general purpose, or you can browse the functions based on [alphabetical order](#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-146">Here are the available functions ordered by their general purpose, or you can browse the functions based on [alphabetical order](#alphabetical-list).</span></span>

<a name="ordered-by-purpose"></a>
<a name="string-functions"></a>

## <a name="string-functions"></a><span data-ttu-id="457d1-147">String functions</span><span class="sxs-lookup"><span data-stu-id="457d1-147">String functions</span></span>

<span data-ttu-id="457d1-148">To work with strings, you can use these string functions and also some [collection functions](#collection-functions).</span><span class="sxs-lookup"><span data-stu-id="457d1-148">To work with strings, you can use these string functions and also some [collection functions](#collection-functions).</span></span> <span data-ttu-id="457d1-149">String functions work only on strings.</span><span class="sxs-lookup"><span data-stu-id="457d1-149">String functions work only on strings.</span></span> 

| <span data-ttu-id="457d1-150">String function</span><span class="sxs-lookup"><span data-stu-id="457d1-150">String function</span></span> | <span data-ttu-id="457d1-151">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-151">Task</span></span> | 
| --------------- | ---- | 
| [<span data-ttu-id="457d1-152">concat</span><span class="sxs-lookup"><span data-stu-id="457d1-152">concat</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#concat) | <span data-ttu-id="457d1-153">Combine two or more strings, and return the combined string.</span><span class="sxs-lookup"><span data-stu-id="457d1-153">Combine two or more strings, and return the combined string.</span></span> | 
| [<span data-ttu-id="457d1-154">endsWith</span><span class="sxs-lookup"><span data-stu-id="457d1-154">endsWith</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#endswith) | <span data-ttu-id="457d1-155">Check whether a string ends with the specified substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-155">Check whether a string ends with the specified substring.</span></span> | 
| [<span data-ttu-id="457d1-156">guid</span><span class="sxs-lookup"><span data-stu-id="457d1-156">guid</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#guid) | <span data-ttu-id="457d1-157">Generate a globally unique identifier (GUID) as a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-157">Generate a globally unique identifier (GUID) as a string.</span></span> | 
| [<span data-ttu-id="457d1-158">indexOf</span><span class="sxs-lookup"><span data-stu-id="457d1-158">indexOf</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#indexof) | <span data-ttu-id="457d1-159">Return the starting position for a substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-159">Return the starting position for a substring.</span></span> | 
| [<span data-ttu-id="457d1-160">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="457d1-160">lastIndexOf</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#lastindexof) | <span data-ttu-id="457d1-161">Return the starting position for the last occurrence of a substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-161">Return the starting position for the last occurrence of a substring.</span></span> | 
| [<span data-ttu-id="457d1-162">replace</span><span class="sxs-lookup"><span data-stu-id="457d1-162">replace</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#replace) | <span data-ttu-id="457d1-163">Replace a substring with the specified string, and return the updated string.</span><span class="sxs-lookup"><span data-stu-id="457d1-163">Replace a substring with the specified string, and return the updated string.</span></span> | 
| [<span data-ttu-id="457d1-164">split</span><span class="sxs-lookup"><span data-stu-id="457d1-164">split</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#split) | <span data-ttu-id="457d1-165">Return an array that has all the characters from a string and separates each character with the specific delimiter character.</span><span class="sxs-lookup"><span data-stu-id="457d1-165">Return an array that has all the characters from a string and separates each character with the specific delimiter character.</span></span> | 
| [<span data-ttu-id="457d1-166">startsWith</span><span class="sxs-lookup"><span data-stu-id="457d1-166">startsWith</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#startswith) | <span data-ttu-id="457d1-167">Check whether a string starts with a specific substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-167">Check whether a string starts with a specific substring.</span></span> | 
| [<span data-ttu-id="457d1-168">substring</span><span class="sxs-lookup"><span data-stu-id="457d1-168">substring</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#substring) | <span data-ttu-id="457d1-169">Return characters from a string, starting from the specified position.</span><span class="sxs-lookup"><span data-stu-id="457d1-169">Return characters from a string, starting from the specified position.</span></span> | 
| [<span data-ttu-id="457d1-170">toLower</span><span class="sxs-lookup"><span data-stu-id="457d1-170">toLower</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#toLower) | <span data-ttu-id="457d1-171">Return a string in lowercase format.</span><span class="sxs-lookup"><span data-stu-id="457d1-171">Return a string in lowercase format.</span></span> | 
| [<span data-ttu-id="457d1-172">toUpper</span><span class="sxs-lookup"><span data-stu-id="457d1-172">toUpper</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#toUpper) | <span data-ttu-id="457d1-173">Return a string in uppercase format.</span><span class="sxs-lookup"><span data-stu-id="457d1-173">Return a string in uppercase format.</span></span> | 
| [<span data-ttu-id="457d1-174">trim</span><span class="sxs-lookup"><span data-stu-id="457d1-174">trim</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#trim) | <span data-ttu-id="457d1-175">Remove leading and trailing whitespace from a string, and return the updated string.</span><span class="sxs-lookup"><span data-stu-id="457d1-175">Remove leading and trailing whitespace from a string, and return the updated string.</span></span> | 
||| 

<a name="collection-functions"></a>

## <a name="collection-functions"></a><span data-ttu-id="457d1-176">Collection functions</span><span class="sxs-lookup"><span data-stu-id="457d1-176">Collection functions</span></span>

<span data-ttu-id="457d1-177">To work with collections, generally arrays, strings, and sometimes, dictionaries, you can use these collection functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-177">To work with collections, generally arrays, strings, and sometimes, dictionaries, you can use these collection functions.</span></span> 

| <span data-ttu-id="457d1-178">Collection function</span><span class="sxs-lookup"><span data-stu-id="457d1-178">Collection function</span></span> | <span data-ttu-id="457d1-179">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-179">Task</span></span> | 
| ------------------- | ---- | 
| [<span data-ttu-id="457d1-180">contains</span><span class="sxs-lookup"><span data-stu-id="457d1-180">contains</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#contains) | <span data-ttu-id="457d1-181">Check whether a collection has a specific item.</span><span class="sxs-lookup"><span data-stu-id="457d1-181">Check whether a collection has a specific item.</span></span> |
| [<span data-ttu-id="457d1-182">empty</span><span class="sxs-lookup"><span data-stu-id="457d1-182">empty</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#empty) | <span data-ttu-id="457d1-183">Check whether a collection is empty.</span><span class="sxs-lookup"><span data-stu-id="457d1-183">Check whether a collection is empty.</span></span> | 
| [<span data-ttu-id="457d1-184">first</span><span class="sxs-lookup"><span data-stu-id="457d1-184">first</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#first) | <span data-ttu-id="457d1-185">Return the first item from a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-185">Return the first item from a collection.</span></span> | 
| [<span data-ttu-id="457d1-186">intersection</span><span class="sxs-lookup"><span data-stu-id="457d1-186">intersection</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#intersection) | <span data-ttu-id="457d1-187">Return a collection that has *only* the common items across the specified collections.</span><span class="sxs-lookup"><span data-stu-id="457d1-187">Return a collection that has *only* the common items across the specified collections.</span></span> | 
| [<span data-ttu-id="457d1-188">join</span><span class="sxs-lookup"><span data-stu-id="457d1-188">join</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#join) | <span data-ttu-id="457d1-189">Return a string that has *all* the items from an array, separated by the specified character.</span><span class="sxs-lookup"><span data-stu-id="457d1-189">Return a string that has *all* the items from an array, separated by the specified character.</span></span> | 
| [<span data-ttu-id="457d1-190">last</span><span class="sxs-lookup"><span data-stu-id="457d1-190">last</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#last) | <span data-ttu-id="457d1-191">Return the last item from a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-191">Return the last item from a collection.</span></span> | 
| [<span data-ttu-id="457d1-192">length</span><span class="sxs-lookup"><span data-stu-id="457d1-192">length</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#length) | <span data-ttu-id="457d1-193">Return the number of items in a string or array.</span><span class="sxs-lookup"><span data-stu-id="457d1-193">Return the number of items in a string or array.</span></span> | 
| [<span data-ttu-id="457d1-194">skip</span><span class="sxs-lookup"><span data-stu-id="457d1-194">skip</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#skip) | <span data-ttu-id="457d1-195">Remove items from the front of a collection, and return *all the other* items.</span><span class="sxs-lookup"><span data-stu-id="457d1-195">Remove items from the front of a collection, and return *all the other* items.</span></span> | 
| [<span data-ttu-id="457d1-196">take</span><span class="sxs-lookup"><span data-stu-id="457d1-196">take</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#take) | <span data-ttu-id="457d1-197">Return items from the front of a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-197">Return items from the front of a collection.</span></span> | 
| [<span data-ttu-id="457d1-198">union</span><span class="sxs-lookup"><span data-stu-id="457d1-198">union</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#union) | <span data-ttu-id="457d1-199">Return a collection that has *all* the items from the specified collections.</span><span class="sxs-lookup"><span data-stu-id="457d1-199">Return a collection that has *all* the items from the specified collections.</span></span> | 
||| 

<a name="comparison-functions"></a>

## <a name="logical-comparison-functions"></a><span data-ttu-id="457d1-200">Logical comparison functions</span><span class="sxs-lookup"><span data-stu-id="457d1-200">Logical comparison functions</span></span>

<span data-ttu-id="457d1-201">To work with conditions, compare values and expression results, or evaluate various kinds of logic, you can use these logical comparison functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-201">To work with conditions, compare values and expression results, or evaluate various kinds of logic, you can use these logical comparison functions.</span></span> <span data-ttu-id="457d1-202">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-202">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-203">Logical comparison function</span><span class="sxs-lookup"><span data-stu-id="457d1-203">Logical comparison function</span></span> | <span data-ttu-id="457d1-204">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-204">Task</span></span> | 
| --------------------------- | ---- | 
| [<span data-ttu-id="457d1-205">and</span><span class="sxs-lookup"><span data-stu-id="457d1-205">and</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#and) | <span data-ttu-id="457d1-206">Check whether all expressions are true.</span><span class="sxs-lookup"><span data-stu-id="457d1-206">Check whether all expressions are true.</span></span> | 
| [<span data-ttu-id="457d1-207">equals</span><span class="sxs-lookup"><span data-stu-id="457d1-207">equals</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#equals) | <span data-ttu-id="457d1-208">Check whether both values are equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-208">Check whether both values are equivalent.</span></span> | 
| [<span data-ttu-id="457d1-209">greater</span><span class="sxs-lookup"><span data-stu-id="457d1-209">greater</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#greater) | <span data-ttu-id="457d1-210">Check whether the first value is greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-210">Check whether the first value is greater than the second value.</span></span> | 
| [<span data-ttu-id="457d1-211">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="457d1-211">greaterOrEquals</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#greaterOrEquals) | <span data-ttu-id="457d1-212">Check whether the first value is greater than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-212">Check whether the first value is greater than or equal to the second value.</span></span> | 
| [<span data-ttu-id="457d1-213">if</span><span class="sxs-lookup"><span data-stu-id="457d1-213">if</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#if) | <span data-ttu-id="457d1-214">Check whether an expression is true or false.</span><span class="sxs-lookup"><span data-stu-id="457d1-214">Check whether an expression is true or false.</span></span> <span data-ttu-id="457d1-215">Based on the result, return a specified value.</span><span class="sxs-lookup"><span data-stu-id="457d1-215">Based on the result, return a specified value.</span></span> | 
| [<span data-ttu-id="457d1-216">less</span><span class="sxs-lookup"><span data-stu-id="457d1-216">less</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#less) | <span data-ttu-id="457d1-217">Check whether the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-217">Check whether the first value is less than the second value.</span></span> | 
| [<span data-ttu-id="457d1-218">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="457d1-218">lessOrEquals</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#lessOrEquals) | <span data-ttu-id="457d1-219">Check whether the first value is less than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-219">Check whether the first value is less than or equal to the second value.</span></span> | 
| [<span data-ttu-id="457d1-220">not</span><span class="sxs-lookup"><span data-stu-id="457d1-220">not</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#not) | <span data-ttu-id="457d1-221">Check whether an expression is false.</span><span class="sxs-lookup"><span data-stu-id="457d1-221">Check whether an expression is false.</span></span> | 
| [<span data-ttu-id="457d1-222">or</span><span class="sxs-lookup"><span data-stu-id="457d1-222">or</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#or) | <span data-ttu-id="457d1-223">Check whether at least one expression is true.</span><span class="sxs-lookup"><span data-stu-id="457d1-223">Check whether at least one expression is true.</span></span> |
||| 

<a name="conversion-functions"></a>

## <a name="conversion-functions"></a><span data-ttu-id="457d1-224">Conversion functions</span><span class="sxs-lookup"><span data-stu-id="457d1-224">Conversion functions</span></span>

<span data-ttu-id="457d1-225">To change a value's type or format, you can use these conversion functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-225">To change a value's type or format, you can use these conversion functions.</span></span> <span data-ttu-id="457d1-226">For example, you can change a value from a Boolean to an integer.</span><span class="sxs-lookup"><span data-stu-id="457d1-226">For example, you can change a value from a Boolean to an integer.</span></span> <span data-ttu-id="457d1-227">To learn how Logic Apps handles content types during conversion, see [Handle content types](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="457d1-227">To learn how Logic Apps handles content types during conversion, see [Handle content types](../logic-apps/logic-apps-content-type.md).</span></span> <span data-ttu-id="457d1-228">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-228">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-229">Conversion function</span><span class="sxs-lookup"><span data-stu-id="457d1-229">Conversion function</span></span> | <span data-ttu-id="457d1-230">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-230">Task</span></span> | 
| ------------------- | ---- | 
| [<span data-ttu-id="457d1-231">array</span><span class="sxs-lookup"><span data-stu-id="457d1-231">array</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#array) | <span data-ttu-id="457d1-232">Return an array from a single specified input.</span><span class="sxs-lookup"><span data-stu-id="457d1-232">Return an array from a single specified input.</span></span> <span data-ttu-id="457d1-233">For multiple inputs, see [createArray](../logic-apps/workflow-definition-language-functions-reference.md#createArray).</span><span class="sxs-lookup"><span data-stu-id="457d1-233">For multiple inputs, see [createArray](../logic-apps/workflow-definition-language-functions-reference.md#createArray).</span></span> | 
| [<span data-ttu-id="457d1-234">base64</span><span class="sxs-lookup"><span data-stu-id="457d1-234">base64</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#base64) | <span data-ttu-id="457d1-235">Return the base64-encoded version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-235">Return the base64-encoded version for a string.</span></span> | 
| [<span data-ttu-id="457d1-236">base64ToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-236">base64ToBinary</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#base64ToBinary) | <span data-ttu-id="457d1-237">Return the binary version for a base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-237">Return the binary version for a base64-encoded string.</span></span> | 
| [<span data-ttu-id="457d1-238">base64ToString</span><span class="sxs-lookup"><span data-stu-id="457d1-238">base64ToString</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#base64ToString) | <span data-ttu-id="457d1-239">Return the string version for a base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-239">Return the string version for a base64-encoded string.</span></span> | 
| [<span data-ttu-id="457d1-240">binary</span><span class="sxs-lookup"><span data-stu-id="457d1-240">binary</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#binary) | <span data-ttu-id="457d1-241">Return the binary version for an input value.</span><span class="sxs-lookup"><span data-stu-id="457d1-241">Return the binary version for an input value.</span></span> | 
| [<span data-ttu-id="457d1-242">bool</span><span class="sxs-lookup"><span data-stu-id="457d1-242">bool</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#bool) | <span data-ttu-id="457d1-243">Return the Boolean version for an input value.</span><span class="sxs-lookup"><span data-stu-id="457d1-243">Return the Boolean version for an input value.</span></span> | 
| [<span data-ttu-id="457d1-244">createArray</span><span class="sxs-lookup"><span data-stu-id="457d1-244">createArray</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#createArray) | <span data-ttu-id="457d1-245">Return an array from multiple inputs.</span><span class="sxs-lookup"><span data-stu-id="457d1-245">Return an array from multiple inputs.</span></span> | 
| [<span data-ttu-id="457d1-246">dataUri</span><span class="sxs-lookup"><span data-stu-id="457d1-246">dataUri</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dataUri) | <span data-ttu-id="457d1-247">Return the data URI for an input value.</span><span class="sxs-lookup"><span data-stu-id="457d1-247">Return the data URI for an input value.</span></span> | 
| [<span data-ttu-id="457d1-248">dataUriToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-248">dataUriToBinary</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dataUriToBinary) | <span data-ttu-id="457d1-249">Return the binary version for a data URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-249">Return the binary version for a data URI.</span></span> | 
| [<span data-ttu-id="457d1-250">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="457d1-250">dataUriToString</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dataUriToString) | <span data-ttu-id="457d1-251">Return the string version for a data URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-251">Return the string version for a data URI.</span></span> | 
| [<span data-ttu-id="457d1-252">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="457d1-252">decodeBase64</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#decodeBase64) | <span data-ttu-id="457d1-253">Return the string version for a base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-253">Return the string version for a base64-encoded string.</span></span> | 
| [<span data-ttu-id="457d1-254">decodeDataUri</span><span class="sxs-lookup"><span data-stu-id="457d1-254">decodeDataUri</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#decodeDataUri) | <span data-ttu-id="457d1-255">Return the binary version for a data URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-255">Return the binary version for a data URI.</span></span> | 
| [<span data-ttu-id="457d1-256">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-256">decodeUriComponent</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#decodeUriComponent) | <span data-ttu-id="457d1-257">Return a string that replaces escape characters with decoded versions.</span><span class="sxs-lookup"><span data-stu-id="457d1-257">Return a string that replaces escape characters with decoded versions.</span></span> | 
| [<span data-ttu-id="457d1-258">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-258">encodeUriComponent</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#encodeUriComponent) | <span data-ttu-id="457d1-259">Return a string that replaces URL-unsafe characters with escape characters.</span><span class="sxs-lookup"><span data-stu-id="457d1-259">Return a string that replaces URL-unsafe characters with escape characters.</span></span> | 
| [<span data-ttu-id="457d1-260">float</span><span class="sxs-lookup"><span data-stu-id="457d1-260">float</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#float) | <span data-ttu-id="457d1-261">Return a floating point number for an input value.</span><span class="sxs-lookup"><span data-stu-id="457d1-261">Return a floating point number for an input value.</span></span> | 
| [<span data-ttu-id="457d1-262">int</span><span class="sxs-lookup"><span data-stu-id="457d1-262">int</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#int) | <span data-ttu-id="457d1-263">Return the integer version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-263">Return the integer version for a string.</span></span> | 
| [<span data-ttu-id="457d1-264">json</span><span class="sxs-lookup"><span data-stu-id="457d1-264">json</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#json) | <span data-ttu-id="457d1-265">Return the JavaScript Object Notation (JSON) type value or object for a string or XML.</span><span class="sxs-lookup"><span data-stu-id="457d1-265">Return the JavaScript Object Notation (JSON) type value or object for a string or XML.</span></span> | 
| [<span data-ttu-id="457d1-266">string</span><span class="sxs-lookup"><span data-stu-id="457d1-266">string</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#string) | <span data-ttu-id="457d1-267">Return the string version for an input value.</span><span class="sxs-lookup"><span data-stu-id="457d1-267">Return the string version for an input value.</span></span> | 
| [<span data-ttu-id="457d1-268">uriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-268">uriComponent</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriComponent) | <span data-ttu-id="457d1-269">Return the URI-encoded version for an input value by replacing URL-unsafe characters with escape characters.</span><span class="sxs-lookup"><span data-stu-id="457d1-269">Return the URI-encoded version for an input value by replacing URL-unsafe characters with escape characters.</span></span> | 
| [<span data-ttu-id="457d1-270">uriComponentToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-270">uriComponentToBinary</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriComponentToBinary) | <span data-ttu-id="457d1-271">Return the binary version for a URI-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-271">Return the binary version for a URI-encoded string.</span></span> | 
| [<span data-ttu-id="457d1-272">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="457d1-272">uriComponentToString</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriComponentToString) | <span data-ttu-id="457d1-273">Return the string version for a URI-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-273">Return the string version for a URI-encoded string.</span></span> | 
| [<span data-ttu-id="457d1-274">xml</span><span class="sxs-lookup"><span data-stu-id="457d1-274">xml</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#xml) | <span data-ttu-id="457d1-275">Return the XML version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-275">Return the XML version for a string.</span></span> | 
||| 

<a name="math-functions"></a>

## <a name="math-functions"></a><span data-ttu-id="457d1-276">Math functions</span><span class="sxs-lookup"><span data-stu-id="457d1-276">Math functions</span></span>

<span data-ttu-id="457d1-277">To work with integers and floats, you can use these math functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-277">To work with integers and floats, you can use these math functions.</span></span> <span data-ttu-id="457d1-278">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-278">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-279">Math function</span><span class="sxs-lookup"><span data-stu-id="457d1-279">Math function</span></span> | <span data-ttu-id="457d1-280">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-280">Task</span></span> | 
| ------------- | ---- | 
| [<span data-ttu-id="457d1-281">add</span><span class="sxs-lookup"><span data-stu-id="457d1-281">add</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#add) | <span data-ttu-id="457d1-282">Return the result from adding two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-282">Return the result from adding two numbers.</span></span> | 
| [<span data-ttu-id="457d1-283">div</span><span class="sxs-lookup"><span data-stu-id="457d1-283">div</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#div) | <span data-ttu-id="457d1-284">Return the result from dividing two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-284">Return the result from dividing two numbers.</span></span> | 
| [<span data-ttu-id="457d1-285">max</span><span class="sxs-lookup"><span data-stu-id="457d1-285">max</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#max) | <span data-ttu-id="457d1-286">Return the highest value from a set of numbers or an array.</span><span class="sxs-lookup"><span data-stu-id="457d1-286">Return the highest value from a set of numbers or an array.</span></span> | 
| [<span data-ttu-id="457d1-287">min</span><span class="sxs-lookup"><span data-stu-id="457d1-287">min</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#min) | <span data-ttu-id="457d1-288">Return the lowest value from a set of numbers or an array.</span><span class="sxs-lookup"><span data-stu-id="457d1-288">Return the lowest value from a set of numbers or an array.</span></span> | 
| [<span data-ttu-id="457d1-289">mod</span><span class="sxs-lookup"><span data-stu-id="457d1-289">mod</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#mod) | <span data-ttu-id="457d1-290">Return the remainder from dividing two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-290">Return the remainder from dividing two numbers.</span></span> | 
| [<span data-ttu-id="457d1-291">mul</span><span class="sxs-lookup"><span data-stu-id="457d1-291">mul</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#mul) | <span data-ttu-id="457d1-292">Return the product from multiplying two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-292">Return the product from multiplying two numbers.</span></span> | 
| [<span data-ttu-id="457d1-293">rand</span><span class="sxs-lookup"><span data-stu-id="457d1-293">rand</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#rand) | <span data-ttu-id="457d1-294">Return a random integer from a specified range.</span><span class="sxs-lookup"><span data-stu-id="457d1-294">Return a random integer from a specified range.</span></span> | 
| [<span data-ttu-id="457d1-295">range</span><span class="sxs-lookup"><span data-stu-id="457d1-295">range</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#range) | <span data-ttu-id="457d1-296">Return an integer array that starts from a specified integer.</span><span class="sxs-lookup"><span data-stu-id="457d1-296">Return an integer array that starts from a specified integer.</span></span> | 
| [<span data-ttu-id="457d1-297">sub</span><span class="sxs-lookup"><span data-stu-id="457d1-297">sub</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#sub) | <span data-ttu-id="457d1-298">Return the result from subtracting the second number from the first number.</span><span class="sxs-lookup"><span data-stu-id="457d1-298">Return the result from subtracting the second number from the first number.</span></span> | 
||| 

<a name="date-time-functions"></a>

## <a name="date-and-time-functions"></a><span data-ttu-id="457d1-299">Date and time functions</span><span class="sxs-lookup"><span data-stu-id="457d1-299">Date and time functions</span></span>

<span data-ttu-id="457d1-300">To work with dates and times, you can use these date and time functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-300">To work with dates and times, you can use these date and time functions.</span></span>
<span data-ttu-id="457d1-301">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-301">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-302">Date or time function</span><span class="sxs-lookup"><span data-stu-id="457d1-302">Date or time function</span></span> | <span data-ttu-id="457d1-303">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-303">Task</span></span> | 
| --------------------- | ---- | 
| [<span data-ttu-id="457d1-304">addDays</span><span class="sxs-lookup"><span data-stu-id="457d1-304">addDays</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addDays) | <span data-ttu-id="457d1-305">Add a number of days to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-305">Add a number of days to a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-306">addHours</span><span class="sxs-lookup"><span data-stu-id="457d1-306">addHours</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addHours) | <span data-ttu-id="457d1-307">Add a number of hours to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-307">Add a number of hours to a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-308">addMinutes</span><span class="sxs-lookup"><span data-stu-id="457d1-308">addMinutes</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addMinutes) | <span data-ttu-id="457d1-309">Add a number of minutes to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-309">Add a number of minutes to a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-310">addSeconds</span><span class="sxs-lookup"><span data-stu-id="457d1-310">addSeconds</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addSeconds) | <span data-ttu-id="457d1-311">Add a number of seconds to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-311">Add a number of seconds to a timestamp.</span></span> |  
| [<span data-ttu-id="457d1-312">addToTime</span><span class="sxs-lookup"><span data-stu-id="457d1-312">addToTime</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addToTime) | <span data-ttu-id="457d1-313">Add a number of time units to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-313">Add a number of time units to a timestamp.</span></span> <span data-ttu-id="457d1-314">See also [getFutureTime](../logic-apps/workflow-definition-language-functions-reference.md#getFutureTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-314">See also [getFutureTime](../logic-apps/workflow-definition-language-functions-reference.md#getFutureTime).</span></span> | 
| [<span data-ttu-id="457d1-315">convertFromUtc</span><span class="sxs-lookup"><span data-stu-id="457d1-315">convertFromUtc</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#convertFromUtc) | <span data-ttu-id="457d1-316">Convert a timestamp from Universal Time Coordinated (UTC) to the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-316">Convert a timestamp from Universal Time Coordinated (UTC) to the target time zone.</span></span> | 
| [<span data-ttu-id="457d1-317">convertTimeZone</span><span class="sxs-lookup"><span data-stu-id="457d1-317">convertTimeZone</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#convertTimeZone) | <span data-ttu-id="457d1-318">Convert a timestamp from the source time zone to the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-318">Convert a timestamp from the source time zone to the target time zone.</span></span> | 
| [<span data-ttu-id="457d1-319">convertToUtc</span><span class="sxs-lookup"><span data-stu-id="457d1-319">convertToUtc</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#convertToUtc) | <span data-ttu-id="457d1-320">Convert a timestamp from the source time zone to Universal Time Coordinated (UTC).</span><span class="sxs-lookup"><span data-stu-id="457d1-320">Convert a timestamp from the source time zone to Universal Time Coordinated (UTC).</span></span> | 
| [<span data-ttu-id="457d1-321">dayOfMonth</span><span class="sxs-lookup"><span data-stu-id="457d1-321">dayOfMonth</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dayOfMonth) | <span data-ttu-id="457d1-322">Return the day of the month component from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-322">Return the day of the month component from a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-323">dayOfWeek</span><span class="sxs-lookup"><span data-stu-id="457d1-323">dayOfWeek</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dayOfWeek) | <span data-ttu-id="457d1-324">Return the day of the week component from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-324">Return the day of the week component from a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-325">dayOfYear</span><span class="sxs-lookup"><span data-stu-id="457d1-325">dayOfYear</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#dayOfYear) | <span data-ttu-id="457d1-326">Return the day of the year component from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-326">Return the day of the year component from a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-327">formatDateTime</span><span class="sxs-lookup"><span data-stu-id="457d1-327">formatDateTime</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#formatDateTime) | <span data-ttu-id="457d1-328">Return the date from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-328">Return the date from a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-329">getFutureTime</span><span class="sxs-lookup"><span data-stu-id="457d1-329">getFutureTime</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#getFutureTime) | <span data-ttu-id="457d1-330">Return the current timestamp plus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="457d1-330">Return the current timestamp plus the specified time units.</span></span> <span data-ttu-id="457d1-331">See also [addToTime](../logic-apps/workflow-definition-language-functions-reference.md#addToTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-331">See also [addToTime](../logic-apps/workflow-definition-language-functions-reference.md#addToTime).</span></span> | 
| [<span data-ttu-id="457d1-332">getPastTime</span><span class="sxs-lookup"><span data-stu-id="457d1-332">getPastTime</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#getPastTime) | <span data-ttu-id="457d1-333">Return the current timestamp minus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="457d1-333">Return the current timestamp minus the specified time units.</span></span> <span data-ttu-id="457d1-334">See also [subtractFromTime](../logic-apps/workflow-definition-language-functions-reference.md#subtractFromTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-334">See also [subtractFromTime](../logic-apps/workflow-definition-language-functions-reference.md#subtractFromTime).</span></span> | 
| [<span data-ttu-id="457d1-335">startOfDay</span><span class="sxs-lookup"><span data-stu-id="457d1-335">startOfDay</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#startOfDay) | <span data-ttu-id="457d1-336">Return the start of the day for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-336">Return the start of the day for a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-337">startOfHour</span><span class="sxs-lookup"><span data-stu-id="457d1-337">startOfHour</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#startOfHour) | <span data-ttu-id="457d1-338">Return the start of the hour for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-338">Return the start of the hour for a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-339">startOfMonth</span><span class="sxs-lookup"><span data-stu-id="457d1-339">startOfMonth</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#startOfMonth) | <span data-ttu-id="457d1-340">Return the start of the month for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-340">Return the start of the month for a timestamp.</span></span> | 
| [<span data-ttu-id="457d1-341">subtractFromTime</span><span class="sxs-lookup"><span data-stu-id="457d1-341">subtractFromTime</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#subtractFromTime) | <span data-ttu-id="457d1-342">Subtract a number of time units from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-342">Subtract a number of time units from a timestamp.</span></span> <span data-ttu-id="457d1-343">See also [getPastTime](../logic-apps/workflow-definition-language-functions-reference.md#getPastTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-343">See also [getPastTime](../logic-apps/workflow-definition-language-functions-reference.md#getPastTime).</span></span> | 
| [<span data-ttu-id="457d1-344">ticks</span><span class="sxs-lookup"><span data-stu-id="457d1-344">ticks</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#ticks) | <span data-ttu-id="457d1-345">Return the `ticks` property value for a specified timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-345">Return the `ticks` property value for a specified timestamp.</span></span> | 
| [<span data-ttu-id="457d1-346">utcNow</span><span class="sxs-lookup"><span data-stu-id="457d1-346">utcNow</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#utcNow) | <span data-ttu-id="457d1-347">Return the current timestamp as a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-347">Return the current timestamp as a string.</span></span> | 
||| 

<a name="workflow-functions"></a>

## <a name="workflow-functions"></a><span data-ttu-id="457d1-348">Workflow functions</span><span class="sxs-lookup"><span data-stu-id="457d1-348">Workflow functions</span></span>

<span data-ttu-id="457d1-349">These workflow functions can help you:</span><span class="sxs-lookup"><span data-stu-id="457d1-349">These workflow functions can help you:</span></span>

* <span data-ttu-id="457d1-350">Get details about a workflow instance at run time.</span><span class="sxs-lookup"><span data-stu-id="457d1-350">Get details about a workflow instance at run time.</span></span> 
* <span data-ttu-id="457d1-351">Work with the inputs used for instantiating logic apps.</span><span class="sxs-lookup"><span data-stu-id="457d1-351">Work with the inputs used for instantiating logic apps.</span></span>
* <span data-ttu-id="457d1-352">Reference the outputs from triggers and actions.</span><span class="sxs-lookup"><span data-stu-id="457d1-352">Reference the outputs from triggers and actions.</span></span>

<span data-ttu-id="457d1-353">For example, you can reference the outputs from one action and use that data in a later action.</span><span class="sxs-lookup"><span data-stu-id="457d1-353">For example, you can reference the outputs from one action and use that data in a later action.</span></span> <span data-ttu-id="457d1-354">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-354">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-355">Workflow function</span><span class="sxs-lookup"><span data-stu-id="457d1-355">Workflow function</span></span> | <span data-ttu-id="457d1-356">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-356">Task</span></span> | 
| ----------------- | ---- | 
| [<span data-ttu-id="457d1-357">action</span><span class="sxs-lookup"><span data-stu-id="457d1-357">action</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#action) | <span data-ttu-id="457d1-358">Return the current action's output at runtime, or values from other JSON name-and-value pairs.</span><span class="sxs-lookup"><span data-stu-id="457d1-358">Return the current action's output at runtime, or values from other JSON name-and-value pairs.</span></span> <span data-ttu-id="457d1-359">See also [actions](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-359">See also [actions](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span></span> | 
| [<span data-ttu-id="457d1-360">actionBody</span><span class="sxs-lookup"><span data-stu-id="457d1-360">actionBody</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#actionBody) | <span data-ttu-id="457d1-361">Return an action's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-361">Return an action's `body` output at runtime.</span></span> <span data-ttu-id="457d1-362">See also [body](../logic-apps/workflow-definition-language-functions-reference.md#body).</span><span class="sxs-lookup"><span data-stu-id="457d1-362">See also [body](../logic-apps/workflow-definition-language-functions-reference.md#body).</span></span> | 
| [<span data-ttu-id="457d1-363">actionOutputs</span><span class="sxs-lookup"><span data-stu-id="457d1-363">actionOutputs</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#actionOutputs) | <span data-ttu-id="457d1-364">Return an action's output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-364">Return an action's output at runtime.</span></span> <span data-ttu-id="457d1-365">See [actions](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-365">See [actions](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span></span> | 
| [<span data-ttu-id="457d1-366">actions</span><span class="sxs-lookup"><span data-stu-id="457d1-366">actions</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#actions) | <span data-ttu-id="457d1-367">Return an action's output at runtime, or values from other JSON name-and-value pairs.</span><span class="sxs-lookup"><span data-stu-id="457d1-367">Return an action's output at runtime, or values from other JSON name-and-value pairs.</span></span> <span data-ttu-id="457d1-368">See also [action](../logic-apps/workflow-definition-language-functions-reference.md#action).</span><span class="sxs-lookup"><span data-stu-id="457d1-368">See also [action](../logic-apps/workflow-definition-language-functions-reference.md#action).</span></span>  | 
| [<span data-ttu-id="457d1-369">body</span><span class="sxs-lookup"><span data-stu-id="457d1-369">body</span></span>](#body) | <span data-ttu-id="457d1-370">Return an action's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-370">Return an action's `body` output at runtime.</span></span> <span data-ttu-id="457d1-371">See also [actionBody](../logic-apps/workflow-definition-language-functions-reference.md#actionBody).</span><span class="sxs-lookup"><span data-stu-id="457d1-371">See also [actionBody](../logic-apps/workflow-definition-language-functions-reference.md#actionBody).</span></span> | 
| [<span data-ttu-id="457d1-372">formDataMultiValues</span><span class="sxs-lookup"><span data-stu-id="457d1-372">formDataMultiValues</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#formDataMultiValues) | <span data-ttu-id="457d1-373">Create an array with the values that match a key name in *form-data* or *form-encoded* action outputs.</span><span class="sxs-lookup"><span data-stu-id="457d1-373">Create an array with the values that match a key name in *form-data* or *form-encoded* action outputs.</span></span> | 
| [<span data-ttu-id="457d1-374">formDataValue</span><span class="sxs-lookup"><span data-stu-id="457d1-374">formDataValue</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#formDataValue) | <span data-ttu-id="457d1-375">Return a single value that matches a key name in an action's *form-data* or *form-encoded output*.</span><span class="sxs-lookup"><span data-stu-id="457d1-375">Return a single value that matches a key name in an action's *form-data* or *form-encoded output*.</span></span> | 
| [<span data-ttu-id="457d1-376">item</span><span class="sxs-lookup"><span data-stu-id="457d1-376">item</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#item) | <span data-ttu-id="457d1-377">When inside a repeating action over an array, return the current item in the array during the action's current iteration.</span><span class="sxs-lookup"><span data-stu-id="457d1-377">When inside a repeating action over an array, return the current item in the array during the action's current iteration.</span></span> | 
| [<span data-ttu-id="457d1-378">items</span><span class="sxs-lookup"><span data-stu-id="457d1-378">items</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#items) | <span data-ttu-id="457d1-379">When inside a for-each or do-until-loop, return the current item from the specified loop.</span><span class="sxs-lookup"><span data-stu-id="457d1-379">When inside a for-each or do-until-loop, return the current item from the specified loop.</span></span>| 
| [<span data-ttu-id="457d1-380">listCallbackUrl</span><span class="sxs-lookup"><span data-stu-id="457d1-380">listCallbackUrl</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#listCallbackUrl) | <span data-ttu-id="457d1-381">Return the "callback URL" that calls a trigger or action.</span><span class="sxs-lookup"><span data-stu-id="457d1-381">Return the "callback URL" that calls a trigger or action.</span></span> | 
| [<span data-ttu-id="457d1-382">multipartBody</span><span class="sxs-lookup"><span data-stu-id="457d1-382">multipartBody</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#multipartBody) | <span data-ttu-id="457d1-383">Return the body for a specific part in an action's output that has multiple parts.</span><span class="sxs-lookup"><span data-stu-id="457d1-383">Return the body for a specific part in an action's output that has multiple parts.</span></span> | 
| [<span data-ttu-id="457d1-384">parameters</span><span class="sxs-lookup"><span data-stu-id="457d1-384">parameters</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#parameters) | <span data-ttu-id="457d1-385">Return the value for a parameter that is described in your logic app definition.</span><span class="sxs-lookup"><span data-stu-id="457d1-385">Return the value for a parameter that is described in your logic app definition.</span></span> | 
| [<span data-ttu-id="457d1-386">trigger</span><span class="sxs-lookup"><span data-stu-id="457d1-386">trigger</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#trigger) | <span data-ttu-id="457d1-387">Return a trigger's output at runtime, or from other JSON name-and-value pairs.</span><span class="sxs-lookup"><span data-stu-id="457d1-387">Return a trigger's output at runtime, or from other JSON name-and-value pairs.</span></span> <span data-ttu-id="457d1-388">See also [triggerOutputs](#triggerOutputs) and [triggerBody](../logic-apps/workflow-definition-language-functions-reference.md#triggerBody).</span><span class="sxs-lookup"><span data-stu-id="457d1-388">See also [triggerOutputs](#triggerOutputs) and [triggerBody](../logic-apps/workflow-definition-language-functions-reference.md#triggerBody).</span></span> | 
| [<span data-ttu-id="457d1-389">triggerBody</span><span class="sxs-lookup"><span data-stu-id="457d1-389">triggerBody</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerBody) | <span data-ttu-id="457d1-390">Return a trigger's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-390">Return a trigger's `body` output at runtime.</span></span> <span data-ttu-id="457d1-391">See [trigger](../logic-apps/workflow-definition-language-functions-reference.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="457d1-391">See [trigger](../logic-apps/workflow-definition-language-functions-reference.md#trigger).</span></span> | 
| [<span data-ttu-id="457d1-392">triggerFormDataValue</span><span class="sxs-lookup"><span data-stu-id="457d1-392">triggerFormDataValue</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerFormDataValue) | <span data-ttu-id="457d1-393">Return a single value matching a key name in *form-data* or *form-encoded* trigger outputs.</span><span class="sxs-lookup"><span data-stu-id="457d1-393">Return a single value matching a key name in *form-data* or *form-encoded* trigger outputs.</span></span> | 
| [<span data-ttu-id="457d1-394">triggerMultipartBody</span><span class="sxs-lookup"><span data-stu-id="457d1-394">triggerMultipartBody</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerMultipartBody) | <span data-ttu-id="457d1-395">Return the body for a specific part in a trigger's multipart output.</span><span class="sxs-lookup"><span data-stu-id="457d1-395">Return the body for a specific part in a trigger's multipart output.</span></span> | 
| [<span data-ttu-id="457d1-396">triggerFormDataMultiValues</span><span class="sxs-lookup"><span data-stu-id="457d1-396">triggerFormDataMultiValues</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerFormDataMultiValues) | <span data-ttu-id="457d1-397">Create an array whose values match a key name in *form-data* or *form-encoded* trigger outputs.</span><span class="sxs-lookup"><span data-stu-id="457d1-397">Create an array whose values match a key name in *form-data* or *form-encoded* trigger outputs.</span></span> | 
| [<span data-ttu-id="457d1-398">triggerOutputs</span><span class="sxs-lookup"><span data-stu-id="457d1-398">triggerOutputs</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#triggerOutputs) | <span data-ttu-id="457d1-399">Return a trigger's output at runtime, or values from other JSON name-and-value pairs.</span><span class="sxs-lookup"><span data-stu-id="457d1-399">Return a trigger's output at runtime, or values from other JSON name-and-value pairs.</span></span> <span data-ttu-id="457d1-400">See [trigger](../logic-apps/workflow-definition-language-functions-reference.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="457d1-400">See [trigger](../logic-apps/workflow-definition-language-functions-reference.md#trigger).</span></span> | 
| [<span data-ttu-id="457d1-401">variables</span><span class="sxs-lookup"><span data-stu-id="457d1-401">variables</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#variables) | <span data-ttu-id="457d1-402">Return the value for a specified variable.</span><span class="sxs-lookup"><span data-stu-id="457d1-402">Return the value for a specified variable.</span></span> | 
| [<span data-ttu-id="457d1-403">workflow</span><span class="sxs-lookup"><span data-stu-id="457d1-403">workflow</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#workflow) | <span data-ttu-id="457d1-404">Return all the details about the workflow itself during run time.</span><span class="sxs-lookup"><span data-stu-id="457d1-404">Return all the details about the workflow itself during run time.</span></span> | 
||| 

<a name="uri-parsing-functions"></a>

## <a name="uri-parsing-functions"></a><span data-ttu-id="457d1-405">URI parsing functions</span><span class="sxs-lookup"><span data-stu-id="457d1-405">URI parsing functions</span></span>

<span data-ttu-id="457d1-406">To work with uniform resource identifiers (URIs) and get various property values for these URIs, you can use these URI parsing functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-406">To work with uniform resource identifiers (URIs) and get various property values for these URIs, you can use these URI parsing functions.</span></span> <span data-ttu-id="457d1-407">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-407">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-408">URI parsing function</span><span class="sxs-lookup"><span data-stu-id="457d1-408">URI parsing function</span></span> | <span data-ttu-id="457d1-409">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-409">Task</span></span> | 
| -------------------- | ---- | 
| [<span data-ttu-id="457d1-410">uriHost</span><span class="sxs-lookup"><span data-stu-id="457d1-410">uriHost</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriHost) | <span data-ttu-id="457d1-411">Return the `host` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-411">Return the `host` value for a uniform resource identifier (URI).</span></span> | 
| [<span data-ttu-id="457d1-412">uriPath</span><span class="sxs-lookup"><span data-stu-id="457d1-412">uriPath</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriPath) | <span data-ttu-id="457d1-413">Return the `path` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-413">Return the `path` value for a uniform resource identifier (URI).</span></span> | 
| [<span data-ttu-id="457d1-414">uriPathAndQuery</span><span class="sxs-lookup"><span data-stu-id="457d1-414">uriPathAndQuery</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriPathAndQuery) | <span data-ttu-id="457d1-415">Return the `path` and `query` values for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-415">Return the `path` and `query` values for a uniform resource identifier (URI).</span></span> | 
| [<span data-ttu-id="457d1-416">uriPort</span><span class="sxs-lookup"><span data-stu-id="457d1-416">uriPort</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriPort) | <span data-ttu-id="457d1-417">Return the `port` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-417">Return the `port` value for a uniform resource identifier (URI).</span></span> | 
| [<span data-ttu-id="457d1-418">uriQuery</span><span class="sxs-lookup"><span data-stu-id="457d1-418">uriQuery</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriQuery) | <span data-ttu-id="457d1-419">Return the `query` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-419">Return the `query` value for a uniform resource identifier (URI).</span></span> | 
| [<span data-ttu-id="457d1-420">uriScheme</span><span class="sxs-lookup"><span data-stu-id="457d1-420">uriScheme</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#uriScheme) | <span data-ttu-id="457d1-421">Return the `scheme` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-421">Return the `scheme` value for a uniform resource identifier (URI).</span></span> | 
||| 

<a name="manipulation-functions"></a>

## <a name="manipulation-functions-json--xml"></a><span data-ttu-id="457d1-422">Manipulation functions: JSON & XML</span><span class="sxs-lookup"><span data-stu-id="457d1-422">Manipulation functions: JSON & XML</span></span>

<span data-ttu-id="457d1-423">To work with JSON objects and XML nodes, you can use these manipulation functions.</span><span class="sxs-lookup"><span data-stu-id="457d1-423">To work with JSON objects and XML nodes, you can use these manipulation functions.</span></span> <span data-ttu-id="457d1-424">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span><span class="sxs-lookup"><span data-stu-id="457d1-424">For the full reference about each function, see the [alphabetical list](../logic-apps/workflow-definition-language-functions-reference.md#alphabetical-list).</span></span>

| <span data-ttu-id="457d1-425">Manipulation function</span><span class="sxs-lookup"><span data-stu-id="457d1-425">Manipulation function</span></span> | <span data-ttu-id="457d1-426">Task</span><span class="sxs-lookup"><span data-stu-id="457d1-426">Task</span></span> | 
| --------------------- | ---- | 
| [<span data-ttu-id="457d1-427">addProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-427">addProperty</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#addProperty) | <span data-ttu-id="457d1-428">Add a property and its value, or name-value pair, to a JSON object, and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-428">Add a property and its value, or name-value pair, to a JSON object, and return the updated object.</span></span> | 
| [<span data-ttu-id="457d1-429">coalesce</span><span class="sxs-lookup"><span data-stu-id="457d1-429">coalesce</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#coalesce) | <span data-ttu-id="457d1-430">Return the first non-null value from one or more parameters.</span><span class="sxs-lookup"><span data-stu-id="457d1-430">Return the first non-null value from one or more parameters.</span></span> | 
| [<span data-ttu-id="457d1-431">removeProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-431">removeProperty</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#removeProperty) | <span data-ttu-id="457d1-432">Remove a property from a JSON object and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-432">Remove a property from a JSON object and return the updated object.</span></span> | 
| [<span data-ttu-id="457d1-433">setProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-433">setProperty</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#setProperty) | <span data-ttu-id="457d1-434">Set the value for a JSON object's property and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-434">Set the value for a JSON object's property and return the updated object.</span></span> | 
| [<span data-ttu-id="457d1-435">xpath</span><span class="sxs-lookup"><span data-stu-id="457d1-435">xpath</span></span>](../logic-apps/workflow-definition-language-functions-reference.md#xpath) | <span data-ttu-id="457d1-436">Check XML for nodes or values that match an XPath (XML Path Language) expression, and return the matching nodes or values.</span><span class="sxs-lookup"><span data-stu-id="457d1-436">Check XML for nodes or values that match an XPath (XML Path Language) expression, and return the matching nodes or values.</span></span> | 
||| 

<a name="alphabetical-list"></a>
<a name="action"></a>

### <a name="action"></a><span data-ttu-id="457d1-437">action</span><span class="sxs-lookup"><span data-stu-id="457d1-437">action</span></span>

<span data-ttu-id="457d1-438">Return the *current* action's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span><span class="sxs-lookup"><span data-stu-id="457d1-438">Return the *current* action's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span></span> <span data-ttu-id="457d1-439">By default, this function references the entire action object, but you can optionally specify a property whose value you want.</span><span class="sxs-lookup"><span data-stu-id="457d1-439">By default, this function references the entire action object, but you can optionally specify a property whose value you want.</span></span> <span data-ttu-id="457d1-440">See also [actions()](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-440">See also [actions()](../logic-apps/workflow-definition-language-functions-reference.md#actions).</span></span>

<span data-ttu-id="457d1-441">You can use the `action()` function only in these places:</span><span class="sxs-lookup"><span data-stu-id="457d1-441">You can use the `action()` function only in these places:</span></span> 

* <span data-ttu-id="457d1-442">The `unsubscribe` property for a webhook action so you can access the result from the original `subscribe` request</span><span class="sxs-lookup"><span data-stu-id="457d1-442">The `unsubscribe` property for a webhook action so you can access the result from the original `subscribe` request</span></span>
* <span data-ttu-id="457d1-443">The `trackedProperties` property for an action</span><span class="sxs-lookup"><span data-stu-id="457d1-443">The `trackedProperties` property for an action</span></span>
* <span data-ttu-id="457d1-444">The `do-until` loop condition for an action</span><span class="sxs-lookup"><span data-stu-id="457d1-444">The `do-until` loop condition for an action</span></span>

```
action()
action().outputs.body.<property> 
```

| <span data-ttu-id="457d1-445">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-445">Parameter</span></span> | <span data-ttu-id="457d1-446">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-446">Required</span></span> | <span data-ttu-id="457d1-447">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-447">Type</span></span> | <span data-ttu-id="457d1-448">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-448">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-449"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-449"><*property*></span></span> | <span data-ttu-id="457d1-450">No</span><span class="sxs-lookup"><span data-stu-id="457d1-450">No</span></span> | <span data-ttu-id="457d1-451">String</span><span class="sxs-lookup"><span data-stu-id="457d1-451">String</span></span> | <span data-ttu-id="457d1-452">The name for the action object's property whose value you want: **name**, **startTime**, **endTime**, **inputs**, **outputs**, **status**, **code**, **trackingId**, and **clientTrackingId**.</span><span class="sxs-lookup"><span data-stu-id="457d1-452">The name for the action object's property whose value you want: **name**, **startTime**, **endTime**, **inputs**, **outputs**, **status**, **code**, **trackingId**, and **clientTrackingId**.</span></span> <span data-ttu-id="457d1-453">In the Azure portal, you can find these properties by reviewing a specific run history's details.</span><span class="sxs-lookup"><span data-stu-id="457d1-453">In the Azure portal, you can find these properties by reviewing a specific run history's details.</span></span> <span data-ttu-id="457d1-454">For more information, see [REST API - Workflow Run Actions](https://docs.microsoft.com/rest/api/logic/workflowrunactions/get).</span><span class="sxs-lookup"><span data-stu-id="457d1-454">For more information, see [REST API - Workflow Run Actions](https://docs.microsoft.com/rest/api/logic/workflowrunactions/get).</span></span> | 
||||| 

| <span data-ttu-id="457d1-455">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-455">Return value</span></span> | <span data-ttu-id="457d1-456">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-456">Type</span></span> | <span data-ttu-id="457d1-457">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-457">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-458"><*action-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-458"><*action-output*></span></span> | <span data-ttu-id="457d1-459">String</span><span class="sxs-lookup"><span data-stu-id="457d1-459">String</span></span> | <span data-ttu-id="457d1-460">The output from the current action or property</span><span class="sxs-lookup"><span data-stu-id="457d1-460">The output from the current action or property</span></span> | 
|||| 

<a name="actionBody"></a>

### <a name="actionbody"></a><span data-ttu-id="457d1-461">actionBody</span><span class="sxs-lookup"><span data-stu-id="457d1-461">actionBody</span></span>

<span data-ttu-id="457d1-462">Return an action's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-462">Return an action's `body` output at runtime.</span></span> <span data-ttu-id="457d1-463">Shorthand for `actions('<actionName>').outputs.body`.</span><span class="sxs-lookup"><span data-stu-id="457d1-463">Shorthand for `actions('<actionName>').outputs.body`.</span></span> <span data-ttu-id="457d1-464">See [body()](#body) and [actions()](#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-464">See [body()](#body) and [actions()](#actions).</span></span>

```
actionBody('<actionName>')
```

| <span data-ttu-id="457d1-465">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-465">Parameter</span></span> | <span data-ttu-id="457d1-466">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-466">Required</span></span> | <span data-ttu-id="457d1-467">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-467">Type</span></span> | <span data-ttu-id="457d1-468">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-468">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-469"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-469"><*actionName*></span></span> | <span data-ttu-id="457d1-470">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-470">Yes</span></span> | <span data-ttu-id="457d1-471">String</span><span class="sxs-lookup"><span data-stu-id="457d1-471">String</span></span> | <span data-ttu-id="457d1-472">The name for the action's `body` output that you want</span><span class="sxs-lookup"><span data-stu-id="457d1-472">The name for the action's `body` output that you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-473">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-473">Return value</span></span> | <span data-ttu-id="457d1-474">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-474">Type</span></span> | <span data-ttu-id="457d1-475">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-475">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-476"><*action-body-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-476"><*action-body-output*></span></span> | <span data-ttu-id="457d1-477">String</span><span class="sxs-lookup"><span data-stu-id="457d1-477">String</span></span> | <span data-ttu-id="457d1-478">The `body` output from the specified action</span><span class="sxs-lookup"><span data-stu-id="457d1-478">The `body` output from the specified action</span></span> | 
|||| 

<span data-ttu-id="457d1-479">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-479">*Example*</span></span>

<span data-ttu-id="457d1-480">This example gets the `body` output from the Twitter action `Get user`:</span><span class="sxs-lookup"><span data-stu-id="457d1-480">This example gets the `body` output from the Twitter action `Get user`:</span></span> 

```
actionBody('Get_user')
```

<span data-ttu-id="457d1-481">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-481">And returns this result:</span></span>

```json
"body": {
  "FullName": "Contoso Corporation",
  "Location": "Generic Town, USA",
  "Id": 283541717,
  "UserName": "ContosoInc",
  "FollowersCount": 172,
  "Description": "Leading the way in transforming the digital workplace.",
  "StatusesCount": 93,
  "FriendsCount": 126,
  "FavouritesCount": 46,
  "ProfileImageUrl": "https://pbs.twimg.com/profile_images/908820389907722240/gG9zaHcd_400x400.jpg"
}
```

<a name="actionOutputs"></a>

### <a name="actionoutputs"></a><span data-ttu-id="457d1-482">actionOutputs</span><span class="sxs-lookup"><span data-stu-id="457d1-482">actionOutputs</span></span>

<span data-ttu-id="457d1-483">Return an action's output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-483">Return an action's output at runtime.</span></span> <span data-ttu-id="457d1-484">Shorthand for `actions('<actionName>').outputs`.</span><span class="sxs-lookup"><span data-stu-id="457d1-484">Shorthand for `actions('<actionName>').outputs`.</span></span> <span data-ttu-id="457d1-485">See [actions()](#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-485">See [actions()](#actions).</span></span>

```
actionOutputs('<actionName>')
```

| <span data-ttu-id="457d1-486">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-486">Parameter</span></span> | <span data-ttu-id="457d1-487">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-487">Required</span></span> | <span data-ttu-id="457d1-488">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-488">Type</span></span> | <span data-ttu-id="457d1-489">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-489">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-490"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-490"><*actionName*></span></span> | <span data-ttu-id="457d1-491">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-491">Yes</span></span> | <span data-ttu-id="457d1-492">String</span><span class="sxs-lookup"><span data-stu-id="457d1-492">String</span></span> | <span data-ttu-id="457d1-493">The name for the action's output that you want</span><span class="sxs-lookup"><span data-stu-id="457d1-493">The name for the action's output that you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-494">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-494">Return value</span></span> | <span data-ttu-id="457d1-495">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-495">Type</span></span> | <span data-ttu-id="457d1-496">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-496">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-497"><*output*></span><span class="sxs-lookup"><span data-stu-id="457d1-497"><*output*></span></span> | <span data-ttu-id="457d1-498">String</span><span class="sxs-lookup"><span data-stu-id="457d1-498">String</span></span> | <span data-ttu-id="457d1-499">The output from the specified action</span><span class="sxs-lookup"><span data-stu-id="457d1-499">The output from the specified action</span></span> | 
|||| 

<span data-ttu-id="457d1-500">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-500">*Example*</span></span>

<span data-ttu-id="457d1-501">This example gets the output from the Twitter action `Get user`:</span><span class="sxs-lookup"><span data-stu-id="457d1-501">This example gets the output from the Twitter action `Get user`:</span></span> 

```
actionOutputs('Get_user')
```

<span data-ttu-id="457d1-502">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-502">And returns this result:</span></span>

```json
{ 
  "statusCode": 200,
  "headers": {
    "Pragma": "no-cache",
    "Vary": "Accept-Encoding",
    "x-ms-request-id": "a916ec8f52211265d98159adde2efe0b",
    "X-Content-Type-Options": "nosniff",
    "Timing-Allow-Origin": "*",
    "Cache-Control": "no-cache",
    "Date": "Mon, 09 Apr 2018 18:47:12 GMT",
    "Set-Cookie": "ARRAffinity=b9400932367ab5e3b6802e3d6158afffb12fcde8666715f5a5fbd4142d0f0b7d;Path=/;HttpOnly;Domain=twitter-wus.azconn-wus.p.azurewebsites.net",
    "X-AspNet-Version": "4.0.30319",
    "X-Powered-By": "ASP.NET",
    "Content-Type": "application/json; charset=utf-8",
    "Expires": "-1",
    "Content-Length": "339"
  },
  "body": {
    "FullName": "Contoso Corporation",
    "Location": "Generic Town, USA",
    "Id": 283541717,
    "UserName": "ContosoInc",
    "FollowersCount": 172,
    "Description": "Leading the way in transforming the digital workplace.",
    "StatusesCount": 93,
    "FriendsCount": 126,
    "FavouritesCount": 46,
    "ProfileImageUrl": "https://pbs.twimg.com/profile_images/908820389907722240/gG9zaHcd_400x400.jpg"
  }
}
```

<a name="actions"></a>

### <a name="actions"></a><span data-ttu-id="457d1-503">actions</span><span class="sxs-lookup"><span data-stu-id="457d1-503">actions</span></span>

<span data-ttu-id="457d1-504">Return an action's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span><span class="sxs-lookup"><span data-stu-id="457d1-504">Return an action's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span></span> <span data-ttu-id="457d1-505">By default, the function references the entire action object, but you can optionally specify a property whose value that you want.</span><span class="sxs-lookup"><span data-stu-id="457d1-505">By default, the function references the entire action object, but you can optionally specify a property whose value that you want.</span></span> <span data-ttu-id="457d1-506">For shorthand versions, see [actionBody()](#actionBody), [actionOutputs()](#actionOutputs), and [body()](#body).</span><span class="sxs-lookup"><span data-stu-id="457d1-506">For shorthand versions, see [actionBody()](#actionBody), [actionOutputs()](#actionOutputs), and [body()](#body).</span></span> <span data-ttu-id="457d1-507">For the current action, see [action()](#action).</span><span class="sxs-lookup"><span data-stu-id="457d1-507">For the current action, see [action()](#action).</span></span>

> [!NOTE] 
> <span data-ttu-id="457d1-508">Previously, you could use the `actions()` function or the `conditions` element when specifying that an action ran based on the output from another action.</span><span class="sxs-lookup"><span data-stu-id="457d1-508">Previously, you could use the `actions()` function or the `conditions` element when specifying that an action ran based on the output from another action.</span></span> <span data-ttu-id="457d1-509">However, to declare explicitly dependencies between actions, you must now use the dependent action's `runAfter` property.</span><span class="sxs-lookup"><span data-stu-id="457d1-509">However, to declare explicitly dependencies between actions, you must now use the dependent action's `runAfter` property.</span></span> <span data-ttu-id="457d1-510">To learn more about the `runAfter` property, see [Catch and handle failures with the runAfter property](../logic-apps/logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="457d1-510">To learn more about the `runAfter` property, see [Catch and handle failures with the runAfter property](../logic-apps/logic-apps-workflow-definition-language.md).</span></span>

```
actions('<actionName>')
actions('<actionName>').outputs.body.<property> 
```

| <span data-ttu-id="457d1-511">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-511">Parameter</span></span> | <span data-ttu-id="457d1-512">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-512">Required</span></span> | <span data-ttu-id="457d1-513">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-513">Type</span></span> | <span data-ttu-id="457d1-514">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-514">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-515"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-515"><*actionName*></span></span> | <span data-ttu-id="457d1-516">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-516">Yes</span></span> | <span data-ttu-id="457d1-517">String</span><span class="sxs-lookup"><span data-stu-id="457d1-517">String</span></span> | <span data-ttu-id="457d1-518">The name for the action object whose output you want</span><span class="sxs-lookup"><span data-stu-id="457d1-518">The name for the action object whose output you want</span></span>  | 
| <span data-ttu-id="457d1-519"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-519"><*property*></span></span> | <span data-ttu-id="457d1-520">No</span><span class="sxs-lookup"><span data-stu-id="457d1-520">No</span></span> | <span data-ttu-id="457d1-521">String</span><span class="sxs-lookup"><span data-stu-id="457d1-521">String</span></span> | <span data-ttu-id="457d1-522">The name for the action object's property whose value you want: **name**, **startTime**, **endTime**, **inputs**, **outputs**, **status**, **code**, **trackingId**, and **clientTrackingId**.</span><span class="sxs-lookup"><span data-stu-id="457d1-522">The name for the action object's property whose value you want: **name**, **startTime**, **endTime**, **inputs**, **outputs**, **status**, **code**, **trackingId**, and **clientTrackingId**.</span></span> <span data-ttu-id="457d1-523">In the Azure portal, you can find these properties by reviewing a specific run history's details.</span><span class="sxs-lookup"><span data-stu-id="457d1-523">In the Azure portal, you can find these properties by reviewing a specific run history's details.</span></span> <span data-ttu-id="457d1-524">For more information, see [REST API - Workflow Run Actions](https://docs.microsoft.com/rest/api/logic/workflowrunactions/get).</span><span class="sxs-lookup"><span data-stu-id="457d1-524">For more information, see [REST API - Workflow Run Actions](https://docs.microsoft.com/rest/api/logic/workflowrunactions/get).</span></span> | 
||||| 

| <span data-ttu-id="457d1-525">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-525">Return value</span></span> | <span data-ttu-id="457d1-526">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-526">Type</span></span> | <span data-ttu-id="457d1-527">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-527">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-528"><*action-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-528"><*action-output*></span></span> | <span data-ttu-id="457d1-529">String</span><span class="sxs-lookup"><span data-stu-id="457d1-529">String</span></span> | <span data-ttu-id="457d1-530">The output from the specified action or property</span><span class="sxs-lookup"><span data-stu-id="457d1-530">The output from the specified action or property</span></span> | 
|||| 

<span data-ttu-id="457d1-531">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-531">*Example*</span></span>

<span data-ttu-id="457d1-532">This example gets the `status` property value from the Twitter action `Get user` at runtime:</span><span class="sxs-lookup"><span data-stu-id="457d1-532">This example gets the `status` property value from the Twitter action `Get user` at runtime:</span></span> 

```
actions('Get_user').outputs.body.status 
```

<span data-ttu-id="457d1-533">And returns this result: `"Succeeded"`</span><span class="sxs-lookup"><span data-stu-id="457d1-533">And returns this result: `"Succeeded"`</span></span>

<a name="add"></a>

### <a name="add"></a><span data-ttu-id="457d1-534">add</span><span class="sxs-lookup"><span data-stu-id="457d1-534">add</span></span>

<span data-ttu-id="457d1-535">Return the result from adding two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-535">Return the result from adding two numbers.</span></span>

```
add(<summand_1>, <summand_2>)
```

| <span data-ttu-id="457d1-536">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-536">Parameter</span></span> | <span data-ttu-id="457d1-537">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-537">Required</span></span> | <span data-ttu-id="457d1-538">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-538">Type</span></span> | <span data-ttu-id="457d1-539">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-539">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-540"><*summand_1*>, <*summand_2*></span><span class="sxs-lookup"><span data-stu-id="457d1-540"><*summand_1*>, <*summand_2*></span></span> | <span data-ttu-id="457d1-541">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-541">Yes</span></span> | <span data-ttu-id="457d1-542">Integer, Float, or mixed</span><span class="sxs-lookup"><span data-stu-id="457d1-542">Integer, Float, or mixed</span></span> | <span data-ttu-id="457d1-543">The numbers to add</span><span class="sxs-lookup"><span data-stu-id="457d1-543">The numbers to add</span></span> | 
||||| 

| <span data-ttu-id="457d1-544">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-544">Return value</span></span> | <span data-ttu-id="457d1-545">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-545">Type</span></span> | <span data-ttu-id="457d1-546">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-546">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-547"><*result-sum*></span><span class="sxs-lookup"><span data-stu-id="457d1-547"><*result-sum*></span></span> | <span data-ttu-id="457d1-548">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-548">Integer or Float</span></span> | <span data-ttu-id="457d1-549">The result from adding the specified numbers</span><span class="sxs-lookup"><span data-stu-id="457d1-549">The result from adding the specified numbers</span></span> | 
|||| 

<span data-ttu-id="457d1-550">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-550">*Example*</span></span>

<span data-ttu-id="457d1-551">This example adds the specified numbers:</span><span class="sxs-lookup"><span data-stu-id="457d1-551">This example adds the specified numbers:</span></span>

```
add(1, 1.5)
```

<span data-ttu-id="457d1-552">And returns this result: `2.5`</span><span class="sxs-lookup"><span data-stu-id="457d1-552">And returns this result: `2.5`</span></span>

<a name="addDays"></a>

### <a name="adddays"></a><span data-ttu-id="457d1-553">addDays</span><span class="sxs-lookup"><span data-stu-id="457d1-553">addDays</span></span>

<span data-ttu-id="457d1-554">Add a number of days to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-554">Add a number of days to a timestamp.</span></span>

```
addDays('<timestamp>', <days>, '<format>'?)
```

| <span data-ttu-id="457d1-555">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-555">Parameter</span></span> | <span data-ttu-id="457d1-556">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-556">Required</span></span> | <span data-ttu-id="457d1-557">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-557">Type</span></span> | <span data-ttu-id="457d1-558">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-558">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-559"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-559"><*timestamp*></span></span> | <span data-ttu-id="457d1-560">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-560">Yes</span></span> | <span data-ttu-id="457d1-561">String</span><span class="sxs-lookup"><span data-stu-id="457d1-561">String</span></span> | <span data-ttu-id="457d1-562">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-562">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-563"><*days*></span><span class="sxs-lookup"><span data-stu-id="457d1-563"><*days*></span></span> | <span data-ttu-id="457d1-564">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-564">Yes</span></span> | <span data-ttu-id="457d1-565">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-565">Integer</span></span> | <span data-ttu-id="457d1-566">The positive or negative number of days to add</span><span class="sxs-lookup"><span data-stu-id="457d1-566">The positive or negative number of days to add</span></span> | 
| <span data-ttu-id="457d1-567"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-567"><*format*></span></span> | <span data-ttu-id="457d1-568">No</span><span class="sxs-lookup"><span data-stu-id="457d1-568">No</span></span> | <span data-ttu-id="457d1-569">String</span><span class="sxs-lookup"><span data-stu-id="457d1-569">String</span></span> | <span data-ttu-id="457d1-570">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-570">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-571">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-571">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-572">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-572">Return value</span></span> | <span data-ttu-id="457d1-573">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-573">Type</span></span> | <span data-ttu-id="457d1-574">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-574">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-575"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-575"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-576">String</span><span class="sxs-lookup"><span data-stu-id="457d1-576">String</span></span> | <span data-ttu-id="457d1-577">The timestamp plus the specified number of days</span><span class="sxs-lookup"><span data-stu-id="457d1-577">The timestamp plus the specified number of days</span></span>  | 
|||| 

<span data-ttu-id="457d1-578">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-578">*Example 1*</span></span>

<span data-ttu-id="457d1-579">This example adds 10 days to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-579">This example adds 10 days to the specified timestamp:</span></span>

```
addDays('2018-03-15T13:00:00Z', 10)
```

<span data-ttu-id="457d1-580">And returns this result: `"2018-03-25T00:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-580">And returns this result: `"2018-03-25T00:00:0000000Z"`</span></span>

<span data-ttu-id="457d1-581">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-581">*Example 2*</span></span>

<span data-ttu-id="457d1-582">This example subtracts five days from the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-582">This example subtracts five days from the specified timestamp:</span></span>

```
addDays('2018-03-15T00:00:00Z', -5)
```

<span data-ttu-id="457d1-583">And returns this result: `"2018-03-10T00:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-583">And returns this result: `"2018-03-10T00:00:0000000Z"`</span></span>

<a name="addHours"></a>

### <a name="addhours"></a><span data-ttu-id="457d1-584">addHours</span><span class="sxs-lookup"><span data-stu-id="457d1-584">addHours</span></span>

<span data-ttu-id="457d1-585">Add a number of hours to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-585">Add a number of hours to a timestamp.</span></span>

```
addHours('<timestamp>', <hours>, '<format>'?)
```

| <span data-ttu-id="457d1-586">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-586">Parameter</span></span> | <span data-ttu-id="457d1-587">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-587">Required</span></span> | <span data-ttu-id="457d1-588">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-588">Type</span></span> | <span data-ttu-id="457d1-589">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-589">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-590"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-590"><*timestamp*></span></span> | <span data-ttu-id="457d1-591">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-591">Yes</span></span> | <span data-ttu-id="457d1-592">String</span><span class="sxs-lookup"><span data-stu-id="457d1-592">String</span></span> | <span data-ttu-id="457d1-593">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-593">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-594"><*hours*></span><span class="sxs-lookup"><span data-stu-id="457d1-594"><*hours*></span></span> | <span data-ttu-id="457d1-595">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-595">Yes</span></span> | <span data-ttu-id="457d1-596">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-596">Integer</span></span> | <span data-ttu-id="457d1-597">The positive or negative number of hours to add</span><span class="sxs-lookup"><span data-stu-id="457d1-597">The positive or negative number of hours to add</span></span> | 
| <span data-ttu-id="457d1-598"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-598"><*format*></span></span> | <span data-ttu-id="457d1-599">No</span><span class="sxs-lookup"><span data-stu-id="457d1-599">No</span></span> | <span data-ttu-id="457d1-600">String</span><span class="sxs-lookup"><span data-stu-id="457d1-600">String</span></span> | <span data-ttu-id="457d1-601">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-601">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-602">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-602">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-603">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-603">Return value</span></span> | <span data-ttu-id="457d1-604">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-604">Type</span></span> | <span data-ttu-id="457d1-605">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-605">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-606"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-606"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-607">String</span><span class="sxs-lookup"><span data-stu-id="457d1-607">String</span></span> | <span data-ttu-id="457d1-608">The timestamp plus the specified number of hours</span><span class="sxs-lookup"><span data-stu-id="457d1-608">The timestamp plus the specified number of hours</span></span>  | 
|||| 

<span data-ttu-id="457d1-609">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-609">*Example 1*</span></span>

<span data-ttu-id="457d1-610">This example adds 10 hours to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-610">This example adds 10 hours to the specified timestamp:</span></span>

```
addHours('2018-03-15T00:00:00Z', 10)
```

<span data-ttu-id="457d1-611">And returns this result: `"2018-03-15T10:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-611">And returns this result: `"2018-03-15T10:00:0000000Z"`</span></span>

<span data-ttu-id="457d1-612">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-612">*Example 2*</span></span>

<span data-ttu-id="457d1-613">This example subtracts five hours from the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-613">This example subtracts five hours from the specified timestamp:</span></span>

```
addHours('2018-03-15T15:00:00Z', -5)
```

<span data-ttu-id="457d1-614">And returns this result: `"2018-03-15T10:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-614">And returns this result: `"2018-03-15T10:00:0000000Z"`</span></span>

<a name="addMinutes"></a>

### <a name="addminutes"></a><span data-ttu-id="457d1-615">addMinutes</span><span class="sxs-lookup"><span data-stu-id="457d1-615">addMinutes</span></span>

<span data-ttu-id="457d1-616">Add a number of minutes to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-616">Add a number of minutes to a timestamp.</span></span>

```
addMinutes('<timestamp>', <minutes>, '<format>'?)
```

| <span data-ttu-id="457d1-617">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-617">Parameter</span></span> | <span data-ttu-id="457d1-618">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-618">Required</span></span> | <span data-ttu-id="457d1-619">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-619">Type</span></span> | <span data-ttu-id="457d1-620">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-620">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-621"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-621"><*timestamp*></span></span> | <span data-ttu-id="457d1-622">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-622">Yes</span></span> | <span data-ttu-id="457d1-623">String</span><span class="sxs-lookup"><span data-stu-id="457d1-623">String</span></span> | <span data-ttu-id="457d1-624">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-624">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-625"><*minutes*></span><span class="sxs-lookup"><span data-stu-id="457d1-625"><*minutes*></span></span> | <span data-ttu-id="457d1-626">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-626">Yes</span></span> | <span data-ttu-id="457d1-627">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-627">Integer</span></span> | <span data-ttu-id="457d1-628">The positive or negative number of minutes to add</span><span class="sxs-lookup"><span data-stu-id="457d1-628">The positive or negative number of minutes to add</span></span> | 
| <span data-ttu-id="457d1-629"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-629"><*format*></span></span> | <span data-ttu-id="457d1-630">No</span><span class="sxs-lookup"><span data-stu-id="457d1-630">No</span></span> | <span data-ttu-id="457d1-631">String</span><span class="sxs-lookup"><span data-stu-id="457d1-631">String</span></span> | <span data-ttu-id="457d1-632">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-632">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-633">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-633">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-634">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-634">Return value</span></span> | <span data-ttu-id="457d1-635">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-635">Type</span></span> | <span data-ttu-id="457d1-636">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-636">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-637"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-637"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-638">String</span><span class="sxs-lookup"><span data-stu-id="457d1-638">String</span></span> | <span data-ttu-id="457d1-639">The timestamp plus the specified number of minutes</span><span class="sxs-lookup"><span data-stu-id="457d1-639">The timestamp plus the specified number of minutes</span></span> | 
|||| 

<span data-ttu-id="457d1-640">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-640">*Example 1*</span></span>

<span data-ttu-id="457d1-641">This example adds 10 minutes to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-641">This example adds 10 minutes to the specified timestamp:</span></span>

```
addMinutes('2018-03-15T00:10:00Z', 10)
```

<span data-ttu-id="457d1-642">And returns this result: `"2018-03-15T00:20:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-642">And returns this result: `"2018-03-15T00:20:00.0000000Z"`</span></span>

<span data-ttu-id="457d1-643">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-643">*Example 2*</span></span>

<span data-ttu-id="457d1-644">This example subtracts five minutes from the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-644">This example subtracts five minutes from the specified timestamp:</span></span>

```
addMinutes('2018-03-15T00:20:00Z', -5)
```

<span data-ttu-id="457d1-645">And returns this result: `"2018-03-15T00:15:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-645">And returns this result: `"2018-03-15T00:15:00.0000000Z"`</span></span>

<a name="addProperty"></a>

### <a name="addproperty"></a><span data-ttu-id="457d1-646">addProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-646">addProperty</span></span>

<span data-ttu-id="457d1-647">Add a property and its value, or name-value pair, to a JSON object, and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-647">Add a property and its value, or name-value pair, to a JSON object, and return the updated object.</span></span> <span data-ttu-id="457d1-648">If the object already exists at runtime, the function throws an error.</span><span class="sxs-lookup"><span data-stu-id="457d1-648">If the object already exists at runtime, the function throws an error.</span></span>

```
addProperty(<object>, '<property>', <value>)
```

| <span data-ttu-id="457d1-649">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-649">Parameter</span></span> | <span data-ttu-id="457d1-650">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-650">Required</span></span> | <span data-ttu-id="457d1-651">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-651">Type</span></span> | <span data-ttu-id="457d1-652">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-652">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-653"><*object*></span><span class="sxs-lookup"><span data-stu-id="457d1-653"><*object*></span></span> | <span data-ttu-id="457d1-654">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-654">Yes</span></span> | <span data-ttu-id="457d1-655">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-655">Object</span></span> | <span data-ttu-id="457d1-656">The JSON object where you want to add a property</span><span class="sxs-lookup"><span data-stu-id="457d1-656">The JSON object where you want to add a property</span></span> | 
| <span data-ttu-id="457d1-657"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-657"><*property*></span></span> | <span data-ttu-id="457d1-658">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-658">Yes</span></span> | <span data-ttu-id="457d1-659">String</span><span class="sxs-lookup"><span data-stu-id="457d1-659">String</span></span> | <span data-ttu-id="457d1-660">The name for the property to add</span><span class="sxs-lookup"><span data-stu-id="457d1-660">The name for the property to add</span></span> | 
| <span data-ttu-id="457d1-661"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-661"><*value*></span></span> | <span data-ttu-id="457d1-662">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-662">Yes</span></span> | <span data-ttu-id="457d1-663">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-663">Any</span></span> | <span data-ttu-id="457d1-664">The value for the property</span><span class="sxs-lookup"><span data-stu-id="457d1-664">The value for the property</span></span> |
||||| 

| <span data-ttu-id="457d1-665">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-665">Return value</span></span> | <span data-ttu-id="457d1-666">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-666">Type</span></span> | <span data-ttu-id="457d1-667">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-667">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-668"><*updated-object*></span><span class="sxs-lookup"><span data-stu-id="457d1-668"><*updated-object*></span></span> | <span data-ttu-id="457d1-669">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-669">Object</span></span> | <span data-ttu-id="457d1-670">The updated JSON object with the specified property</span><span class="sxs-lookup"><span data-stu-id="457d1-670">The updated JSON object with the specified property</span></span> | 
|||| 

<span data-ttu-id="457d1-671">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-671">*Example*</span></span>

<span data-ttu-id="457d1-672">This example adds the `accountNumber` property to the `customerProfile` object, which is converted to JSON with the [JSON()](#json) function.</span><span class="sxs-lookup"><span data-stu-id="457d1-672">This example adds the `accountNumber` property to the `customerProfile` object, which is converted to JSON with the [JSON()](#json) function.</span></span> <span data-ttu-id="457d1-673">The function assigns a value that is generated by the [guid()](#guid) function, and returns the updated object:</span><span class="sxs-lookup"><span data-stu-id="457d1-673">The function assigns a value that is generated by the [guid()](#guid) function, and returns the updated object:</span></span>

```
addProperty(json('customerProfile'), 'accountNumber', guid())
```

<a name="addSeconds"></a>

### <a name="addseconds"></a><span data-ttu-id="457d1-674">addSeconds</span><span class="sxs-lookup"><span data-stu-id="457d1-674">addSeconds</span></span>

<span data-ttu-id="457d1-675">Add a number of seconds to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-675">Add a number of seconds to a timestamp.</span></span>

```
addSeconds('<timestamp>', <seconds>, '<format>'?)
```

| <span data-ttu-id="457d1-676">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-676">Parameter</span></span> | <span data-ttu-id="457d1-677">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-677">Required</span></span> | <span data-ttu-id="457d1-678">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-678">Type</span></span> | <span data-ttu-id="457d1-679">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-679">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-680"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-680"><*timestamp*></span></span> | <span data-ttu-id="457d1-681">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-681">Yes</span></span> | <span data-ttu-id="457d1-682">String</span><span class="sxs-lookup"><span data-stu-id="457d1-682">String</span></span> | <span data-ttu-id="457d1-683">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-683">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-684"><*seconds*></span><span class="sxs-lookup"><span data-stu-id="457d1-684"><*seconds*></span></span> | <span data-ttu-id="457d1-685">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-685">Yes</span></span> | <span data-ttu-id="457d1-686">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-686">Integer</span></span> | <span data-ttu-id="457d1-687">The positive or negative number of seconds to add</span><span class="sxs-lookup"><span data-stu-id="457d1-687">The positive or negative number of seconds to add</span></span> | 
| <span data-ttu-id="457d1-688"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-688"><*format*></span></span> | <span data-ttu-id="457d1-689">No</span><span class="sxs-lookup"><span data-stu-id="457d1-689">No</span></span> | <span data-ttu-id="457d1-690">String</span><span class="sxs-lookup"><span data-stu-id="457d1-690">String</span></span> | <span data-ttu-id="457d1-691">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-691">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-692">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-692">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-693">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-693">Return value</span></span> | <span data-ttu-id="457d1-694">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-694">Type</span></span> | <span data-ttu-id="457d1-695">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-695">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-696"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-696"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-697">String</span><span class="sxs-lookup"><span data-stu-id="457d1-697">String</span></span> | <span data-ttu-id="457d1-698">The timestamp plus the specified number of seconds</span><span class="sxs-lookup"><span data-stu-id="457d1-698">The timestamp plus the specified number of seconds</span></span>  | 
|||| 

<span data-ttu-id="457d1-699">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-699">*Example 1*</span></span>

<span data-ttu-id="457d1-700">This example adds 10 seconds to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-700">This example adds 10 seconds to the specified timestamp:</span></span>

```
addSeconds('2018-03-15T00:00:00Z', 10)
```

<span data-ttu-id="457d1-701">And returns this result: `"2018-03-15T00:00:10.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-701">And returns this result: `"2018-03-15T00:00:10.0000000Z"`</span></span>

<span data-ttu-id="457d1-702">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-702">*Example 2*</span></span>

<span data-ttu-id="457d1-703">This example subtracts five seconds to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-703">This example subtracts five seconds to the specified timestamp:</span></span>

```
addSeconds('2018-03-15T00:00:30Z', -5)
```

<span data-ttu-id="457d1-704">And returns this result: `"2018-03-15T00:00:25.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-704">And returns this result: `"2018-03-15T00:00:25.0000000Z"`</span></span>

<a name="addToTime"></a>

### <a name="addtotime"></a><span data-ttu-id="457d1-705">addToTime</span><span class="sxs-lookup"><span data-stu-id="457d1-705">addToTime</span></span>

<span data-ttu-id="457d1-706">Add a number of time units to a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-706">Add a number of time units to a timestamp.</span></span> <span data-ttu-id="457d1-707">See also [getFutureTime()](#getFutureTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-707">See also [getFutureTime()](#getFutureTime).</span></span>

```
addToTime('<timestamp>', <interval>, '<timeUnit>', '<format>'?)
```

| <span data-ttu-id="457d1-708">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-708">Parameter</span></span> | <span data-ttu-id="457d1-709">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-709">Required</span></span> | <span data-ttu-id="457d1-710">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-710">Type</span></span> | <span data-ttu-id="457d1-711">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-711">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-712"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-712"><*timestamp*></span></span> | <span data-ttu-id="457d1-713">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-713">Yes</span></span> | <span data-ttu-id="457d1-714">String</span><span class="sxs-lookup"><span data-stu-id="457d1-714">String</span></span> | <span data-ttu-id="457d1-715">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-715">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-716"><*interval*></span><span class="sxs-lookup"><span data-stu-id="457d1-716"><*interval*></span></span> | <span data-ttu-id="457d1-717">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-717">Yes</span></span> | <span data-ttu-id="457d1-718">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-718">Integer</span></span> | <span data-ttu-id="457d1-719">The number of specified time units to add</span><span class="sxs-lookup"><span data-stu-id="457d1-719">The number of specified time units to add</span></span> | 
| <span data-ttu-id="457d1-720"><*timeUnit*></span><span class="sxs-lookup"><span data-stu-id="457d1-720"><*timeUnit*></span></span> | <span data-ttu-id="457d1-721">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-721">Yes</span></span> | <span data-ttu-id="457d1-722">String</span><span class="sxs-lookup"><span data-stu-id="457d1-722">String</span></span> | <span data-ttu-id="457d1-723">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span><span class="sxs-lookup"><span data-stu-id="457d1-723">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span></span> | 
| <span data-ttu-id="457d1-724"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-724"><*format*></span></span> | <span data-ttu-id="457d1-725">No</span><span class="sxs-lookup"><span data-stu-id="457d1-725">No</span></span> | <span data-ttu-id="457d1-726">String</span><span class="sxs-lookup"><span data-stu-id="457d1-726">String</span></span> | <span data-ttu-id="457d1-727">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-727">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-728">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-728">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-729">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-729">Return value</span></span> | <span data-ttu-id="457d1-730">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-730">Type</span></span> | <span data-ttu-id="457d1-731">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-731">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-732"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-732"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-733">String</span><span class="sxs-lookup"><span data-stu-id="457d1-733">String</span></span> | <span data-ttu-id="457d1-734">The timestamp plus the specified number of time units</span><span class="sxs-lookup"><span data-stu-id="457d1-734">The timestamp plus the specified number of time units</span></span>  | 
|||| 

<span data-ttu-id="457d1-735">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-735">*Example 1*</span></span>

<span data-ttu-id="457d1-736">This example adds one day to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-736">This example adds one day to the specified timestamp:</span></span>

```
addToTime('2018-01-01T00:00:00Z', 1, 'Day') 
```

<span data-ttu-id="457d1-737">And returns this result: `"2018-01-02T00:00:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-737">And returns this result: `"2018-01-02T00:00:00:0000000Z"`</span></span>

<span data-ttu-id="457d1-738">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-738">*Example 2*</span></span>

<span data-ttu-id="457d1-739">This example adds one day to the specified timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-739">This example adds one day to the specified timestamp:</span></span>

```
addToTime('2018-01-01T00:00:00Z', 1, 'Day', 'D')
```

<span data-ttu-id="457d1-740">And returns the result using the optional "D" format: `"Tuesday, January 2, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-740">And returns the result using the optional "D" format: `"Tuesday, January 2, 2018"`</span></span>

<a name="and"></a>

### <a name="and"></a><span data-ttu-id="457d1-741">and</span><span class="sxs-lookup"><span data-stu-id="457d1-741">and</span></span>

<span data-ttu-id="457d1-742">Check whether all expressions are true.</span><span class="sxs-lookup"><span data-stu-id="457d1-742">Check whether all expressions are true.</span></span> <span data-ttu-id="457d1-743">Return true when all expressions are true, or return false when at least one expression is false.</span><span class="sxs-lookup"><span data-stu-id="457d1-743">Return true when all expressions are true, or return false when at least one expression is false.</span></span>

```
and(<expression1>, <expression2>, ...)
```

| <span data-ttu-id="457d1-744">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-744">Parameter</span></span> | <span data-ttu-id="457d1-745">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-745">Required</span></span> | <span data-ttu-id="457d1-746">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-746">Type</span></span> | <span data-ttu-id="457d1-747">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-747">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-748"><*expression1*>, <*expression2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-748"><*expression1*>, <*expression2*>, ...</span></span> | <span data-ttu-id="457d1-749">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-749">Yes</span></span> | <span data-ttu-id="457d1-750">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-750">Boolean</span></span> | <span data-ttu-id="457d1-751">The expressions to check</span><span class="sxs-lookup"><span data-stu-id="457d1-751">The expressions to check</span></span> | 
||||| 

| <span data-ttu-id="457d1-752">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-752">Return value</span></span> | <span data-ttu-id="457d1-753">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-753">Type</span></span> | <span data-ttu-id="457d1-754">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-754">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-755">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-755">true or false</span></span> | <span data-ttu-id="457d1-756">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-756">Boolean</span></span> | <span data-ttu-id="457d1-757">Return true when all expressions are true.</span><span class="sxs-lookup"><span data-stu-id="457d1-757">Return true when all expressions are true.</span></span> <span data-ttu-id="457d1-758">Return false when at least one expression is false.</span><span class="sxs-lookup"><span data-stu-id="457d1-758">Return false when at least one expression is false.</span></span> | 
|||| 

<span data-ttu-id="457d1-759">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-759">*Example 1*</span></span>

<span data-ttu-id="457d1-760">These examples check whether the specified Boolean values are all true:</span><span class="sxs-lookup"><span data-stu-id="457d1-760">These examples check whether the specified Boolean values are all true:</span></span>

```
and(true, true)
and(false, true)
and(false, false)
```

<span data-ttu-id="457d1-761">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-761">And returns these results:</span></span>

* <span data-ttu-id="457d1-762">First example: Both expressions are true, so returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-762">First example: Both expressions are true, so returns `true`.</span></span> 
* <span data-ttu-id="457d1-763">Second example: One expression is false, so returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-763">Second example: One expression is false, so returns `false`.</span></span>
* <span data-ttu-id="457d1-764">Third example: Both expressions are false, so returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-764">Third example: Both expressions are false, so returns `false`.</span></span>

<span data-ttu-id="457d1-765">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-765">*Example 2*</span></span>

<span data-ttu-id="457d1-766">These examples check whether the specified expressions are all true:</span><span class="sxs-lookup"><span data-stu-id="457d1-766">These examples check whether the specified expressions are all true:</span></span>

```
and(equals(1, 1), equals(2, 2))
and(equals(1, 1), equals(1, 2))
and(equals(1, 2), equals(1, 3))
```

<span data-ttu-id="457d1-767">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-767">And returns these results:</span></span>

* <span data-ttu-id="457d1-768">First example: Both expressions are true, so returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-768">First example: Both expressions are true, so returns `true`.</span></span> 
* <span data-ttu-id="457d1-769">Second example: One expression is false, so returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-769">Second example: One expression is false, so returns `false`.</span></span>
* <span data-ttu-id="457d1-770">Third example: Both expressions are false, so returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-770">Third example: Both expressions are false, so returns `false`.</span></span>

<a name="array"></a>

### <a name="array"></a><span data-ttu-id="457d1-771">array</span><span class="sxs-lookup"><span data-stu-id="457d1-771">array</span></span>

<span data-ttu-id="457d1-772">Return an array from a single specified input.</span><span class="sxs-lookup"><span data-stu-id="457d1-772">Return an array from a single specified input.</span></span> <span data-ttu-id="457d1-773">For multiple inputs, see [createArray()](#createArray).</span><span class="sxs-lookup"><span data-stu-id="457d1-773">For multiple inputs, see [createArray()](#createArray).</span></span> 

```
array('<value>')
```

| <span data-ttu-id="457d1-774">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-774">Parameter</span></span> | <span data-ttu-id="457d1-775">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-775">Required</span></span> | <span data-ttu-id="457d1-776">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-776">Type</span></span> | <span data-ttu-id="457d1-777">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-777">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-778"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-778"><*value*></span></span> | <span data-ttu-id="457d1-779">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-779">Yes</span></span> | <span data-ttu-id="457d1-780">String</span><span class="sxs-lookup"><span data-stu-id="457d1-780">String</span></span> | <span data-ttu-id="457d1-781">The string for creating an array</span><span class="sxs-lookup"><span data-stu-id="457d1-781">The string for creating an array</span></span> | 
||||| 

| <span data-ttu-id="457d1-782">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-782">Return value</span></span> | <span data-ttu-id="457d1-783">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-783">Type</span></span> | <span data-ttu-id="457d1-784">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-784">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-785">[<*value*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-785">[<*value*>]</span></span> | <span data-ttu-id="457d1-786">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-786">Array</span></span> | <span data-ttu-id="457d1-787">An array that contains the single specified input</span><span class="sxs-lookup"><span data-stu-id="457d1-787">An array that contains the single specified input</span></span> | 
|||| 

<span data-ttu-id="457d1-788">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-788">*Example*</span></span>

<span data-ttu-id="457d1-789">This example creates an array from the "hello" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-789">This example creates an array from the "hello" string:</span></span>

```
array('hello')
```

<span data-ttu-id="457d1-790">And returns this result: `["hello"]`</span><span class="sxs-lookup"><span data-stu-id="457d1-790">And returns this result: `["hello"]`</span></span>

<a name="base64"></a>

### <a name="base64"></a><span data-ttu-id="457d1-791">base64</span><span class="sxs-lookup"><span data-stu-id="457d1-791">base64</span></span>

<span data-ttu-id="457d1-792">Return the base64-encoded version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-792">Return the base64-encoded version for a string.</span></span>

```
base64('<value>')
```

| <span data-ttu-id="457d1-793">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-793">Parameter</span></span> | <span data-ttu-id="457d1-794">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-794">Required</span></span> | <span data-ttu-id="457d1-795">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-795">Type</span></span> | <span data-ttu-id="457d1-796">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-796">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-797"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-797"><*value*></span></span> | <span data-ttu-id="457d1-798">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-798">Yes</span></span> | <span data-ttu-id="457d1-799">String</span><span class="sxs-lookup"><span data-stu-id="457d1-799">String</span></span> | <span data-ttu-id="457d1-800">The input string</span><span class="sxs-lookup"><span data-stu-id="457d1-800">The input string</span></span> | 
||||| 

| <span data-ttu-id="457d1-801">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-801">Return value</span></span> | <span data-ttu-id="457d1-802">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-802">Type</span></span> | <span data-ttu-id="457d1-803">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-803">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-804"><*base64-string*></span><span class="sxs-lookup"><span data-stu-id="457d1-804"><*base64-string*></span></span> | <span data-ttu-id="457d1-805">String</span><span class="sxs-lookup"><span data-stu-id="457d1-805">String</span></span> | <span data-ttu-id="457d1-806">The base64-encoded version for the input string</span><span class="sxs-lookup"><span data-stu-id="457d1-806">The base64-encoded version for the input string</span></span> | 
|||| 

<span data-ttu-id="457d1-807">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-807">*Example*</span></span>

<span data-ttu-id="457d1-808">This example converts the "hello" string to a base64-encoded string:</span><span class="sxs-lookup"><span data-stu-id="457d1-808">This example converts the "hello" string to a base64-encoded string:</span></span>

```
base64('hello')
```

<span data-ttu-id="457d1-809">And returns this result: `"aGVsbG8="`</span><span class="sxs-lookup"><span data-stu-id="457d1-809">And returns this result: `"aGVsbG8="`</span></span>

<a name="base64ToBinary"></a>

### <a name="base64tobinary"></a><span data-ttu-id="457d1-810">base64ToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-810">base64ToBinary</span></span>

<span data-ttu-id="457d1-811">Return the binary version for a base64-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-811">Return the binary version for a base64-encoded string.</span></span>

```
base64ToBinary('<value>')
```

| <span data-ttu-id="457d1-812">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-812">Parameter</span></span> | <span data-ttu-id="457d1-813">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-813">Required</span></span> | <span data-ttu-id="457d1-814">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-814">Type</span></span> | <span data-ttu-id="457d1-815">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-815">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-816"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-816"><*value*></span></span> | <span data-ttu-id="457d1-817">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-817">Yes</span></span> | <span data-ttu-id="457d1-818">String</span><span class="sxs-lookup"><span data-stu-id="457d1-818">String</span></span> | <span data-ttu-id="457d1-819">The base64-encoded string to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-819">The base64-encoded string to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-820">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-820">Return value</span></span> | <span data-ttu-id="457d1-821">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-821">Type</span></span> | <span data-ttu-id="457d1-822">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-822">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-823"><*binary-for-base64-string*></span><span class="sxs-lookup"><span data-stu-id="457d1-823"><*binary-for-base64-string*></span></span> | <span data-ttu-id="457d1-824">String</span><span class="sxs-lookup"><span data-stu-id="457d1-824">String</span></span> | <span data-ttu-id="457d1-825">The binary version for the base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="457d1-825">The binary version for the base64-encoded string</span></span> | 
|||| 

<span data-ttu-id="457d1-826">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-826">*Example*</span></span>

<span data-ttu-id="457d1-827">This example converts the "aGVsbG8=" base64-encoded string to a binary string:</span><span class="sxs-lookup"><span data-stu-id="457d1-827">This example converts the "aGVsbG8=" base64-encoded string to a binary string:</span></span>

```
base64ToBinary('aGVsbG8=')
```

<span data-ttu-id="457d1-828">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-828">And returns this result:</span></span> 

`"0110000101000111010101100111001101100010010001110011100000111101"`

<a name="base64ToString"></a>

### <a name="base64tostring"></a><span data-ttu-id="457d1-829">base64ToString</span><span class="sxs-lookup"><span data-stu-id="457d1-829">base64ToString</span></span>

<span data-ttu-id="457d1-830">Return the string version for a base64-encoded string, effectively decoding the base64 string.</span><span class="sxs-lookup"><span data-stu-id="457d1-830">Return the string version for a base64-encoded string, effectively decoding the base64 string.</span></span> <span data-ttu-id="457d1-831">Use this function rather than [decodeBase64()](#decodeBase64).</span><span class="sxs-lookup"><span data-stu-id="457d1-831">Use this function rather than [decodeBase64()](#decodeBase64).</span></span> <span data-ttu-id="457d1-832">Although both functions work the same way, `base64ToString()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-832">Although both functions work the same way, `base64ToString()` is preferred.</span></span>

```
base64ToString('<value>')
```

| <span data-ttu-id="457d1-833">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-833">Parameter</span></span> | <span data-ttu-id="457d1-834">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-834">Required</span></span> | <span data-ttu-id="457d1-835">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-835">Type</span></span> | <span data-ttu-id="457d1-836">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-836">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-837"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-837"><*value*></span></span> | <span data-ttu-id="457d1-838">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-838">Yes</span></span> | <span data-ttu-id="457d1-839">String</span><span class="sxs-lookup"><span data-stu-id="457d1-839">String</span></span> | <span data-ttu-id="457d1-840">The base64-encoded string to decode</span><span class="sxs-lookup"><span data-stu-id="457d1-840">The base64-encoded string to decode</span></span> | 
||||| 

| <span data-ttu-id="457d1-841">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-841">Return value</span></span> | <span data-ttu-id="457d1-842">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-842">Type</span></span> | <span data-ttu-id="457d1-843">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-843">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-844"><*decoded-base64-string*></span><span class="sxs-lookup"><span data-stu-id="457d1-844"><*decoded-base64-string*></span></span> | <span data-ttu-id="457d1-845">String</span><span class="sxs-lookup"><span data-stu-id="457d1-845">String</span></span> | <span data-ttu-id="457d1-846">The string version for a base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="457d1-846">The string version for a base64-encoded string</span></span> | 
|||| 

<span data-ttu-id="457d1-847">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-847">*Example*</span></span>

<span data-ttu-id="457d1-848">This example converts the "aGVsbG8=" base64-encoded string to just a string:</span><span class="sxs-lookup"><span data-stu-id="457d1-848">This example converts the "aGVsbG8=" base64-encoded string to just a string:</span></span>

```
base64ToString('aGVsbG8=')
```

<span data-ttu-id="457d1-849">And returns this result: `"hello"`</span><span class="sxs-lookup"><span data-stu-id="457d1-849">And returns this result: `"hello"`</span></span>

<a name="binary"></a>

### <a name="binary"></a><span data-ttu-id="457d1-850">binary</span><span class="sxs-lookup"><span data-stu-id="457d1-850">binary</span></span> 

<span data-ttu-id="457d1-851">Return the binary version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-851">Return the binary version for a string.</span></span>

```
binary('<value>')
```

| <span data-ttu-id="457d1-852">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-852">Parameter</span></span> | <span data-ttu-id="457d1-853">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-853">Required</span></span> | <span data-ttu-id="457d1-854">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-854">Type</span></span> | <span data-ttu-id="457d1-855">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-855">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-856"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-856"><*value*></span></span> | <span data-ttu-id="457d1-857">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-857">Yes</span></span> | <span data-ttu-id="457d1-858">String</span><span class="sxs-lookup"><span data-stu-id="457d1-858">String</span></span> | <span data-ttu-id="457d1-859">The string to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-859">The string to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-860">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-860">Return value</span></span> | <span data-ttu-id="457d1-861">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-861">Type</span></span> | <span data-ttu-id="457d1-862">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-862">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-863"><*binary-for-input-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-863"><*binary-for-input-value*></span></span> | <span data-ttu-id="457d1-864">String</span><span class="sxs-lookup"><span data-stu-id="457d1-864">String</span></span> | <span data-ttu-id="457d1-865">The binary version for the specified string</span><span class="sxs-lookup"><span data-stu-id="457d1-865">The binary version for the specified string</span></span> | 
|||| 

<span data-ttu-id="457d1-866">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-866">*Example*</span></span>

<span data-ttu-id="457d1-867">This example converts the "hello" string to a binary string:</span><span class="sxs-lookup"><span data-stu-id="457d1-867">This example converts the "hello" string to a binary string:</span></span>

```
binary('hello')
```

<span data-ttu-id="457d1-868">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-868">And returns this result:</span></span> 

`"0110100001100101011011000110110001101111"`

<a name="body"></a>

### <a name="body"></a><span data-ttu-id="457d1-869">body</span><span class="sxs-lookup"><span data-stu-id="457d1-869">body</span></span>

<span data-ttu-id="457d1-870">Return an action's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-870">Return an action's `body` output at runtime.</span></span> <span data-ttu-id="457d1-871">Shorthand for `actions('<actionName>').outputs.body`.</span><span class="sxs-lookup"><span data-stu-id="457d1-871">Shorthand for `actions('<actionName>').outputs.body`.</span></span> <span data-ttu-id="457d1-872">See [actionBody()](#actionBody) and [actions()](#actions).</span><span class="sxs-lookup"><span data-stu-id="457d1-872">See [actionBody()](#actionBody) and [actions()](#actions).</span></span>

```
body('<actionName>')
```

| <span data-ttu-id="457d1-873">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-873">Parameter</span></span> | <span data-ttu-id="457d1-874">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-874">Required</span></span> | <span data-ttu-id="457d1-875">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-875">Type</span></span> | <span data-ttu-id="457d1-876">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-876">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-877"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-877"><*actionName*></span></span> | <span data-ttu-id="457d1-878">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-878">Yes</span></span> | <span data-ttu-id="457d1-879">String</span><span class="sxs-lookup"><span data-stu-id="457d1-879">String</span></span> | <span data-ttu-id="457d1-880">The name for the action's `body` output that you want</span><span class="sxs-lookup"><span data-stu-id="457d1-880">The name for the action's `body` output that you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-881">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-881">Return value</span></span> | <span data-ttu-id="457d1-882">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-882">Type</span></span> | <span data-ttu-id="457d1-883">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-883">Description</span></span> | 
| ------------ | -----| ----------- | 
| <span data-ttu-id="457d1-884"><*action-body-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-884"><*action-body-output*></span></span> | <span data-ttu-id="457d1-885">String</span><span class="sxs-lookup"><span data-stu-id="457d1-885">String</span></span> | <span data-ttu-id="457d1-886">The `body` output from the specified action</span><span class="sxs-lookup"><span data-stu-id="457d1-886">The `body` output from the specified action</span></span> | 
|||| 

<span data-ttu-id="457d1-887">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-887">*Example*</span></span>

<span data-ttu-id="457d1-888">This example gets the `body` output from the `Get user` Twitter action:</span><span class="sxs-lookup"><span data-stu-id="457d1-888">This example gets the `body` output from the `Get user` Twitter action:</span></span> 

```
body('Get_user')
```

<span data-ttu-id="457d1-889">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-889">And returns this result:</span></span> 

```json
"body": {
    "FullName": "Contoso Corporation",
    "Location": "Generic Town, USA",
    "Id": 283541717,
    "UserName": "ContosoInc",
    "FollowersCount": 172,
    "Description": "Leading the way in transforming the digital workplace.",
    "StatusesCount": 93,
    "FriendsCount": 126,
    "FavouritesCount": 46,
    "ProfileImageUrl": "https://pbs.twimg.com/profile_images/908820389907722240/gG9zaHcd_400x400.jpg"
}
```

<a name="bool"></a>

### <a name="bool"></a><span data-ttu-id="457d1-890">bool</span><span class="sxs-lookup"><span data-stu-id="457d1-890">bool</span></span>

<span data-ttu-id="457d1-891">Return the Boolean version for a value.</span><span class="sxs-lookup"><span data-stu-id="457d1-891">Return the Boolean version for a value.</span></span>

```
bool(<value>)
```

| <span data-ttu-id="457d1-892">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-892">Parameter</span></span> | <span data-ttu-id="457d1-893">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-893">Required</span></span> | <span data-ttu-id="457d1-894">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-894">Type</span></span> | <span data-ttu-id="457d1-895">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-895">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-896"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-896"><*value*></span></span> | <span data-ttu-id="457d1-897">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-897">Yes</span></span> | <span data-ttu-id="457d1-898">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-898">Any</span></span> | <span data-ttu-id="457d1-899">The value to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-899">The value to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-900">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-900">Return value</span></span> | <span data-ttu-id="457d1-901">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-901">Type</span></span> | <span data-ttu-id="457d1-902">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-902">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-903">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-903">true or false</span></span> | <span data-ttu-id="457d1-904">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-904">Boolean</span></span> | <span data-ttu-id="457d1-905">The Boolean version for the specified value</span><span class="sxs-lookup"><span data-stu-id="457d1-905">The Boolean version for the specified value</span></span> | 
|||| 

<span data-ttu-id="457d1-906">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-906">*Example*</span></span>

<span data-ttu-id="457d1-907">These examples convert the specified values to Boolean values:</span><span class="sxs-lookup"><span data-stu-id="457d1-907">These examples convert the specified values to Boolean values:</span></span> 

```
bool(1)
bool(0)
```

<span data-ttu-id="457d1-908">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-908">And returns these results:</span></span> 

* <span data-ttu-id="457d1-909">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-909">First example: `true`</span></span> 
* <span data-ttu-id="457d1-910">Second example: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-910">Second example: `false`</span></span>

<a name="coalesce"></a>

### <a name="coalesce"></a><span data-ttu-id="457d1-911">coalesce</span><span class="sxs-lookup"><span data-stu-id="457d1-911">coalesce</span></span>

<span data-ttu-id="457d1-912">Return the first non-null value from one or more parameters.</span><span class="sxs-lookup"><span data-stu-id="457d1-912">Return the first non-null value from one or more parameters.</span></span> <span data-ttu-id="457d1-913">Empty strings, empty arrays, and empty objects are not null.</span><span class="sxs-lookup"><span data-stu-id="457d1-913">Empty strings, empty arrays, and empty objects are not null.</span></span>

```
coalesce(<object_1>, <object_2>, ...)
```

| <span data-ttu-id="457d1-914">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-914">Parameter</span></span> | <span data-ttu-id="457d1-915">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-915">Required</span></span> | <span data-ttu-id="457d1-916">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-916">Type</span></span> | <span data-ttu-id="457d1-917">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-917">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-918"><*object_1*>, <*object_2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-918"><*object_1*>, <*object_2*>, ...</span></span> | <span data-ttu-id="457d1-919">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-919">Yes</span></span> | <span data-ttu-id="457d1-920">Any, can mix types</span><span class="sxs-lookup"><span data-stu-id="457d1-920">Any, can mix types</span></span> | <span data-ttu-id="457d1-921">One or more items to check for null</span><span class="sxs-lookup"><span data-stu-id="457d1-921">One or more items to check for null</span></span> | 
||||| 

| <span data-ttu-id="457d1-922">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-922">Return value</span></span> | <span data-ttu-id="457d1-923">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-923">Type</span></span> | <span data-ttu-id="457d1-924">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-924">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-925"><*first-non-null-item*></span><span class="sxs-lookup"><span data-stu-id="457d1-925"><*first-non-null-item*></span></span> | <span data-ttu-id="457d1-926">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-926">Any</span></span> | <span data-ttu-id="457d1-927">The first item or value that is not null.</span><span class="sxs-lookup"><span data-stu-id="457d1-927">The first item or value that is not null.</span></span> <span data-ttu-id="457d1-928">If all parameters are null, this function returns null.</span><span class="sxs-lookup"><span data-stu-id="457d1-928">If all parameters are null, this function returns null.</span></span> | 
|||| 

<span data-ttu-id="457d1-929">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-929">*Example*</span></span>

<span data-ttu-id="457d1-930">These examples return the first non-null value from the specified values, or null when all the values are null:</span><span class="sxs-lookup"><span data-stu-id="457d1-930">These examples return the first non-null value from the specified values, or null when all the values are null:</span></span>

```
coalesce(null, true, false)
coalesce(null, 'hello', 'world')
coalesce(null, null, null)
```

<span data-ttu-id="457d1-931">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-931">And returns these results:</span></span> 

* <span data-ttu-id="457d1-932">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-932">First example: `true`</span></span> 
* <span data-ttu-id="457d1-933">Second example: `"hello"`</span><span class="sxs-lookup"><span data-stu-id="457d1-933">Second example: `"hello"`</span></span>
* <span data-ttu-id="457d1-934">Third example: `null`</span><span class="sxs-lookup"><span data-stu-id="457d1-934">Third example: `null`</span></span>

<a name="concat"></a>

### <a name="concat"></a><span data-ttu-id="457d1-935">concat</span><span class="sxs-lookup"><span data-stu-id="457d1-935">concat</span></span>

<span data-ttu-id="457d1-936">Combine two or more strings, and return the combined string.</span><span class="sxs-lookup"><span data-stu-id="457d1-936">Combine two or more strings, and return the combined string.</span></span> 

```
concat('<text1>', '<text2>', ...)
```

| <span data-ttu-id="457d1-937">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-937">Parameter</span></span> | <span data-ttu-id="457d1-938">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-938">Required</span></span> | <span data-ttu-id="457d1-939">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-939">Type</span></span> | <span data-ttu-id="457d1-940">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-940">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-941"><*text1*>, <*text2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-941"><*text1*>, <*text2*>, ...</span></span> | <span data-ttu-id="457d1-942">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-942">Yes</span></span> | <span data-ttu-id="457d1-943">String</span><span class="sxs-lookup"><span data-stu-id="457d1-943">String</span></span> | <span data-ttu-id="457d1-944">At least two strings to combine</span><span class="sxs-lookup"><span data-stu-id="457d1-944">At least two strings to combine</span></span> | 
||||| 

| <span data-ttu-id="457d1-945">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-945">Return value</span></span> | <span data-ttu-id="457d1-946">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-946">Type</span></span> | <span data-ttu-id="457d1-947">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-947">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-948"><*text1text2...*></span><span class="sxs-lookup"><span data-stu-id="457d1-948"><*text1text2...*></span></span> | <span data-ttu-id="457d1-949">String</span><span class="sxs-lookup"><span data-stu-id="457d1-949">String</span></span> | <span data-ttu-id="457d1-950">The string created from the combined input strings</span><span class="sxs-lookup"><span data-stu-id="457d1-950">The string created from the combined input strings</span></span> | 
|||| 

<span data-ttu-id="457d1-951">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-951">*Example*</span></span>

<span data-ttu-id="457d1-952">This example combines the strings "Hello" and "World":</span><span class="sxs-lookup"><span data-stu-id="457d1-952">This example combines the strings "Hello" and "World":</span></span>

```
concat('Hello', 'World')
```

<span data-ttu-id="457d1-953">And returns this result: `"HelloWorld"`</span><span class="sxs-lookup"><span data-stu-id="457d1-953">And returns this result: `"HelloWorld"`</span></span>

<a name="contains"></a>

### <a name="contains"></a><span data-ttu-id="457d1-954">contains</span><span class="sxs-lookup"><span data-stu-id="457d1-954">contains</span></span>

<span data-ttu-id="457d1-955">Check whether a collection has a specific item.</span><span class="sxs-lookup"><span data-stu-id="457d1-955">Check whether a collection has a specific item.</span></span> <span data-ttu-id="457d1-956">Return true when the item is found, or return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-956">Return true when the item is found, or return false when not found.</span></span> <span data-ttu-id="457d1-957">This function is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="457d1-957">This function is case-sensitive.</span></span>

```
contains('<collection>', '<value>')
contains([<collection>], '<value>')
```

<span data-ttu-id="457d1-958">Specifically, this function works on these collection types:</span><span class="sxs-lookup"><span data-stu-id="457d1-958">Specifically, this function works on these collection types:</span></span> 

* <span data-ttu-id="457d1-959">A *string* to find a *substring*</span><span class="sxs-lookup"><span data-stu-id="457d1-959">A *string* to find a *substring*</span></span>
* <span data-ttu-id="457d1-960">An *array* to find a *value*</span><span class="sxs-lookup"><span data-stu-id="457d1-960">An *array* to find a *value*</span></span>
* <span data-ttu-id="457d1-961">A *dictionary* to find a *key*</span><span class="sxs-lookup"><span data-stu-id="457d1-961">A *dictionary* to find a *key*</span></span>

| <span data-ttu-id="457d1-962">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-962">Parameter</span></span> | <span data-ttu-id="457d1-963">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-963">Required</span></span> | <span data-ttu-id="457d1-964">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-964">Type</span></span> | <span data-ttu-id="457d1-965">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-965">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-966"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-966"><*collection*></span></span> | <span data-ttu-id="457d1-967">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-967">Yes</span></span> | <span data-ttu-id="457d1-968">String, Array, or Dictionary</span><span class="sxs-lookup"><span data-stu-id="457d1-968">String, Array, or Dictionary</span></span> | <span data-ttu-id="457d1-969">The collection to check</span><span class="sxs-lookup"><span data-stu-id="457d1-969">The collection to check</span></span> | 
| <span data-ttu-id="457d1-970"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-970"><*value*></span></span> | <span data-ttu-id="457d1-971">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-971">Yes</span></span> | <span data-ttu-id="457d1-972">String, Array, or Dictionary, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-972">String, Array, or Dictionary, respectively</span></span> | <span data-ttu-id="457d1-973">The item to find</span><span class="sxs-lookup"><span data-stu-id="457d1-973">The item to find</span></span> | 
||||| 

| <span data-ttu-id="457d1-974">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-974">Return value</span></span> | <span data-ttu-id="457d1-975">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-975">Type</span></span> | <span data-ttu-id="457d1-976">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-976">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-977">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-977">true or false</span></span> | <span data-ttu-id="457d1-978">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-978">Boolean</span></span> | <span data-ttu-id="457d1-979">Return true when the item is found.</span><span class="sxs-lookup"><span data-stu-id="457d1-979">Return true when the item is found.</span></span> <span data-ttu-id="457d1-980">Return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-980">Return false when not found.</span></span> |
|||| 

<span data-ttu-id="457d1-981">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-981">*Example 1*</span></span>

<span data-ttu-id="457d1-982">This example checks the string "hello world" for the substring "world" and returns true:</span><span class="sxs-lookup"><span data-stu-id="457d1-982">This example checks the string "hello world" for the substring "world" and returns true:</span></span>

```
contains('hello world', 'world')
```

<span data-ttu-id="457d1-983">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-983">*Example 2*</span></span>

<span data-ttu-id="457d1-984">This example checks the string "hello world" for the substring "universe" and returns false:</span><span class="sxs-lookup"><span data-stu-id="457d1-984">This example checks the string "hello world" for the substring "universe" and returns false:</span></span>

```
contains('hello world', 'universe')
```

<a name="convertFromUtc"></a>

### <a name="convertfromutc"></a><span data-ttu-id="457d1-985">convertFromUtc</span><span class="sxs-lookup"><span data-stu-id="457d1-985">convertFromUtc</span></span>

<span data-ttu-id="457d1-986">Convert a timestamp from Universal Time Coordinated (UTC) to the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-986">Convert a timestamp from Universal Time Coordinated (UTC) to the target time zone.</span></span>

```
convertFromUtc('<timestamp>', '<destinationTimeZone>', '<format>'?)
```

| <span data-ttu-id="457d1-987">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-987">Parameter</span></span> | <span data-ttu-id="457d1-988">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-988">Required</span></span> | <span data-ttu-id="457d1-989">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-989">Type</span></span> | <span data-ttu-id="457d1-990">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-990">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-991"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-991"><*timestamp*></span></span> | <span data-ttu-id="457d1-992">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-992">Yes</span></span> | <span data-ttu-id="457d1-993">String</span><span class="sxs-lookup"><span data-stu-id="457d1-993">String</span></span> | <span data-ttu-id="457d1-994">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-994">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-995"><*destinationTimeZone*></span><span class="sxs-lookup"><span data-stu-id="457d1-995"><*destinationTimeZone*></span></span> | <span data-ttu-id="457d1-996">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-996">Yes</span></span> | <span data-ttu-id="457d1-997">String</span><span class="sxs-lookup"><span data-stu-id="457d1-997">String</span></span> | <span data-ttu-id="457d1-998">The name for the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-998">The name for the target time zone.</span></span> <span data-ttu-id="457d1-999">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span><span class="sxs-lookup"><span data-stu-id="457d1-999">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span></span> | 
| <span data-ttu-id="457d1-1000"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1000"><*format*></span></span> | <span data-ttu-id="457d1-1001">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1001">No</span></span> | <span data-ttu-id="457d1-1002">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1002">String</span></span> | <span data-ttu-id="457d1-1003">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1003">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1004">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1004">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-1005">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1005">Return value</span></span> | <span data-ttu-id="457d1-1006">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1006">Type</span></span> | <span data-ttu-id="457d1-1007">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1007">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1008"><*converted-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1008"><*converted-timestamp*></span></span> | <span data-ttu-id="457d1-1009">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1009">String</span></span> | <span data-ttu-id="457d1-1010">The timestamp converted to the target time zone</span><span class="sxs-lookup"><span data-stu-id="457d1-1010">The timestamp converted to the target time zone</span></span> | 
|||| 

<span data-ttu-id="457d1-1011">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1011">*Example 1*</span></span>

<span data-ttu-id="457d1-1012">This example converts a timestamp to the specified time zone:</span><span class="sxs-lookup"><span data-stu-id="457d1-1012">This example converts a timestamp to the specified time zone:</span></span> 

```
convertFromUtc('2018-01-01T08:00:00.0000000Z', 'Pacific Standard Time')
```

<span data-ttu-id="457d1-1013">And returns this result: `"2018-01-01T00:00:00.0000000"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1013">And returns this result: `"2018-01-01T00:00:00.0000000"`</span></span>

<span data-ttu-id="457d1-1014">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1014">*Example 2*</span></span>

<span data-ttu-id="457d1-1015">This example converts a timestamp to the specified time zone and format:</span><span class="sxs-lookup"><span data-stu-id="457d1-1015">This example converts a timestamp to the specified time zone and format:</span></span>

```
convertFromUtc('2018-01-01T08:00:00.0000000Z', 'Pacific Standard Time', 'D')
```

<span data-ttu-id="457d1-1016">And returns this result: `"Monday, January 1, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1016">And returns this result: `"Monday, January 1, 2018"`</span></span>

<a name="convertTimeZone"></a>

### <a name="converttimezone"></a><span data-ttu-id="457d1-1017">convertTimeZone</span><span class="sxs-lookup"><span data-stu-id="457d1-1017">convertTimeZone</span></span>

<span data-ttu-id="457d1-1018">Convert a timestamp from the source time zone to the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-1018">Convert a timestamp from the source time zone to the target time zone.</span></span>

```
convertTimeZone('<timestamp>', '<sourceTimeZone>', '<destinationTimeZone>', '<format>'?)
```

| <span data-ttu-id="457d1-1019">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1019">Parameter</span></span> | <span data-ttu-id="457d1-1020">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1020">Required</span></span> | <span data-ttu-id="457d1-1021">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1021">Type</span></span> | <span data-ttu-id="457d1-1022">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1022">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1023"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1023"><*timestamp*></span></span> | <span data-ttu-id="457d1-1024">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1024">Yes</span></span> | <span data-ttu-id="457d1-1025">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1025">String</span></span> | <span data-ttu-id="457d1-1026">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1026">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-1027"><*sourceTimeZone*></span><span class="sxs-lookup"><span data-stu-id="457d1-1027"><*sourceTimeZone*></span></span> | <span data-ttu-id="457d1-1028">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1028">Yes</span></span> | <span data-ttu-id="457d1-1029">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1029">String</span></span> | <span data-ttu-id="457d1-1030">The name for the source time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-1030">The name for the source time zone.</span></span> <span data-ttu-id="457d1-1031">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span><span class="sxs-lookup"><span data-stu-id="457d1-1031">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span></span> | 
| <span data-ttu-id="457d1-1032"><*destinationTimeZone*></span><span class="sxs-lookup"><span data-stu-id="457d1-1032"><*destinationTimeZone*></span></span> | <span data-ttu-id="457d1-1033">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1033">Yes</span></span> | <span data-ttu-id="457d1-1034">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1034">String</span></span> | <span data-ttu-id="457d1-1035">The name for the target time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-1035">The name for the target time zone.</span></span> <span data-ttu-id="457d1-1036">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span><span class="sxs-lookup"><span data-stu-id="457d1-1036">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span></span> | 
| <span data-ttu-id="457d1-1037"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1037"><*format*></span></span> | <span data-ttu-id="457d1-1038">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1038">No</span></span> | <span data-ttu-id="457d1-1039">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1039">String</span></span> | <span data-ttu-id="457d1-1040">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1040">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1041">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1041">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-1042">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1042">Return value</span></span> | <span data-ttu-id="457d1-1043">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1043">Type</span></span> | <span data-ttu-id="457d1-1044">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1044">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1045"><*converted-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1045"><*converted-timestamp*></span></span> | <span data-ttu-id="457d1-1046">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1046">String</span></span> | <span data-ttu-id="457d1-1047">The timestamp converted to the target time zone</span><span class="sxs-lookup"><span data-stu-id="457d1-1047">The timestamp converted to the target time zone</span></span> | 
|||| 

<span data-ttu-id="457d1-1048">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1048">*Example 1*</span></span>

<span data-ttu-id="457d1-1049">This example converts the source time zone to the target time zone:</span><span class="sxs-lookup"><span data-stu-id="457d1-1049">This example converts the source time zone to the target time zone:</span></span> 

```
convertTimeZone('2018-01-01T08:00:00.0000000Z', 'UTC', 'Pacific Standard Time')
```

<span data-ttu-id="457d1-1050">And returns this result: `"2018-01-01T00:00:00.0000000"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1050">And returns this result: `"2018-01-01T00:00:00.0000000"`</span></span>

<span data-ttu-id="457d1-1051">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1051">*Example 2*</span></span>

<span data-ttu-id="457d1-1052">This example converts a time zone to the specified time zone and format:</span><span class="sxs-lookup"><span data-stu-id="457d1-1052">This example converts a time zone to the specified time zone and format:</span></span>

```
convertTimeZone('2018-01-01T80:00:00.0000000Z', 'UTC', 'Pacific Standard Time', 'D')
```

<span data-ttu-id="457d1-1053">And returns this result: `"Monday, January 1, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1053">And returns this result: `"Monday, January 1, 2018"`</span></span>

<a name="convertToUtc"></a>

### <a name="converttoutc"></a><span data-ttu-id="457d1-1054">convertToUtc</span><span class="sxs-lookup"><span data-stu-id="457d1-1054">convertToUtc</span></span>

<span data-ttu-id="457d1-1055">Convert a timestamp from the source time zone to Universal Time Coordinated (UTC).</span><span class="sxs-lookup"><span data-stu-id="457d1-1055">Convert a timestamp from the source time zone to Universal Time Coordinated (UTC).</span></span>

```
convertToUtc('<timestamp>', '<sourceTimeZone>', '<format>'?)
```

| <span data-ttu-id="457d1-1056">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1056">Parameter</span></span> | <span data-ttu-id="457d1-1057">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1057">Required</span></span> | <span data-ttu-id="457d1-1058">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1058">Type</span></span> | <span data-ttu-id="457d1-1059">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1059">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1060"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1060"><*timestamp*></span></span> | <span data-ttu-id="457d1-1061">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1061">Yes</span></span> | <span data-ttu-id="457d1-1062">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1062">String</span></span> | <span data-ttu-id="457d1-1063">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1063">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-1064"><*sourceTimeZone*></span><span class="sxs-lookup"><span data-stu-id="457d1-1064"><*sourceTimeZone*></span></span> | <span data-ttu-id="457d1-1065">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1065">Yes</span></span> | <span data-ttu-id="457d1-1066">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1066">String</span></span> | <span data-ttu-id="457d1-1067">The name for the source time zone.</span><span class="sxs-lookup"><span data-stu-id="457d1-1067">The name for the source time zone.</span></span> <span data-ttu-id="457d1-1068">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span><span class="sxs-lookup"><span data-stu-id="457d1-1068">For more information, see [Time Zone IDs](https://docs.microsoft.com/previous-versions/windows/embedded/gg154758(v=winembedded.80)).</span></span> | 
| <span data-ttu-id="457d1-1069"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1069"><*format*></span></span> | <span data-ttu-id="457d1-1070">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1070">No</span></span> | <span data-ttu-id="457d1-1071">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1071">String</span></span> | <span data-ttu-id="457d1-1072">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1072">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1073">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1073">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-1074">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1074">Return value</span></span> | <span data-ttu-id="457d1-1075">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1075">Type</span></span> | <span data-ttu-id="457d1-1076">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1076">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1077"><*converted-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1077"><*converted-timestamp*></span></span> | <span data-ttu-id="457d1-1078">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1078">String</span></span> | <span data-ttu-id="457d1-1079">The timestamp converted to UTC</span><span class="sxs-lookup"><span data-stu-id="457d1-1079">The timestamp converted to UTC</span></span> | 
|||| 

<span data-ttu-id="457d1-1080">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1080">*Example 1*</span></span>

<span data-ttu-id="457d1-1081">This example converts a timestamp to UTC:</span><span class="sxs-lookup"><span data-stu-id="457d1-1081">This example converts a timestamp to UTC:</span></span> 

```
convertToUtc('01/01/2018 00:00:00', 'Pacific Standard Time')
```

<span data-ttu-id="457d1-1082">And returns this result: `"2018-01-01T08:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1082">And returns this result: `"2018-01-01T08:00:00.0000000Z"`</span></span>

<span data-ttu-id="457d1-1083">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1083">*Example 2*</span></span>

<span data-ttu-id="457d1-1084">This example converts a timestamp to UTC:</span><span class="sxs-lookup"><span data-stu-id="457d1-1084">This example converts a timestamp to UTC:</span></span>

```
convertToUtc('01/01/2018 00:00:00', 'Pacific Standard Time', 'D')
```

<span data-ttu-id="457d1-1085">And returns this result: `"Monday, January 1, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1085">And returns this result: `"Monday, January 1, 2018"`</span></span>

<a name="createArray"></a>

### <a name="createarray"></a><span data-ttu-id="457d1-1086">createArray</span><span class="sxs-lookup"><span data-stu-id="457d1-1086">createArray</span></span>

<span data-ttu-id="457d1-1087">Return an array from multiple inputs.</span><span class="sxs-lookup"><span data-stu-id="457d1-1087">Return an array from multiple inputs.</span></span> <span data-ttu-id="457d1-1088">For single input arrays, see [array()](#array).</span><span class="sxs-lookup"><span data-stu-id="457d1-1088">For single input arrays, see [array()](#array).</span></span>

```
createArray('<object1>', '<object2>', ...)
```

| <span data-ttu-id="457d1-1089">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1089">Parameter</span></span> | <span data-ttu-id="457d1-1090">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1090">Required</span></span> | <span data-ttu-id="457d1-1091">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1091">Type</span></span> | <span data-ttu-id="457d1-1092">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1092">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1093"><*object1*>, <*object2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-1093"><*object1*>, <*object2*>, ...</span></span> | <span data-ttu-id="457d1-1094">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1094">Yes</span></span> | <span data-ttu-id="457d1-1095">Any, but not mixed</span><span class="sxs-lookup"><span data-stu-id="457d1-1095">Any, but not mixed</span></span> | <span data-ttu-id="457d1-1096">At least two items to create the array</span><span class="sxs-lookup"><span data-stu-id="457d1-1096">At least two items to create the array</span></span> | 
||||| 

| <span data-ttu-id="457d1-1097">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1097">Return value</span></span> | <span data-ttu-id="457d1-1098">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1098">Type</span></span> | <span data-ttu-id="457d1-1099">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1099">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1100">[<*object1*>, <*object2*>, ...]</span><span class="sxs-lookup"><span data-stu-id="457d1-1100">[<*object1*>, <*object2*>, ...]</span></span> | <span data-ttu-id="457d1-1101">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1101">Array</span></span> | <span data-ttu-id="457d1-1102">The array created from all the input items</span><span class="sxs-lookup"><span data-stu-id="457d1-1102">The array created from all the input items</span></span> | 
|||| 

<span data-ttu-id="457d1-1103">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1103">*Example*</span></span>

<span data-ttu-id="457d1-1104">This example creates an array from these inputs:</span><span class="sxs-lookup"><span data-stu-id="457d1-1104">This example creates an array from these inputs:</span></span>

```
createArray('h', 'e', 'l', 'l', 'o')
```

<span data-ttu-id="457d1-1105">And returns this result: `["h", "e", "l", "l", "o"]`</span><span class="sxs-lookup"><span data-stu-id="457d1-1105">And returns this result: `["h", "e", "l", "l", "o"]`</span></span>

<a name="dataUri"></a>

### <a name="datauri"></a><span data-ttu-id="457d1-1106">dataUri</span><span class="sxs-lookup"><span data-stu-id="457d1-1106">dataUri</span></span>

<span data-ttu-id="457d1-1107">Return a data uniform resource identifier (URI) for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-1107">Return a data uniform resource identifier (URI) for a string.</span></span> 

```
dataUri('<value>')
```

| <span data-ttu-id="457d1-1108">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1108">Parameter</span></span> | <span data-ttu-id="457d1-1109">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1109">Required</span></span> | <span data-ttu-id="457d1-1110">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1110">Type</span></span> | <span data-ttu-id="457d1-1111">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1111">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1112"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1112"><*value*></span></span> | <span data-ttu-id="457d1-1113">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1113">Yes</span></span> | <span data-ttu-id="457d1-1114">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1114">String</span></span> | <span data-ttu-id="457d1-1115">The string to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1115">The string to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-1116">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1116">Return value</span></span> | <span data-ttu-id="457d1-1117">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1117">Type</span></span> | <span data-ttu-id="457d1-1118">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1118">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1119"><*data-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1119"><*data-uri*></span></span> | <span data-ttu-id="457d1-1120">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1120">String</span></span> | <span data-ttu-id="457d1-1121">The data URI for the input string</span><span class="sxs-lookup"><span data-stu-id="457d1-1121">The data URI for the input string</span></span> | 
|||| 

<span data-ttu-id="457d1-1122">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1122">*Example*</span></span>

<span data-ttu-id="457d1-1123">This example creates a data URI for the "hello" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1123">This example creates a data URI for the "hello" string:</span></span>

```
dataUri('hello') 
```

<span data-ttu-id="457d1-1124">And returns this result: `"data:text/plain;charset=utf-8;base64,aGVsbG8="`</span><span class="sxs-lookup"><span data-stu-id="457d1-1124">And returns this result: `"data:text/plain;charset=utf-8;base64,aGVsbG8="`</span></span>

<a name="dataUriToBinary"></a>

### <a name="datauritobinary"></a><span data-ttu-id="457d1-1125">dataUriToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-1125">dataUriToBinary</span></span>

<span data-ttu-id="457d1-1126">Return the binary version for a data uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-1126">Return the binary version for a data uniform resource identifier (URI).</span></span> <span data-ttu-id="457d1-1127">Use this function rather than [decodeDataUri()](#decodeDataUri).</span><span class="sxs-lookup"><span data-stu-id="457d1-1127">Use this function rather than [decodeDataUri()](#decodeDataUri).</span></span> <span data-ttu-id="457d1-1128">Although both functions work the same way, `decodeDataUri()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-1128">Although both functions work the same way, `decodeDataUri()` is preferred.</span></span>

```
dataUriToBinary('<value>')
```

| <span data-ttu-id="457d1-1129">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1129">Parameter</span></span> | <span data-ttu-id="457d1-1130">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1130">Required</span></span> | <span data-ttu-id="457d1-1131">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1131">Type</span></span> | <span data-ttu-id="457d1-1132">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1132">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1133"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1133"><*value*></span></span> | <span data-ttu-id="457d1-1134">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1134">Yes</span></span> | <span data-ttu-id="457d1-1135">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1135">String</span></span> | <span data-ttu-id="457d1-1136">The data URI to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1136">The data URI to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-1137">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1137">Return value</span></span> | <span data-ttu-id="457d1-1138">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1138">Type</span></span> | <span data-ttu-id="457d1-1139">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1139">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1140"><*binary-for-data-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1140"><*binary-for-data-uri*></span></span> | <span data-ttu-id="457d1-1141">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1141">String</span></span> | <span data-ttu-id="457d1-1142">The binary version for the data URI</span><span class="sxs-lookup"><span data-stu-id="457d1-1142">The binary version for the data URI</span></span> | 
|||| 

<span data-ttu-id="457d1-1143">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1143">*Example*</span></span>

<span data-ttu-id="457d1-1144">This example creates a binary version for this data URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-1144">This example creates a binary version for this data URI:</span></span>

```
dataUriToBinary('data:text/plain;charset=utf-8;base64,aGVsbG8=')
```

<span data-ttu-id="457d1-1145">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-1145">And returns this result:</span></span> 

`"01100100011000010111010001100001001110100111010001100101011110000111010000101111011100000
1101100011000010110100101101110001110110110001101101000011000010111001001110011011001010111
0100001111010111010101110100011001100010110100111000001110110110001001100001011100110110010
10011011000110100001011000110000101000111010101100111001101100010010001110011100000111101"`

<a name="dataUriToString"></a>

### <a name="datauritostring"></a><span data-ttu-id="457d1-1146">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="457d1-1146">dataUriToString</span></span>

<span data-ttu-id="457d1-1147">Return the string version for a data uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-1147">Return the string version for a data uniform resource identifier (URI).</span></span>

```
dataUriToString('<value>')
```

| <span data-ttu-id="457d1-1148">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1148">Parameter</span></span> | <span data-ttu-id="457d1-1149">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1149">Required</span></span> | <span data-ttu-id="457d1-1150">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1150">Type</span></span> | <span data-ttu-id="457d1-1151">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1151">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1152"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1152"><*value*></span></span> | <span data-ttu-id="457d1-1153">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1153">Yes</span></span> | <span data-ttu-id="457d1-1154">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1154">String</span></span> | <span data-ttu-id="457d1-1155">The data URI to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1155">The data URI to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-1156">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1156">Return value</span></span> | <span data-ttu-id="457d1-1157">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1157">Type</span></span> | <span data-ttu-id="457d1-1158">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1158">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1159"><*string-for-data-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1159"><*string-for-data-uri*></span></span> | <span data-ttu-id="457d1-1160">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1160">String</span></span> | <span data-ttu-id="457d1-1161">The string version for the data URI</span><span class="sxs-lookup"><span data-stu-id="457d1-1161">The string version for the data URI</span></span> | 
|||| 

<span data-ttu-id="457d1-1162">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1162">*Example*</span></span>

<span data-ttu-id="457d1-1163">This example creates a string for this data URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-1163">This example creates a string for this data URI:</span></span>

```
dataUriToString('data:text/plain;charset=utf-8;base64,aGVsbG8=')
```

<span data-ttu-id="457d1-1164">And returns this result: `"hello"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1164">And returns this result: `"hello"`</span></span>

<a name="dayOfMonth"></a>

### <a name="dayofmonth"></a><span data-ttu-id="457d1-1165">dayOfMonth</span><span class="sxs-lookup"><span data-stu-id="457d1-1165">dayOfMonth</span></span>

<span data-ttu-id="457d1-1166">Return the day of the month from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-1166">Return the day of the month from a timestamp.</span></span> 

```
dayOfMonth('<timestamp>')
```

| <span data-ttu-id="457d1-1167">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1167">Parameter</span></span> | <span data-ttu-id="457d1-1168">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1168">Required</span></span> | <span data-ttu-id="457d1-1169">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1169">Type</span></span> | <span data-ttu-id="457d1-1170">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1170">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1171"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1171"><*timestamp*></span></span> | <span data-ttu-id="457d1-1172">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1172">Yes</span></span> | <span data-ttu-id="457d1-1173">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1173">String</span></span> | <span data-ttu-id="457d1-1174">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1174">The string that contains the timestamp</span></span> | 
||||| 

| <span data-ttu-id="457d1-1175">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1175">Return value</span></span> | <span data-ttu-id="457d1-1176">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1176">Type</span></span> | <span data-ttu-id="457d1-1177">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1177">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1178"><*day-of-month*></span><span class="sxs-lookup"><span data-stu-id="457d1-1178"><*day-of-month*></span></span> | <span data-ttu-id="457d1-1179">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1179">Integer</span></span> | <span data-ttu-id="457d1-1180">The day of the month from the specified timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1180">The day of the month from the specified timestamp</span></span> | 
|||| 

<span data-ttu-id="457d1-1181">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1181">*Example*</span></span>

<span data-ttu-id="457d1-1182">This example returns the number for the day of the month from this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-1182">This example returns the number for the day of the month from this timestamp:</span></span>

```
dayOfMonth('2018-03-15T13:27:36Z')
```

<span data-ttu-id="457d1-1183">And returns this result: `15`</span><span class="sxs-lookup"><span data-stu-id="457d1-1183">And returns this result: `15`</span></span>

<a name="dayOfWeek"></a>

### <a name="dayofweek"></a><span data-ttu-id="457d1-1184">dayOfWeek</span><span class="sxs-lookup"><span data-stu-id="457d1-1184">dayOfWeek</span></span>

<span data-ttu-id="457d1-1185">Return the day of the week from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-1185">Return the day of the week from a timestamp.</span></span>  

```
dayOfWeek('<timestamp>')
```

| <span data-ttu-id="457d1-1186">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1186">Parameter</span></span> | <span data-ttu-id="457d1-1187">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1187">Required</span></span> | <span data-ttu-id="457d1-1188">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1188">Type</span></span> | <span data-ttu-id="457d1-1189">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1189">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1190"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1190"><*timestamp*></span></span> | <span data-ttu-id="457d1-1191">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1191">Yes</span></span> | <span data-ttu-id="457d1-1192">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1192">String</span></span> | <span data-ttu-id="457d1-1193">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1193">The string that contains the timestamp</span></span> | 
||||| 

| <span data-ttu-id="457d1-1194">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1194">Return value</span></span> | <span data-ttu-id="457d1-1195">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1195">Type</span></span> | <span data-ttu-id="457d1-1196">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1196">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1197"><*day-of-week*></span><span class="sxs-lookup"><span data-stu-id="457d1-1197"><*day-of-week*></span></span> | <span data-ttu-id="457d1-1198">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1198">Integer</span></span> | <span data-ttu-id="457d1-1199">The day of the week from the specified timestamp where Sunday is 0, Monday is 1, and so on</span><span class="sxs-lookup"><span data-stu-id="457d1-1199">The day of the week from the specified timestamp where Sunday is 0, Monday is 1, and so on</span></span> | 
|||| 

<span data-ttu-id="457d1-1200">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1200">*Example*</span></span>

<span data-ttu-id="457d1-1201">This example returns the number for the day of the week from this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-1201">This example returns the number for the day of the week from this timestamp:</span></span>

```
dayOfWeek('2018-03-15T13:27:36Z')
```

<span data-ttu-id="457d1-1202">And returns this result: `3`</span><span class="sxs-lookup"><span data-stu-id="457d1-1202">And returns this result: `3`</span></span>

<a name="dayOfYear"></a>

### <a name="dayofyear"></a><span data-ttu-id="457d1-1203">dayOfYear</span><span class="sxs-lookup"><span data-stu-id="457d1-1203">dayOfYear</span></span>

<span data-ttu-id="457d1-1204">Return the day of the year from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-1204">Return the day of the year from a timestamp.</span></span> 

```
dayOfYear('<timestamp>')
```

| <span data-ttu-id="457d1-1205">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1205">Parameter</span></span> | <span data-ttu-id="457d1-1206">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1206">Required</span></span> | <span data-ttu-id="457d1-1207">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1207">Type</span></span> | <span data-ttu-id="457d1-1208">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1208">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1209"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1209"><*timestamp*></span></span> | <span data-ttu-id="457d1-1210">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1210">Yes</span></span> | <span data-ttu-id="457d1-1211">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1211">String</span></span> | <span data-ttu-id="457d1-1212">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1212">The string that contains the timestamp</span></span> | 
||||| 

| <span data-ttu-id="457d1-1213">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1213">Return value</span></span> | <span data-ttu-id="457d1-1214">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1214">Type</span></span> | <span data-ttu-id="457d1-1215">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1215">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1216"><*day-of-year*></span><span class="sxs-lookup"><span data-stu-id="457d1-1216"><*day-of-year*></span></span> | <span data-ttu-id="457d1-1217">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1217">Integer</span></span> | <span data-ttu-id="457d1-1218">The day of the year from the specified timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1218">The day of the year from the specified timestamp</span></span> | 
|||| 

<span data-ttu-id="457d1-1219">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1219">*Example*</span></span>

<span data-ttu-id="457d1-1220">This example returns the number of the day of the year from this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-1220">This example returns the number of the day of the year from this timestamp:</span></span>

```
dayOfYear('2018-03-15T13:27:36Z')
```

<span data-ttu-id="457d1-1221">And returns this result: `74`</span><span class="sxs-lookup"><span data-stu-id="457d1-1221">And returns this result: `74`</span></span>

<a name="decodeBase64"></a>

### <a name="decodebase64"></a><span data-ttu-id="457d1-1222">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="457d1-1222">decodeBase64</span></span>

<span data-ttu-id="457d1-1223">Return the string version for a base64-encoded string, effectively decoding the base64 string.</span><span class="sxs-lookup"><span data-stu-id="457d1-1223">Return the string version for a base64-encoded string, effectively decoding the base64 string.</span></span> <span data-ttu-id="457d1-1224">Consider using [base64ToString()](#base64ToString) rather than `decodeBase64()`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1224">Consider using [base64ToString()](#base64ToString) rather than `decodeBase64()`.</span></span> <span data-ttu-id="457d1-1225">Although both functions work the same way, `base64ToString()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-1225">Although both functions work the same way, `base64ToString()` is preferred.</span></span>

```
decodeBase64('<value>')
```

| <span data-ttu-id="457d1-1226">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1226">Parameter</span></span> | <span data-ttu-id="457d1-1227">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1227">Required</span></span> | <span data-ttu-id="457d1-1228">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1228">Type</span></span> | <span data-ttu-id="457d1-1229">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1229">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1230"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1230"><*value*></span></span> | <span data-ttu-id="457d1-1231">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1231">Yes</span></span> | <span data-ttu-id="457d1-1232">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1232">String</span></span> | <span data-ttu-id="457d1-1233">The base64-encoded string to decode</span><span class="sxs-lookup"><span data-stu-id="457d1-1233">The base64-encoded string to decode</span></span> | 
||||| 

| <span data-ttu-id="457d1-1234">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1234">Return value</span></span> | <span data-ttu-id="457d1-1235">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1235">Type</span></span> | <span data-ttu-id="457d1-1236">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1236">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1237"><*decoded-base64-string*></span><span class="sxs-lookup"><span data-stu-id="457d1-1237"><*decoded-base64-string*></span></span> | <span data-ttu-id="457d1-1238">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1238">String</span></span> | <span data-ttu-id="457d1-1239">The string version for a base64-encoded string</span><span class="sxs-lookup"><span data-stu-id="457d1-1239">The string version for a base64-encoded string</span></span> | 
|||| 

<span data-ttu-id="457d1-1240">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1240">*Example*</span></span>

<span data-ttu-id="457d1-1241">This example creates a string for a base64-encoded string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1241">This example creates a string for a base64-encoded string:</span></span>

```
decodeBase64('aGVsbG8=')
```

<span data-ttu-id="457d1-1242">And returns this result: `"hello"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1242">And returns this result: `"hello"`</span></span>

<a name="decodeDataUri"></a>

### <a name="decodedatauri"></a><span data-ttu-id="457d1-1243">decodeDataUri</span><span class="sxs-lookup"><span data-stu-id="457d1-1243">decodeDataUri</span></span>

<span data-ttu-id="457d1-1244">Return the binary version for a data uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-1244">Return the binary version for a data uniform resource identifier (URI).</span></span> <span data-ttu-id="457d1-1245">Consider using [dataUriToBinary()](#dataUriToBinary), rather than `decodeDataUri()`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1245">Consider using [dataUriToBinary()](#dataUriToBinary), rather than `decodeDataUri()`.</span></span> <span data-ttu-id="457d1-1246">Although both functions work the same way, `dataUriToBinary()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-1246">Although both functions work the same way, `dataUriToBinary()` is preferred.</span></span>

```
decodeDataUri('<value>')
```

| <span data-ttu-id="457d1-1247">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1247">Parameter</span></span> | <span data-ttu-id="457d1-1248">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1248">Required</span></span> | <span data-ttu-id="457d1-1249">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1249">Type</span></span> | <span data-ttu-id="457d1-1250">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1250">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1251"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1251"><*value*></span></span> | <span data-ttu-id="457d1-1252">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1252">Yes</span></span> | <span data-ttu-id="457d1-1253">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1253">String</span></span> | <span data-ttu-id="457d1-1254">The data URI string to decode</span><span class="sxs-lookup"><span data-stu-id="457d1-1254">The data URI string to decode</span></span> | 
||||| 

| <span data-ttu-id="457d1-1255">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1255">Return value</span></span> | <span data-ttu-id="457d1-1256">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1256">Type</span></span> | <span data-ttu-id="457d1-1257">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1257">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1258"><*binary-for-data-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1258"><*binary-for-data-uri*></span></span> | <span data-ttu-id="457d1-1259">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1259">String</span></span> | <span data-ttu-id="457d1-1260">The binary version for a data URI string</span><span class="sxs-lookup"><span data-stu-id="457d1-1260">The binary version for a data URI string</span></span> | 
|||| 

<span data-ttu-id="457d1-1261">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1261">*Example*</span></span>

<span data-ttu-id="457d1-1262">This example returns the binary version for this data URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-1262">This example returns the binary version for this data URI:</span></span>

```
decodeDataUri('data:text/plain;charset=utf-8;base64,aGVsbG8=')
```

<span data-ttu-id="457d1-1263">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-1263">And returns this result:</span></span> 

`"01100100011000010111010001100001001110100111010001100101011110000111010000101111011100000
1101100011000010110100101101110001110110110001101101000011000010111001001110011011001010111
0100001111010111010101110100011001100010110100111000001110110110001001100001011100110110010
10011011000110100001011000110000101000111010101100111001101100010010001110011100000111101"`

<a name="decodeUriComponent"></a>

### <a name="decodeuricomponent"></a><span data-ttu-id="457d1-1264">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-1264">decodeUriComponent</span></span>

<span data-ttu-id="457d1-1265">Return a string that replaces escape characters with decoded versions.</span><span class="sxs-lookup"><span data-stu-id="457d1-1265">Return a string that replaces escape characters with decoded versions.</span></span> 

```
decodeUriComponent('<value>')
```

| <span data-ttu-id="457d1-1266">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1266">Parameter</span></span> | <span data-ttu-id="457d1-1267">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1267">Required</span></span> | <span data-ttu-id="457d1-1268">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1268">Type</span></span> | <span data-ttu-id="457d1-1269">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1269">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1270"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1270"><*value*></span></span> | <span data-ttu-id="457d1-1271">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1271">Yes</span></span> | <span data-ttu-id="457d1-1272">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1272">String</span></span> | <span data-ttu-id="457d1-1273">The string with the escape characters to decode</span><span class="sxs-lookup"><span data-stu-id="457d1-1273">The string with the escape characters to decode</span></span> | 
||||| 

| <span data-ttu-id="457d1-1274">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1274">Return value</span></span> | <span data-ttu-id="457d1-1275">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1275">Type</span></span> | <span data-ttu-id="457d1-1276">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1276">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1277"><*decoded-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1277"><*decoded-uri*></span></span> | <span data-ttu-id="457d1-1278">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1278">String</span></span> | <span data-ttu-id="457d1-1279">The updated string with the decoded escape characters</span><span class="sxs-lookup"><span data-stu-id="457d1-1279">The updated string with the decoded escape characters</span></span> | 
|||| 

<span data-ttu-id="457d1-1280">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1280">*Example*</span></span>

<span data-ttu-id="457d1-1281">This example replaces the escape characters in this string with decoded versions:</span><span class="sxs-lookup"><span data-stu-id="457d1-1281">This example replaces the escape characters in this string with decoded versions:</span></span>

```
decodeUriComponent('http%3A%2F%2Fcontoso.com')
```

<span data-ttu-id="457d1-1282">And returns this result: `"https://contoso.com"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1282">And returns this result: `"https://contoso.com"`</span></span>

<a name="div"></a>

### <a name="div"></a><span data-ttu-id="457d1-1283">div</span><span class="sxs-lookup"><span data-stu-id="457d1-1283">div</span></span>

<span data-ttu-id="457d1-1284">Return the integer result from dividing two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-1284">Return the integer result from dividing two numbers.</span></span> <span data-ttu-id="457d1-1285">To get the remainder result, see [mod()](#mod).</span><span class="sxs-lookup"><span data-stu-id="457d1-1285">To get the remainder result, see [mod()](#mod).</span></span>

```
div(<dividend>, <divisor>)
```

| <span data-ttu-id="457d1-1286">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1286">Parameter</span></span> | <span data-ttu-id="457d1-1287">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1287">Required</span></span> | <span data-ttu-id="457d1-1288">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1288">Type</span></span> | <span data-ttu-id="457d1-1289">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1289">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1290"><*dividend*></span><span class="sxs-lookup"><span data-stu-id="457d1-1290"><*dividend*></span></span> | <span data-ttu-id="457d1-1291">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1291">Yes</span></span> | <span data-ttu-id="457d1-1292">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-1292">Integer or Float</span></span> | <span data-ttu-id="457d1-1293">The number to divide by the *divisor*</span><span class="sxs-lookup"><span data-stu-id="457d1-1293">The number to divide by the *divisor*</span></span> | 
| <span data-ttu-id="457d1-1294"><*divisor*></span><span class="sxs-lookup"><span data-stu-id="457d1-1294"><*divisor*></span></span> | <span data-ttu-id="457d1-1295">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1295">Yes</span></span> | <span data-ttu-id="457d1-1296">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-1296">Integer or Float</span></span> | <span data-ttu-id="457d1-1297">The number that divides the *dividend*, but cannot be 0</span><span class="sxs-lookup"><span data-stu-id="457d1-1297">The number that divides the *dividend*, but cannot be 0</span></span> | 
||||| 

| <span data-ttu-id="457d1-1298">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1298">Return value</span></span> | <span data-ttu-id="457d1-1299">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1299">Type</span></span> | <span data-ttu-id="457d1-1300">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1300">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1301"><*quotient-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-1301"><*quotient-result*></span></span> | <span data-ttu-id="457d1-1302">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1302">Integer</span></span> | <span data-ttu-id="457d1-1303">The integer result from dividing the first number by the second number</span><span class="sxs-lookup"><span data-stu-id="457d1-1303">The integer result from dividing the first number by the second number</span></span> | 
|||| 

<span data-ttu-id="457d1-1304">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1304">*Example*</span></span>

<span data-ttu-id="457d1-1305">Both examples divide the first number by the second number:</span><span class="sxs-lookup"><span data-stu-id="457d1-1305">Both examples divide the first number by the second number:</span></span>

```
div(10, 5)
div(11, 5)
```

<span data-ttu-id="457d1-1306">And return this result: `2`</span><span class="sxs-lookup"><span data-stu-id="457d1-1306">And return this result: `2`</span></span>

<a name="encodeUriComponent"></a>

### <a name="encodeuricomponent"></a><span data-ttu-id="457d1-1307">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-1307">encodeUriComponent</span></span>

<span data-ttu-id="457d1-1308">Return a uniform resource identifier (URI) encoded version for a string by replacing URL-unsafe characters with escape characters.</span><span class="sxs-lookup"><span data-stu-id="457d1-1308">Return a uniform resource identifier (URI) encoded version for a string by replacing URL-unsafe characters with escape characters.</span></span> <span data-ttu-id="457d1-1309">Consider using [uriComponent()](#uriComponent), rather than `encodeUriComponent()`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1309">Consider using [uriComponent()](#uriComponent), rather than `encodeUriComponent()`.</span></span> <span data-ttu-id="457d1-1310">Although both functions work the same way, `uriComponent()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-1310">Although both functions work the same way, `uriComponent()` is preferred.</span></span>

```
encodeUriComponent('<value>')
```

| <span data-ttu-id="457d1-1311">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1311">Parameter</span></span> | <span data-ttu-id="457d1-1312">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1312">Required</span></span> | <span data-ttu-id="457d1-1313">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1313">Type</span></span> | <span data-ttu-id="457d1-1314">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1314">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1315"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1315"><*value*></span></span> | <span data-ttu-id="457d1-1316">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1316">Yes</span></span> | <span data-ttu-id="457d1-1317">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1317">String</span></span> | <span data-ttu-id="457d1-1318">The string to convert to URI-encoded format</span><span class="sxs-lookup"><span data-stu-id="457d1-1318">The string to convert to URI-encoded format</span></span> | 
||||| 

| <span data-ttu-id="457d1-1319">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1319">Return value</span></span> | <span data-ttu-id="457d1-1320">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1320">Type</span></span> | <span data-ttu-id="457d1-1321">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1321">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1322"><*encoded-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-1322"><*encoded-uri*></span></span> | <span data-ttu-id="457d1-1323">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1323">String</span></span> | <span data-ttu-id="457d1-1324">The URI-encoded string with escape characters</span><span class="sxs-lookup"><span data-stu-id="457d1-1324">The URI-encoded string with escape characters</span></span> | 
|||| 

<span data-ttu-id="457d1-1325">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1325">*Example*</span></span>

<span data-ttu-id="457d1-1326">This example creates a URI-encoded version for this string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1326">This example creates a URI-encoded version for this string:</span></span>

```
encodeUriComponent('https://contoso.com')
```

<span data-ttu-id="457d1-1327">And returns this result: `"http%3A%2F%2Fcontoso.com"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1327">And returns this result: `"http%3A%2F%2Fcontoso.com"`</span></span>

<a name="empty"></a>

### <a name="empty"></a><span data-ttu-id="457d1-1328">empty</span><span class="sxs-lookup"><span data-stu-id="457d1-1328">empty</span></span>

<span data-ttu-id="457d1-1329">Check whether a collection is empty.</span><span class="sxs-lookup"><span data-stu-id="457d1-1329">Check whether a collection is empty.</span></span> <span data-ttu-id="457d1-1330">Return true when the collection is empty, or return false when not empty.</span><span class="sxs-lookup"><span data-stu-id="457d1-1330">Return true when the collection is empty, or return false when not empty.</span></span>

```
empty('<collection>')
empty([<collection>])
```

| <span data-ttu-id="457d1-1331">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1331">Parameter</span></span> | <span data-ttu-id="457d1-1332">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1332">Required</span></span> | <span data-ttu-id="457d1-1333">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1333">Type</span></span> | <span data-ttu-id="457d1-1334">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1334">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1335"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-1335"><*collection*></span></span> | <span data-ttu-id="457d1-1336">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1336">Yes</span></span> | <span data-ttu-id="457d1-1337">String, Array, or Object</span><span class="sxs-lookup"><span data-stu-id="457d1-1337">String, Array, or Object</span></span> | <span data-ttu-id="457d1-1338">The collection to check</span><span class="sxs-lookup"><span data-stu-id="457d1-1338">The collection to check</span></span> | 
||||| 

| <span data-ttu-id="457d1-1339">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1339">Return value</span></span> | <span data-ttu-id="457d1-1340">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1340">Type</span></span> | <span data-ttu-id="457d1-1341">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1341">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1342">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1342">true or false</span></span> | <span data-ttu-id="457d1-1343">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1343">Boolean</span></span> | <span data-ttu-id="457d1-1344">Return true when the collection is empty.</span><span class="sxs-lookup"><span data-stu-id="457d1-1344">Return true when the collection is empty.</span></span> <span data-ttu-id="457d1-1345">Return false when not empty.</span><span class="sxs-lookup"><span data-stu-id="457d1-1345">Return false when not empty.</span></span> | 
|||| 

<span data-ttu-id="457d1-1346">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1346">*Example*</span></span> 

<span data-ttu-id="457d1-1347">These examples check whether the specified collections are empty:</span><span class="sxs-lookup"><span data-stu-id="457d1-1347">These examples check whether the specified collections are empty:</span></span>

```
empty('')
empty('abc')
```

<span data-ttu-id="457d1-1348">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1348">And returns these results:</span></span> 

* <span data-ttu-id="457d1-1349">First example: Passes an empty string, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1349">First example: Passes an empty string, so the function returns `true`.</span></span> 
* <span data-ttu-id="457d1-1350">Second example: Passes the string "abc", so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1350">Second example: Passes the string "abc", so the function returns `false`.</span></span> 

<a name="endswith"></a>

### <a name="endswith"></a><span data-ttu-id="457d1-1351">endsWith</span><span class="sxs-lookup"><span data-stu-id="457d1-1351">endsWith</span></span>

<span data-ttu-id="457d1-1352">Check whether a string ends with a specific substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-1352">Check whether a string ends with a specific substring.</span></span> <span data-ttu-id="457d1-1353">Return true when the substring is found, or return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-1353">Return true when the substring is found, or return false when not found.</span></span> <span data-ttu-id="457d1-1354">This function is not case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="457d1-1354">This function is not case-sensitive.</span></span>

```
endsWith('<text>', '<searchText>')
```

| <span data-ttu-id="457d1-1355">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1355">Parameter</span></span> | <span data-ttu-id="457d1-1356">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1356">Required</span></span> | <span data-ttu-id="457d1-1357">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1357">Type</span></span> | <span data-ttu-id="457d1-1358">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1358">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1359"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-1359"><*text*></span></span> | <span data-ttu-id="457d1-1360">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1360">Yes</span></span> | <span data-ttu-id="457d1-1361">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1361">String</span></span> | <span data-ttu-id="457d1-1362">The string to check</span><span class="sxs-lookup"><span data-stu-id="457d1-1362">The string to check</span></span> | 
| <span data-ttu-id="457d1-1363"><*searchText*></span><span class="sxs-lookup"><span data-stu-id="457d1-1363"><*searchText*></span></span> | <span data-ttu-id="457d1-1364">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1364">Yes</span></span> | <span data-ttu-id="457d1-1365">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1365">String</span></span> | <span data-ttu-id="457d1-1366">The ending substring to find</span><span class="sxs-lookup"><span data-stu-id="457d1-1366">The ending substring to find</span></span> | 
||||| 

| <span data-ttu-id="457d1-1367">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1367">Return value</span></span> | <span data-ttu-id="457d1-1368">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1368">Type</span></span> | <span data-ttu-id="457d1-1369">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1369">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1370">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1370">true or false</span></span>  | <span data-ttu-id="457d1-1371">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1371">Boolean</span></span> | <span data-ttu-id="457d1-1372">Return true when the ending substring is found.</span><span class="sxs-lookup"><span data-stu-id="457d1-1372">Return true when the ending substring is found.</span></span> <span data-ttu-id="457d1-1373">Return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-1373">Return false when not found.</span></span> | 
|||| 

<span data-ttu-id="457d1-1374">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1374">*Example 1*</span></span> 

<span data-ttu-id="457d1-1375">This example checks whether the "hello world" string ends with the "world" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1375">This example checks whether the "hello world" string ends with the "world" string:</span></span>

```
endsWith('hello world', 'world')
```

<span data-ttu-id="457d1-1376">And returns this result: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-1376">And returns this result: `true`</span></span>

<span data-ttu-id="457d1-1377">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1377">*Example 2*</span></span>

<span data-ttu-id="457d1-1378">This example checks whether the "hello world" string ends with the "universe" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1378">This example checks whether the "hello world" string ends with the "universe" string:</span></span>

```
endsWith('hello world', 'universe')
```

<span data-ttu-id="457d1-1379">And returns this result: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-1379">And returns this result: `false`</span></span>

<a name="equals"></a>

### <a name="equals"></a><span data-ttu-id="457d1-1380">equals</span><span class="sxs-lookup"><span data-stu-id="457d1-1380">equals</span></span>

<span data-ttu-id="457d1-1381">Check whether both values, expressions, or objects are equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-1381">Check whether both values, expressions, or objects are equivalent.</span></span> <span data-ttu-id="457d1-1382">Return true when both are equivalent, or return false when they're not equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-1382">Return true when both are equivalent, or return false when they're not equivalent.</span></span>

```
equals('<object1>', '<object2>')
```

| <span data-ttu-id="457d1-1383">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1383">Parameter</span></span> | <span data-ttu-id="457d1-1384">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1384">Required</span></span> | <span data-ttu-id="457d1-1385">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1385">Type</span></span> | <span data-ttu-id="457d1-1386">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1386">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1387"><*object1*>, <*object2*></span><span class="sxs-lookup"><span data-stu-id="457d1-1387"><*object1*>, <*object2*></span></span> | <span data-ttu-id="457d1-1388">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1388">Yes</span></span> | <span data-ttu-id="457d1-1389">Various</span><span class="sxs-lookup"><span data-stu-id="457d1-1389">Various</span></span> | <span data-ttu-id="457d1-1390">The values, expressions, or objects to compare</span><span class="sxs-lookup"><span data-stu-id="457d1-1390">The values, expressions, or objects to compare</span></span> | 
||||| 

| <span data-ttu-id="457d1-1391">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1391">Return value</span></span> | <span data-ttu-id="457d1-1392">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1392">Type</span></span> | <span data-ttu-id="457d1-1393">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1393">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1394">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1394">true or false</span></span> | <span data-ttu-id="457d1-1395">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1395">Boolean</span></span> | <span data-ttu-id="457d1-1396">Return true when both are equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-1396">Return true when both are equivalent.</span></span> <span data-ttu-id="457d1-1397">Return false when not equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-1397">Return false when not equivalent.</span></span> | 
|||| 

<span data-ttu-id="457d1-1398">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1398">*Example*</span></span>

<span data-ttu-id="457d1-1399">These examples check whether the specified inputs are equivalent.</span><span class="sxs-lookup"><span data-stu-id="457d1-1399">These examples check whether the specified inputs are equivalent.</span></span> 

```
equals(true, 1)
equals('abc', 'abcd')
```

<span data-ttu-id="457d1-1400">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1400">And returns these results:</span></span> 

* <span data-ttu-id="457d1-1401">First example: Both values are equivalent, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1401">First example: Both values are equivalent, so the function returns `true`.</span></span>
* <span data-ttu-id="457d1-1402">Second exmaple: Both values aren't equivalent, so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-1402">Second exmaple: Both values aren't equivalent, so the function returns `false`.</span></span>

<a name="first"></a>

### <a name="first"></a><span data-ttu-id="457d1-1403">first</span><span class="sxs-lookup"><span data-stu-id="457d1-1403">first</span></span>

<span data-ttu-id="457d1-1404">Return the first item from a string or array.</span><span class="sxs-lookup"><span data-stu-id="457d1-1404">Return the first item from a string or array.</span></span>

```
first('<collection>')
first([<collection>])
```

| <span data-ttu-id="457d1-1405">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1405">Parameter</span></span> | <span data-ttu-id="457d1-1406">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1406">Required</span></span> | <span data-ttu-id="457d1-1407">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1407">Type</span></span> | <span data-ttu-id="457d1-1408">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1408">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1409"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-1409"><*collection*></span></span> | <span data-ttu-id="457d1-1410">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1410">Yes</span></span> | <span data-ttu-id="457d1-1411">String or Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1411">String or Array</span></span> | <span data-ttu-id="457d1-1412">The collection where to find the first item</span><span class="sxs-lookup"><span data-stu-id="457d1-1412">The collection where to find the first item</span></span> |
||||| 

| <span data-ttu-id="457d1-1413">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1413">Return value</span></span> | <span data-ttu-id="457d1-1414">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1414">Type</span></span> | <span data-ttu-id="457d1-1415">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1415">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1416"><*first-collection-item*></span><span class="sxs-lookup"><span data-stu-id="457d1-1416"><*first-collection-item*></span></span> | <span data-ttu-id="457d1-1417">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1417">Any</span></span> | <span data-ttu-id="457d1-1418">The first item in the collection</span><span class="sxs-lookup"><span data-stu-id="457d1-1418">The first item in the collection</span></span> | 
|||| 

<span data-ttu-id="457d1-1419">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1419">*Example*</span></span>

<span data-ttu-id="457d1-1420">These examples find the first item in these collections:</span><span class="sxs-lookup"><span data-stu-id="457d1-1420">These examples find the first item in these collections:</span></span>

```
first('hello')
first([0, 1, 2])
```

<span data-ttu-id="457d1-1421">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1421">And return these results:</span></span> 

* <span data-ttu-id="457d1-1422">First example: `"h"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1422">First example: `"h"`</span></span>
* <span data-ttu-id="457d1-1423">Second exmaple: `0`</span><span class="sxs-lookup"><span data-stu-id="457d1-1423">Second exmaple: `0`</span></span>

<a name="float"></a>

### <a name="float"></a><span data-ttu-id="457d1-1424">float</span><span class="sxs-lookup"><span data-stu-id="457d1-1424">float</span></span>

<span data-ttu-id="457d1-1425">Convert a string version for a floating-point number to an actual floating point number.</span><span class="sxs-lookup"><span data-stu-id="457d1-1425">Convert a string version for a floating-point number to an actual floating point number.</span></span> <span data-ttu-id="457d1-1426">You can use this function only when passing custom parameters to an app, such as a logic app.</span><span class="sxs-lookup"><span data-stu-id="457d1-1426">You can use this function only when passing custom parameters to an app, such as a logic app.</span></span>

```
float('<value>')
```

| <span data-ttu-id="457d1-1427">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1427">Parameter</span></span> | <span data-ttu-id="457d1-1428">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1428">Required</span></span> | <span data-ttu-id="457d1-1429">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1429">Type</span></span> | <span data-ttu-id="457d1-1430">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1430">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1431"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1431"><*value*></span></span> | <span data-ttu-id="457d1-1432">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1432">Yes</span></span> | <span data-ttu-id="457d1-1433">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1433">String</span></span> | <span data-ttu-id="457d1-1434">The string that has a valid floating-point number to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1434">The string that has a valid floating-point number to convert</span></span> |
||||| 

| <span data-ttu-id="457d1-1435">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1435">Return value</span></span> | <span data-ttu-id="457d1-1436">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1436">Type</span></span> | <span data-ttu-id="457d1-1437">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1437">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1438"><*float-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1438"><*float-value*></span></span> | <span data-ttu-id="457d1-1439">Float</span><span class="sxs-lookup"><span data-stu-id="457d1-1439">Float</span></span> | <span data-ttu-id="457d1-1440">The floating-point number for the specified string</span><span class="sxs-lookup"><span data-stu-id="457d1-1440">The floating-point number for the specified string</span></span> | 
|||| 

<span data-ttu-id="457d1-1441">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1441">*Example*</span></span>

<span data-ttu-id="457d1-1442">This example creates a string version for this floating-point number:</span><span class="sxs-lookup"><span data-stu-id="457d1-1442">This example creates a string version for this floating-point number:</span></span>

```
float('10.333')
```

<span data-ttu-id="457d1-1443">And returns this result: `10.333`</span><span class="sxs-lookup"><span data-stu-id="457d1-1443">And returns this result: `10.333`</span></span>

<a name="formatDateTime"></a>

### <a name="formatdatetime"></a><span data-ttu-id="457d1-1444">formatDateTime</span><span class="sxs-lookup"><span data-stu-id="457d1-1444">formatDateTime</span></span>

<span data-ttu-id="457d1-1445">Return a timestamp in the specified format.</span><span class="sxs-lookup"><span data-stu-id="457d1-1445">Return a timestamp in the specified format.</span></span>

```
formatDateTime('<timestamp>', '<format>'?)
```

| <span data-ttu-id="457d1-1446">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1446">Parameter</span></span> | <span data-ttu-id="457d1-1447">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1447">Required</span></span> | <span data-ttu-id="457d1-1448">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1448">Type</span></span> | <span data-ttu-id="457d1-1449">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1449">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1450"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1450"><*timestamp*></span></span> | <span data-ttu-id="457d1-1451">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1451">Yes</span></span> | <span data-ttu-id="457d1-1452">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1452">String</span></span> | <span data-ttu-id="457d1-1453">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-1453">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-1454"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1454"><*format*></span></span> | <span data-ttu-id="457d1-1455">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1455">No</span></span> | <span data-ttu-id="457d1-1456">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1456">String</span></span> | <span data-ttu-id="457d1-1457">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1457">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1458">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1458">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-1459">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1459">Return value</span></span> | <span data-ttu-id="457d1-1460">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1460">Type</span></span> | <span data-ttu-id="457d1-1461">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1461">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1462"><*reformatted-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1462"><*reformatted-timestamp*></span></span> | <span data-ttu-id="457d1-1463">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1463">String</span></span> | <span data-ttu-id="457d1-1464">The updated timestamp in the specified format</span><span class="sxs-lookup"><span data-stu-id="457d1-1464">The updated timestamp in the specified format</span></span> | 
|||| 

<span data-ttu-id="457d1-1465">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1465">*Example*</span></span>

<span data-ttu-id="457d1-1466">This example converts a timestamp to the specified format:</span><span class="sxs-lookup"><span data-stu-id="457d1-1466">This example converts a timestamp to the specified format:</span></span>

```
formatDateTime('03/15/2018 12:00:00', 'yyyy-MM-ddTHH:mm:ss')
```

<span data-ttu-id="457d1-1467">And returns this result: `"2018-03-15T12:00:00"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1467">And returns this result: `"2018-03-15T12:00:00"`</span></span>

<a name="formDataMultiValues"></a>

### <a name="formdatamultivalues"></a><span data-ttu-id="457d1-1468">formDataMultiValues</span><span class="sxs-lookup"><span data-stu-id="457d1-1468">formDataMultiValues</span></span>

<span data-ttu-id="457d1-1469">Return an array with values that match a key name in an action's *form-data* or *form-encoded* output.</span><span class="sxs-lookup"><span data-stu-id="457d1-1469">Return an array with values that match a key name in an action's *form-data* or *form-encoded* output.</span></span> 

```
formDataMultiValues('<actionName>', '<key>')
```

| <span data-ttu-id="457d1-1470">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1470">Parameter</span></span> | <span data-ttu-id="457d1-1471">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1471">Required</span></span> | <span data-ttu-id="457d1-1472">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1472">Type</span></span> | <span data-ttu-id="457d1-1473">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1473">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1474"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-1474"><*actionName*></span></span> | <span data-ttu-id="457d1-1475">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1475">Yes</span></span> | <span data-ttu-id="457d1-1476">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1476">String</span></span> | <span data-ttu-id="457d1-1477">The action whose output has the key value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-1477">The action whose output has the key value you want</span></span> | 
| <span data-ttu-id="457d1-1478"><*key*></span><span class="sxs-lookup"><span data-stu-id="457d1-1478"><*key*></span></span> | <span data-ttu-id="457d1-1479">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1479">Yes</span></span> | <span data-ttu-id="457d1-1480">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1480">String</span></span> | <span data-ttu-id="457d1-1481">The name for the key whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-1481">The name for the key whose value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-1482">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1482">Return value</span></span> | <span data-ttu-id="457d1-1483">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1483">Type</span></span> | <span data-ttu-id="457d1-1484">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1484">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1485">[<*array-with-key-values*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-1485">[<*array-with-key-values*>]</span></span> | <span data-ttu-id="457d1-1486">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1486">Array</span></span> | <span data-ttu-id="457d1-1487">An array with all the values that match the specified key</span><span class="sxs-lookup"><span data-stu-id="457d1-1487">An array with all the values that match the specified key</span></span> | 
|||| 

<span data-ttu-id="457d1-1488">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1488">*Example*</span></span> 

<span data-ttu-id="457d1-1489">This example creates an array from the "Subject" key's value in the specified action's form-data or form-encoded output:</span><span class="sxs-lookup"><span data-stu-id="457d1-1489">This example creates an array from the "Subject" key's value in the specified action's form-data or form-encoded output:</span></span>  

```
formDataMultiValues('Send_an_email', 'Subject')
```

<span data-ttu-id="457d1-1490">And returns the subject text in an array, for example: `["Hello world"]`</span><span class="sxs-lookup"><span data-stu-id="457d1-1490">And returns the subject text in an array, for example: `["Hello world"]`</span></span>

<a name="formDataValue"></a>

### <a name="formdatavalue"></a><span data-ttu-id="457d1-1491">formDataValue</span><span class="sxs-lookup"><span data-stu-id="457d1-1491">formDataValue</span></span>

<span data-ttu-id="457d1-1492">Return a single value that matches a key name in an action's *form-data* or *form-encoded* output.</span><span class="sxs-lookup"><span data-stu-id="457d1-1492">Return a single value that matches a key name in an action's *form-data* or *form-encoded* output.</span></span> <span data-ttu-id="457d1-1493">If the function finds more than one match, the function throws an error.</span><span class="sxs-lookup"><span data-stu-id="457d1-1493">If the function finds more than one match, the function throws an error.</span></span>

```
formDataValue('<actionName>', '<key>')
```

| <span data-ttu-id="457d1-1494">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1494">Parameter</span></span> | <span data-ttu-id="457d1-1495">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1495">Required</span></span> | <span data-ttu-id="457d1-1496">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1496">Type</span></span> | <span data-ttu-id="457d1-1497">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1497">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1498"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-1498"><*actionName*></span></span> | <span data-ttu-id="457d1-1499">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1499">Yes</span></span> | <span data-ttu-id="457d1-1500">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1500">String</span></span> | <span data-ttu-id="457d1-1501">The action whose output has the key value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-1501">The action whose output has the key value you want</span></span> | 
| <span data-ttu-id="457d1-1502"><*key*></span><span class="sxs-lookup"><span data-stu-id="457d1-1502"><*key*></span></span> | <span data-ttu-id="457d1-1503">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1503">Yes</span></span> | <span data-ttu-id="457d1-1504">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1504">String</span></span> | <span data-ttu-id="457d1-1505">The name for the key whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-1505">The name for the key whose value you want</span></span> |
||||| 

| <span data-ttu-id="457d1-1506">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1506">Return value</span></span> | <span data-ttu-id="457d1-1507">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1507">Type</span></span> | <span data-ttu-id="457d1-1508">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1508">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1509"><*key-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1509"><*key-value*></span></span> | <span data-ttu-id="457d1-1510">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1510">String</span></span> | <span data-ttu-id="457d1-1511">The value in the specified key</span><span class="sxs-lookup"><span data-stu-id="457d1-1511">The value in the specified key</span></span>  | 
|||| 

<span data-ttu-id="457d1-1512">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1512">*Example*</span></span> 

<span data-ttu-id="457d1-1513">This example creates a string from the "Subject" key's value in the specified action's form-data or form-encoded output:</span><span class="sxs-lookup"><span data-stu-id="457d1-1513">This example creates a string from the "Subject" key's value in the specified action's form-data or form-encoded output:</span></span>  

```
formDataValue('Send_an_email', 'Subject')
```

<span data-ttu-id="457d1-1514">And returns the subject text as a string, for example: `"Hello world"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1514">And returns the subject text as a string, for example: `"Hello world"`</span></span>

<a name="getFutureTime"></a>

### <a name="getfuturetime"></a><span data-ttu-id="457d1-1515">getFutureTime</span><span class="sxs-lookup"><span data-stu-id="457d1-1515">getFutureTime</span></span>

<span data-ttu-id="457d1-1516">Return the current timestamp plus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="457d1-1516">Return the current timestamp plus the specified time units.</span></span>

```
getFutureTime(<interval>, <timeUnit>, <format>?)
```

| <span data-ttu-id="457d1-1517">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1517">Parameter</span></span> | <span data-ttu-id="457d1-1518">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1518">Required</span></span> | <span data-ttu-id="457d1-1519">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1519">Type</span></span> | <span data-ttu-id="457d1-1520">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1520">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1521"><*interval*></span><span class="sxs-lookup"><span data-stu-id="457d1-1521"><*interval*></span></span> | <span data-ttu-id="457d1-1522">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1522">Yes</span></span> | <span data-ttu-id="457d1-1523">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1523">Integer</span></span> | <span data-ttu-id="457d1-1524">The number of specified time units to subtract</span><span class="sxs-lookup"><span data-stu-id="457d1-1524">The number of specified time units to subtract</span></span> | 
| <span data-ttu-id="457d1-1525"><*timeUnit*></span><span class="sxs-lookup"><span data-stu-id="457d1-1525"><*timeUnit*></span></span> | <span data-ttu-id="457d1-1526">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1526">Yes</span></span> | <span data-ttu-id="457d1-1527">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1527">String</span></span> | <span data-ttu-id="457d1-1528">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span><span class="sxs-lookup"><span data-stu-id="457d1-1528">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span></span> | 
| <span data-ttu-id="457d1-1529"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1529"><*format*></span></span> | <span data-ttu-id="457d1-1530">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1530">No</span></span> | <span data-ttu-id="457d1-1531">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1531">String</span></span> | <span data-ttu-id="457d1-1532">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1532">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1533">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1533">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> | 
||||| 

| <span data-ttu-id="457d1-1534">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1534">Return value</span></span> | <span data-ttu-id="457d1-1535">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1535">Type</span></span> | <span data-ttu-id="457d1-1536">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1536">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1537"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1537"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-1538">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1538">String</span></span> | <span data-ttu-id="457d1-1539">The current timestamp plus the specified number of time units</span><span class="sxs-lookup"><span data-stu-id="457d1-1539">The current timestamp plus the specified number of time units</span></span> | 
|||| 

<span data-ttu-id="457d1-1540">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1540">*Example 1*</span></span>

<span data-ttu-id="457d1-1541">Suppose the current timestamp is "2018-03-01T00:00:00.0000000Z".</span><span class="sxs-lookup"><span data-stu-id="457d1-1541">Suppose the current timestamp is "2018-03-01T00:00:00.0000000Z".</span></span> <span data-ttu-id="457d1-1542">This example adds five days to that timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-1542">This example adds five days to that timestamp:</span></span>

```
getFutureTime(5, 'Day')
```

<span data-ttu-id="457d1-1543">And returns this result: `"2018-03-06T00:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1543">And returns this result: `"2018-03-06T00:00:00.0000000Z"`</span></span>

<span data-ttu-id="457d1-1544">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1544">*Example 2*</span></span>

<span data-ttu-id="457d1-1545">Suppose the current timestamp is "2018-03-01T00:00:00.0000000Z".</span><span class="sxs-lookup"><span data-stu-id="457d1-1545">Suppose the current timestamp is "2018-03-01T00:00:00.0000000Z".</span></span> <span data-ttu-id="457d1-1546">This example adds five days and converts the result to "D" format:</span><span class="sxs-lookup"><span data-stu-id="457d1-1546">This example adds five days and converts the result to "D" format:</span></span>

```
getFutureTime(5, 'Day', 'D')
```

<span data-ttu-id="457d1-1547">And returns this result: `"Tuesday, March 6, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1547">And returns this result: `"Tuesday, March 6, 2018"`</span></span>

<a name="getPastTime"></a>

### <a name="getpasttime"></a><span data-ttu-id="457d1-1548">getPastTime</span><span class="sxs-lookup"><span data-stu-id="457d1-1548">getPastTime</span></span>

<span data-ttu-id="457d1-1549">Return the current timestamp minus the specified time units.</span><span class="sxs-lookup"><span data-stu-id="457d1-1549">Return the current timestamp minus the specified time units.</span></span>

```
getPastTime(<interval>, <timeUnit>, <format>?)
```

| <span data-ttu-id="457d1-1550">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1550">Parameter</span></span> | <span data-ttu-id="457d1-1551">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1551">Required</span></span> | <span data-ttu-id="457d1-1552">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1552">Type</span></span> | <span data-ttu-id="457d1-1553">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1553">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1554"><*interval*></span><span class="sxs-lookup"><span data-stu-id="457d1-1554"><*interval*></span></span> | <span data-ttu-id="457d1-1555">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1555">Yes</span></span> | <span data-ttu-id="457d1-1556">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1556">Integer</span></span> | <span data-ttu-id="457d1-1557">The number of specified time units to subtract</span><span class="sxs-lookup"><span data-stu-id="457d1-1557">The number of specified time units to subtract</span></span> | 
| <span data-ttu-id="457d1-1558"><*timeUnit*></span><span class="sxs-lookup"><span data-stu-id="457d1-1558"><*timeUnit*></span></span> | <span data-ttu-id="457d1-1559">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1559">Yes</span></span> | <span data-ttu-id="457d1-1560">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1560">String</span></span> | <span data-ttu-id="457d1-1561">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span><span class="sxs-lookup"><span data-stu-id="457d1-1561">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span></span> | 
| <span data-ttu-id="457d1-1562"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1562"><*format*></span></span> | <span data-ttu-id="457d1-1563">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1563">No</span></span> | <span data-ttu-id="457d1-1564">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1564">String</span></span> | <span data-ttu-id="457d1-1565">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-1565">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-1566">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-1566">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> | 
||||| 

| <span data-ttu-id="457d1-1567">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1567">Return value</span></span> | <span data-ttu-id="457d1-1568">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1568">Type</span></span> | <span data-ttu-id="457d1-1569">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1569">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1570"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-1570"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-1571">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1571">String</span></span> | <span data-ttu-id="457d1-1572">The current timestamp minus the specified number of time units</span><span class="sxs-lookup"><span data-stu-id="457d1-1572">The current timestamp minus the specified number of time units</span></span> | 
|||| 

<span data-ttu-id="457d1-1573">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1573">*Example 1*</span></span>

<span data-ttu-id="457d1-1574">Suppose the current timestamp is "2018-02-01T00:00:00.0000000Z".</span><span class="sxs-lookup"><span data-stu-id="457d1-1574">Suppose the current timestamp is "2018-02-01T00:00:00.0000000Z".</span></span> <span data-ttu-id="457d1-1575">This example subtracts five days from that timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-1575">This example subtracts five days from that timestamp:</span></span>

```
getPastTime(5, 'Day')
```

<span data-ttu-id="457d1-1576">And returns this result: `"2018-01-27T00:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1576">And returns this result: `"2018-01-27T00:00:00.0000000Z"`</span></span>

<span data-ttu-id="457d1-1577">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1577">*Example 2*</span></span>

<span data-ttu-id="457d1-1578">Suppose the current timestamp is "2018-02-01T00:00:00.0000000Z".</span><span class="sxs-lookup"><span data-stu-id="457d1-1578">Suppose the current timestamp is "2018-02-01T00:00:00.0000000Z".</span></span> <span data-ttu-id="457d1-1579">This example subtracts five days and converts the result to "D" format:</span><span class="sxs-lookup"><span data-stu-id="457d1-1579">This example subtracts five days and converts the result to "D" format:</span></span>

```
getPastTime(5, 'Day', 'D')
```

<span data-ttu-id="457d1-1580">And returns this result: `"Saturday, January 27, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1580">And returns this result: `"Saturday, January 27, 2018"`</span></span>

<a name="greater"></a>

### <a name="greater"></a><span data-ttu-id="457d1-1581">greater</span><span class="sxs-lookup"><span data-stu-id="457d1-1581">greater</span></span>

<span data-ttu-id="457d1-1582">Check whether the first value is greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1582">Check whether the first value is greater than the second value.</span></span> <span data-ttu-id="457d1-1583">Return true when the first value is more, or return false when less.</span><span class="sxs-lookup"><span data-stu-id="457d1-1583">Return true when the first value is more, or return false when less.</span></span>

```
greater(<value>, <compareTo>)
greater('<value>', '<compareTo>')
```

| <span data-ttu-id="457d1-1584">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1584">Parameter</span></span> | <span data-ttu-id="457d1-1585">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1585">Required</span></span> | <span data-ttu-id="457d1-1586">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1586">Type</span></span> | <span data-ttu-id="457d1-1587">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1587">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1588"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1588"><*value*></span></span> | <span data-ttu-id="457d1-1589">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1589">Yes</span></span> | <span data-ttu-id="457d1-1590">Integer, Float, or String</span><span class="sxs-lookup"><span data-stu-id="457d1-1590">Integer, Float, or String</span></span> | <span data-ttu-id="457d1-1591">The first value to check whether greater than the second value</span><span class="sxs-lookup"><span data-stu-id="457d1-1591">The first value to check whether greater than the second value</span></span> | 
| <span data-ttu-id="457d1-1592"><*compareTo*></span><span class="sxs-lookup"><span data-stu-id="457d1-1592"><*compareTo*></span></span> | <span data-ttu-id="457d1-1593">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1593">Yes</span></span> | <span data-ttu-id="457d1-1594">Integer, Float, or String, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1594">Integer, Float, or String, respectively</span></span> | <span data-ttu-id="457d1-1595">The comparison value</span><span class="sxs-lookup"><span data-stu-id="457d1-1595">The comparison value</span></span> | 
||||| 

| <span data-ttu-id="457d1-1596">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1596">Return value</span></span> | <span data-ttu-id="457d1-1597">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1597">Type</span></span> | <span data-ttu-id="457d1-1598">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1598">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1599">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1599">true or false</span></span> | <span data-ttu-id="457d1-1600">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1600">Boolean</span></span> | <span data-ttu-id="457d1-1601">Return true when the first value is greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1601">Return true when the first value is greater than the second value.</span></span> <span data-ttu-id="457d1-1602">Return false when the first value is equal to or less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1602">Return false when the first value is equal to or less than the second value.</span></span> | 
|||| 

<span data-ttu-id="457d1-1603">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1603">*Example*</span></span>

<span data-ttu-id="457d1-1604">These examples check whether the first value is greater than the second value:</span><span class="sxs-lookup"><span data-stu-id="457d1-1604">These examples check whether the first value is greater than the second value:</span></span>

```
greater(10, 5)
greater('apple', 'banana')
```

<span data-ttu-id="457d1-1605">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1605">And return these results:</span></span> 

* <span data-ttu-id="457d1-1606">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-1606">First example: `true`</span></span>
* <span data-ttu-id="457d1-1607">Second example: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-1607">Second example: `false`</span></span>

<a name="greaterOrEquals"></a>

### <a name="greaterorequals"></a><span data-ttu-id="457d1-1608">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="457d1-1608">greaterOrEquals</span></span>

<span data-ttu-id="457d1-1609">Check whether the first value is greater than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1609">Check whether the first value is greater than or equal to the second value.</span></span>
<span data-ttu-id="457d1-1610">Return true when the first value is greater or equal, or return false when the first value is less.</span><span class="sxs-lookup"><span data-stu-id="457d1-1610">Return true when the first value is greater or equal, or return false when the first value is less.</span></span>

```
greaterOrEquals(<value>, <compareTo>)
greaterOrEquals('<value>', '<compareTo>')
```

| <span data-ttu-id="457d1-1611">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1611">Parameter</span></span> | <span data-ttu-id="457d1-1612">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1612">Required</span></span> | <span data-ttu-id="457d1-1613">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1613">Type</span></span> | <span data-ttu-id="457d1-1614">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1614">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1615"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1615"><*value*></span></span> | <span data-ttu-id="457d1-1616">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1616">Yes</span></span> | <span data-ttu-id="457d1-1617">Integer, Float, or String</span><span class="sxs-lookup"><span data-stu-id="457d1-1617">Integer, Float, or String</span></span> | <span data-ttu-id="457d1-1618">The first value to check whether greater than or equal to the second value</span><span class="sxs-lookup"><span data-stu-id="457d1-1618">The first value to check whether greater than or equal to the second value</span></span> | 
| <span data-ttu-id="457d1-1619"><*compareTo*></span><span class="sxs-lookup"><span data-stu-id="457d1-1619"><*compareTo*></span></span> | <span data-ttu-id="457d1-1620">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1620">Yes</span></span> | <span data-ttu-id="457d1-1621">Integer, Float, or String, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1621">Integer, Float, or String, respectively</span></span> | <span data-ttu-id="457d1-1622">The comparison value</span><span class="sxs-lookup"><span data-stu-id="457d1-1622">The comparison value</span></span> | 
||||| 

| <span data-ttu-id="457d1-1623">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1623">Return value</span></span> | <span data-ttu-id="457d1-1624">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1624">Type</span></span> | <span data-ttu-id="457d1-1625">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1625">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1626">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1626">true or false</span></span> | <span data-ttu-id="457d1-1627">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1627">Boolean</span></span> | <span data-ttu-id="457d1-1628">Return true when the first value is greater than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1628">Return true when the first value is greater than or equal to the second value.</span></span> <span data-ttu-id="457d1-1629">Return false when the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1629">Return false when the first value is less than the second value.</span></span> | 
|||| 

<span data-ttu-id="457d1-1630">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1630">*Example*</span></span>

<span data-ttu-id="457d1-1631">These examples check whether the first value is greater or equal than the second value:</span><span class="sxs-lookup"><span data-stu-id="457d1-1631">These examples check whether the first value is greater or equal than the second value:</span></span>

```
greaterOrEquals(5, 5)
greaterOrEquals('apple', 'banana')
```

<span data-ttu-id="457d1-1632">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1632">And return these results:</span></span> 

* <span data-ttu-id="457d1-1633">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-1633">First example: `true`</span></span>
* <span data-ttu-id="457d1-1634">Second example: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-1634">Second example: `false`</span></span>

<a name="guid"></a>

### <a name="guid"></a><span data-ttu-id="457d1-1635">guid</span><span class="sxs-lookup"><span data-stu-id="457d1-1635">guid</span></span>

<span data-ttu-id="457d1-1636">Generate a globally unique identifier (GUID) as a string, for example, "c2ecc88d-88c8-4096-912c-d6f2e2b138ce":</span><span class="sxs-lookup"><span data-stu-id="457d1-1636">Generate a globally unique identifier (GUID) as a string, for example, "c2ecc88d-88c8-4096-912c-d6f2e2b138ce":</span></span> 

```
guid()
```

<span data-ttu-id="457d1-1637">Also, you can specify a different format for the GUID other than the default format, "D", which is 32 digits separated by hyphens.</span><span class="sxs-lookup"><span data-stu-id="457d1-1637">Also, you can specify a different format for the GUID other than the default format, "D", which is 32 digits separated by hyphens.</span></span>

```
guid('<format>')
```

| <span data-ttu-id="457d1-1638">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1638">Parameter</span></span> | <span data-ttu-id="457d1-1639">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1639">Required</span></span> | <span data-ttu-id="457d1-1640">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1640">Type</span></span> | <span data-ttu-id="457d1-1641">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1641">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1642"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-1642"><*format*></span></span> | <span data-ttu-id="457d1-1643">No</span><span class="sxs-lookup"><span data-stu-id="457d1-1643">No</span></span> | <span data-ttu-id="457d1-1644">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1644">String</span></span> | <span data-ttu-id="457d1-1645">A single [format specifier](https://msdn.microsoft.com/library/97af8hh4) for the returned GUID.</span><span class="sxs-lookup"><span data-stu-id="457d1-1645">A single [format specifier](https://msdn.microsoft.com/library/97af8hh4) for the returned GUID.</span></span> <span data-ttu-id="457d1-1646">By default, the format is "D", but you can use "N", "D", "B", "P", or "X".</span><span class="sxs-lookup"><span data-stu-id="457d1-1646">By default, the format is "D", but you can use "N", "D", "B", "P", or "X".</span></span> | 
||||| 

| <span data-ttu-id="457d1-1647">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1647">Return value</span></span> | <span data-ttu-id="457d1-1648">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1648">Type</span></span> | <span data-ttu-id="457d1-1649">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1649">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1650"><*GUID-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1650"><*GUID-value*></span></span> | <span data-ttu-id="457d1-1651">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1651">String</span></span> | <span data-ttu-id="457d1-1652">A randomly generated GUID</span><span class="sxs-lookup"><span data-stu-id="457d1-1652">A randomly generated GUID</span></span> | 
|||| 

<span data-ttu-id="457d1-1653">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1653">*Example*</span></span> 

<span data-ttu-id="457d1-1654">This example generates the same GUID, but as 32 digits, separated by hyphens, and enclosed in parentheses:</span><span class="sxs-lookup"><span data-stu-id="457d1-1654">This example generates the same GUID, but as 32 digits, separated by hyphens, and enclosed in parentheses:</span></span> 

```
guid('P')
```

<span data-ttu-id="457d1-1655">And returns this result: `"(c2ecc88d-88c8-4096-912c-d6f2e2b138ce)"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1655">And returns this result: `"(c2ecc88d-88c8-4096-912c-d6f2e2b138ce)"`</span></span>

<a name="if"></a>

### <a name="if"></a><span data-ttu-id="457d1-1656">if</span><span class="sxs-lookup"><span data-stu-id="457d1-1656">if</span></span>

<span data-ttu-id="457d1-1657">Check whether an expression is true or false.</span><span class="sxs-lookup"><span data-stu-id="457d1-1657">Check whether an expression is true or false.</span></span> <span data-ttu-id="457d1-1658">Based on the result, return a specified value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1658">Based on the result, return a specified value.</span></span>

```
if(<expression>, <valueIfTrue>, <valueIfFalse>)
```

| <span data-ttu-id="457d1-1659">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1659">Parameter</span></span> | <span data-ttu-id="457d1-1660">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1660">Required</span></span> | <span data-ttu-id="457d1-1661">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1661">Type</span></span> | <span data-ttu-id="457d1-1662">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1662">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1663"><*expression*></span><span class="sxs-lookup"><span data-stu-id="457d1-1663"><*expression*></span></span> | <span data-ttu-id="457d1-1664">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1664">Yes</span></span> | <span data-ttu-id="457d1-1665">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1665">Boolean</span></span> | <span data-ttu-id="457d1-1666">The expression to check</span><span class="sxs-lookup"><span data-stu-id="457d1-1666">The expression to check</span></span> | 
| <span data-ttu-id="457d1-1667"><*valueIfTrue*></span><span class="sxs-lookup"><span data-stu-id="457d1-1667"><*valueIfTrue*></span></span> | <span data-ttu-id="457d1-1668">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1668">Yes</span></span> | <span data-ttu-id="457d1-1669">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1669">Any</span></span> | <span data-ttu-id="457d1-1670">The value to return when the expression is true</span><span class="sxs-lookup"><span data-stu-id="457d1-1670">The value to return when the expression is true</span></span> | 
| <span data-ttu-id="457d1-1671"><*valueIfFalse*></span><span class="sxs-lookup"><span data-stu-id="457d1-1671"><*valueIfFalse*></span></span> | <span data-ttu-id="457d1-1672">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1672">Yes</span></span> | <span data-ttu-id="457d1-1673">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1673">Any</span></span> | <span data-ttu-id="457d1-1674">The value to return when the expression is false</span><span class="sxs-lookup"><span data-stu-id="457d1-1674">The value to return when the expression is false</span></span> | 
||||| 

| <span data-ttu-id="457d1-1675">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1675">Return value</span></span> | <span data-ttu-id="457d1-1676">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1676">Type</span></span> | <span data-ttu-id="457d1-1677">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1677">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1678"><*specified-return-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1678"><*specified-return-value*></span></span> | <span data-ttu-id="457d1-1679">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1679">Any</span></span> | <span data-ttu-id="457d1-1680">The specified value that returns based on whether the expression is true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1680">The specified value that returns based on whether the expression is true or false</span></span> | 
|||| 

<span data-ttu-id="457d1-1681">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1681">*Example*</span></span> 

<span data-ttu-id="457d1-1682">This example returns `"yes"` because the specified expression returns true.</span><span class="sxs-lookup"><span data-stu-id="457d1-1682">This example returns `"yes"` because the specified expression returns true.</span></span> <span data-ttu-id="457d1-1683">Otherwise, the example returns `"no"`:</span><span class="sxs-lookup"><span data-stu-id="457d1-1683">Otherwise, the example returns `"no"`:</span></span>

```
if(equals(1, 1), 'yes', 'no')
```

<a name="indexof"></a>

### <a name="indexof"></a><span data-ttu-id="457d1-1684">indexOf</span><span class="sxs-lookup"><span data-stu-id="457d1-1684">indexOf</span></span>

<span data-ttu-id="457d1-1685">Return the starting position or index value for a substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-1685">Return the starting position or index value for a substring.</span></span> <span data-ttu-id="457d1-1686">This function is not case-sensitive, and indexes start with the number 0.</span><span class="sxs-lookup"><span data-stu-id="457d1-1686">This function is not case-sensitive, and indexes start with the number 0.</span></span> 

```
indexOf('<text>', '<searchText>')
```

| <span data-ttu-id="457d1-1687">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1687">Parameter</span></span> | <span data-ttu-id="457d1-1688">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1688">Required</span></span> | <span data-ttu-id="457d1-1689">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1689">Type</span></span> | <span data-ttu-id="457d1-1690">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1690">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1691"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-1691"><*text*></span></span> | <span data-ttu-id="457d1-1692">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1692">Yes</span></span> | <span data-ttu-id="457d1-1693">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1693">String</span></span> | <span data-ttu-id="457d1-1694">The string that has the substring to find</span><span class="sxs-lookup"><span data-stu-id="457d1-1694">The string that has the substring to find</span></span> | 
| <span data-ttu-id="457d1-1695"><*searchText*></span><span class="sxs-lookup"><span data-stu-id="457d1-1695"><*searchText*></span></span> | <span data-ttu-id="457d1-1696">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1696">Yes</span></span> | <span data-ttu-id="457d1-1697">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1697">String</span></span> | <span data-ttu-id="457d1-1698">The substring to find</span><span class="sxs-lookup"><span data-stu-id="457d1-1698">The substring to find</span></span> | 
||||| 

| <span data-ttu-id="457d1-1699">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1699">Return value</span></span> | <span data-ttu-id="457d1-1700">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1700">Type</span></span> | <span data-ttu-id="457d1-1701">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1701">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1702"><*index-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1702"><*index-value*></span></span>| <span data-ttu-id="457d1-1703">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1703">Integer</span></span> | <span data-ttu-id="457d1-1704">The starting position or index value for the specified substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-1704">The starting position or index value for the specified substring.</span></span> <p><span data-ttu-id="457d1-1705">If the string is not found, return the number -1.</span><span class="sxs-lookup"><span data-stu-id="457d1-1705">If the string is not found, return the number -1.</span></span> | 
|||| 

<span data-ttu-id="457d1-1706">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1706">*Example*</span></span> 

<span data-ttu-id="457d1-1707">This example finds the starting index value for the "world" substring in the "hello world" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1707">This example finds the starting index value for the "world" substring in the "hello world" string:</span></span>

```
indexOf('hello world', 'world')
```

<span data-ttu-id="457d1-1708">And returns this result: `6`</span><span class="sxs-lookup"><span data-stu-id="457d1-1708">And returns this result: `6`</span></span>

<a name="int"></a>

### <a name="int"></a><span data-ttu-id="457d1-1709">int</span><span class="sxs-lookup"><span data-stu-id="457d1-1709">int</span></span>

<span data-ttu-id="457d1-1710">Return the integer version for a string.</span><span class="sxs-lookup"><span data-stu-id="457d1-1710">Return the integer version for a string.</span></span>

```
int('<value>')
```

| <span data-ttu-id="457d1-1711">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1711">Parameter</span></span> | <span data-ttu-id="457d1-1712">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1712">Required</span></span> | <span data-ttu-id="457d1-1713">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1713">Type</span></span> | <span data-ttu-id="457d1-1714">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1714">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1715"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1715"><*value*></span></span> | <span data-ttu-id="457d1-1716">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1716">Yes</span></span> | <span data-ttu-id="457d1-1717">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1717">String</span></span> | <span data-ttu-id="457d1-1718">The string to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1718">The string to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-1719">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1719">Return value</span></span> | <span data-ttu-id="457d1-1720">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1720">Type</span></span> | <span data-ttu-id="457d1-1721">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1721">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1722"><*integer-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-1722"><*integer-result*></span></span> | <span data-ttu-id="457d1-1723">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1723">Integer</span></span> | <span data-ttu-id="457d1-1724">The integer version for the specified string</span><span class="sxs-lookup"><span data-stu-id="457d1-1724">The integer version for the specified string</span></span> | 
|||| 

<span data-ttu-id="457d1-1725">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1725">*Example*</span></span> 

<span data-ttu-id="457d1-1726">This example creates an integer version for the string "10":</span><span class="sxs-lookup"><span data-stu-id="457d1-1726">This example creates an integer version for the string "10":</span></span>

```
int('10')
```

<span data-ttu-id="457d1-1727">And returns this result: `10`</span><span class="sxs-lookup"><span data-stu-id="457d1-1727">And returns this result: `10`</span></span>

<a name="item"></a>

### <a name="item"></a><span data-ttu-id="457d1-1728">item</span><span class="sxs-lookup"><span data-stu-id="457d1-1728">item</span></span>

<span data-ttu-id="457d1-1729">When used inside a repeating action over an array, return the current item in the array during the action's current iteration.</span><span class="sxs-lookup"><span data-stu-id="457d1-1729">When used inside a repeating action over an array, return the current item in the array during the action's current iteration.</span></span> <span data-ttu-id="457d1-1730">You can also get the values from that item's properties.</span><span class="sxs-lookup"><span data-stu-id="457d1-1730">You can also get the values from that item's properties.</span></span> 

```
item()
```

| <span data-ttu-id="457d1-1731">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1731">Return value</span></span> | <span data-ttu-id="457d1-1732">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1732">Type</span></span> | <span data-ttu-id="457d1-1733">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1733">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1734"><*current-array-item*></span><span class="sxs-lookup"><span data-stu-id="457d1-1734"><*current-array-item*></span></span> | <span data-ttu-id="457d1-1735">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1735">Any</span></span> | <span data-ttu-id="457d1-1736">The current item in the array for the action's current iteration</span><span class="sxs-lookup"><span data-stu-id="457d1-1736">The current item in the array for the action's current iteration</span></span> | 
|||| 

<span data-ttu-id="457d1-1737">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1737">*Example*</span></span> 

<span data-ttu-id="457d1-1738">This example gets the `body` element from the current message for the "Send_an_email" action inside a for-each loop's current iteration:</span><span class="sxs-lookup"><span data-stu-id="457d1-1738">This example gets the `body` element from the current message for the "Send_an_email" action inside a for-each loop's current iteration:</span></span>

```
item().body
```

<a name="items"></a>

### <a name="items"></a><span data-ttu-id="457d1-1739">items</span><span class="sxs-lookup"><span data-stu-id="457d1-1739">items</span></span>

<span data-ttu-id="457d1-1740">Return the current item from each cycle in a for-each loop.</span><span class="sxs-lookup"><span data-stu-id="457d1-1740">Return the current item from each cycle in a for-each loop.</span></span> <span data-ttu-id="457d1-1741">Use this function inside the for-each loop.</span><span class="sxs-lookup"><span data-stu-id="457d1-1741">Use this function inside the for-each loop.</span></span>

```
items('<loopName>')
```

| <span data-ttu-id="457d1-1742">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1742">Parameter</span></span> | <span data-ttu-id="457d1-1743">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1743">Required</span></span> | <span data-ttu-id="457d1-1744">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1744">Type</span></span> | <span data-ttu-id="457d1-1745">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1745">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1746"><*loopName*></span><span class="sxs-lookup"><span data-stu-id="457d1-1746"><*loopName*></span></span> | <span data-ttu-id="457d1-1747">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1747">Yes</span></span> | <span data-ttu-id="457d1-1748">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1748">String</span></span> | <span data-ttu-id="457d1-1749">The name for the for-each loop</span><span class="sxs-lookup"><span data-stu-id="457d1-1749">The name for the for-each loop</span></span> | 
||||| 

| <span data-ttu-id="457d1-1750">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1750">Return value</span></span> | <span data-ttu-id="457d1-1751">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1751">Type</span></span> | <span data-ttu-id="457d1-1752">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1752">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1753"><*item*></span><span class="sxs-lookup"><span data-stu-id="457d1-1753"><*item*></span></span> | <span data-ttu-id="457d1-1754">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-1754">Any</span></span> | <span data-ttu-id="457d1-1755">The item from the current cycle in the specified for-each loop</span><span class="sxs-lookup"><span data-stu-id="457d1-1755">The item from the current cycle in the specified for-each loop</span></span> | 
|||| 

<span data-ttu-id="457d1-1756">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1756">*Example*</span></span> 

<span data-ttu-id="457d1-1757">This example gets the current item from the specified for-each loop:</span><span class="sxs-lookup"><span data-stu-id="457d1-1757">This example gets the current item from the specified for-each loop:</span></span>

```
items('myForEachLoopName')
```

<a name="json"></a>

### <a name="json"></a><span data-ttu-id="457d1-1758">json</span><span class="sxs-lookup"><span data-stu-id="457d1-1758">json</span></span>

<span data-ttu-id="457d1-1759">Return the JavaScript Object Notation (JSON) type value or object for a string or XML.</span><span class="sxs-lookup"><span data-stu-id="457d1-1759">Return the JavaScript Object Notation (JSON) type value or object for a string or XML.</span></span>

```
json('<value>')
```

| <span data-ttu-id="457d1-1760">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1760">Parameter</span></span> | <span data-ttu-id="457d1-1761">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1761">Required</span></span> | <span data-ttu-id="457d1-1762">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1762">Type</span></span> | <span data-ttu-id="457d1-1763">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1763">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1764"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1764"><*value*></span></span> | <span data-ttu-id="457d1-1765">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1765">Yes</span></span> | <span data-ttu-id="457d1-1766">String or XML</span><span class="sxs-lookup"><span data-stu-id="457d1-1766">String or XML</span></span> | <span data-ttu-id="457d1-1767">The string or XML to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-1767">The string or XML to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-1768">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1768">Return value</span></span> | <span data-ttu-id="457d1-1769">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1769">Type</span></span> | <span data-ttu-id="457d1-1770">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1770">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1771"><*JSON-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-1771"><*JSON-result*></span></span> | <span data-ttu-id="457d1-1772">JSON native type or object</span><span class="sxs-lookup"><span data-stu-id="457d1-1772">JSON native type or object</span></span> | <span data-ttu-id="457d1-1773">The JSON native type value or object for the specified string or XML.</span><span class="sxs-lookup"><span data-stu-id="457d1-1773">The JSON native type value or object for the specified string or XML.</span></span> <span data-ttu-id="457d1-1774">If the string is null, the function returns an empty object.</span><span class="sxs-lookup"><span data-stu-id="457d1-1774">If the string is null, the function returns an empty object.</span></span> | 
|||| 

<span data-ttu-id="457d1-1775">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-1775">*Example 1*</span></span> 

<span data-ttu-id="457d1-1776">This example converts this string to the JSON value:</span><span class="sxs-lookup"><span data-stu-id="457d1-1776">This example converts this string to the JSON value:</span></span>

```
json('[1, 2, 3]')
```

<span data-ttu-id="457d1-1777">And returns this result: `[1, 2, 3]`</span><span class="sxs-lookup"><span data-stu-id="457d1-1777">And returns this result: `[1, 2, 3]`</span></span>

<span data-ttu-id="457d1-1778">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-1778">*Example 2*</span></span>

<span data-ttu-id="457d1-1779">This example converts this string to JSON:</span><span class="sxs-lookup"><span data-stu-id="457d1-1779">This example converts this string to JSON:</span></span> 

```
json('{"fullName": "Sophia Owen"}')
```

<span data-ttu-id="457d1-1780">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-1780">And returns this result:</span></span>

```
{
  "fullName": "Sophia Owen"
}
```

<span data-ttu-id="457d1-1781">*Example 3*</span><span class="sxs-lookup"><span data-stu-id="457d1-1781">*Example 3*</span></span>

<span data-ttu-id="457d1-1782">This example converts this XML to JSON:</span><span class="sxs-lookup"><span data-stu-id="457d1-1782">This example converts this XML to JSON:</span></span> 

```
json(xml('<?xml version="1.0"?> <root> <person id='1'> <name>Sophia Owen</name> <occupation>Engineer</occupation> </person> </root>'))
```

<span data-ttu-id="457d1-1783">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-1783">And returns this result:</span></span>

```json
{ 
   "?xml": { "@version": "1.0" }, 
   "root": { 
      "person": [ { 
         "@id": "1", 
         "name": "Sophia Owen", 
         "occupation": "Engineer" 
       } ] 
   } 
}
```

<a name="intersection"></a>

### <a name="intersection"></a><span data-ttu-id="457d1-1784">intersection</span><span class="sxs-lookup"><span data-stu-id="457d1-1784">intersection</span></span>

<span data-ttu-id="457d1-1785">Return a collection that has *only* the common items across the specified collections.</span><span class="sxs-lookup"><span data-stu-id="457d1-1785">Return a collection that has *only* the common items across the specified collections.</span></span> <span data-ttu-id="457d1-1786">To appear in the result, an item must appear in all the collections passed to this function.</span><span class="sxs-lookup"><span data-stu-id="457d1-1786">To appear in the result, an item must appear in all the collections passed to this function.</span></span> <span data-ttu-id="457d1-1787">If one or more items have the same name, the last item with that name appears in the result.</span><span class="sxs-lookup"><span data-stu-id="457d1-1787">If one or more items have the same name, the last item with that name appears in the result.</span></span>

```
intersection([<collection1>], [<collection2>], ...)
intersection('<collection1>', '<collection2>', ...)
```

| <span data-ttu-id="457d1-1788">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1788">Parameter</span></span> | <span data-ttu-id="457d1-1789">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1789">Required</span></span> | <span data-ttu-id="457d1-1790">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1790">Type</span></span> | <span data-ttu-id="457d1-1791">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1791">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1792"><*collection1*>, <*collection2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-1792"><*collection1*>, <*collection2*>, ...</span></span> | <span data-ttu-id="457d1-1793">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1793">Yes</span></span> | <span data-ttu-id="457d1-1794">Array or Object, but not both</span><span class="sxs-lookup"><span data-stu-id="457d1-1794">Array or Object, but not both</span></span> | <span data-ttu-id="457d1-1795">The collections from where you want *only* the common items</span><span class="sxs-lookup"><span data-stu-id="457d1-1795">The collections from where you want *only* the common items</span></span> | 
||||| 

| <span data-ttu-id="457d1-1796">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1796">Return value</span></span> | <span data-ttu-id="457d1-1797">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1797">Type</span></span> | <span data-ttu-id="457d1-1798">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1798">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1799"><*common-items*></span><span class="sxs-lookup"><span data-stu-id="457d1-1799"><*common-items*></span></span> | <span data-ttu-id="457d1-1800">Array or Object, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1800">Array or Object, respectively</span></span> | <span data-ttu-id="457d1-1801">A collection that has only the common items across the specified collections</span><span class="sxs-lookup"><span data-stu-id="457d1-1801">A collection that has only the common items across the specified collections</span></span> | 
|||| 

<span data-ttu-id="457d1-1802">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1802">*Example*</span></span> 

<span data-ttu-id="457d1-1803">This example finds the common items across these arrays:</span><span class="sxs-lookup"><span data-stu-id="457d1-1803">This example finds the common items across these arrays:</span></span>  

```
intersection([1, 2, 3], [101, 2, 1, 10], [6, 8, 1, 2])
```

<span data-ttu-id="457d1-1804">And returns an array with *only* these items: `[1, 2]`</span><span class="sxs-lookup"><span data-stu-id="457d1-1804">And returns an array with *only* these items: `[1, 2]`</span></span>

<a name="join"></a>

### <a name="join"></a><span data-ttu-id="457d1-1805">join</span><span class="sxs-lookup"><span data-stu-id="457d1-1805">join</span></span>

<span data-ttu-id="457d1-1806">Return a string that has all the items from an array and has each character separated by a *delimiter*.</span><span class="sxs-lookup"><span data-stu-id="457d1-1806">Return a string that has all the items from an array and has each character separated by a *delimiter*.</span></span>

```
join([<collection>], '<delimiter>')
```

| <span data-ttu-id="457d1-1807">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1807">Parameter</span></span> | <span data-ttu-id="457d1-1808">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1808">Required</span></span> | <span data-ttu-id="457d1-1809">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1809">Type</span></span> | <span data-ttu-id="457d1-1810">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1810">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1811"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-1811"><*collection*></span></span> | <span data-ttu-id="457d1-1812">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1812">Yes</span></span> | <span data-ttu-id="457d1-1813">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1813">Array</span></span> | <span data-ttu-id="457d1-1814">The array that has the items to join</span><span class="sxs-lookup"><span data-stu-id="457d1-1814">The array that has the items to join</span></span> |  
| <span data-ttu-id="457d1-1815"><*delimiter*></span><span class="sxs-lookup"><span data-stu-id="457d1-1815"><*delimiter*></span></span> | <span data-ttu-id="457d1-1816">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1816">Yes</span></span> | <span data-ttu-id="457d1-1817">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1817">String</span></span> | <span data-ttu-id="457d1-1818">The separator that appears between each character in the resulting string</span><span class="sxs-lookup"><span data-stu-id="457d1-1818">The separator that appears between each character in the resulting string</span></span> | 
||||| 

| <span data-ttu-id="457d1-1819">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1819">Return value</span></span> | <span data-ttu-id="457d1-1820">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1820">Type</span></span> | <span data-ttu-id="457d1-1821">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1821">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1822"><*char1*><*delimiter*><*char2*><*delimiter*>...</span><span class="sxs-lookup"><span data-stu-id="457d1-1822"><*char1*><*delimiter*><*char2*><*delimiter*>...</span></span> | <span data-ttu-id="457d1-1823">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1823">String</span></span> | <span data-ttu-id="457d1-1824">The resulting string created from all the items in the specified array</span><span class="sxs-lookup"><span data-stu-id="457d1-1824">The resulting string created from all the items in the specified array</span></span> |
|||| 

<span data-ttu-id="457d1-1825">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1825">*Example*</span></span> 

<span data-ttu-id="457d1-1826">This example creates a string from all the items in this array with the specified character as the delimiter:</span><span class="sxs-lookup"><span data-stu-id="457d1-1826">This example creates a string from all the items in this array with the specified character as the delimiter:</span></span>

```
join([a, b, c], '.')
```

<span data-ttu-id="457d1-1827">And returns this result: `"a.b.c"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1827">And returns this result: `"a.b.c"`</span></span>

<a name="last"></a>

### <a name="last"></a><span data-ttu-id="457d1-1828">last</span><span class="sxs-lookup"><span data-stu-id="457d1-1828">last</span></span>

<span data-ttu-id="457d1-1829">Return the last item from a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-1829">Return the last item from a collection.</span></span>

```
last('<collection>')
last([<collection>])
```

| <span data-ttu-id="457d1-1830">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1830">Parameter</span></span> | <span data-ttu-id="457d1-1831">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1831">Required</span></span> | <span data-ttu-id="457d1-1832">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1832">Type</span></span> | <span data-ttu-id="457d1-1833">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1833">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1834"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-1834"><*collection*></span></span> | <span data-ttu-id="457d1-1835">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1835">Yes</span></span> | <span data-ttu-id="457d1-1836">String or Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1836">String or Array</span></span> | <span data-ttu-id="457d1-1837">The collection where to find the last item</span><span class="sxs-lookup"><span data-stu-id="457d1-1837">The collection where to find the last item</span></span> | 
||||| 

| <span data-ttu-id="457d1-1838">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1838">Return value</span></span> | <span data-ttu-id="457d1-1839">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1839">Type</span></span> | <span data-ttu-id="457d1-1840">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1840">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1841"><*last-collection-item*></span><span class="sxs-lookup"><span data-stu-id="457d1-1841"><*last-collection-item*></span></span> | <span data-ttu-id="457d1-1842">String or Array, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1842">String or Array, respectively</span></span> | <span data-ttu-id="457d1-1843">The last item in the collection</span><span class="sxs-lookup"><span data-stu-id="457d1-1843">The last item in the collection</span></span> | 
|||| 

<span data-ttu-id="457d1-1844">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1844">*Example*</span></span> 

<span data-ttu-id="457d1-1845">These examples find the last item in these collections:</span><span class="sxs-lookup"><span data-stu-id="457d1-1845">These examples find the last item in these collections:</span></span>

```
last('abcd')
last([0, 1, 2, 3])
```

<span data-ttu-id="457d1-1846">And returns these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1846">And returns these results:</span></span> 

* <span data-ttu-id="457d1-1847">First example: `"d"`</span><span class="sxs-lookup"><span data-stu-id="457d1-1847">First example: `"d"`</span></span>
* <span data-ttu-id="457d1-1848">Second example: `3`</span><span class="sxs-lookup"><span data-stu-id="457d1-1848">Second example: `3`</span></span>

<a name="lastindexof"></a>

### <a name="lastindexof"></a><span data-ttu-id="457d1-1849">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="457d1-1849">lastIndexOf</span></span>

<span data-ttu-id="457d1-1850">Return the starting position or index value for the last occurrence of a substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-1850">Return the starting position or index value for the last occurrence of a substring.</span></span> <span data-ttu-id="457d1-1851">This function is not case-sensitive, and indexes start with the number 0.</span><span class="sxs-lookup"><span data-stu-id="457d1-1851">This function is not case-sensitive, and indexes start with the number 0.</span></span>

```
lastIndexOf('<text>', '<searchText>')
```

| <span data-ttu-id="457d1-1852">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1852">Parameter</span></span> | <span data-ttu-id="457d1-1853">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1853">Required</span></span> | <span data-ttu-id="457d1-1854">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1854">Type</span></span> | <span data-ttu-id="457d1-1855">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1855">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1856"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-1856"><*text*></span></span> | <span data-ttu-id="457d1-1857">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1857">Yes</span></span> | <span data-ttu-id="457d1-1858">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1858">String</span></span> | <span data-ttu-id="457d1-1859">The string that has the substring to find</span><span class="sxs-lookup"><span data-stu-id="457d1-1859">The string that has the substring to find</span></span> | 
| <span data-ttu-id="457d1-1860"><*searchText*></span><span class="sxs-lookup"><span data-stu-id="457d1-1860"><*searchText*></span></span> | <span data-ttu-id="457d1-1861">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1861">Yes</span></span> | <span data-ttu-id="457d1-1862">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1862">String</span></span> | <span data-ttu-id="457d1-1863">The substring to find</span><span class="sxs-lookup"><span data-stu-id="457d1-1863">The substring to find</span></span> | 
||||| 

| <span data-ttu-id="457d1-1864">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1864">Return value</span></span> | <span data-ttu-id="457d1-1865">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1865">Type</span></span> | <span data-ttu-id="457d1-1866">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1866">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1867"><*ending-index-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1867"><*ending-index-value*></span></span> | <span data-ttu-id="457d1-1868">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1868">Integer</span></span> | <span data-ttu-id="457d1-1869">The starting position or index value for the last occurrence of the specified substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-1869">The starting position or index value for the last occurrence of the specified substring.</span></span> <p><span data-ttu-id="457d1-1870">If the string is not found, return the number -1.</span><span class="sxs-lookup"><span data-stu-id="457d1-1870">If the string is not found, return the number -1.</span></span> | 
|||| 

<span data-ttu-id="457d1-1871">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1871">*Example*</span></span> 

<span data-ttu-id="457d1-1872">This example finds the starting index value for the last occurrence of the "world" substring in the "hello world" string:</span><span class="sxs-lookup"><span data-stu-id="457d1-1872">This example finds the starting index value for the last occurrence of the "world" substring in the "hello world" string:</span></span>

```
lastIndexOf('hello world', 'world')
```

<span data-ttu-id="457d1-1873">And returns this result: `6`</span><span class="sxs-lookup"><span data-stu-id="457d1-1873">And returns this result: `6`</span></span>

<a name="length"></a>

### <a name="length"></a><span data-ttu-id="457d1-1874">length</span><span class="sxs-lookup"><span data-stu-id="457d1-1874">length</span></span>

<span data-ttu-id="457d1-1875">Return the number of items in a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-1875">Return the number of items in a collection.</span></span>

```
length('<collection>')
length([<collection>])
```

| <span data-ttu-id="457d1-1876">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1876">Parameter</span></span> | <span data-ttu-id="457d1-1877">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1877">Required</span></span> | <span data-ttu-id="457d1-1878">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1878">Type</span></span> | <span data-ttu-id="457d1-1879">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1879">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1880"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-1880"><*collection*></span></span> | <span data-ttu-id="457d1-1881">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1881">Yes</span></span> | <span data-ttu-id="457d1-1882">String or Array</span><span class="sxs-lookup"><span data-stu-id="457d1-1882">String or Array</span></span> | <span data-ttu-id="457d1-1883">The collection with the items to count</span><span class="sxs-lookup"><span data-stu-id="457d1-1883">The collection with the items to count</span></span> | 
||||| 

| <span data-ttu-id="457d1-1884">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1884">Return value</span></span> | <span data-ttu-id="457d1-1885">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1885">Type</span></span> | <span data-ttu-id="457d1-1886">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1886">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1887"><*length-or-count*></span><span class="sxs-lookup"><span data-stu-id="457d1-1887"><*length-or-count*></span></span> | <span data-ttu-id="457d1-1888">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-1888">Integer</span></span> | <span data-ttu-id="457d1-1889">The number of items in the collection</span><span class="sxs-lookup"><span data-stu-id="457d1-1889">The number of items in the collection</span></span> | 
|||| 

<span data-ttu-id="457d1-1890">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1890">*Example*</span></span>

<span data-ttu-id="457d1-1891">These examples count the number of items in these collections:</span><span class="sxs-lookup"><span data-stu-id="457d1-1891">These examples count the number of items in these collections:</span></span> 

```
length('abcd')
length([0, 1, 2, 3])
```

<span data-ttu-id="457d1-1892">And return this result: `4`</span><span class="sxs-lookup"><span data-stu-id="457d1-1892">And return this result: `4`</span></span>

<a name="less"></a>

### <a name="less"></a><span data-ttu-id="457d1-1893">less</span><span class="sxs-lookup"><span data-stu-id="457d1-1893">less</span></span>

<span data-ttu-id="457d1-1894">Check whether the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1894">Check whether the first value is less than the second value.</span></span>
<span data-ttu-id="457d1-1895">Return true when the first value is less, or return false when the first value is more.</span><span class="sxs-lookup"><span data-stu-id="457d1-1895">Return true when the first value is less, or return false when the first value is more.</span></span>

```
less(<value>, <compareTo>)
less('<value>', '<compareTo>')
```

| <span data-ttu-id="457d1-1896">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1896">Parameter</span></span> | <span data-ttu-id="457d1-1897">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1897">Required</span></span> | <span data-ttu-id="457d1-1898">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1898">Type</span></span> | <span data-ttu-id="457d1-1899">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1899">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1900"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1900"><*value*></span></span> | <span data-ttu-id="457d1-1901">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1901">Yes</span></span> | <span data-ttu-id="457d1-1902">Integer, Float, or String</span><span class="sxs-lookup"><span data-stu-id="457d1-1902">Integer, Float, or String</span></span> | <span data-ttu-id="457d1-1903">The first value to check whether less than the second value</span><span class="sxs-lookup"><span data-stu-id="457d1-1903">The first value to check whether less than the second value</span></span> | 
| <span data-ttu-id="457d1-1904"><*compareTo*></span><span class="sxs-lookup"><span data-stu-id="457d1-1904"><*compareTo*></span></span> | <span data-ttu-id="457d1-1905">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1905">Yes</span></span> | <span data-ttu-id="457d1-1906">Integer, Float, or String, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1906">Integer, Float, or String, respectively</span></span> | <span data-ttu-id="457d1-1907">The comparison item</span><span class="sxs-lookup"><span data-stu-id="457d1-1907">The comparison item</span></span> | 
||||| 

| <span data-ttu-id="457d1-1908">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1908">Return value</span></span> | <span data-ttu-id="457d1-1909">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1909">Type</span></span> | <span data-ttu-id="457d1-1910">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1910">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1911">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1911">true or false</span></span> | <span data-ttu-id="457d1-1912">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1912">Boolean</span></span> | <span data-ttu-id="457d1-1913">Return true when the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1913">Return true when the first value is less than the second value.</span></span> <span data-ttu-id="457d1-1914">Return false when the first value is equal to or greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1914">Return false when the first value is equal to or greater than the second value.</span></span> | 
|||| 

<span data-ttu-id="457d1-1915">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1915">*Example*</span></span>

<span data-ttu-id="457d1-1916">These examples check whether the first value is less than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1916">These examples check whether the first value is less than the second value.</span></span>

```
less(5, 10)
less('banana', 'apple')
```

<span data-ttu-id="457d1-1917">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1917">And return these results:</span></span> 

* <span data-ttu-id="457d1-1918">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-1918">First example: `true`</span></span>
* <span data-ttu-id="457d1-1919">Second example: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-1919">Second example: `false`</span></span>

<a name="lessOrEquals"></a>

### <a name="lessorequals"></a><span data-ttu-id="457d1-1920">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="457d1-1920">lessOrEquals</span></span>

<span data-ttu-id="457d1-1921">Check whether the first value is less than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1921">Check whether the first value is less than or equal to the second value.</span></span>
<span data-ttu-id="457d1-1922">Return true when the first value is less than or equal, or return false when the first value is more.</span><span class="sxs-lookup"><span data-stu-id="457d1-1922">Return true when the first value is less than or equal, or return false when the first value is more.</span></span>

```
lessOrEquals(<value>, <compareTo>)
lessOrEquals('<value>', '<compareTo>')
```

| <span data-ttu-id="457d1-1923">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1923">Parameter</span></span> | <span data-ttu-id="457d1-1924">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1924">Required</span></span> | <span data-ttu-id="457d1-1925">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1925">Type</span></span> | <span data-ttu-id="457d1-1926">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1926">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1927"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1927"><*value*></span></span> | <span data-ttu-id="457d1-1928">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1928">Yes</span></span> | <span data-ttu-id="457d1-1929">Integer, Float, or String</span><span class="sxs-lookup"><span data-stu-id="457d1-1929">Integer, Float, or String</span></span> | <span data-ttu-id="457d1-1930">The first value to check whether less than or equal to the second value</span><span class="sxs-lookup"><span data-stu-id="457d1-1930">The first value to check whether less than or equal to the second value</span></span> | 
| <span data-ttu-id="457d1-1931"><*compareTo*></span><span class="sxs-lookup"><span data-stu-id="457d1-1931"><*compareTo*></span></span> | <span data-ttu-id="457d1-1932">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1932">Yes</span></span> | <span data-ttu-id="457d1-1933">Integer, Float, or String, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-1933">Integer, Float, or String, respectively</span></span> | <span data-ttu-id="457d1-1934">The comparison item</span><span class="sxs-lookup"><span data-stu-id="457d1-1934">The comparison item</span></span> | 
||||| 

| <span data-ttu-id="457d1-1935">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1935">Return value</span></span> | <span data-ttu-id="457d1-1936">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1936">Type</span></span> | <span data-ttu-id="457d1-1937">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1937">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1938">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-1938">true or false</span></span>  | <span data-ttu-id="457d1-1939">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-1939">Boolean</span></span> | <span data-ttu-id="457d1-1940">Return true when the first value is less than or equal to the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1940">Return true when the first value is less than or equal to the second value.</span></span> <span data-ttu-id="457d1-1941">Return false when the first value is greater than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1941">Return false when the first value is greater than the second value.</span></span> |  
|||| 

<span data-ttu-id="457d1-1942">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1942">*Example*</span></span>

<span data-ttu-id="457d1-1943">These examples check whether the first value is less or equal than the second value.</span><span class="sxs-lookup"><span data-stu-id="457d1-1943">These examples check whether the first value is less or equal than the second value.</span></span>

```
lessOrEquals(10, 10)
lessOrEquals('apply', 'apple')
```

<span data-ttu-id="457d1-1944">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-1944">And return these results:</span></span> 

* <span data-ttu-id="457d1-1945">First example: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-1945">First example: `true`</span></span>
* <span data-ttu-id="457d1-1946">Second example: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-1946">Second example: `false`</span></span>

<a name="listCallbackUrl"></a>

### <a name="listcallbackurl"></a><span data-ttu-id="457d1-1947">listCallbackUrl</span><span class="sxs-lookup"><span data-stu-id="457d1-1947">listCallbackUrl</span></span>

<span data-ttu-id="457d1-1948">Return the "callback URL" that calls a trigger or action.</span><span class="sxs-lookup"><span data-stu-id="457d1-1948">Return the "callback URL" that calls a trigger or action.</span></span> <span data-ttu-id="457d1-1949">This function works only with triggers and actions for the **HttpWebhook** and **ApiConnectionWebhook** connector types, but not the **Manual**, **Recurrence**, **HTTP**, and **APIConnection** types.</span><span class="sxs-lookup"><span data-stu-id="457d1-1949">This function works only with triggers and actions for the **HttpWebhook** and **ApiConnectionWebhook** connector types, but not the **Manual**, **Recurrence**, **HTTP**, and **APIConnection** types.</span></span> 

```
listCallbackUrl()
```

| <span data-ttu-id="457d1-1950">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1950">Return value</span></span> | <span data-ttu-id="457d1-1951">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1951">Type</span></span> | <span data-ttu-id="457d1-1952">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1952">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1953"><*callback-URL*></span><span class="sxs-lookup"><span data-stu-id="457d1-1953"><*callback-URL*></span></span> | <span data-ttu-id="457d1-1954">String</span><span class="sxs-lookup"><span data-stu-id="457d1-1954">String</span></span> | <span data-ttu-id="457d1-1955">The callback URL for a trigger or action</span><span class="sxs-lookup"><span data-stu-id="457d1-1955">The callback URL for a trigger or action</span></span> |  
|||| 

<span data-ttu-id="457d1-1956">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1956">*Example*</span></span>

<span data-ttu-id="457d1-1957">This example shows a sample callback URL that this function might return:</span><span class="sxs-lookup"><span data-stu-id="457d1-1957">This example shows a sample callback URL that this function might return:</span></span>

`"https://prod-01.westus.logic.azure.com:443/workflows/<*workflow-ID*>/triggers/manual/run?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=<*signature-ID*>"`

<a name="max"></a>

### <a name="max"></a><span data-ttu-id="457d1-1958">max</span><span class="sxs-lookup"><span data-stu-id="457d1-1958">max</span></span>

<span data-ttu-id="457d1-1959">Return the highest value from a list or array with numbers that is inclusive at both ends.</span><span class="sxs-lookup"><span data-stu-id="457d1-1959">Return the highest value from a list or array with numbers that is inclusive at both ends.</span></span> 

```
max(<number1>, <number2>, ...)
max([<number1>, <number2>, ...])
```

| <span data-ttu-id="457d1-1960">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1960">Parameter</span></span> | <span data-ttu-id="457d1-1961">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1961">Required</span></span> | <span data-ttu-id="457d1-1962">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1962">Type</span></span> | <span data-ttu-id="457d1-1963">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1963">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1964"><*number1*>, <*number2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-1964"><*number1*>, <*number2*>, ...</span></span> | <span data-ttu-id="457d1-1965">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1965">Yes</span></span> | <span data-ttu-id="457d1-1966">Integer, Float, or both</span><span class="sxs-lookup"><span data-stu-id="457d1-1966">Integer, Float, or both</span></span> | <span data-ttu-id="457d1-1967">The set of numbers from which you want the highest value</span><span class="sxs-lookup"><span data-stu-id="457d1-1967">The set of numbers from which you want the highest value</span></span> | 
| <span data-ttu-id="457d1-1968">[<*number1*>, <*number2*>, ...]</span><span class="sxs-lookup"><span data-stu-id="457d1-1968">[<*number1*>, <*number2*>, ...]</span></span> | <span data-ttu-id="457d1-1969">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1969">Yes</span></span> | <span data-ttu-id="457d1-1970">Array - Integer, Float, or both</span><span class="sxs-lookup"><span data-stu-id="457d1-1970">Array - Integer, Float, or both</span></span> | <span data-ttu-id="457d1-1971">The array of numbers from which you want the highest value</span><span class="sxs-lookup"><span data-stu-id="457d1-1971">The array of numbers from which you want the highest value</span></span> | 
||||| 

| <span data-ttu-id="457d1-1972">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1972">Return value</span></span> | <span data-ttu-id="457d1-1973">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1973">Type</span></span> | <span data-ttu-id="457d1-1974">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1974">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1975"><*max-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1975"><*max-value*></span></span> | <span data-ttu-id="457d1-1976">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-1976">Integer or Float</span></span> | <span data-ttu-id="457d1-1977">The highest value in the specified array or set of numbers</span><span class="sxs-lookup"><span data-stu-id="457d1-1977">The highest value in the specified array or set of numbers</span></span> | 
|||| 

<span data-ttu-id="457d1-1978">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-1978">*Example*</span></span> 

<span data-ttu-id="457d1-1979">These examples get the highest value from the set of numbers and the array:</span><span class="sxs-lookup"><span data-stu-id="457d1-1979">These examples get the highest value from the set of numbers and the array:</span></span>

```
max(1, 2, 3)
max([1, 2, 3])
```

<span data-ttu-id="457d1-1980">And return this result: `3`</span><span class="sxs-lookup"><span data-stu-id="457d1-1980">And return this result: `3`</span></span>

<a name="min"></a>

### <a name="min"></a><span data-ttu-id="457d1-1981">min</span><span class="sxs-lookup"><span data-stu-id="457d1-1981">min</span></span>

<span data-ttu-id="457d1-1982">Return the lowest value from a set of numbers or an array.</span><span class="sxs-lookup"><span data-stu-id="457d1-1982">Return the lowest value from a set of numbers or an array.</span></span>

```
min(<number1>, <number2>, ...)
min([<number1>, <number2>, ...])
```

| <span data-ttu-id="457d1-1983">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-1983">Parameter</span></span> | <span data-ttu-id="457d1-1984">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-1984">Required</span></span> | <span data-ttu-id="457d1-1985">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1985">Type</span></span> | <span data-ttu-id="457d1-1986">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1986">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-1987"><*number1*>, <*number2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-1987"><*number1*>, <*number2*>, ...</span></span> | <span data-ttu-id="457d1-1988">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1988">Yes</span></span> | <span data-ttu-id="457d1-1989">Integer, Float, or both</span><span class="sxs-lookup"><span data-stu-id="457d1-1989">Integer, Float, or both</span></span> | <span data-ttu-id="457d1-1990">The set of numbers from which you want the lowest value</span><span class="sxs-lookup"><span data-stu-id="457d1-1990">The set of numbers from which you want the lowest value</span></span> | 
| <span data-ttu-id="457d1-1991">[<*number1*>, <*number2*>, ...]</span><span class="sxs-lookup"><span data-stu-id="457d1-1991">[<*number1*>, <*number2*>, ...]</span></span> | <span data-ttu-id="457d1-1992">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-1992">Yes</span></span> | <span data-ttu-id="457d1-1993">Array - Integer, Float, or both</span><span class="sxs-lookup"><span data-stu-id="457d1-1993">Array - Integer, Float, or both</span></span> | <span data-ttu-id="457d1-1994">The array of numbers from which you want the lowest value</span><span class="sxs-lookup"><span data-stu-id="457d1-1994">The array of numbers from which you want the lowest value</span></span> | 
||||| 

| <span data-ttu-id="457d1-1995">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-1995">Return value</span></span> | <span data-ttu-id="457d1-1996">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-1996">Type</span></span> | <span data-ttu-id="457d1-1997">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-1997">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-1998"><*min-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-1998"><*min-value*></span></span> | <span data-ttu-id="457d1-1999">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-1999">Integer or Float</span></span> | <span data-ttu-id="457d1-2000">The lowest value in the specified set of numbers or specified array</span><span class="sxs-lookup"><span data-stu-id="457d1-2000">The lowest value in the specified set of numbers or specified array</span></span> | 
|||| 

<span data-ttu-id="457d1-2001">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2001">*Example*</span></span> 

<span data-ttu-id="457d1-2002">These examples get the lowest value in the set of numbers and the array:</span><span class="sxs-lookup"><span data-stu-id="457d1-2002">These examples get the lowest value in the set of numbers and the array:</span></span>

```
min(1, 2, 3)
min([1, 2, 3])
```

<span data-ttu-id="457d1-2003">And return this result: `1`</span><span class="sxs-lookup"><span data-stu-id="457d1-2003">And return this result: `1`</span></span>

<a name="mod"></a>

### <a name="mod"></a><span data-ttu-id="457d1-2004">mod</span><span class="sxs-lookup"><span data-stu-id="457d1-2004">mod</span></span>

<span data-ttu-id="457d1-2005">Return the remainder from dividing two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-2005">Return the remainder from dividing two numbers.</span></span> <span data-ttu-id="457d1-2006">To get the integer result, see [div()](#div).</span><span class="sxs-lookup"><span data-stu-id="457d1-2006">To get the integer result, see [div()](#div).</span></span>

```
mod(<dividend>, <divisor>)
```

| <span data-ttu-id="457d1-2007">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2007">Parameter</span></span> | <span data-ttu-id="457d1-2008">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2008">Required</span></span> | <span data-ttu-id="457d1-2009">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2009">Type</span></span> | <span data-ttu-id="457d1-2010">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2010">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2011"><*dividend*></span><span class="sxs-lookup"><span data-stu-id="457d1-2011"><*dividend*></span></span> | <span data-ttu-id="457d1-2012">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2012">Yes</span></span> | <span data-ttu-id="457d1-2013">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2013">Integer or Float</span></span> | <span data-ttu-id="457d1-2014">The number to divide by the *divisor*</span><span class="sxs-lookup"><span data-stu-id="457d1-2014">The number to divide by the *divisor*</span></span> | 
| <span data-ttu-id="457d1-2015"><*divisor*></span><span class="sxs-lookup"><span data-stu-id="457d1-2015"><*divisor*></span></span> | <span data-ttu-id="457d1-2016">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2016">Yes</span></span> | <span data-ttu-id="457d1-2017">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2017">Integer or Float</span></span> | <span data-ttu-id="457d1-2018">The number that divides the *dividend*, but cannot be 0.</span><span class="sxs-lookup"><span data-stu-id="457d1-2018">The number that divides the *dividend*, but cannot be 0.</span></span> | 
||||| 

| <span data-ttu-id="457d1-2019">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2019">Return value</span></span> | <span data-ttu-id="457d1-2020">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2020">Type</span></span> | <span data-ttu-id="457d1-2021">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2021">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2022"><*modulo-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-2022"><*modulo-result*></span></span> | <span data-ttu-id="457d1-2023">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2023">Integer or Float</span></span> | <span data-ttu-id="457d1-2024">The remainder from dividing the first number by the second number</span><span class="sxs-lookup"><span data-stu-id="457d1-2024">The remainder from dividing the first number by the second number</span></span> | 
|||| 

<span data-ttu-id="457d1-2025">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2025">*Example*</span></span> 

<span data-ttu-id="457d1-2026">This example divides the first number by the second number:</span><span class="sxs-lookup"><span data-stu-id="457d1-2026">This example divides the first number by the second number:</span></span>

```
mod(3, 2)
```

<span data-ttu-id="457d1-2027">And return this result: `1`</span><span class="sxs-lookup"><span data-stu-id="457d1-2027">And return this result: `1`</span></span>

<a name="mul"></a>

### <a name="mul"></a><span data-ttu-id="457d1-2028">mul</span><span class="sxs-lookup"><span data-stu-id="457d1-2028">mul</span></span>

<span data-ttu-id="457d1-2029">Return the product from multiplying two numbers.</span><span class="sxs-lookup"><span data-stu-id="457d1-2029">Return the product from multiplying two numbers.</span></span>

```
mul(<multiplicand1>, <multiplicand2>)
```

| <span data-ttu-id="457d1-2030">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2030">Parameter</span></span> | <span data-ttu-id="457d1-2031">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2031">Required</span></span> | <span data-ttu-id="457d1-2032">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2032">Type</span></span> | <span data-ttu-id="457d1-2033">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2033">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2034"><*multiplicand1*></span><span class="sxs-lookup"><span data-stu-id="457d1-2034"><*multiplicand1*></span></span> | <span data-ttu-id="457d1-2035">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2035">Yes</span></span> | <span data-ttu-id="457d1-2036">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2036">Integer or Float</span></span> | <span data-ttu-id="457d1-2037">The number to multiply by *multiplicand2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2037">The number to multiply by *multiplicand2*</span></span> | 
| <span data-ttu-id="457d1-2038"><*multiplicand2*></span><span class="sxs-lookup"><span data-stu-id="457d1-2038"><*multiplicand2*></span></span> | <span data-ttu-id="457d1-2039">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2039">Yes</span></span> | <span data-ttu-id="457d1-2040">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2040">Integer or Float</span></span> | <span data-ttu-id="457d1-2041">The number that multiples *multiplicand1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2041">The number that multiples *multiplicand1*</span></span> | 
||||| 

| <span data-ttu-id="457d1-2042">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2042">Return value</span></span> | <span data-ttu-id="457d1-2043">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2043">Type</span></span> | <span data-ttu-id="457d1-2044">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2044">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2045"><*product-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-2045"><*product-result*></span></span> | <span data-ttu-id="457d1-2046">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2046">Integer or Float</span></span> | <span data-ttu-id="457d1-2047">The product from multiplying the first number by the second number</span><span class="sxs-lookup"><span data-stu-id="457d1-2047">The product from multiplying the first number by the second number</span></span> | 
|||| 

<span data-ttu-id="457d1-2048">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2048">*Example*</span></span> 

<span data-ttu-id="457d1-2049">These examples multiple the first number by the second number:</span><span class="sxs-lookup"><span data-stu-id="457d1-2049">These examples multiple the first number by the second number:</span></span>

```
mul(1, 2)
mul(1.5, 2)
```

<span data-ttu-id="457d1-2050">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2050">And return these results:</span></span>

* <span data-ttu-id="457d1-2051">First example: `2`</span><span class="sxs-lookup"><span data-stu-id="457d1-2051">First example: `2`</span></span>
* <span data-ttu-id="457d1-2052">Second example `3`</span><span class="sxs-lookup"><span data-stu-id="457d1-2052">Second example `3`</span></span>

<a name="multipartBody"></a>

### <a name="multipartbody"></a><span data-ttu-id="457d1-2053">multipartBody</span><span class="sxs-lookup"><span data-stu-id="457d1-2053">multipartBody</span></span>

<span data-ttu-id="457d1-2054">Return the body for a specific part in an action's output that has multiple parts.</span><span class="sxs-lookup"><span data-stu-id="457d1-2054">Return the body for a specific part in an action's output that has multiple parts.</span></span>

```
multipartBody('<actionName>', <index>)
```

| <span data-ttu-id="457d1-2055">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2055">Parameter</span></span> | <span data-ttu-id="457d1-2056">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2056">Required</span></span> | <span data-ttu-id="457d1-2057">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2057">Type</span></span> | <span data-ttu-id="457d1-2058">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2058">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2059"><*actionName*></span><span class="sxs-lookup"><span data-stu-id="457d1-2059"><*actionName*></span></span> | <span data-ttu-id="457d1-2060">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2060">Yes</span></span> | <span data-ttu-id="457d1-2061">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2061">String</span></span> | <span data-ttu-id="457d1-2062">The name for the action that has output with multiple parts</span><span class="sxs-lookup"><span data-stu-id="457d1-2062">The name for the action that has output with multiple parts</span></span> | 
| <span data-ttu-id="457d1-2063"><*index*></span><span class="sxs-lookup"><span data-stu-id="457d1-2063"><*index*></span></span> | <span data-ttu-id="457d1-2064">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2064">Yes</span></span> | <span data-ttu-id="457d1-2065">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2065">Integer</span></span> | <span data-ttu-id="457d1-2066">The index value for the part that you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2066">The index value for the part that you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2067">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2067">Return value</span></span> | <span data-ttu-id="457d1-2068">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2068">Type</span></span> | <span data-ttu-id="457d1-2069">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2069">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2070"><*body*></span><span class="sxs-lookup"><span data-stu-id="457d1-2070"><*body*></span></span> | <span data-ttu-id="457d1-2071">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2071">String</span></span> | <span data-ttu-id="457d1-2072">The body for the specified part</span><span class="sxs-lookup"><span data-stu-id="457d1-2072">The body for the specified part</span></span> | 
|||| 

<a name="not"></a>

### <a name="not"></a><span data-ttu-id="457d1-2073">not</span><span class="sxs-lookup"><span data-stu-id="457d1-2073">not</span></span>

<span data-ttu-id="457d1-2074">Check whether an expression is false.</span><span class="sxs-lookup"><span data-stu-id="457d1-2074">Check whether an expression is false.</span></span> <span data-ttu-id="457d1-2075">Return true when the expression is false, or return false when true.</span><span class="sxs-lookup"><span data-stu-id="457d1-2075">Return true when the expression is false, or return false when true.</span></span>

```
not(<expression>)
```

| <span data-ttu-id="457d1-2076">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2076">Parameter</span></span> | <span data-ttu-id="457d1-2077">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2077">Required</span></span> | <span data-ttu-id="457d1-2078">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2078">Type</span></span> | <span data-ttu-id="457d1-2079">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2079">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2080"><*expression*></span><span class="sxs-lookup"><span data-stu-id="457d1-2080"><*expression*></span></span> | <span data-ttu-id="457d1-2081">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2081">Yes</span></span> | <span data-ttu-id="457d1-2082">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-2082">Boolean</span></span> | <span data-ttu-id="457d1-2083">The expression to check</span><span class="sxs-lookup"><span data-stu-id="457d1-2083">The expression to check</span></span> | 
||||| 

| <span data-ttu-id="457d1-2084">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2084">Return value</span></span> | <span data-ttu-id="457d1-2085">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2085">Type</span></span> | <span data-ttu-id="457d1-2086">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2086">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2087">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-2087">true or false</span></span> | <span data-ttu-id="457d1-2088">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-2088">Boolean</span></span> | <span data-ttu-id="457d1-2089">Return true when the expression is false.</span><span class="sxs-lookup"><span data-stu-id="457d1-2089">Return true when the expression is false.</span></span> <span data-ttu-id="457d1-2090">Return false when the expression is true.</span><span class="sxs-lookup"><span data-stu-id="457d1-2090">Return false when the expression is true.</span></span> |  
|||| 

<span data-ttu-id="457d1-2091">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2091">*Example 1*</span></span>

<span data-ttu-id="457d1-2092">These examples check whether the specified expressions are false:</span><span class="sxs-lookup"><span data-stu-id="457d1-2092">These examples check whether the specified expressions are false:</span></span> 

```
not(false)
not(true)
```

<span data-ttu-id="457d1-2093">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2093">And return these results:</span></span>

* <span data-ttu-id="457d1-2094">First example: The expression is false, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2094">First example: The expression is false, so the function returns `true`.</span></span>
* <span data-ttu-id="457d1-2095">Second example: The expression is true, so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2095">Second example: The expression is true, so the function returns `false`.</span></span>

<span data-ttu-id="457d1-2096">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2096">*Example 2*</span></span>

<span data-ttu-id="457d1-2097">These examples check whether the specified expressions are false:</span><span class="sxs-lookup"><span data-stu-id="457d1-2097">These examples check whether the specified expressions are false:</span></span> 

```
not(equals(1, 2))
not(equals(1, 1))
```

<span data-ttu-id="457d1-2098">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2098">And return these results:</span></span>

* <span data-ttu-id="457d1-2099">First example: The expression is false, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2099">First example: The expression is false, so the function returns `true`.</span></span>
* <span data-ttu-id="457d1-2100">Second example: The expression is true, so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2100">Second example: The expression is true, so the function returns `false`.</span></span>

<a name="or"></a>

### <a name="or"></a><span data-ttu-id="457d1-2101">or</span><span class="sxs-lookup"><span data-stu-id="457d1-2101">or</span></span>

<span data-ttu-id="457d1-2102">Check whether at least one expression is true.</span><span class="sxs-lookup"><span data-stu-id="457d1-2102">Check whether at least one expression is true.</span></span> <span data-ttu-id="457d1-2103">Return true when at least one expression is true, or return false when all are false.</span><span class="sxs-lookup"><span data-stu-id="457d1-2103">Return true when at least one expression is true, or return false when all are false.</span></span>

```
or(<expression1>, <expression2>, ...)
```

| <span data-ttu-id="457d1-2104">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2104">Parameter</span></span> | <span data-ttu-id="457d1-2105">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2105">Required</span></span> | <span data-ttu-id="457d1-2106">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2106">Type</span></span> | <span data-ttu-id="457d1-2107">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2107">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2108"><*expression1*>, <*expression2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-2108"><*expression1*>, <*expression2*>, ...</span></span> | <span data-ttu-id="457d1-2109">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2109">Yes</span></span> | <span data-ttu-id="457d1-2110">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-2110">Boolean</span></span> | <span data-ttu-id="457d1-2111">The expressions to check</span><span class="sxs-lookup"><span data-stu-id="457d1-2111">The expressions to check</span></span> | 
||||| 

| <span data-ttu-id="457d1-2112">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2112">Return value</span></span> | <span data-ttu-id="457d1-2113">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2113">Type</span></span> | <span data-ttu-id="457d1-2114">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2114">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2115">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-2115">true or false</span></span> | <span data-ttu-id="457d1-2116">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-2116">Boolean</span></span> | <span data-ttu-id="457d1-2117">Return true when at least one expression is true.</span><span class="sxs-lookup"><span data-stu-id="457d1-2117">Return true when at least one expression is true.</span></span> <span data-ttu-id="457d1-2118">Return false when all expressions are false.</span><span class="sxs-lookup"><span data-stu-id="457d1-2118">Return false when all expressions are false.</span></span> |  
|||| 

<span data-ttu-id="457d1-2119">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2119">*Example 1*</span></span>

<span data-ttu-id="457d1-2120">These examples check whether at least one expression is true:</span><span class="sxs-lookup"><span data-stu-id="457d1-2120">These examples check whether at least one expression is true:</span></span>

```
or(true, false)
or(false, false)
```

<span data-ttu-id="457d1-2121">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2121">And return these results:</span></span>

* <span data-ttu-id="457d1-2122">First example: At least one expression is true, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2122">First example: At least one expression is true, so the function returns `true`.</span></span>
* <span data-ttu-id="457d1-2123">Second example: Both expressions are false, so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2123">Second example: Both expressions are false, so the function returns `false`.</span></span>

<span data-ttu-id="457d1-2124">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2124">*Example 2*</span></span>

<span data-ttu-id="457d1-2125">These examples check whether at least one expression is true:</span><span class="sxs-lookup"><span data-stu-id="457d1-2125">These examples check whether at least one expression is true:</span></span>

```
or(equals(1, 1), equals(1, 2))
or(equals(1, 2), equals(1, 3))
```

<span data-ttu-id="457d1-2126">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2126">And return these results:</span></span>

* <span data-ttu-id="457d1-2127">First example: At least one expression is true, so the function returns `true`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2127">First example: At least one expression is true, so the function returns `true`.</span></span>
* <span data-ttu-id="457d1-2128">Second example: Both expressions are false, so the function returns `false`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2128">Second example: Both expressions are false, so the function returns `false`.</span></span>

<a name="parameters"></a>

### <a name="parameters"></a><span data-ttu-id="457d1-2129">parameters</span><span class="sxs-lookup"><span data-stu-id="457d1-2129">parameters</span></span>

<span data-ttu-id="457d1-2130">Return the value for a parameter that is described in your logic app definition.</span><span class="sxs-lookup"><span data-stu-id="457d1-2130">Return the value for a parameter that is described in your logic app definition.</span></span> 

```
parameters('<parameterName>')
```

| <span data-ttu-id="457d1-2131">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2131">Parameter</span></span> | <span data-ttu-id="457d1-2132">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2132">Required</span></span> | <span data-ttu-id="457d1-2133">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2133">Type</span></span> | <span data-ttu-id="457d1-2134">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2134">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2135"><*parameterName*></span><span class="sxs-lookup"><span data-stu-id="457d1-2135"><*parameterName*></span></span> | <span data-ttu-id="457d1-2136">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2136">Yes</span></span> | <span data-ttu-id="457d1-2137">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2137">String</span></span> | <span data-ttu-id="457d1-2138">The name for the parameter whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2138">The name for the parameter whose value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2139">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2139">Return value</span></span> | <span data-ttu-id="457d1-2140">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2140">Type</span></span> | <span data-ttu-id="457d1-2141">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2141">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2142"><*parameter-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2142"><*parameter-value*></span></span> | <span data-ttu-id="457d1-2143">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-2143">Any</span></span> | <span data-ttu-id="457d1-2144">The value for the specified parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2144">The value for the specified parameter</span></span> | 
|||| 

<span data-ttu-id="457d1-2145">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2145">*Example*</span></span> 

<span data-ttu-id="457d1-2146">Suppose that you have this JSON value:</span><span class="sxs-lookup"><span data-stu-id="457d1-2146">Suppose that you have this JSON value:</span></span>

```json
{
  "fullName": "Sophia Owen"
}
```

<span data-ttu-id="457d1-2147">This example gets the value for the specified parameter:</span><span class="sxs-lookup"><span data-stu-id="457d1-2147">This example gets the value for the specified parameter:</span></span>

```
parameters('fullName')
```

<span data-ttu-id="457d1-2148">And returns this result: `"Sophia Owen"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2148">And returns this result: `"Sophia Owen"`</span></span>

<a name="rand"></a>

### <a name="rand"></a><span data-ttu-id="457d1-2149">rand</span><span class="sxs-lookup"><span data-stu-id="457d1-2149">rand</span></span>

<span data-ttu-id="457d1-2150">Return a random integer from a specified range, which is inclusive only at the starting end.</span><span class="sxs-lookup"><span data-stu-id="457d1-2150">Return a random integer from a specified range, which is inclusive only at the starting end.</span></span>

```
rand(<minValue>, <maxValue>)
```

| <span data-ttu-id="457d1-2151">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2151">Parameter</span></span> | <span data-ttu-id="457d1-2152">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2152">Required</span></span> | <span data-ttu-id="457d1-2153">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2153">Type</span></span> | <span data-ttu-id="457d1-2154">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2154">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2155"><*minValue*></span><span class="sxs-lookup"><span data-stu-id="457d1-2155"><*minValue*></span></span> | <span data-ttu-id="457d1-2156">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2156">Yes</span></span> | <span data-ttu-id="457d1-2157">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2157">Integer</span></span> | <span data-ttu-id="457d1-2158">The lowest integer in the range</span><span class="sxs-lookup"><span data-stu-id="457d1-2158">The lowest integer in the range</span></span> | 
| <span data-ttu-id="457d1-2159"><*maxValue*></span><span class="sxs-lookup"><span data-stu-id="457d1-2159"><*maxValue*></span></span> | <span data-ttu-id="457d1-2160">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2160">Yes</span></span> | <span data-ttu-id="457d1-2161">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2161">Integer</span></span> | <span data-ttu-id="457d1-2162">The integer that follows the highest integer in the range that the function can return</span><span class="sxs-lookup"><span data-stu-id="457d1-2162">The integer that follows the highest integer in the range that the function can return</span></span> | 
||||| 

| <span data-ttu-id="457d1-2163">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2163">Return value</span></span> | <span data-ttu-id="457d1-2164">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2164">Type</span></span> | <span data-ttu-id="457d1-2165">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2165">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2166"><*random-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-2166"><*random-result*></span></span> | <span data-ttu-id="457d1-2167">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2167">Integer</span></span> | <span data-ttu-id="457d1-2168">The random integer returned from the specified range</span><span class="sxs-lookup"><span data-stu-id="457d1-2168">The random integer returned from the specified range</span></span> |  
|||| 

<span data-ttu-id="457d1-2169">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2169">*Example*</span></span>

<span data-ttu-id="457d1-2170">This example gets a random integer from the specified range, excluding the maximum value:</span><span class="sxs-lookup"><span data-stu-id="457d1-2170">This example gets a random integer from the specified range, excluding the maximum value:</span></span> 

```
rand(1, 5)
```

<span data-ttu-id="457d1-2171">And returns one of these numbers as the result: `1`, `2`, `3`, or `4`</span><span class="sxs-lookup"><span data-stu-id="457d1-2171">And returns one of these numbers as the result: `1`, `2`, `3`, or `4`</span></span> 

<a name="range"></a>

### <a name="range"></a><span data-ttu-id="457d1-2172">range</span><span class="sxs-lookup"><span data-stu-id="457d1-2172">range</span></span>

<span data-ttu-id="457d1-2173">Return an integer array that starts from a specified integer.</span><span class="sxs-lookup"><span data-stu-id="457d1-2173">Return an integer array that starts from a specified integer.</span></span>

```
range(<startIndex>, <count>)
```

| <span data-ttu-id="457d1-2174">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2174">Parameter</span></span> | <span data-ttu-id="457d1-2175">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2175">Required</span></span> | <span data-ttu-id="457d1-2176">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2176">Type</span></span> | <span data-ttu-id="457d1-2177">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2177">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2178"><*startIndex*></span><span class="sxs-lookup"><span data-stu-id="457d1-2178"><*startIndex*></span></span> | <span data-ttu-id="457d1-2179">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2179">Yes</span></span> | <span data-ttu-id="457d1-2180">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2180">Integer</span></span> | <span data-ttu-id="457d1-2181">The integer value that starts the array as the first item</span><span class="sxs-lookup"><span data-stu-id="457d1-2181">The integer value that starts the array as the first item</span></span> | 
| <span data-ttu-id="457d1-2182"><*count*></span><span class="sxs-lookup"><span data-stu-id="457d1-2182"><*count*></span></span> | <span data-ttu-id="457d1-2183">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2183">Yes</span></span> | <span data-ttu-id="457d1-2184">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2184">Integer</span></span> | <span data-ttu-id="457d1-2185">The number of integers in the array</span><span class="sxs-lookup"><span data-stu-id="457d1-2185">The number of integers in the array</span></span> | 
||||| 

| <span data-ttu-id="457d1-2186">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2186">Return value</span></span> | <span data-ttu-id="457d1-2187">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2187">Type</span></span> | <span data-ttu-id="457d1-2188">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2188">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2189">[<*range-result*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-2189">[<*range-result*>]</span></span> | <span data-ttu-id="457d1-2190">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2190">Array</span></span> | <span data-ttu-id="457d1-2191">The array with integers starting from the specified index</span><span class="sxs-lookup"><span data-stu-id="457d1-2191">The array with integers starting from the specified index</span></span> |  
|||| 

<span data-ttu-id="457d1-2192">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2192">*Example*</span></span>

<span data-ttu-id="457d1-2193">This example creates an integer array that starts from the specified index and has the specified number of integers:</span><span class="sxs-lookup"><span data-stu-id="457d1-2193">This example creates an integer array that starts from the specified index and has the specified number of integers:</span></span>

```
range(1, 4)
```

<span data-ttu-id="457d1-2194">And returns this result: `[1, 2, 3, 4]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2194">And returns this result: `[1, 2, 3, 4]`</span></span>

<a name="replace"></a>

### <a name="replace"></a><span data-ttu-id="457d1-2195">replace</span><span class="sxs-lookup"><span data-stu-id="457d1-2195">replace</span></span>

<span data-ttu-id="457d1-2196">Replace a substring with the specified string, and return the result string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2196">Replace a substring with the specified string, and return the result string.</span></span> <span data-ttu-id="457d1-2197">This function is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="457d1-2197">This function is case-sensitive.</span></span>

```
replace('<text>', '<oldText>', '<newText>')
```

| <span data-ttu-id="457d1-2198">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2198">Parameter</span></span> | <span data-ttu-id="457d1-2199">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2199">Required</span></span> | <span data-ttu-id="457d1-2200">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2200">Type</span></span> | <span data-ttu-id="457d1-2201">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2201">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2202"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2202"><*text*></span></span> | <span data-ttu-id="457d1-2203">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2203">Yes</span></span> | <span data-ttu-id="457d1-2204">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2204">String</span></span> | <span data-ttu-id="457d1-2205">The string that has the substring to replace</span><span class="sxs-lookup"><span data-stu-id="457d1-2205">The string that has the substring to replace</span></span> | 
| <span data-ttu-id="457d1-2206"><*oldText*></span><span class="sxs-lookup"><span data-stu-id="457d1-2206"><*oldText*></span></span> | <span data-ttu-id="457d1-2207">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2207">Yes</span></span> | <span data-ttu-id="457d1-2208">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2208">String</span></span> | <span data-ttu-id="457d1-2209">The substring to replace</span><span class="sxs-lookup"><span data-stu-id="457d1-2209">The substring to replace</span></span> | 
| <span data-ttu-id="457d1-2210"><*newText*></span><span class="sxs-lookup"><span data-stu-id="457d1-2210"><*newText*></span></span> | <span data-ttu-id="457d1-2211">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2211">Yes</span></span> | <span data-ttu-id="457d1-2212">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2212">String</span></span> | <span data-ttu-id="457d1-2213">The replacement string</span><span class="sxs-lookup"><span data-stu-id="457d1-2213">The replacement string</span></span> | 
||||| 

| <span data-ttu-id="457d1-2214">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2214">Return value</span></span> | <span data-ttu-id="457d1-2215">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2215">Type</span></span> | <span data-ttu-id="457d1-2216">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2216">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2217"><*updated-text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2217"><*updated-text*></span></span> | <span data-ttu-id="457d1-2218">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2218">String</span></span> | <span data-ttu-id="457d1-2219">The updated string after replacing the substring</span><span class="sxs-lookup"><span data-stu-id="457d1-2219">The updated string after replacing the substring</span></span> <p><span data-ttu-id="457d1-2220">If the substring is not found, return the original string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2220">If the substring is not found, return the original string.</span></span> | 
|||| 

<span data-ttu-id="457d1-2221">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2221">*Example*</span></span> 

<span data-ttu-id="457d1-2222">This example finds the "old" substring in "the old string" and replaces "old" with "new":</span><span class="sxs-lookup"><span data-stu-id="457d1-2222">This example finds the "old" substring in "the old string" and replaces "old" with "new":</span></span> 

```
replace('the old string', 'old', 'new')
```

<span data-ttu-id="457d1-2223">And returns this result: `"the new string"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2223">And returns this result: `"the new string"`</span></span>

<a name="removeProperty"></a>

### <a name="removeproperty"></a><span data-ttu-id="457d1-2224">removeProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-2224">removeProperty</span></span>

<span data-ttu-id="457d1-2225">Remove a property from an object and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-2225">Remove a property from an object and return the updated object.</span></span>

```
removeProperty(<object>, '<property>')
```

| <span data-ttu-id="457d1-2226">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2226">Parameter</span></span> | <span data-ttu-id="457d1-2227">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2227">Required</span></span> | <span data-ttu-id="457d1-2228">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2228">Type</span></span> | <span data-ttu-id="457d1-2229">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2229">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2230"><*object*></span><span class="sxs-lookup"><span data-stu-id="457d1-2230"><*object*></span></span> | <span data-ttu-id="457d1-2231">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2231">Yes</span></span> | <span data-ttu-id="457d1-2232">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-2232">Object</span></span> | <span data-ttu-id="457d1-2233">The JSON object from where you want to remove a property</span><span class="sxs-lookup"><span data-stu-id="457d1-2233">The JSON object from where you want to remove a property</span></span> | 
| <span data-ttu-id="457d1-2234"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-2234"><*property*></span></span> | <span data-ttu-id="457d1-2235">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2235">Yes</span></span> | <span data-ttu-id="457d1-2236">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2236">String</span></span> | <span data-ttu-id="457d1-2237">The name for the property to remove</span><span class="sxs-lookup"><span data-stu-id="457d1-2237">The name for the property to remove</span></span> | 
||||| 

| <span data-ttu-id="457d1-2238">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2238">Return value</span></span> | <span data-ttu-id="457d1-2239">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2239">Type</span></span> | <span data-ttu-id="457d1-2240">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2240">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2241"><*updated-object*></span><span class="sxs-lookup"><span data-stu-id="457d1-2241"><*updated-object*></span></span> | <span data-ttu-id="457d1-2242">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-2242">Object</span></span> | <span data-ttu-id="457d1-2243">The updated JSON object without the specified property</span><span class="sxs-lookup"><span data-stu-id="457d1-2243">The updated JSON object without the specified property</span></span> | 
|||| 

<span data-ttu-id="457d1-2244">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2244">*Example*</span></span>

<span data-ttu-id="457d1-2245">This example removes the `"accountLocation"` property from a `"customerProfile"` object, which is converted to JSON with the [JSON()](#json) function, and returns the updated object:</span><span class="sxs-lookup"><span data-stu-id="457d1-2245">This example removes the `"accountLocation"` property from a `"customerProfile"` object, which is converted to JSON with the [JSON()](#json) function, and returns the updated object:</span></span>

```
removeProperty(json('customerProfile'), 'accountLocation')
```

<a name="setProperty"></a>

### <a name="setproperty"></a><span data-ttu-id="457d1-2246">setProperty</span><span class="sxs-lookup"><span data-stu-id="457d1-2246">setProperty</span></span>

<span data-ttu-id="457d1-2247">Set the value for an object's property and return the updated object.</span><span class="sxs-lookup"><span data-stu-id="457d1-2247">Set the value for an object's property and return the updated object.</span></span> <span data-ttu-id="457d1-2248">To add a new property, you can use this function or the [addProperty()](#addProperty) function.</span><span class="sxs-lookup"><span data-stu-id="457d1-2248">To add a new property, you can use this function or the [addProperty()](#addProperty) function.</span></span>

```
setProperty(<object>, '<property>', <value>)
```

| <span data-ttu-id="457d1-2249">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2249">Parameter</span></span> | <span data-ttu-id="457d1-2250">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2250">Required</span></span> | <span data-ttu-id="457d1-2251">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2251">Type</span></span> | <span data-ttu-id="457d1-2252">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2252">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2253"><*object*></span><span class="sxs-lookup"><span data-stu-id="457d1-2253"><*object*></span></span> | <span data-ttu-id="457d1-2254">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2254">Yes</span></span> | <span data-ttu-id="457d1-2255">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-2255">Object</span></span> | <span data-ttu-id="457d1-2256">The JSON object whose property you want to set</span><span class="sxs-lookup"><span data-stu-id="457d1-2256">The JSON object whose property you want to set</span></span> | 
| <span data-ttu-id="457d1-2257"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-2257"><*property*></span></span> | <span data-ttu-id="457d1-2258">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2258">Yes</span></span> | <span data-ttu-id="457d1-2259">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2259">String</span></span> | <span data-ttu-id="457d1-2260">The name for the existing or new property to set</span><span class="sxs-lookup"><span data-stu-id="457d1-2260">The name for the existing or new property to set</span></span> | 
| <span data-ttu-id="457d1-2261"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2261"><*value*></span></span> | <span data-ttu-id="457d1-2262">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2262">Yes</span></span> | <span data-ttu-id="457d1-2263">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-2263">Any</span></span> | <span data-ttu-id="457d1-2264">The value to set for the specified property</span><span class="sxs-lookup"><span data-stu-id="457d1-2264">The value to set for the specified property</span></span> |
||||| 

| <span data-ttu-id="457d1-2265">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2265">Return value</span></span> | <span data-ttu-id="457d1-2266">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2266">Type</span></span> | <span data-ttu-id="457d1-2267">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2267">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2268"><*updated-object*></span><span class="sxs-lookup"><span data-stu-id="457d1-2268"><*updated-object*></span></span> | <span data-ttu-id="457d1-2269">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-2269">Object</span></span> | <span data-ttu-id="457d1-2270">The updated JSON object whose property you set</span><span class="sxs-lookup"><span data-stu-id="457d1-2270">The updated JSON object whose property you set</span></span> | 
|||| 

<span data-ttu-id="457d1-2271">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2271">*Example*</span></span>

<span data-ttu-id="457d1-2272">This example sets the `"accountNumber"` property on a `"customerProfile"` object, which is converted to JSON with the [JSON()](#json) function.</span><span class="sxs-lookup"><span data-stu-id="457d1-2272">This example sets the `"accountNumber"` property on a `"customerProfile"` object, which is converted to JSON with the [JSON()](#json) function.</span></span> <span data-ttu-id="457d1-2273">The function assigns a value generated by [guid()](#guid) function, and returns the updated JSON object:</span><span class="sxs-lookup"><span data-stu-id="457d1-2273">The function assigns a value generated by [guid()](#guid) function, and returns the updated JSON object:</span></span>

```
setProperty(json('customerProfile'), 'accountNumber', guid())
```

<a name="skip"></a>

### <a name="skip"></a><span data-ttu-id="457d1-2274">skip</span><span class="sxs-lookup"><span data-stu-id="457d1-2274">skip</span></span>

<span data-ttu-id="457d1-2275">Remove items from the front of a collection, and return *all the other* items.</span><span class="sxs-lookup"><span data-stu-id="457d1-2275">Remove items from the front of a collection, and return *all the other* items.</span></span>

```
skip([<collection>], <count>)
```

| <span data-ttu-id="457d1-2276">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2276">Parameter</span></span> | <span data-ttu-id="457d1-2277">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2277">Required</span></span> | <span data-ttu-id="457d1-2278">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2278">Type</span></span> | <span data-ttu-id="457d1-2279">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2279">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2280"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-2280"><*collection*></span></span> | <span data-ttu-id="457d1-2281">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2281">Yes</span></span> | <span data-ttu-id="457d1-2282">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2282">Array</span></span> | <span data-ttu-id="457d1-2283">The collection whose items you want to remove</span><span class="sxs-lookup"><span data-stu-id="457d1-2283">The collection whose items you want to remove</span></span> | 
| <span data-ttu-id="457d1-2284"><*count*></span><span class="sxs-lookup"><span data-stu-id="457d1-2284"><*count*></span></span> | <span data-ttu-id="457d1-2285">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2285">Yes</span></span> | <span data-ttu-id="457d1-2286">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2286">Integer</span></span> | <span data-ttu-id="457d1-2287">A positive integer for the number of items to remove at the front</span><span class="sxs-lookup"><span data-stu-id="457d1-2287">A positive integer for the number of items to remove at the front</span></span> | 
||||| 

| <span data-ttu-id="457d1-2288">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2288">Return value</span></span> | <span data-ttu-id="457d1-2289">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2289">Type</span></span> | <span data-ttu-id="457d1-2290">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2290">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2291">[<*updated-collection*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-2291">[<*updated-collection*>]</span></span> | <span data-ttu-id="457d1-2292">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2292">Array</span></span> | <span data-ttu-id="457d1-2293">The updated collection after removing the specified items</span><span class="sxs-lookup"><span data-stu-id="457d1-2293">The updated collection after removing the specified items</span></span> | 
|||| 

<span data-ttu-id="457d1-2294">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2294">*Example*</span></span>

<span data-ttu-id="457d1-2295">This example removes one item, the number 0, from the front of the specified array:</span><span class="sxs-lookup"><span data-stu-id="457d1-2295">This example removes one item, the number 0, from the front of the specified array:</span></span> 

```
skip([0, 1, 2, 3], 1)
```

<span data-ttu-id="457d1-2296">And returns this array with the remaining items: `[1,2,3]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2296">And returns this array with the remaining items: `[1,2,3]`</span></span>

<a name="split"></a>

### <a name="split"></a><span data-ttu-id="457d1-2297">split</span><span class="sxs-lookup"><span data-stu-id="457d1-2297">split</span></span>

<span data-ttu-id="457d1-2298">Return an array that has all the characters from a string and has each character separated by a *delimiter*.</span><span class="sxs-lookup"><span data-stu-id="457d1-2298">Return an array that has all the characters from a string and has each character separated by a *delimiter*.</span></span>

```
split('<text>', '<separator>')
```

| <span data-ttu-id="457d1-2299">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2299">Parameter</span></span> | <span data-ttu-id="457d1-2300">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2300">Required</span></span> | <span data-ttu-id="457d1-2301">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2301">Type</span></span> | <span data-ttu-id="457d1-2302">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2302">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2303"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2303"><*text*></span></span> | <span data-ttu-id="457d1-2304">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2304">Yes</span></span> | <span data-ttu-id="457d1-2305">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2305">String</span></span> | <span data-ttu-id="457d1-2306">The string that has the characters to split</span><span class="sxs-lookup"><span data-stu-id="457d1-2306">The string that has the characters to split</span></span> |  
| <span data-ttu-id="457d1-2307"><*separator*></span><span class="sxs-lookup"><span data-stu-id="457d1-2307"><*separator*></span></span> | <span data-ttu-id="457d1-2308">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2308">Yes</span></span> | <span data-ttu-id="457d1-2309">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2309">String</span></span> | <span data-ttu-id="457d1-2310">The separator that appears between each character in the resulting array</span><span class="sxs-lookup"><span data-stu-id="457d1-2310">The separator that appears between each character in the resulting array</span></span> | 
||||| 

| <span data-ttu-id="457d1-2311">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2311">Return value</span></span> | <span data-ttu-id="457d1-2312">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2312">Type</span></span> | <span data-ttu-id="457d1-2313">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2313">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2314">[<*char1*><*separator*><*char2*><*separator*>...]</span><span class="sxs-lookup"><span data-stu-id="457d1-2314">[<*char1*><*separator*><*char2*><*separator*>...]</span></span> | <span data-ttu-id="457d1-2315">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2315">Array</span></span> | <span data-ttu-id="457d1-2316">The resulting array created from all the items in the specified string</span><span class="sxs-lookup"><span data-stu-id="457d1-2316">The resulting array created from all the items in the specified string</span></span> |
|||| 

<span data-ttu-id="457d1-2317">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2317">*Example*</span></span> 

<span data-ttu-id="457d1-2318">This example creates an array from the specified string, separating each character with a comma as the delimiter:</span><span class="sxs-lookup"><span data-stu-id="457d1-2318">This example creates an array from the specified string, separating each character with a comma as the delimiter:</span></span>

```
split('abc', ',')
```

<span data-ttu-id="457d1-2319">And returns this result: `[a, b, c]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2319">And returns this result: `[a, b, c]`</span></span>

<a name="startOfDay"></a>

### <a name="startofday"></a><span data-ttu-id="457d1-2320">startOfDay</span><span class="sxs-lookup"><span data-stu-id="457d1-2320">startOfDay</span></span>

<span data-ttu-id="457d1-2321">Return the start of the day for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2321">Return the start of the day for a timestamp.</span></span> 

```
startOfDay('<timestamp>', '<format>'?)
```

| <span data-ttu-id="457d1-2322">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2322">Parameter</span></span> | <span data-ttu-id="457d1-2323">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2323">Required</span></span> | <span data-ttu-id="457d1-2324">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2324">Type</span></span> | <span data-ttu-id="457d1-2325">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2325">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2326"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2326"><*timestamp*></span></span> | <span data-ttu-id="457d1-2327">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2327">Yes</span></span> | <span data-ttu-id="457d1-2328">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2328">String</span></span> | <span data-ttu-id="457d1-2329">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2329">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-2330"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-2330"><*format*></span></span> | <span data-ttu-id="457d1-2331">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2331">No</span></span> | <span data-ttu-id="457d1-2332">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2332">String</span></span> | <span data-ttu-id="457d1-2333">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-2333">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-2334">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-2334">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-2335">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2335">Return value</span></span> | <span data-ttu-id="457d1-2336">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2336">Type</span></span> | <span data-ttu-id="457d1-2337">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2337">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2338"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2338"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-2339">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2339">String</span></span> | <span data-ttu-id="457d1-2340">The specified timestamp but starting at the zero-hour mark for the day</span><span class="sxs-lookup"><span data-stu-id="457d1-2340">The specified timestamp but starting at the zero-hour mark for the day</span></span> | 
|||| 

<span data-ttu-id="457d1-2341">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2341">*Example*</span></span> 

<span data-ttu-id="457d1-2342">This example finds the start of the day for this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2342">This example finds the start of the day for this timestamp:</span></span>

```
startOfDay('2018-03-15T13:30:30Z')
```

<span data-ttu-id="457d1-2343">And returns this result: `"2018-03-15T00:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2343">And returns this result: `"2018-03-15T00:00:00.0000000Z"`</span></span>

<a name="startOfHour"></a>

### <a name="startofhour"></a><span data-ttu-id="457d1-2344">startOfHour</span><span class="sxs-lookup"><span data-stu-id="457d1-2344">startOfHour</span></span>

<span data-ttu-id="457d1-2345">Return the start of the hour for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2345">Return the start of the hour for a timestamp.</span></span> 

```
startOfHour('<timestamp>', '<format>'?)
```

| <span data-ttu-id="457d1-2346">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2346">Parameter</span></span> | <span data-ttu-id="457d1-2347">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2347">Required</span></span> | <span data-ttu-id="457d1-2348">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2348">Type</span></span> | <span data-ttu-id="457d1-2349">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2349">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2350"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2350"><*timestamp*></span></span> | <span data-ttu-id="457d1-2351">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2351">Yes</span></span> | <span data-ttu-id="457d1-2352">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2352">String</span></span> | <span data-ttu-id="457d1-2353">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2353">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-2354"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-2354"><*format*></span></span> | <span data-ttu-id="457d1-2355">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2355">No</span></span> | <span data-ttu-id="457d1-2356">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2356">String</span></span> | <span data-ttu-id="457d1-2357">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-2357">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-2358">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-2358">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-2359">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2359">Return value</span></span> | <span data-ttu-id="457d1-2360">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2360">Type</span></span> | <span data-ttu-id="457d1-2361">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2361">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2362"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2362"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-2363">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2363">String</span></span> | <span data-ttu-id="457d1-2364">The specified timestamp but starting at the zero-minute mark for the hour</span><span class="sxs-lookup"><span data-stu-id="457d1-2364">The specified timestamp but starting at the zero-minute mark for the hour</span></span> | 
|||| 

<span data-ttu-id="457d1-2365">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2365">*Example*</span></span> 

<span data-ttu-id="457d1-2366">This example finds the start of the hour for this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2366">This example finds the start of the hour for this timestamp:</span></span>

```
startOfHour('2018-03-15T13:30:30Z')
```

<span data-ttu-id="457d1-2367">And returns this result: `"2018-03-15T13:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2367">And returns this result: `"2018-03-15T13:00:00.0000000Z"`</span></span>

<a name="startOfMonth"></a>

### <a name="startofmonth"></a><span data-ttu-id="457d1-2368">startOfMonth</span><span class="sxs-lookup"><span data-stu-id="457d1-2368">startOfMonth</span></span>

<span data-ttu-id="457d1-2369">Return the start of the month for a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2369">Return the start of the month for a timestamp.</span></span> 

```
startOfMonth('<timestamp>', '<format>'?)
```

| <span data-ttu-id="457d1-2370">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2370">Parameter</span></span> | <span data-ttu-id="457d1-2371">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2371">Required</span></span> | <span data-ttu-id="457d1-2372">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2372">Type</span></span> | <span data-ttu-id="457d1-2373">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2373">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2374"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2374"><*timestamp*></span></span> | <span data-ttu-id="457d1-2375">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2375">Yes</span></span> | <span data-ttu-id="457d1-2376">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2376">String</span></span> | <span data-ttu-id="457d1-2377">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2377">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-2378"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-2378"><*format*></span></span> | <span data-ttu-id="457d1-2379">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2379">No</span></span> | <span data-ttu-id="457d1-2380">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2380">String</span></span> | <span data-ttu-id="457d1-2381">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-2381">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-2382">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-2382">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> |
||||| 

| <span data-ttu-id="457d1-2383">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2383">Return value</span></span> | <span data-ttu-id="457d1-2384">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2384">Type</span></span> | <span data-ttu-id="457d1-2385">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2385">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2386"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2386"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-2387">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2387">String</span></span> | <span data-ttu-id="457d1-2388">The specified timestamp but starting on the first day of the month at the zero-hour mark</span><span class="sxs-lookup"><span data-stu-id="457d1-2388">The specified timestamp but starting on the first day of the month at the zero-hour mark</span></span> | 
|||| 

<span data-ttu-id="457d1-2389">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2389">*Example*</span></span> 

<span data-ttu-id="457d1-2390">This example returns the start of the month for this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2390">This example returns the start of the month for this timestamp:</span></span>

```
startOfMonth('2018-03-15T13:30:30Z')
```

<span data-ttu-id="457d1-2391">And returns this result: `"2018-03-01T00:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2391">And returns this result: `"2018-03-01T00:00:00.0000000Z"`</span></span>

<a name="startswith"></a>

### <a name="startswith"></a><span data-ttu-id="457d1-2392">startsWith</span><span class="sxs-lookup"><span data-stu-id="457d1-2392">startsWith</span></span>

<span data-ttu-id="457d1-2393">Check whether a string starts with a specific substring.</span><span class="sxs-lookup"><span data-stu-id="457d1-2393">Check whether a string starts with a specific substring.</span></span> <span data-ttu-id="457d1-2394">Return true when the substring is found, or return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-2394">Return true when the substring is found, or return false when not found.</span></span> <span data-ttu-id="457d1-2395">This function is not case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="457d1-2395">This function is not case-sensitive.</span></span>

```
startsWith('<text>', '<searchText>')
```

| <span data-ttu-id="457d1-2396">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2396">Parameter</span></span> | <span data-ttu-id="457d1-2397">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2397">Required</span></span> | <span data-ttu-id="457d1-2398">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2398">Type</span></span> | <span data-ttu-id="457d1-2399">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2399">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2400"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2400"><*text*></span></span> | <span data-ttu-id="457d1-2401">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2401">Yes</span></span> | <span data-ttu-id="457d1-2402">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2402">String</span></span> | <span data-ttu-id="457d1-2403">The string to check</span><span class="sxs-lookup"><span data-stu-id="457d1-2403">The string to check</span></span> | 
| <span data-ttu-id="457d1-2404"><*searchText*></span><span class="sxs-lookup"><span data-stu-id="457d1-2404"><*searchText*></span></span> | <span data-ttu-id="457d1-2405">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2405">Yes</span></span> | <span data-ttu-id="457d1-2406">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2406">String</span></span> | <span data-ttu-id="457d1-2407">The starting string to find</span><span class="sxs-lookup"><span data-stu-id="457d1-2407">The starting string to find</span></span> | 
||||| 

| <span data-ttu-id="457d1-2408">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2408">Return value</span></span> | <span data-ttu-id="457d1-2409">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2409">Type</span></span> | <span data-ttu-id="457d1-2410">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2410">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2411">true or false</span><span class="sxs-lookup"><span data-stu-id="457d1-2411">true or false</span></span>  | <span data-ttu-id="457d1-2412">Boolean</span><span class="sxs-lookup"><span data-stu-id="457d1-2412">Boolean</span></span> | <span data-ttu-id="457d1-2413">Return true when the starting substring is found.</span><span class="sxs-lookup"><span data-stu-id="457d1-2413">Return true when the starting substring is found.</span></span> <span data-ttu-id="457d1-2414">Return false when not found.</span><span class="sxs-lookup"><span data-stu-id="457d1-2414">Return false when not found.</span></span> | 
|||| 

<span data-ttu-id="457d1-2415">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2415">*Example 1*</span></span> 

<span data-ttu-id="457d1-2416">This example checks whether the "hello world" string starts with the "hello" substring:</span><span class="sxs-lookup"><span data-stu-id="457d1-2416">This example checks whether the "hello world" string starts with the "hello" substring:</span></span>

```
startsWith('hello world', 'hello')
```

<span data-ttu-id="457d1-2417">And returns this result: `true`</span><span class="sxs-lookup"><span data-stu-id="457d1-2417">And returns this result: `true`</span></span>

<span data-ttu-id="457d1-2418">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2418">*Example 2*</span></span>

<span data-ttu-id="457d1-2419">This example checks whether the "hello world" string starts with the "greetings" substring:</span><span class="sxs-lookup"><span data-stu-id="457d1-2419">This example checks whether the "hello world" string starts with the "greetings" substring:</span></span>

```
startsWith('hello world', 'greetings')
```

<span data-ttu-id="457d1-2420">And returns this result: `false`</span><span class="sxs-lookup"><span data-stu-id="457d1-2420">And returns this result: `false`</span></span>

<a name="string"></a>

### <a name="string"></a><span data-ttu-id="457d1-2421">string</span><span class="sxs-lookup"><span data-stu-id="457d1-2421">string</span></span>

<span data-ttu-id="457d1-2422">Return the string version for a value.</span><span class="sxs-lookup"><span data-stu-id="457d1-2422">Return the string version for a value.</span></span>

```
string(<value>)
```

| <span data-ttu-id="457d1-2423">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2423">Parameter</span></span> | <span data-ttu-id="457d1-2424">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2424">Required</span></span> | <span data-ttu-id="457d1-2425">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2425">Type</span></span> | <span data-ttu-id="457d1-2426">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2426">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2427"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2427"><*value*></span></span> | <span data-ttu-id="457d1-2428">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2428">Yes</span></span> | <span data-ttu-id="457d1-2429">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-2429">Any</span></span> | <span data-ttu-id="457d1-2430">The value to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-2430">The value to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-2431">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2431">Return value</span></span> | <span data-ttu-id="457d1-2432">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2432">Type</span></span> | <span data-ttu-id="457d1-2433">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2433">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2434"><*string-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2434"><*string-value*></span></span> | <span data-ttu-id="457d1-2435">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2435">String</span></span> | <span data-ttu-id="457d1-2436">The string version for the specified value</span><span class="sxs-lookup"><span data-stu-id="457d1-2436">The string version for the specified value</span></span> | 
|||| 

<span data-ttu-id="457d1-2437">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2437">*Example 1*</span></span> 

<span data-ttu-id="457d1-2438">This example creates the string version for this number:</span><span class="sxs-lookup"><span data-stu-id="457d1-2438">This example creates the string version for this number:</span></span>

```
string(10)
```

<span data-ttu-id="457d1-2439">And returns this result: `"10"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2439">And returns this result: `"10"`</span></span>

<span data-ttu-id="457d1-2440">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2440">*Example 2*</span></span>

<span data-ttu-id="457d1-2441">This example creates a string for the specified JSON object and uses the backslash character (\\) as an escape character for the double-quotation mark (").</span><span class="sxs-lookup"><span data-stu-id="457d1-2441">This example creates a string for the specified JSON object and uses the backslash character (\\) as an escape character for the double-quotation mark (").</span></span>

```
string( { "name": "Sophie Owen" } )
```

<span data-ttu-id="457d1-2442">And returns this result: `"{ \\"name\\": \\"Sophie Owen\\" }"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2442">And returns this result: `"{ \\"name\\": \\"Sophie Owen\\" }"`</span></span>

<a name="sub"></a>

### <a name="sub"></a><span data-ttu-id="457d1-2443">sub</span><span class="sxs-lookup"><span data-stu-id="457d1-2443">sub</span></span>

<span data-ttu-id="457d1-2444">Return the result from subtracting the second number from the first number.</span><span class="sxs-lookup"><span data-stu-id="457d1-2444">Return the result from subtracting the second number from the first number.</span></span>

```
sub(<minuend>, <subtrahend>)
```

| <span data-ttu-id="457d1-2445">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2445">Parameter</span></span> | <span data-ttu-id="457d1-2446">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2446">Required</span></span> | <span data-ttu-id="457d1-2447">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2447">Type</span></span> | <span data-ttu-id="457d1-2448">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2448">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2449"><*minuend*></span><span class="sxs-lookup"><span data-stu-id="457d1-2449"><*minuend*></span></span> | <span data-ttu-id="457d1-2450">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2450">Yes</span></span> | <span data-ttu-id="457d1-2451">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2451">Integer or Float</span></span> | <span data-ttu-id="457d1-2452">The number from which to subtract the *subtrahend*</span><span class="sxs-lookup"><span data-stu-id="457d1-2452">The number from which to subtract the *subtrahend*</span></span> | 
| <span data-ttu-id="457d1-2453"><*subtrahend*></span><span class="sxs-lookup"><span data-stu-id="457d1-2453"><*subtrahend*></span></span> | <span data-ttu-id="457d1-2454">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2454">Yes</span></span> | <span data-ttu-id="457d1-2455">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2455">Integer or Float</span></span> | <span data-ttu-id="457d1-2456">The number to subtract from the *minuend*</span><span class="sxs-lookup"><span data-stu-id="457d1-2456">The number to subtract from the *minuend*</span></span> | 
||||| 

| <span data-ttu-id="457d1-2457">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2457">Return value</span></span> | <span data-ttu-id="457d1-2458">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2458">Type</span></span> | <span data-ttu-id="457d1-2459">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2459">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2460"><*result*></span><span class="sxs-lookup"><span data-stu-id="457d1-2460"><*result*></span></span> | <span data-ttu-id="457d1-2461">Integer or Float</span><span class="sxs-lookup"><span data-stu-id="457d1-2461">Integer or Float</span></span> | <span data-ttu-id="457d1-2462">The result from subtracting the second number from the first number</span><span class="sxs-lookup"><span data-stu-id="457d1-2462">The result from subtracting the second number from the first number</span></span> | 
|||| 

<span data-ttu-id="457d1-2463">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2463">*Example*</span></span> 

<span data-ttu-id="457d1-2464">This example subtracts the second number from the first number:</span><span class="sxs-lookup"><span data-stu-id="457d1-2464">This example subtracts the second number from the first number:</span></span>

```
sub(10.3, .3)
```

<span data-ttu-id="457d1-2465">And returns this result: `10`</span><span class="sxs-lookup"><span data-stu-id="457d1-2465">And returns this result: `10`</span></span>

<a name="substring"></a>

### <a name="substring"></a><span data-ttu-id="457d1-2466">substring</span><span class="sxs-lookup"><span data-stu-id="457d1-2466">substring</span></span>

<span data-ttu-id="457d1-2467">Return characters from a string, starting from the specified position, or index.</span><span class="sxs-lookup"><span data-stu-id="457d1-2467">Return characters from a string, starting from the specified position, or index.</span></span> <span data-ttu-id="457d1-2468">Index values start with the number 0.</span><span class="sxs-lookup"><span data-stu-id="457d1-2468">Index values start with the number 0.</span></span> 

```
substring('<text>', <startIndex>, <length>)
```

| <span data-ttu-id="457d1-2469">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2469">Parameter</span></span> | <span data-ttu-id="457d1-2470">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2470">Required</span></span> | <span data-ttu-id="457d1-2471">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2471">Type</span></span> | <span data-ttu-id="457d1-2472">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2472">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2473"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2473"><*text*></span></span> | <span data-ttu-id="457d1-2474">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2474">Yes</span></span> | <span data-ttu-id="457d1-2475">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2475">String</span></span> | <span data-ttu-id="457d1-2476">The string whose characters you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2476">The string whose characters you want</span></span> | 
| <span data-ttu-id="457d1-2477"><*startIndex*></span><span class="sxs-lookup"><span data-stu-id="457d1-2477"><*startIndex*></span></span> | <span data-ttu-id="457d1-2478">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2478">Yes</span></span> | <span data-ttu-id="457d1-2479">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2479">Integer</span></span> | <span data-ttu-id="457d1-2480">A positive number for the starting position, or index value</span><span class="sxs-lookup"><span data-stu-id="457d1-2480">A positive number for the starting position, or index value</span></span> | 
| <span data-ttu-id="457d1-2481"><*length*></span><span class="sxs-lookup"><span data-stu-id="457d1-2481"><*length*></span></span> | <span data-ttu-id="457d1-2482">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2482">Yes</span></span> | <span data-ttu-id="457d1-2483">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2483">Integer</span></span> | <span data-ttu-id="457d1-2484">A positive number of characters that you want in the substring</span><span class="sxs-lookup"><span data-stu-id="457d1-2484">A positive number of characters that you want in the substring</span></span> | 
||||| 

| <span data-ttu-id="457d1-2485">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2485">Return value</span></span> | <span data-ttu-id="457d1-2486">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2486">Type</span></span> | <span data-ttu-id="457d1-2487">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2487">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2488"><*substring-result*></span><span class="sxs-lookup"><span data-stu-id="457d1-2488"><*substring-result*></span></span> | <span data-ttu-id="457d1-2489">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2489">String</span></span> | <span data-ttu-id="457d1-2490">A substring with the specified number of characters, starting at the specified index position in the source string</span><span class="sxs-lookup"><span data-stu-id="457d1-2490">A substring with the specified number of characters, starting at the specified index position in the source string</span></span> | 
|||| 

<span data-ttu-id="457d1-2491">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2491">*Example*</span></span> 

<span data-ttu-id="457d1-2492">This example creates a five-character substring from the specified string, starting from the index value 6:</span><span class="sxs-lookup"><span data-stu-id="457d1-2492">This example creates a five-character substring from the specified string, starting from the index value 6:</span></span>

```
substring('hello world', 6, 5)
```

<span data-ttu-id="457d1-2493">And returns this result: `"world"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2493">And returns this result: `"world"`</span></span>

<a name="subtractFromTime"></a>

### <a name="subtractfromtime"></a><span data-ttu-id="457d1-2494">subtractFromTime</span><span class="sxs-lookup"><span data-stu-id="457d1-2494">subtractFromTime</span></span>

<span data-ttu-id="457d1-2495">Subtract a number of time units from a timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2495">Subtract a number of time units from a timestamp.</span></span> <span data-ttu-id="457d1-2496">See also [getPastTime](#getPastTime).</span><span class="sxs-lookup"><span data-stu-id="457d1-2496">See also [getPastTime](#getPastTime).</span></span>

```
subtractFromTime('<timestamp>', <interval>, '<timeUnit>', '<format>'?)
```

| <span data-ttu-id="457d1-2497">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2497">Parameter</span></span> | <span data-ttu-id="457d1-2498">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2498">Required</span></span> | <span data-ttu-id="457d1-2499">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2499">Type</span></span> | <span data-ttu-id="457d1-2500">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2500">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2501"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2501"><*timestamp*></span></span> | <span data-ttu-id="457d1-2502">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2502">Yes</span></span> | <span data-ttu-id="457d1-2503">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2503">String</span></span> | <span data-ttu-id="457d1-2504">The string that contains the timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2504">The string that contains the timestamp</span></span> | 
| <span data-ttu-id="457d1-2505"><*interval*></span><span class="sxs-lookup"><span data-stu-id="457d1-2505"><*interval*></span></span> | <span data-ttu-id="457d1-2506">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2506">Yes</span></span> | <span data-ttu-id="457d1-2507">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2507">Integer</span></span> | <span data-ttu-id="457d1-2508">The number of specified time units to subtract</span><span class="sxs-lookup"><span data-stu-id="457d1-2508">The number of specified time units to subtract</span></span> | 
| <span data-ttu-id="457d1-2509"><*timeUnit*></span><span class="sxs-lookup"><span data-stu-id="457d1-2509"><*timeUnit*></span></span> | <span data-ttu-id="457d1-2510">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2510">Yes</span></span> | <span data-ttu-id="457d1-2511">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2511">String</span></span> | <span data-ttu-id="457d1-2512">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span><span class="sxs-lookup"><span data-stu-id="457d1-2512">The unit of time to use with *interval*: "Second", "Minute", "Hour", "Day", "Week", "Month", "Year"</span></span> | 
| <span data-ttu-id="457d1-2513"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-2513"><*format*></span></span> | <span data-ttu-id="457d1-2514">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2514">No</span></span> | <span data-ttu-id="457d1-2515">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2515">String</span></span> | <span data-ttu-id="457d1-2516">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-2516">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-2517">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-2517">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> | 
||||| 

| <span data-ttu-id="457d1-2518">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2518">Return value</span></span> | <span data-ttu-id="457d1-2519">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2519">Type</span></span> | <span data-ttu-id="457d1-2520">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2520">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2521"><*updated-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2521"><*updated-timestamp*></span></span> | <span data-ttu-id="457d1-2522">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2522">String</span></span> | <span data-ttu-id="457d1-2523">The timestamp minus the specified number of time units</span><span class="sxs-lookup"><span data-stu-id="457d1-2523">The timestamp minus the specified number of time units</span></span> | 
|||| 

<span data-ttu-id="457d1-2524">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2524">*Example 1*</span></span>

<span data-ttu-id="457d1-2525">This example subtracts one day from this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2525">This example subtracts one day from this timestamp:</span></span>

```
subtractFromTime('2018-01-02T00:00:00Z', 1, 'Day') 
```

<span data-ttu-id="457d1-2526">And returns this result: `"2018-01-01T00:00:00:0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2526">And returns this result: `"2018-01-01T00:00:00:0000000Z"`</span></span>

<span data-ttu-id="457d1-2527">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2527">*Example 2*</span></span>

<span data-ttu-id="457d1-2528">This example subtracts one day from this timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2528">This example subtracts one day from this timestamp:</span></span>

```
subtractFromTime('2018-01-02T00:00:00Z', 1, 'Day', 'D') 
```

<span data-ttu-id="457d1-2529">And returns this result using the optional "D" format: `"Monday, January, 1, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2529">And returns this result using the optional "D" format: `"Monday, January, 1, 2018"`</span></span>

<a name="take"></a>

### <a name="take"></a><span data-ttu-id="457d1-2530">take</span><span class="sxs-lookup"><span data-stu-id="457d1-2530">take</span></span>

<span data-ttu-id="457d1-2531">Return items from the front of a collection.</span><span class="sxs-lookup"><span data-stu-id="457d1-2531">Return items from the front of a collection.</span></span> 

```
take('<collection>', <count>)
take([<collection>], <count>)
```

| <span data-ttu-id="457d1-2532">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2532">Parameter</span></span> | <span data-ttu-id="457d1-2533">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2533">Required</span></span> | <span data-ttu-id="457d1-2534">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2534">Type</span></span> | <span data-ttu-id="457d1-2535">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2535">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2536"><*collection*></span><span class="sxs-lookup"><span data-stu-id="457d1-2536"><*collection*></span></span> | <span data-ttu-id="457d1-2537">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2537">Yes</span></span> | <span data-ttu-id="457d1-2538">String or Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2538">String or Array</span></span> | <span data-ttu-id="457d1-2539">The collection whose items you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2539">The collection whose items you want</span></span> | 
| <span data-ttu-id="457d1-2540"><*count*></span><span class="sxs-lookup"><span data-stu-id="457d1-2540"><*count*></span></span> | <span data-ttu-id="457d1-2541">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2541">Yes</span></span> | <span data-ttu-id="457d1-2542">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2542">Integer</span></span> | <span data-ttu-id="457d1-2543">A positive integer for the number of items that you want from the front</span><span class="sxs-lookup"><span data-stu-id="457d1-2543">A positive integer for the number of items that you want from the front</span></span> | 
||||| 

| <span data-ttu-id="457d1-2544">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2544">Return value</span></span> | <span data-ttu-id="457d1-2545">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2545">Type</span></span> | <span data-ttu-id="457d1-2546">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2546">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2547"><*subset*> or [<*subset*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-2547"><*subset*> or [<*subset*>]</span></span> | <span data-ttu-id="457d1-2548">String or Array, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-2548">String or Array, respectively</span></span> | <span data-ttu-id="457d1-2549">A string or array that has the specified number of items taken from the front of the original collection</span><span class="sxs-lookup"><span data-stu-id="457d1-2549">A string or array that has the specified number of items taken from the front of the original collection</span></span> | 
|||| 

<span data-ttu-id="457d1-2550">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2550">*Example*</span></span>

<span data-ttu-id="457d1-2551">These examples get the specified number of items from the front of these collections:</span><span class="sxs-lookup"><span data-stu-id="457d1-2551">These examples get the specified number of items from the front of these collections:</span></span>

```
take('abcde`, 3)
take([0, 1, 2, 3, 4], 3)
```

<span data-ttu-id="457d1-2552">And return these results:</span><span class="sxs-lookup"><span data-stu-id="457d1-2552">And return these results:</span></span>

* <span data-ttu-id="457d1-2553">First example: `"abc"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2553">First example: `"abc"`</span></span>
* <span data-ttu-id="457d1-2554">Second example: `[0, 1, 2]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2554">Second example: `[0, 1, 2]`</span></span>

<a name="ticks"></a>

### <a name="ticks"></a><span data-ttu-id="457d1-2555">ticks</span><span class="sxs-lookup"><span data-stu-id="457d1-2555">ticks</span></span>

<span data-ttu-id="457d1-2556">Return the `ticks` property value for a specified timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2556">Return the `ticks` property value for a specified timestamp.</span></span> <span data-ttu-id="457d1-2557">A *tick* is a 100-nanosecond interval.</span><span class="sxs-lookup"><span data-stu-id="457d1-2557">A *tick* is a 100-nanosecond interval.</span></span>

```
ticks('<timestamp>')
```

| <span data-ttu-id="457d1-2558">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2558">Parameter</span></span> | <span data-ttu-id="457d1-2559">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2559">Required</span></span> | <span data-ttu-id="457d1-2560">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2560">Type</span></span> | <span data-ttu-id="457d1-2561">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2561">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2562"><*timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2562"><*timestamp*></span></span> | <span data-ttu-id="457d1-2563">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2563">Yes</span></span> | <span data-ttu-id="457d1-2564">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2564">String</span></span> | <span data-ttu-id="457d1-2565">The string for a timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2565">The string for a timestamp</span></span> | 
||||| 

| <span data-ttu-id="457d1-2566">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2566">Return value</span></span> | <span data-ttu-id="457d1-2567">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2567">Type</span></span> | <span data-ttu-id="457d1-2568">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2568">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2569"><*ticks-number*></span><span class="sxs-lookup"><span data-stu-id="457d1-2569"><*ticks-number*></span></span> | <span data-ttu-id="457d1-2570">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2570">Integer</span></span> | <span data-ttu-id="457d1-2571">The number of ticks since the specified timestamp</span><span class="sxs-lookup"><span data-stu-id="457d1-2571">The number of ticks since the specified timestamp</span></span> | 
|||| 

<a name="toLower"></a>

### <a name="tolower"></a><span data-ttu-id="457d1-2572">toLower</span><span class="sxs-lookup"><span data-stu-id="457d1-2572">toLower</span></span>

<span data-ttu-id="457d1-2573">Return a string in lowercase format.</span><span class="sxs-lookup"><span data-stu-id="457d1-2573">Return a string in lowercase format.</span></span> <span data-ttu-id="457d1-2574">If a character in the string doesn't have a lowercase version, that character stays unchanged in the returned string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2574">If a character in the string doesn't have a lowercase version, that character stays unchanged in the returned string.</span></span>

```
toLower('<text>')
```

| <span data-ttu-id="457d1-2575">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2575">Parameter</span></span> | <span data-ttu-id="457d1-2576">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2576">Required</span></span> | <span data-ttu-id="457d1-2577">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2577">Type</span></span> | <span data-ttu-id="457d1-2578">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2578">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2579"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2579"><*text*></span></span> | <span data-ttu-id="457d1-2580">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2580">Yes</span></span> | <span data-ttu-id="457d1-2581">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2581">String</span></span> | <span data-ttu-id="457d1-2582">The string to return in lowercase format</span><span class="sxs-lookup"><span data-stu-id="457d1-2582">The string to return in lowercase format</span></span> | 
||||| 

| <span data-ttu-id="457d1-2583">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2583">Return value</span></span> | <span data-ttu-id="457d1-2584">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2584">Type</span></span> | <span data-ttu-id="457d1-2585">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2585">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2586"><*lowercase-text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2586"><*lowercase-text*></span></span> | <span data-ttu-id="457d1-2587">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2587">String</span></span> | <span data-ttu-id="457d1-2588">The original string in lowercase format</span><span class="sxs-lookup"><span data-stu-id="457d1-2588">The original string in lowercase format</span></span> | 
|||| 

<span data-ttu-id="457d1-2589">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2589">*Example*</span></span> 

<span data-ttu-id="457d1-2590">This example converts this string to lowercase:</span><span class="sxs-lookup"><span data-stu-id="457d1-2590">This example converts this string to lowercase:</span></span> 

```
toLower('Hello World')
```

<span data-ttu-id="457d1-2591">And returns this result: `"hello world"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2591">And returns this result: `"hello world"`</span></span>

<a name="toUpper"></a>

### <a name="toupper"></a><span data-ttu-id="457d1-2592">toUpper</span><span class="sxs-lookup"><span data-stu-id="457d1-2592">toUpper</span></span>

<span data-ttu-id="457d1-2593">Return a string in uppercase format.</span><span class="sxs-lookup"><span data-stu-id="457d1-2593">Return a string in uppercase format.</span></span> <span data-ttu-id="457d1-2594">If a character in the string doesn't have an uppercase version, that character stays unchanged in the returned string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2594">If a character in the string doesn't have an uppercase version, that character stays unchanged in the returned string.</span></span>

```
toUpper('<text>')
```

| <span data-ttu-id="457d1-2595">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2595">Parameter</span></span> | <span data-ttu-id="457d1-2596">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2596">Required</span></span> | <span data-ttu-id="457d1-2597">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2597">Type</span></span> | <span data-ttu-id="457d1-2598">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2598">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2599"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2599"><*text*></span></span> | <span data-ttu-id="457d1-2600">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2600">Yes</span></span> | <span data-ttu-id="457d1-2601">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2601">String</span></span> | <span data-ttu-id="457d1-2602">The string to return in uppercase format</span><span class="sxs-lookup"><span data-stu-id="457d1-2602">The string to return in uppercase format</span></span> | 
||||| 

| <span data-ttu-id="457d1-2603">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2603">Return value</span></span> | <span data-ttu-id="457d1-2604">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2604">Type</span></span> | <span data-ttu-id="457d1-2605">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2605">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2606"><*uppercase-text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2606"><*uppercase-text*></span></span> | <span data-ttu-id="457d1-2607">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2607">String</span></span> | <span data-ttu-id="457d1-2608">The original string in uppercase format</span><span class="sxs-lookup"><span data-stu-id="457d1-2608">The original string in uppercase format</span></span> | 
|||| 

<span data-ttu-id="457d1-2609">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2609">*Example*</span></span> 

<span data-ttu-id="457d1-2610">This example converts this string to uppercase:</span><span class="sxs-lookup"><span data-stu-id="457d1-2610">This example converts this string to uppercase:</span></span>

```
toUpper('Hello World')
```

<span data-ttu-id="457d1-2611">And returns this result: `"HELLO WORLD"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2611">And returns this result: `"HELLO WORLD"`</span></span>

<a name="trigger"></a>

### <a name="trigger"></a><span data-ttu-id="457d1-2612">trigger</span><span class="sxs-lookup"><span data-stu-id="457d1-2612">trigger</span></span>

<span data-ttu-id="457d1-2613">Return a trigger's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span><span class="sxs-lookup"><span data-stu-id="457d1-2613">Return a trigger's output at runtime, or values from other JSON name-and-value pairs, which you can assign to an expression.</span></span> 

* <span data-ttu-id="457d1-2614">Inside a trigger's inputs, this function returns the output from the previous execution.</span><span class="sxs-lookup"><span data-stu-id="457d1-2614">Inside a trigger's inputs, this function returns the output from the previous execution.</span></span> 

* <span data-ttu-id="457d1-2615">Inside a trigger's condition, this function returns the output from the current execution.</span><span class="sxs-lookup"><span data-stu-id="457d1-2615">Inside a trigger's condition, this function returns the output from the current execution.</span></span> 

<span data-ttu-id="457d1-2616">By default, the function references the entire trigger object, but you can optionally specify a property whose value that you want.</span><span class="sxs-lookup"><span data-stu-id="457d1-2616">By default, the function references the entire trigger object, but you can optionally specify a property whose value that you want.</span></span> <span data-ttu-id="457d1-2617">Also, this function has shorthand versions available, see [triggerOutputs()](#triggerOutputs) and [triggerBody()](#triggerBody).</span><span class="sxs-lookup"><span data-stu-id="457d1-2617">Also, this function has shorthand versions available, see [triggerOutputs()](#triggerOutputs) and [triggerBody()](#triggerBody).</span></span> 

```
trigger()
```

| <span data-ttu-id="457d1-2618">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2618">Return value</span></span> | <span data-ttu-id="457d1-2619">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2619">Type</span></span> | <span data-ttu-id="457d1-2620">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2620">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2621"><*trigger-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-2621"><*trigger-output*></span></span> | <span data-ttu-id="457d1-2622">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2622">String</span></span> | <span data-ttu-id="457d1-2623">The output from a trigger at runtime</span><span class="sxs-lookup"><span data-stu-id="457d1-2623">The output from a trigger at runtime</span></span> | 
|||| 

<a name="triggerBody"></a>

### <a name="triggerbody"></a><span data-ttu-id="457d1-2624">triggerBody</span><span class="sxs-lookup"><span data-stu-id="457d1-2624">triggerBody</span></span>

<span data-ttu-id="457d1-2625">Return a trigger's `body` output at runtime.</span><span class="sxs-lookup"><span data-stu-id="457d1-2625">Return a trigger's `body` output at runtime.</span></span> <span data-ttu-id="457d1-2626">Shorthand for `trigger().outputs.body`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2626">Shorthand for `trigger().outputs.body`.</span></span> <span data-ttu-id="457d1-2627">See [trigger()](#trigger).</span><span class="sxs-lookup"><span data-stu-id="457d1-2627">See [trigger()](#trigger).</span></span> 

```
triggerBody()
```

| <span data-ttu-id="457d1-2628">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2628">Return value</span></span> | <span data-ttu-id="457d1-2629">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2629">Type</span></span> | <span data-ttu-id="457d1-2630">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2630">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2631"><*trigger-body-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-2631"><*trigger-body-output*></span></span> | <span data-ttu-id="457d1-2632">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2632">String</span></span> | <span data-ttu-id="457d1-2633">The `body` output from the trigger</span><span class="sxs-lookup"><span data-stu-id="457d1-2633">The `body` output from the trigger</span></span> | 
|||| 

<a name="triggerFormDataMultiValues"></a>

### <a name="triggerformdatamultivalues"></a><span data-ttu-id="457d1-2634">triggerFormDataMultiValues</span><span class="sxs-lookup"><span data-stu-id="457d1-2634">triggerFormDataMultiValues</span></span>

<span data-ttu-id="457d1-2635">Return an array with values that match a key name in a trigger's *form-data* or *form-encoded* output.</span><span class="sxs-lookup"><span data-stu-id="457d1-2635">Return an array with values that match a key name in a trigger's *form-data* or *form-encoded* output.</span></span> 

```
triggerFormDataMultiValues('<key>')
```

| <span data-ttu-id="457d1-2636">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2636">Parameter</span></span> | <span data-ttu-id="457d1-2637">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2637">Required</span></span> | <span data-ttu-id="457d1-2638">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2638">Type</span></span> | <span data-ttu-id="457d1-2639">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2639">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2640"><*key*></span><span class="sxs-lookup"><span data-stu-id="457d1-2640"><*key*></span></span> | <span data-ttu-id="457d1-2641">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2641">Yes</span></span> | <span data-ttu-id="457d1-2642">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2642">String</span></span> | <span data-ttu-id="457d1-2643">The name for the key whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2643">The name for the key whose value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2644">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2644">Return value</span></span> | <span data-ttu-id="457d1-2645">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2645">Type</span></span> | <span data-ttu-id="457d1-2646">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2646">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2647">[<*array-with-key-values*>]</span><span class="sxs-lookup"><span data-stu-id="457d1-2647">[<*array-with-key-values*>]</span></span> | <span data-ttu-id="457d1-2648">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-2648">Array</span></span> | <span data-ttu-id="457d1-2649">An array with all the values that match the specified key</span><span class="sxs-lookup"><span data-stu-id="457d1-2649">An array with all the values that match the specified key</span></span> | 
|||| 

<span data-ttu-id="457d1-2650">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2650">*Example*</span></span> 

<span data-ttu-id="457d1-2651">This example creates an array from the "feedUrl" key value in an RSS trigger's form-data or form-encoded output:</span><span class="sxs-lookup"><span data-stu-id="457d1-2651">This example creates an array from the "feedUrl" key value in an RSS trigger's form-data or form-encoded output:</span></span> 

```
triggerFormDataMultiValues('feedUrl')
```

<span data-ttu-id="457d1-2652">And returns this array as an example result: `["http://feeds.reuters.com/reuters/topNews"]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2652">And returns this array as an example result: `["http://feeds.reuters.com/reuters/topNews"]`</span></span>

<a name="triggerFormDataValue"></a>

### <a name="triggerformdatavalue"></a><span data-ttu-id="457d1-2653">triggerFormDataValue</span><span class="sxs-lookup"><span data-stu-id="457d1-2653">triggerFormDataValue</span></span>

<span data-ttu-id="457d1-2654">Return a string with a single value that matches a key name in a trigger's *form-data* or *form-encoded* output.</span><span class="sxs-lookup"><span data-stu-id="457d1-2654">Return a string with a single value that matches a key name in a trigger's *form-data* or *form-encoded* output.</span></span> <span data-ttu-id="457d1-2655">If the function finds more than one match, the function throws an error.</span><span class="sxs-lookup"><span data-stu-id="457d1-2655">If the function finds more than one match, the function throws an error.</span></span>

```
triggerFormDataValue('<key>')
```

| <span data-ttu-id="457d1-2656">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2656">Parameter</span></span> | <span data-ttu-id="457d1-2657">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2657">Required</span></span> | <span data-ttu-id="457d1-2658">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2658">Type</span></span> | <span data-ttu-id="457d1-2659">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2659">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2660"><*key*></span><span class="sxs-lookup"><span data-stu-id="457d1-2660"><*key*></span></span> | <span data-ttu-id="457d1-2661">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2661">Yes</span></span> | <span data-ttu-id="457d1-2662">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2662">String</span></span> | <span data-ttu-id="457d1-2663">The name for the key whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2663">The name for the key whose value you want</span></span> |
||||| 

| <span data-ttu-id="457d1-2664">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2664">Return value</span></span> | <span data-ttu-id="457d1-2665">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2665">Type</span></span> | <span data-ttu-id="457d1-2666">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2666">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2667"><*key-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2667"><*key-value*></span></span> | <span data-ttu-id="457d1-2668">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2668">String</span></span> | <span data-ttu-id="457d1-2669">The value in the specified key</span><span class="sxs-lookup"><span data-stu-id="457d1-2669">The value in the specified key</span></span> | 
|||| 

<span data-ttu-id="457d1-2670">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2670">*Example*</span></span> 

<span data-ttu-id="457d1-2671">This example creates a string from the "feedUrl" key value in an RSS trigger's form-data or form-encoded output:</span><span class="sxs-lookup"><span data-stu-id="457d1-2671">This example creates a string from the "feedUrl" key value in an RSS trigger's form-data or form-encoded output:</span></span>

```
triggerFormDataValue('feedUrl')
```

<span data-ttu-id="457d1-2672">And returns this string as an example result: `"http://feeds.reuters.com/reuters/topNews"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2672">And returns this string as an example result: `"http://feeds.reuters.com/reuters/topNews"`</span></span> 

<a name="triggerMultipartBody"></a>

### <a name="triggermultipartbody"></a><span data-ttu-id="457d1-2673">triggerMultipartBody</span><span class="sxs-lookup"><span data-stu-id="457d1-2673">triggerMultipartBody</span></span>

<span data-ttu-id="457d1-2674">Return the body for a specific part in a trigger's output that has multiple parts.</span><span class="sxs-lookup"><span data-stu-id="457d1-2674">Return the body for a specific part in a trigger's output that has multiple parts.</span></span> 

```
triggerMultipartBody(<index>)
```

| <span data-ttu-id="457d1-2675">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2675">Parameter</span></span> | <span data-ttu-id="457d1-2676">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2676">Required</span></span> | <span data-ttu-id="457d1-2677">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2677">Type</span></span> | <span data-ttu-id="457d1-2678">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2678">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2679"><*index*></span><span class="sxs-lookup"><span data-stu-id="457d1-2679"><*index*></span></span> | <span data-ttu-id="457d1-2680">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2680">Yes</span></span> | <span data-ttu-id="457d1-2681">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2681">Integer</span></span> | <span data-ttu-id="457d1-2682">The index value for the part that you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2682">The index value for the part that you want</span></span> |
||||| 

| <span data-ttu-id="457d1-2683">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2683">Return value</span></span> | <span data-ttu-id="457d1-2684">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2684">Type</span></span> | <span data-ttu-id="457d1-2685">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2685">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2686"><*body*></span><span class="sxs-lookup"><span data-stu-id="457d1-2686"><*body*></span></span> | <span data-ttu-id="457d1-2687">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2687">String</span></span> | <span data-ttu-id="457d1-2688">The body for the specified part in a trigger's multipart output</span><span class="sxs-lookup"><span data-stu-id="457d1-2688">The body for the specified part in a trigger's multipart output</span></span> | 
|||| 

<a name="triggerOutputs"></a>

### <a name="triggeroutputs"></a><span data-ttu-id="457d1-2689">triggerOutputs</span><span class="sxs-lookup"><span data-stu-id="457d1-2689">triggerOutputs</span></span>

<span data-ttu-id="457d1-2690">Return a trigger's output at runtime, or values from other JSON name-and-value pairs.</span><span class="sxs-lookup"><span data-stu-id="457d1-2690">Return a trigger's output at runtime, or values from other JSON name-and-value pairs.</span></span> <span data-ttu-id="457d1-2691">Shorthand for `trigger().outputs`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2691">Shorthand for `trigger().outputs`.</span></span> <span data-ttu-id="457d1-2692">See [trigger()](#trigger).</span><span class="sxs-lookup"><span data-stu-id="457d1-2692">See [trigger()](#trigger).</span></span> 

```
triggerOutputs()
```

| <span data-ttu-id="457d1-2693">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2693">Return value</span></span> | <span data-ttu-id="457d1-2694">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2694">Type</span></span> | <span data-ttu-id="457d1-2695">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2695">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2696"><*trigger-output*></span><span class="sxs-lookup"><span data-stu-id="457d1-2696"><*trigger-output*></span></span> | <span data-ttu-id="457d1-2697">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2697">String</span></span> | <span data-ttu-id="457d1-2698">The output from a trigger at runtime</span><span class="sxs-lookup"><span data-stu-id="457d1-2698">The output from a trigger at runtime</span></span>  | 
|||| 

<a name="trim"></a>

### <a name="trim"></a><span data-ttu-id="457d1-2699">trim</span><span class="sxs-lookup"><span data-stu-id="457d1-2699">trim</span></span>

<span data-ttu-id="457d1-2700">Remove leading and trailing whitespace from a string, and return the updated string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2700">Remove leading and trailing whitespace from a string, and return the updated string.</span></span>

```
trim('<text>')
```

| <span data-ttu-id="457d1-2701">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2701">Parameter</span></span> | <span data-ttu-id="457d1-2702">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2702">Required</span></span> | <span data-ttu-id="457d1-2703">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2703">Type</span></span> | <span data-ttu-id="457d1-2704">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2704">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2705"><*text*></span><span class="sxs-lookup"><span data-stu-id="457d1-2705"><*text*></span></span> | <span data-ttu-id="457d1-2706">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2706">Yes</span></span> | <span data-ttu-id="457d1-2707">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2707">String</span></span> | <span data-ttu-id="457d1-2708">The string that has the leading and trailing whitespace to remove</span><span class="sxs-lookup"><span data-stu-id="457d1-2708">The string that has the leading and trailing whitespace to remove</span></span> | 
||||| 

| <span data-ttu-id="457d1-2709">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2709">Return value</span></span> | <span data-ttu-id="457d1-2710">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2710">Type</span></span> | <span data-ttu-id="457d1-2711">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2711">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2712"><*updatedText*></span><span class="sxs-lookup"><span data-stu-id="457d1-2712"><*updatedText*></span></span> | <span data-ttu-id="457d1-2713">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2713">String</span></span> | <span data-ttu-id="457d1-2714">An updated version for the original string without leading or trailing whitespace</span><span class="sxs-lookup"><span data-stu-id="457d1-2714">An updated version for the original string without leading or trailing whitespace</span></span> | 
|||| 

<span data-ttu-id="457d1-2715">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2715">*Example*</span></span> 

<span data-ttu-id="457d1-2716">This example removes the leading and trailing whitespace from the string " Hello World  ":</span><span class="sxs-lookup"><span data-stu-id="457d1-2716">This example removes the leading and trailing whitespace from the string " Hello World  ":</span></span>  

```
trim(' Hello World  ')
```

<span data-ttu-id="457d1-2717">And returns this result: `"Hello World"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2717">And returns this result: `"Hello World"`</span></span>

<a name="union"></a>

### <a name="union"></a><span data-ttu-id="457d1-2718">union</span><span class="sxs-lookup"><span data-stu-id="457d1-2718">union</span></span>

<span data-ttu-id="457d1-2719">Return a collection that has *all* the items from the specified collections.</span><span class="sxs-lookup"><span data-stu-id="457d1-2719">Return a collection that has *all* the items from the specified collections.</span></span> <span data-ttu-id="457d1-2720">To appear in the result, an item can appear in any collection passed to this function.</span><span class="sxs-lookup"><span data-stu-id="457d1-2720">To appear in the result, an item can appear in any collection passed to this function.</span></span> <span data-ttu-id="457d1-2721">If one or more items have the same name, the last item with that name appears in the result.</span><span class="sxs-lookup"><span data-stu-id="457d1-2721">If one or more items have the same name, the last item with that name appears in the result.</span></span> 

```
union('<collection1>', '<collection2>', ...)
union([<collection1>], [<collection2>], ...)
```

| <span data-ttu-id="457d1-2722">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2722">Parameter</span></span> | <span data-ttu-id="457d1-2723">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2723">Required</span></span> | <span data-ttu-id="457d1-2724">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2724">Type</span></span> | <span data-ttu-id="457d1-2725">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2725">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2726"><*collection1*>, <*collection2*>, ...</span><span class="sxs-lookup"><span data-stu-id="457d1-2726"><*collection1*>, <*collection2*>, ...</span></span>  | <span data-ttu-id="457d1-2727">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2727">Yes</span></span> | <span data-ttu-id="457d1-2728">Array or Object, but not both</span><span class="sxs-lookup"><span data-stu-id="457d1-2728">Array or Object, but not both</span></span> | <span data-ttu-id="457d1-2729">The collections from where you want *all* the items</span><span class="sxs-lookup"><span data-stu-id="457d1-2729">The collections from where you want *all* the items</span></span> | 
||||| 

| <span data-ttu-id="457d1-2730">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2730">Return value</span></span> | <span data-ttu-id="457d1-2731">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2731">Type</span></span> | <span data-ttu-id="457d1-2732">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2732">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2733"><*updatedCollection*></span><span class="sxs-lookup"><span data-stu-id="457d1-2733"><*updatedCollection*></span></span> | <span data-ttu-id="457d1-2734">Array or Object, respectively</span><span class="sxs-lookup"><span data-stu-id="457d1-2734">Array or Object, respectively</span></span> | <span data-ttu-id="457d1-2735">A collection with all the items from the specified collections - no duplicates</span><span class="sxs-lookup"><span data-stu-id="457d1-2735">A collection with all the items from the specified collections - no duplicates</span></span> | 
|||| 

<span data-ttu-id="457d1-2736">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2736">*Example*</span></span> 

<span data-ttu-id="457d1-2737">This example gets *all* the items from these collections:</span><span class="sxs-lookup"><span data-stu-id="457d1-2737">This example gets *all* the items from these collections:</span></span> 

```
union([1, 2, 3], [1, 2, 10, 101])
```

<span data-ttu-id="457d1-2738">And returns this result: `[1, 2, 3, 10, 101]`</span><span class="sxs-lookup"><span data-stu-id="457d1-2738">And returns this result: `[1, 2, 3, 10, 101]`</span></span>

<a name="uriComponent"></a>

### <a name="uricomponent"></a><span data-ttu-id="457d1-2739">uriComponent</span><span class="sxs-lookup"><span data-stu-id="457d1-2739">uriComponent</span></span>

<span data-ttu-id="457d1-2740">Return a uniform resource identifier (URI) encoded version for a string by replacing URL-unsafe characters with escape characters.</span><span class="sxs-lookup"><span data-stu-id="457d1-2740">Return a uniform resource identifier (URI) encoded version for a string by replacing URL-unsafe characters with escape characters.</span></span> <span data-ttu-id="457d1-2741">Use this function rather than [encodeUriComponent()](#encodeUriComponent).</span><span class="sxs-lookup"><span data-stu-id="457d1-2741">Use this function rather than [encodeUriComponent()](#encodeUriComponent).</span></span> <span data-ttu-id="457d1-2742">Although both functions work the same way, `uriComponent()` is preferred.</span><span class="sxs-lookup"><span data-stu-id="457d1-2742">Although both functions work the same way, `uriComponent()` is preferred.</span></span>

```
uriComponent('<value>')
```

| <span data-ttu-id="457d1-2743">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2743">Parameter</span></span> | <span data-ttu-id="457d1-2744">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2744">Required</span></span> | <span data-ttu-id="457d1-2745">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2745">Type</span></span> | <span data-ttu-id="457d1-2746">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2746">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2747"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2747"><*value*></span></span> | <span data-ttu-id="457d1-2748">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2748">Yes</span></span> | <span data-ttu-id="457d1-2749">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2749">String</span></span> | <span data-ttu-id="457d1-2750">The string to convert to URI-encoded format</span><span class="sxs-lookup"><span data-stu-id="457d1-2750">The string to convert to URI-encoded format</span></span> | 
||||| 

| <span data-ttu-id="457d1-2751">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2751">Return value</span></span> | <span data-ttu-id="457d1-2752">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2752">Type</span></span> | <span data-ttu-id="457d1-2753">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2753">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2754"><*encoded-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2754"><*encoded-uri*></span></span> | <span data-ttu-id="457d1-2755">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2755">String</span></span> | <span data-ttu-id="457d1-2756">The URI-encoded string with escape characters</span><span class="sxs-lookup"><span data-stu-id="457d1-2756">The URI-encoded string with escape characters</span></span> | 
|||| 

<span data-ttu-id="457d1-2757">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2757">*Example*</span></span>

<span data-ttu-id="457d1-2758">This example creates a URI-encoded version for this string:</span><span class="sxs-lookup"><span data-stu-id="457d1-2758">This example creates a URI-encoded version for this string:</span></span>

```
uriComponent('https://contoso.com')
```

<span data-ttu-id="457d1-2759">And returns this result: `"http%3A%2F%2Fcontoso.com"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2759">And returns this result: `"http%3A%2F%2Fcontoso.com"`</span></span>

<a name="uriComponentToBinary"></a>

### <a name="uricomponenttobinary"></a><span data-ttu-id="457d1-2760">uriComponentToBinary</span><span class="sxs-lookup"><span data-stu-id="457d1-2760">uriComponentToBinary</span></span>

<span data-ttu-id="457d1-2761">Return the binary version for a uniform resource identifier (URI) component.</span><span class="sxs-lookup"><span data-stu-id="457d1-2761">Return the binary version for a uniform resource identifier (URI) component.</span></span>

```
uriComponentToBinary('<value>')
```

| <span data-ttu-id="457d1-2762">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2762">Parameter</span></span> | <span data-ttu-id="457d1-2763">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2763">Required</span></span> | <span data-ttu-id="457d1-2764">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2764">Type</span></span> | <span data-ttu-id="457d1-2765">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2765">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2766"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2766"><*value*></span></span> | <span data-ttu-id="457d1-2767">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2767">Yes</span></span> | <span data-ttu-id="457d1-2768">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2768">String</span></span> | <span data-ttu-id="457d1-2769">The URI-encoded string to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-2769">The URI-encoded string to convert</span></span> | 
||||| 

| <span data-ttu-id="457d1-2770">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2770">Return value</span></span> | <span data-ttu-id="457d1-2771">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2771">Type</span></span> | <span data-ttu-id="457d1-2772">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2772">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2773"><*binary-for-encoded-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2773"><*binary-for-encoded-uri*></span></span> | <span data-ttu-id="457d1-2774">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2774">String</span></span> | <span data-ttu-id="457d1-2775">The binary version for the URI-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2775">The binary version for the URI-encoded string.</span></span> <span data-ttu-id="457d1-2776">The binary content is base64-encoded and represented by `$content`.</span><span class="sxs-lookup"><span data-stu-id="457d1-2776">The binary content is base64-encoded and represented by `$content`.</span></span> | 
|||| 

<span data-ttu-id="457d1-2777">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2777">*Example*</span></span>

<span data-ttu-id="457d1-2778">This example creates the binary version for this URI-encoded string:</span><span class="sxs-lookup"><span data-stu-id="457d1-2778">This example creates the binary version for this URI-encoded string:</span></span> 

```
uriComponentToBinary('http%3A%2F%2Fcontoso.com')
```

<span data-ttu-id="457d1-2779">And returns this result:</span><span class="sxs-lookup"><span data-stu-id="457d1-2779">And returns this result:</span></span> 

`"001000100110100001110100011101000111000000100101001100
11010000010010010100110010010001100010010100110010010001
10011000110110111101101110011101000110111101110011011011
110010111001100011011011110110110100100010"`

<a name="uriComponentToString"></a>

### <a name="uricomponenttostring"></a><span data-ttu-id="457d1-2780">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="457d1-2780">uriComponentToString</span></span>

<span data-ttu-id="457d1-2781">Return the string version for a uniform resource identifier (URI) encoded string, effectively decoding the URI-encoded string.</span><span class="sxs-lookup"><span data-stu-id="457d1-2781">Return the string version for a uniform resource identifier (URI) encoded string, effectively decoding the URI-encoded string.</span></span>

```
uriComponentToString('<value>')
```

| <span data-ttu-id="457d1-2782">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2782">Parameter</span></span> | <span data-ttu-id="457d1-2783">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2783">Required</span></span> | <span data-ttu-id="457d1-2784">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2784">Type</span></span> | <span data-ttu-id="457d1-2785">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2785">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2786"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2786"><*value*></span></span> | <span data-ttu-id="457d1-2787">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2787">Yes</span></span> | <span data-ttu-id="457d1-2788">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2788">String</span></span> | <span data-ttu-id="457d1-2789">The URI-encoded string to decode</span><span class="sxs-lookup"><span data-stu-id="457d1-2789">The URI-encoded string to decode</span></span> | 
||||| 

| <span data-ttu-id="457d1-2790">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2790">Return value</span></span> | <span data-ttu-id="457d1-2791">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2791">Type</span></span> | <span data-ttu-id="457d1-2792">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2792">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2793"><*decoded-uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2793"><*decoded-uri*></span></span> | <span data-ttu-id="457d1-2794">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2794">String</span></span> | <span data-ttu-id="457d1-2795">The decoded version for the URI-encoded string</span><span class="sxs-lookup"><span data-stu-id="457d1-2795">The decoded version for the URI-encoded string</span></span> | 
|||| 

<span data-ttu-id="457d1-2796">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2796">*Example*</span></span>

<span data-ttu-id="457d1-2797">This example creates the decoded string version for this URI-encoded string:</span><span class="sxs-lookup"><span data-stu-id="457d1-2797">This example creates the decoded string version for this URI-encoded string:</span></span> 

```
uriComponentToString('http%3A%2F%2Fcontoso.com')
```

<span data-ttu-id="457d1-2798">And returns this result: `"https://contoso.com"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2798">And returns this result: `"https://contoso.com"`</span></span> 

<a name="uriHost"></a>

### <a name="urihost"></a><span data-ttu-id="457d1-2799">uriHost</span><span class="sxs-lookup"><span data-stu-id="457d1-2799">uriHost</span></span>

<span data-ttu-id="457d1-2800">Return the `host` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2800">Return the `host` value for a uniform resource identifier (URI).</span></span>

```
uriHost('<uri>')
```

| <span data-ttu-id="457d1-2801">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2801">Parameter</span></span> | <span data-ttu-id="457d1-2802">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2802">Required</span></span> | <span data-ttu-id="457d1-2803">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2803">Type</span></span> | <span data-ttu-id="457d1-2804">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2804">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2805"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2805"><*uri*></span></span> | <span data-ttu-id="457d1-2806">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2806">Yes</span></span> | <span data-ttu-id="457d1-2807">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2807">String</span></span> | <span data-ttu-id="457d1-2808">The URI whose `host` value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2808">The URI whose `host` value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2809">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2809">Return value</span></span> | <span data-ttu-id="457d1-2810">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2810">Type</span></span> | <span data-ttu-id="457d1-2811">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2811">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2812"><*host-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2812"><*host-value*></span></span> | <span data-ttu-id="457d1-2813">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2813">String</span></span> | <span data-ttu-id="457d1-2814">The `host` value for the specified URI</span><span class="sxs-lookup"><span data-stu-id="457d1-2814">The `host` value for the specified URI</span></span> | 
|||| 

<span data-ttu-id="457d1-2815">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2815">*Example*</span></span>

<span data-ttu-id="457d1-2816">This example finds the `host` value for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2816">This example finds the `host` value for this URI:</span></span> 

```
uriHost('https://www.localhost.com:8080')
```

<span data-ttu-id="457d1-2817">And returns this result: `"www.localhost.com"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2817">And returns this result: `"www.localhost.com"`</span></span>

<a name="uriPath"></a>

### <a name="uripath"></a><span data-ttu-id="457d1-2818">uriPath</span><span class="sxs-lookup"><span data-stu-id="457d1-2818">uriPath</span></span>

<span data-ttu-id="457d1-2819">Return the `path` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2819">Return the `path` value for a uniform resource identifier (URI).</span></span> 

```
uriPath('<uri>')
```

| <span data-ttu-id="457d1-2820">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2820">Parameter</span></span> | <span data-ttu-id="457d1-2821">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2821">Required</span></span> | <span data-ttu-id="457d1-2822">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2822">Type</span></span> | <span data-ttu-id="457d1-2823">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2823">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2824"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2824"><*uri*></span></span> | <span data-ttu-id="457d1-2825">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2825">Yes</span></span> | <span data-ttu-id="457d1-2826">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2826">String</span></span> | <span data-ttu-id="457d1-2827">The URI whose `path` value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2827">The URI whose `path` value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2828">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2828">Return value</span></span> | <span data-ttu-id="457d1-2829">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2829">Type</span></span> | <span data-ttu-id="457d1-2830">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2830">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2831"><*path-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2831"><*path-value*></span></span> | <span data-ttu-id="457d1-2832">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2832">String</span></span> | <span data-ttu-id="457d1-2833">The `path` value for the specified URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-2833">The `path` value for the specified URI.</span></span> <span data-ttu-id="457d1-2834">If `path` doesn't have a value, return the "/" character.</span><span class="sxs-lookup"><span data-stu-id="457d1-2834">If `path` doesn't have a value, return the "/" character.</span></span> | 
|||| 

<span data-ttu-id="457d1-2835">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2835">*Example*</span></span>

<span data-ttu-id="457d1-2836">This example finds the `path` value for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2836">This example finds the `path` value for this URI:</span></span> 

```
uriPath('http://www.contoso.com/catalog/shownew.htm?date=today')
```

<span data-ttu-id="457d1-2837">And returns this result: `"/catalog/shownew.htm"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2837">And returns this result: `"/catalog/shownew.htm"`</span></span>

<a name="uriPathAndQuery"></a>

### <a name="uripathandquery"></a><span data-ttu-id="457d1-2838">uriPathAndQuery</span><span class="sxs-lookup"><span data-stu-id="457d1-2838">uriPathAndQuery</span></span>

<span data-ttu-id="457d1-2839">Return the `path` and `query` values for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2839">Return the `path` and `query` values for a uniform resource identifier (URI).</span></span>

```
uriPathAndQuery('<uri>')
```

| <span data-ttu-id="457d1-2840">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2840">Parameter</span></span> | <span data-ttu-id="457d1-2841">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2841">Required</span></span> | <span data-ttu-id="457d1-2842">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2842">Type</span></span> | <span data-ttu-id="457d1-2843">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2843">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2844"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2844"><*uri*></span></span> | <span data-ttu-id="457d1-2845">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2845">Yes</span></span> | <span data-ttu-id="457d1-2846">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2846">String</span></span> | <span data-ttu-id="457d1-2847">The URI whose `path` and `query` values you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2847">The URI whose `path` and `query` values you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2848">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2848">Return value</span></span> | <span data-ttu-id="457d1-2849">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2849">Type</span></span> | <span data-ttu-id="457d1-2850">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2850">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2851"><*path-query-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2851"><*path-query-value*></span></span> | <span data-ttu-id="457d1-2852">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2852">String</span></span> | <span data-ttu-id="457d1-2853">The `path` and `query` values for the specified URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-2853">The `path` and `query` values for the specified URI.</span></span> <span data-ttu-id="457d1-2854">If `path` doesn't specify a value, return the "/" character.</span><span class="sxs-lookup"><span data-stu-id="457d1-2854">If `path` doesn't specify a value, return the "/" character.</span></span> | 
|||| 

<span data-ttu-id="457d1-2855">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2855">*Example*</span></span>

<span data-ttu-id="457d1-2856">This example finds the `path` and `query` values for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2856">This example finds the `path` and `query` values for this URI:</span></span>

```
uriPathAndQuery('http://www.contoso.com/catalog/shownew.htm?date=today')
```

<span data-ttu-id="457d1-2857">And returns this result: `"/catalog/shownew.htm?date=today"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2857">And returns this result: `"/catalog/shownew.htm?date=today"`</span></span>

<a name="uriPort"></a>

### <a name="uriport"></a><span data-ttu-id="457d1-2858">uriPort</span><span class="sxs-lookup"><span data-stu-id="457d1-2858">uriPort</span></span>

<span data-ttu-id="457d1-2859">Return the `port` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2859">Return the `port` value for a uniform resource identifier (URI).</span></span>

```
uriPort('<uri>')
```

| <span data-ttu-id="457d1-2860">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2860">Parameter</span></span> | <span data-ttu-id="457d1-2861">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2861">Required</span></span> | <span data-ttu-id="457d1-2862">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2862">Type</span></span> | <span data-ttu-id="457d1-2863">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2863">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2864"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2864"><*uri*></span></span> | <span data-ttu-id="457d1-2865">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2865">Yes</span></span> | <span data-ttu-id="457d1-2866">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2866">String</span></span> | <span data-ttu-id="457d1-2867">The URI whose `port` value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2867">The URI whose `port` value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2868">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2868">Return value</span></span> | <span data-ttu-id="457d1-2869">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2869">Type</span></span> | <span data-ttu-id="457d1-2870">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2870">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2871"><*port-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2871"><*port-value*></span></span> | <span data-ttu-id="457d1-2872">Integer</span><span class="sxs-lookup"><span data-stu-id="457d1-2872">Integer</span></span> | <span data-ttu-id="457d1-2873">The `port` value for the specified URI.</span><span class="sxs-lookup"><span data-stu-id="457d1-2873">The `port` value for the specified URI.</span></span> <span data-ttu-id="457d1-2874">If `port` doesn't specify a value, return the default port for the protocol.</span><span class="sxs-lookup"><span data-stu-id="457d1-2874">If `port` doesn't specify a value, return the default port for the protocol.</span></span> | 
|||| 

<span data-ttu-id="457d1-2875">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2875">*Example*</span></span>

<span data-ttu-id="457d1-2876">This example returns the `port` value for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2876">This example returns the `port` value for this URI:</span></span>

```
uriPort('http://www.localhost:8080')
```

<span data-ttu-id="457d1-2877">And returns this result: `8080`</span><span class="sxs-lookup"><span data-stu-id="457d1-2877">And returns this result: `8080`</span></span>

<a name="uriQuery"></a>

### <a name="uriquery"></a><span data-ttu-id="457d1-2878">uriQuery</span><span class="sxs-lookup"><span data-stu-id="457d1-2878">uriQuery</span></span>

<span data-ttu-id="457d1-2879">Return the `query` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2879">Return the `query` value for a uniform resource identifier (URI).</span></span>

```
uriQuery('<uri>')
```

| <span data-ttu-id="457d1-2880">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2880">Parameter</span></span> | <span data-ttu-id="457d1-2881">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2881">Required</span></span> | <span data-ttu-id="457d1-2882">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2882">Type</span></span> | <span data-ttu-id="457d1-2883">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2883">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2884"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2884"><*uri*></span></span> | <span data-ttu-id="457d1-2885">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2885">Yes</span></span> | <span data-ttu-id="457d1-2886">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2886">String</span></span> | <span data-ttu-id="457d1-2887">The URI whose `query` value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2887">The URI whose `query` value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2888">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2888">Return value</span></span> | <span data-ttu-id="457d1-2889">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2889">Type</span></span> | <span data-ttu-id="457d1-2890">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2890">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2891"><*query-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2891"><*query-value*></span></span> | <span data-ttu-id="457d1-2892">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2892">String</span></span> | <span data-ttu-id="457d1-2893">The `query` value for the specified URI</span><span class="sxs-lookup"><span data-stu-id="457d1-2893">The `query` value for the specified URI</span></span> | 
|||| 

<span data-ttu-id="457d1-2894">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2894">*Example*</span></span>

<span data-ttu-id="457d1-2895">This example returns the `query` value for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2895">This example returns the `query` value for this URI:</span></span> 

```
uriQuery('http://www.contoso.com/catalog/shownew.htm?date=today')
```

<span data-ttu-id="457d1-2896">And returns this result: `"?date=today"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2896">And returns this result: `"?date=today"`</span></span>

<a name="uriScheme"></a>

### <a name="urischeme"></a><span data-ttu-id="457d1-2897">uriScheme</span><span class="sxs-lookup"><span data-stu-id="457d1-2897">uriScheme</span></span>

<span data-ttu-id="457d1-2898">Return the `scheme` value for a uniform resource identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="457d1-2898">Return the `scheme` value for a uniform resource identifier (URI).</span></span>

```
uriScheme('<uri>')
```

| <span data-ttu-id="457d1-2899">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2899">Parameter</span></span> | <span data-ttu-id="457d1-2900">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2900">Required</span></span> | <span data-ttu-id="457d1-2901">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2901">Type</span></span> | <span data-ttu-id="457d1-2902">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2902">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2903"><*uri*></span><span class="sxs-lookup"><span data-stu-id="457d1-2903"><*uri*></span></span> | <span data-ttu-id="457d1-2904">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2904">Yes</span></span> | <span data-ttu-id="457d1-2905">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2905">String</span></span> | <span data-ttu-id="457d1-2906">The URI whose `scheme` value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2906">The URI whose `scheme` value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2907">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2907">Return value</span></span> | <span data-ttu-id="457d1-2908">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2908">Type</span></span> | <span data-ttu-id="457d1-2909">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2909">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2910"><*scheme-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2910"><*scheme-value*></span></span> | <span data-ttu-id="457d1-2911">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2911">String</span></span> | <span data-ttu-id="457d1-2912">The `scheme` value for the specified URI</span><span class="sxs-lookup"><span data-stu-id="457d1-2912">The `scheme` value for the specified URI</span></span> | 
|||| 

<span data-ttu-id="457d1-2913">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2913">*Example*</span></span>

<span data-ttu-id="457d1-2914">This example returns the `scheme` value for this URI:</span><span class="sxs-lookup"><span data-stu-id="457d1-2914">This example returns the `scheme` value for this URI:</span></span>

```
uriScheme('http://www.contoso.com/catalog/shownew.htm?date=today')
```

<span data-ttu-id="457d1-2915">And returns this result: `"http"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2915">And returns this result: `"http"`</span></span>

<a name="utcNow"></a>

### <a name="utcnow"></a><span data-ttu-id="457d1-2916">utcNow</span><span class="sxs-lookup"><span data-stu-id="457d1-2916">utcNow</span></span>

<span data-ttu-id="457d1-2917">Return the current timestamp.</span><span class="sxs-lookup"><span data-stu-id="457d1-2917">Return the current timestamp.</span></span> 

```
utcNow('<format>')
```

<span data-ttu-id="457d1-2918">Optionally, you can specify a different format with the <*format*> parameter.</span><span class="sxs-lookup"><span data-stu-id="457d1-2918">Optionally, you can specify a different format with the <*format*> parameter.</span></span> 


| <span data-ttu-id="457d1-2919">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2919">Parameter</span></span> | <span data-ttu-id="457d1-2920">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2920">Required</span></span> | <span data-ttu-id="457d1-2921">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2921">Type</span></span> | <span data-ttu-id="457d1-2922">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2922">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2923"><*format*></span><span class="sxs-lookup"><span data-stu-id="457d1-2923"><*format*></span></span> | <span data-ttu-id="457d1-2924">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2924">No</span></span> | <span data-ttu-id="457d1-2925">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2925">String</span></span> | <span data-ttu-id="457d1-2926">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span><span class="sxs-lookup"><span data-stu-id="457d1-2926">Either a [single format specifier](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) or a [custom format pattern](https://docs.microsoft.com/dotnet/standard/base-types/custom-date-and-time-format-strings).</span></span> <span data-ttu-id="457d1-2927">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span><span class="sxs-lookup"><span data-stu-id="457d1-2927">The default format for the timestamp is ["o"](https://docs.microsoft.com/dotnet/standard/base-types/standard-date-and-time-format-strings) (yyyy-MM-ddT:mm:ss:fffffffK), which complies with [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) and preserves time zone information.</span></span> | 
||||| 

| <span data-ttu-id="457d1-2928">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2928">Return value</span></span> | <span data-ttu-id="457d1-2929">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2929">Type</span></span> | <span data-ttu-id="457d1-2930">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2930">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2931"><*current-timestamp*></span><span class="sxs-lookup"><span data-stu-id="457d1-2931"><*current-timestamp*></span></span> | <span data-ttu-id="457d1-2932">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2932">String</span></span> | <span data-ttu-id="457d1-2933">The current date and time</span><span class="sxs-lookup"><span data-stu-id="457d1-2933">The current date and time</span></span> | 
|||| 

<span data-ttu-id="457d1-2934">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2934">*Example 1*</span></span>

<span data-ttu-id="457d1-2935">Suppose today is April 15, 2018 at 1:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="457d1-2935">Suppose today is April 15, 2018 at 1:00:00 PM.</span></span> <span data-ttu-id="457d1-2936">This example gets the current timestamp:</span><span class="sxs-lookup"><span data-stu-id="457d1-2936">This example gets the current timestamp:</span></span> 

```
utcNow()
```

<span data-ttu-id="457d1-2937">And returns this result: `"2018-04-15T13:00:00.0000000Z"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2937">And returns this result: `"2018-04-15T13:00:00.0000000Z"`</span></span>

<span data-ttu-id="457d1-2938">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2938">*Example 2*</span></span>

<span data-ttu-id="457d1-2939">Suppose today is April 15, 2018 at 1:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="457d1-2939">Suppose today is April 15, 2018 at 1:00:00 PM.</span></span> <span data-ttu-id="457d1-2940">This example gets the current timestamp using the optional "D" format:</span><span class="sxs-lookup"><span data-stu-id="457d1-2940">This example gets the current timestamp using the optional "D" format:</span></span>

```
utcNow('D')
```

<span data-ttu-id="457d1-2941">And returns this result: `"Sunday, April 15, 2018"`</span><span class="sxs-lookup"><span data-stu-id="457d1-2941">And returns this result: `"Sunday, April 15, 2018"`</span></span>

<a name="variables"></a>

### <a name="variables"></a><span data-ttu-id="457d1-2942">variables</span><span class="sxs-lookup"><span data-stu-id="457d1-2942">variables</span></span>

<span data-ttu-id="457d1-2943">Return the value for a specified variable.</span><span class="sxs-lookup"><span data-stu-id="457d1-2943">Return the value for a specified variable.</span></span> 

```
variables('<variableName>')
```

| <span data-ttu-id="457d1-2944">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2944">Parameter</span></span> | <span data-ttu-id="457d1-2945">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2945">Required</span></span> | <span data-ttu-id="457d1-2946">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2946">Type</span></span> | <span data-ttu-id="457d1-2947">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2947">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2948"><*variableName*></span><span class="sxs-lookup"><span data-stu-id="457d1-2948"><*variableName*></span></span> | <span data-ttu-id="457d1-2949">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2949">Yes</span></span> | <span data-ttu-id="457d1-2950">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2950">String</span></span> | <span data-ttu-id="457d1-2951">The name for the variable whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2951">The name for the variable whose value you want</span></span> | 
||||| 

| <span data-ttu-id="457d1-2952">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2952">Return value</span></span> | <span data-ttu-id="457d1-2953">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2953">Type</span></span> | <span data-ttu-id="457d1-2954">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2954">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2955"><*variable-value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2955"><*variable-value*></span></span> | <span data-ttu-id="457d1-2956">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-2956">Any</span></span> | <span data-ttu-id="457d1-2957">The value for the specified variable</span><span class="sxs-lookup"><span data-stu-id="457d1-2957">The value for the specified variable</span></span> | 
|||| 

<span data-ttu-id="457d1-2958">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2958">*Example*</span></span>

<span data-ttu-id="457d1-2959">Suppose the current value for a "numItems" variable is 20.</span><span class="sxs-lookup"><span data-stu-id="457d1-2959">Suppose the current value for a "numItems" variable is 20.</span></span> <span data-ttu-id="457d1-2960">This example gets the integer value for this variable:</span><span class="sxs-lookup"><span data-stu-id="457d1-2960">This example gets the integer value for this variable:</span></span>

```
variables('numItems')
```

<span data-ttu-id="457d1-2961">And returns this result: `20`</span><span class="sxs-lookup"><span data-stu-id="457d1-2961">And returns this result: `20`</span></span>

<a name="workflow"></a>

### <a name="workflow"></a><span data-ttu-id="457d1-2962">workflow</span><span class="sxs-lookup"><span data-stu-id="457d1-2962">workflow</span></span>

<span data-ttu-id="457d1-2963">Return all the details about the workflow itself during run time.</span><span class="sxs-lookup"><span data-stu-id="457d1-2963">Return all the details about the workflow itself during run time.</span></span> 

```
workflow().<property>
```

| <span data-ttu-id="457d1-2964">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2964">Parameter</span></span> | <span data-ttu-id="457d1-2965">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2965">Required</span></span> | <span data-ttu-id="457d1-2966">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2966">Type</span></span> | <span data-ttu-id="457d1-2967">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2967">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2968"><*property*></span><span class="sxs-lookup"><span data-stu-id="457d1-2968"><*property*></span></span> | <span data-ttu-id="457d1-2969">No</span><span class="sxs-lookup"><span data-stu-id="457d1-2969">No</span></span> | <span data-ttu-id="457d1-2970">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2970">String</span></span> | <span data-ttu-id="457d1-2971">The name for the workflow property whose value you want</span><span class="sxs-lookup"><span data-stu-id="457d1-2971">The name for the workflow property whose value you want</span></span> <p><span data-ttu-id="457d1-2972">A workflow object has these properties: **name**, **type**, **id**, **location**, and **run**.</span><span class="sxs-lookup"><span data-stu-id="457d1-2972">A workflow object has these properties: **name**, **type**, **id**, **location**, and **run**.</span></span> <span data-ttu-id="457d1-2973">The **run** property value is also an object that has these properties: **name**, **type**, and **id**.</span><span class="sxs-lookup"><span data-stu-id="457d1-2973">The **run** property value is also an object that has these properties: **name**, **type**, and **id**.</span></span> | 
||||| 

<span data-ttu-id="457d1-2974">*Example*</span><span class="sxs-lookup"><span data-stu-id="457d1-2974">*Example*</span></span>

<span data-ttu-id="457d1-2975">This example returns the name for a workflow's current run:</span><span class="sxs-lookup"><span data-stu-id="457d1-2975">This example returns the name for a workflow's current run:</span></span>

```
workflow().run.name
```

<a name="xml"></a>

### <a name="xml"></a><span data-ttu-id="457d1-2976">xml</span><span class="sxs-lookup"><span data-stu-id="457d1-2976">xml</span></span>

<span data-ttu-id="457d1-2977">Return the XML version for a string that contains a JSON object.</span><span class="sxs-lookup"><span data-stu-id="457d1-2977">Return the XML version for a string that contains a JSON object.</span></span> 

```
xml('<value>')
```

| <span data-ttu-id="457d1-2978">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-2978">Parameter</span></span> | <span data-ttu-id="457d1-2979">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-2979">Required</span></span> | <span data-ttu-id="457d1-2980">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2980">Type</span></span> | <span data-ttu-id="457d1-2981">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2981">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-2982"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-2982"><*value*></span></span> | <span data-ttu-id="457d1-2983">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-2983">Yes</span></span> | <span data-ttu-id="457d1-2984">String</span><span class="sxs-lookup"><span data-stu-id="457d1-2984">String</span></span> | <span data-ttu-id="457d1-2985">The string with the JSON object to convert</span><span class="sxs-lookup"><span data-stu-id="457d1-2985">The string with the JSON object to convert</span></span> <p><span data-ttu-id="457d1-2986">The JSON object must have only one root property.</span><span class="sxs-lookup"><span data-stu-id="457d1-2986">The JSON object must have only one root property.</span></span> <br><span data-ttu-id="457d1-2987">Use the backslash character (\\) as an escape character for the double quotation mark (").</span><span class="sxs-lookup"><span data-stu-id="457d1-2987">Use the backslash character (\\) as an escape character for the double quotation mark (").</span></span> | 
||||| 

| <span data-ttu-id="457d1-2988">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-2988">Return value</span></span> | <span data-ttu-id="457d1-2989">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-2989">Type</span></span> | <span data-ttu-id="457d1-2990">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-2990">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-2991"><*xml-version*></span><span class="sxs-lookup"><span data-stu-id="457d1-2991"><*xml-version*></span></span> | <span data-ttu-id="457d1-2992">Object</span><span class="sxs-lookup"><span data-stu-id="457d1-2992">Object</span></span> | <span data-ttu-id="457d1-2993">The encoded XML for the specified string or JSON object</span><span class="sxs-lookup"><span data-stu-id="457d1-2993">The encoded XML for the specified string or JSON object</span></span> | 
|||| 

<span data-ttu-id="457d1-2994">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-2994">*Example 1*</span></span>

<span data-ttu-id="457d1-2995">This example creates the XML version for this string, which contains a JSON object:</span><span class="sxs-lookup"><span data-stu-id="457d1-2995">This example creates the XML version for this string, which contains a JSON object:</span></span> 

`xml( '{ \"name\": \"Sophia Owen\" }' )`

<span data-ttu-id="457d1-2996">And returns this result XML:</span><span class="sxs-lookup"><span data-stu-id="457d1-2996">And returns this result XML:</span></span> 

```xml
<name>Sophia Owen</name>
```

<span data-ttu-id="457d1-2997">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-2997">*Example 2*</span></span>

<span data-ttu-id="457d1-2998">Suppose you have this JSON object:</span><span class="sxs-lookup"><span data-stu-id="457d1-2998">Suppose you have this JSON object:</span></span>

```json
{ 
  "person": { 
    "name": "Sophia Owen", 
    "city": "Seattle" 
  } 
}
```

<span data-ttu-id="457d1-2999">This example creates XML for a string that contains this JSON object:</span><span class="sxs-lookup"><span data-stu-id="457d1-2999">This example creates XML for a string that contains this JSON object:</span></span>

`xml( '{ \"person\": { \"name\": \"Sophia Owen\", \"city\": \"Seattle\" } }' )`

<span data-ttu-id="457d1-3000">And returns this result XML:</span><span class="sxs-lookup"><span data-stu-id="457d1-3000">And returns this result XML:</span></span> 

```xml
<person>
  <name>Sophia Owen</name>
  <city>Seattle</city>
<person>
```

<a name="xpath"></a>

### <a name="xpath"></a><span data-ttu-id="457d1-3001">xpath</span><span class="sxs-lookup"><span data-stu-id="457d1-3001">xpath</span></span>

<span data-ttu-id="457d1-3002">Check XML for nodes or values that match an XPath (XML Path Language) expression, and return the matching nodes or values.</span><span class="sxs-lookup"><span data-stu-id="457d1-3002">Check XML for nodes or values that match an XPath (XML Path Language) expression, and return the matching nodes or values.</span></span> <span data-ttu-id="457d1-3003">An XPath expression, or just "XPath", helps you navigate an XML document structure so that you can select nodes or compute values in the XML content.</span><span class="sxs-lookup"><span data-stu-id="457d1-3003">An XPath expression, or just "XPath", helps you navigate an XML document structure so that you can select nodes or compute values in the XML content.</span></span>

```
xpath('<xml>', '<xpath>')
```

| <span data-ttu-id="457d1-3004">Parameter</span><span class="sxs-lookup"><span data-stu-id="457d1-3004">Parameter</span></span> | <span data-ttu-id="457d1-3005">Required</span><span class="sxs-lookup"><span data-stu-id="457d1-3005">Required</span></span> | <span data-ttu-id="457d1-3006">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-3006">Type</span></span> | <span data-ttu-id="457d1-3007">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-3007">Description</span></span> | 
| --------- | -------- | ---- | ----------- | 
| <span data-ttu-id="457d1-3008"><*xml*></span><span class="sxs-lookup"><span data-stu-id="457d1-3008"><*xml*></span></span> | <span data-ttu-id="457d1-3009">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-3009">Yes</span></span> | <span data-ttu-id="457d1-3010">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-3010">Any</span></span> | <span data-ttu-id="457d1-3011">The XML string to search for nodes or values that match an XPath expression value</span><span class="sxs-lookup"><span data-stu-id="457d1-3011">The XML string to search for nodes or values that match an XPath expression value</span></span> | 
| <span data-ttu-id="457d1-3012"><*xpath*></span><span class="sxs-lookup"><span data-stu-id="457d1-3012"><*xpath*></span></span> | <span data-ttu-id="457d1-3013">Yes</span><span class="sxs-lookup"><span data-stu-id="457d1-3013">Yes</span></span> | <span data-ttu-id="457d1-3014">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-3014">Any</span></span> | <span data-ttu-id="457d1-3015">The XPath expression used to find matching XML nodes or values</span><span class="sxs-lookup"><span data-stu-id="457d1-3015">The XPath expression used to find matching XML nodes or values</span></span> | 
||||| 

| <span data-ttu-id="457d1-3016">Return value</span><span class="sxs-lookup"><span data-stu-id="457d1-3016">Return value</span></span> | <span data-ttu-id="457d1-3017">Type</span><span class="sxs-lookup"><span data-stu-id="457d1-3017">Type</span></span> | <span data-ttu-id="457d1-3018">Description</span><span class="sxs-lookup"><span data-stu-id="457d1-3018">Description</span></span> | 
| ------------ | ---- | ----------- | 
| <span data-ttu-id="457d1-3019"><*xml-node*></span><span class="sxs-lookup"><span data-stu-id="457d1-3019"><*xml-node*></span></span> | <span data-ttu-id="457d1-3020">XML</span><span class="sxs-lookup"><span data-stu-id="457d1-3020">XML</span></span> | <span data-ttu-id="457d1-3021">An XML node when only a single node matches the specified XPath expression</span><span class="sxs-lookup"><span data-stu-id="457d1-3021">An XML node when only a single node matches the specified XPath expression</span></span> | 
| <span data-ttu-id="457d1-3022"><*value*></span><span class="sxs-lookup"><span data-stu-id="457d1-3022"><*value*></span></span> | <span data-ttu-id="457d1-3023">Any</span><span class="sxs-lookup"><span data-stu-id="457d1-3023">Any</span></span> | <span data-ttu-id="457d1-3024">The value from an XML node when only a single value matches the specified XPath expression</span><span class="sxs-lookup"><span data-stu-id="457d1-3024">The value from an XML node when only a single value matches the specified XPath expression</span></span> | 
| <span data-ttu-id="457d1-3025">[<*xml-node1*>, <*xml-node2*>, ...]</span><span class="sxs-lookup"><span data-stu-id="457d1-3025">[<*xml-node1*>, <*xml-node2*>, ...]</span></span> </br><span data-ttu-id="457d1-3026">-or-</span><span class="sxs-lookup"><span data-stu-id="457d1-3026">-or-</span></span> </br><span data-ttu-id="457d1-3027">[<*value1*>, <*value2*>, ...]</span><span class="sxs-lookup"><span data-stu-id="457d1-3027">[<*value1*>, <*value2*>, ...]</span></span> | <span data-ttu-id="457d1-3028">Array</span><span class="sxs-lookup"><span data-stu-id="457d1-3028">Array</span></span> | <span data-ttu-id="457d1-3029">An array with XML nodes or values that match the specified XPath expression</span><span class="sxs-lookup"><span data-stu-id="457d1-3029">An array with XML nodes or values that match the specified XPath expression</span></span> | 
|||| 

<span data-ttu-id="457d1-3030">*Example 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-3030">*Example 1*</span></span>

<span data-ttu-id="457d1-3031">This example finds nodes that match the `<name></name>` node in the specified arguments, and returns an array with those node values:</span><span class="sxs-lookup"><span data-stu-id="457d1-3031">This example finds nodes that match the `<name></name>` node in the specified arguments, and returns an array with those node values:</span></span> 

`xpath(xml(parameters('items')), '/produce/item/name')`

<span data-ttu-id="457d1-3032">Here are the arguments:</span><span class="sxs-lookup"><span data-stu-id="457d1-3032">Here are the arguments:</span></span>

* <span data-ttu-id="457d1-3033">The "items" string, which contains this XML:</span><span class="sxs-lookup"><span data-stu-id="457d1-3033">The "items" string, which contains this XML:</span></span>

  `"<?xml version="1.0"?> <produce> <item> <name>Gala</name> <type>apple</type> <count>20</count> </item> <item> <name>Honeycrisp</name> <type>apple</type> <count>10</count> </item> </produce>"`

  <span data-ttu-id="457d1-3034">The example uses the [parameters()](#parameters) function to get the XML string from the "items" argument, but must also convert the string to XML format by using the [xml()](#xml) function.</span><span class="sxs-lookup"><span data-stu-id="457d1-3034">The example uses the [parameters()](#parameters) function to get the XML string from the "items" argument, but must also convert the string to XML format by using the [xml()](#xml) function.</span></span> 

* <span data-ttu-id="457d1-3035">This XPath expression, which is passed as a string:</span><span class="sxs-lookup"><span data-stu-id="457d1-3035">This XPath expression, which is passed as a string:</span></span>

  `"/produce/item/name"`

<span data-ttu-id="457d1-3036">Here is the result array with the nodes that match `<name></name`:</span><span class="sxs-lookup"><span data-stu-id="457d1-3036">Here is the result array with the nodes that match `<name></name`:</span></span>

`[ <name>Gala</name>, <name>Honeycrisp</name> ]`

<span data-ttu-id="457d1-3037">*Example 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-3037">*Example 2*</span></span>

<span data-ttu-id="457d1-3038">Following on Example 1, this example finds nodes that match the `<count></count>` node and adds those node values with the `sum()` function:</span><span class="sxs-lookup"><span data-stu-id="457d1-3038">Following on Example 1, this example finds nodes that match the `<count></count>` node and adds those node values with the `sum()` function:</span></span>

`xpath(xml(parameters('items')), 'sum(/produce/item/count)')`

<span data-ttu-id="457d1-3039">And returns this result: `30`</span><span class="sxs-lookup"><span data-stu-id="457d1-3039">And returns this result: `30`</span></span>

<span data-ttu-id="457d1-3040">*Example 3*</span><span class="sxs-lookup"><span data-stu-id="457d1-3040">*Example 3*</span></span>

<span data-ttu-id="457d1-3041">For this example, both expressions find nodes that match the `<location></location>` node, in the specified arguments, which include XML with a namespace.</span><span class="sxs-lookup"><span data-stu-id="457d1-3041">For this example, both expressions find nodes that match the `<location></location>` node, in the specified arguments, which include XML with a namespace.</span></span> <span data-ttu-id="457d1-3042">The expressions use the backslash character (\\) as an escape character for the double quotation mark (").</span><span class="sxs-lookup"><span data-stu-id="457d1-3042">The expressions use the backslash character (\\) as an escape character for the double quotation mark (").</span></span>

* <span data-ttu-id="457d1-3043">*Expression 1*</span><span class="sxs-lookup"><span data-stu-id="457d1-3043">*Expression 1*</span></span>

  `xpath(xml(body('Http')), '/*[name()=\"file\"]/*[name()=\"location\"]')`

* <span data-ttu-id="457d1-3044">*Expression 2*</span><span class="sxs-lookup"><span data-stu-id="457d1-3044">*Expression 2*</span></span> 

  `xpath(xml(body('Http')), '/*[local-name=()=\"file\"] and namespace-uri()=\"http://contoso.com\"/*[local-name()]=\"location\" and namespace-uri()=\"\"]')`

<span data-ttu-id="457d1-3045">Here are the arguments:</span><span class="sxs-lookup"><span data-stu-id="457d1-3045">Here are the arguments:</span></span>

* <span data-ttu-id="457d1-3046">This XML, which includes the XML document namespace, `xmlns="http://contoso.com"`:</span><span class="sxs-lookup"><span data-stu-id="457d1-3046">This XML, which includes the XML document namespace, `xmlns="http://contoso.com"`:</span></span> 

  ```xml
  <?xml version="1.0"?> <file xmlns="http://contoso.com"> <location>Paris</location> </file>
  ```

* <span data-ttu-id="457d1-3047">Either XPath expression here:</span><span class="sxs-lookup"><span data-stu-id="457d1-3047">Either XPath expression here:</span></span>

  * `/*[name()=\"file\"]/*[name()=\"location\"]`

  * `/*[local-name=()=\"file\"] and namespace-uri()=\"http://contoso.com\"/*[local-name()]=\"location\" and namespace-uri()=\"\"]`

<span data-ttu-id="457d1-3048">Here is the result node that matches the `<location></location` node:</span><span class="sxs-lookup"><span data-stu-id="457d1-3048">Here is the result node that matches the `<location></location` node:</span></span>

```xml
<location xmlns="https://contoso.com">Paris</location>
```

<span data-ttu-id="457d1-3049">*Example 4*</span><span class="sxs-lookup"><span data-stu-id="457d1-3049">*Example 4*</span></span>

<span data-ttu-id="457d1-3050">Following on Example 3, this example finds the value in the `<location></location>` node:</span><span class="sxs-lookup"><span data-stu-id="457d1-3050">Following on Example 3, this example finds the value in the `<location></location>` node:</span></span> 

`xpath(xml(body('Http')), 'string(/*[name()=\"file\"]/*[name()=\"location\"])')`

<span data-ttu-id="457d1-3051">And returns this result: `"Paris"`</span><span class="sxs-lookup"><span data-stu-id="457d1-3051">And returns this result: `"Paris"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="457d1-3052">Next steps</span><span class="sxs-lookup"><span data-stu-id="457d1-3052">Next steps</span></span>

<span data-ttu-id="457d1-3053">Learn about the [Workflow Definition Language](../logic-apps/logic-apps-workflow-definition-language.md)</span><span class="sxs-lookup"><span data-stu-id="457d1-3053">Learn about the [Workflow Definition Language](../logic-apps/logic-apps-workflow-definition-language.md)</span></span>
