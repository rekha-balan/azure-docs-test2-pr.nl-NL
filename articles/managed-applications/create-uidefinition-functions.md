---
title: Azure Managed Application create UI definition functions | Microsoft Docs
description: Describes the functions to use when constructing UI definitions for Azure Managed Applications
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: a01a59a7e8c9757cb41d328cd26a34fa219f9152
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871616"
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="dfca2-103">CreateUiDefinition functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="dfca2-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="dfca2-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="dfca2-105">To use a function, surround the declaration with square brackets.</span><span class="sxs-lookup"><span data-stu-id="dfca2-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="dfca2-106">For example:</span><span class="sxs-lookup"><span data-stu-id="dfca2-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="dfca2-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span><span class="sxs-lookup"><span data-stu-id="dfca2-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="dfca2-108">For example:</span><span class="sxs-lookup"><span data-stu-id="dfca2-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="dfca2-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span><span class="sxs-lookup"><span data-stu-id="dfca2-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="dfca2-110">For example:</span><span class="sxs-lookup"><span data-stu-id="dfca2-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="dfca2-111">Referencing functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-111">Referencing functions</span></span>
<span data-ttu-id="dfca2-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="dfca2-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="dfca2-113">basics</span><span class="sxs-lookup"><span data-stu-id="dfca2-113">basics</span></span>
<span data-ttu-id="dfca2-114">Returns the output values of an element that is defined in the Basics step.</span><span class="sxs-lookup"><span data-stu-id="dfca2-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="dfca2-115">The following example returns the output of the element named `foo` in the Basics step:</span><span class="sxs-lookup"><span data-stu-id="dfca2-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="dfca2-116">steps</span><span class="sxs-lookup"><span data-stu-id="dfca2-116">steps</span></span>
<span data-ttu-id="dfca2-117">Returns the output values of an element that is defined in the specified step.</span><span class="sxs-lookup"><span data-stu-id="dfca2-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="dfca2-118">To get the output values of elements in the Basics step, use `basics()` instead.</span><span class="sxs-lookup"><span data-stu-id="dfca2-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="dfca2-119">The following example returns the output of the element named `bar` in the step named `foo`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="dfca2-120">location</span><span class="sxs-lookup"><span data-stu-id="dfca2-120">location</span></span>
<span data-ttu-id="dfca2-121">Returns the location selected in the Basics step or the current context.</span><span class="sxs-lookup"><span data-stu-id="dfca2-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="dfca2-122">The following example could return `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="dfca2-123">String functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-123">String functions</span></span>
<span data-ttu-id="dfca2-124">These functions can only be used with JSON strings.</span><span class="sxs-lookup"><span data-stu-id="dfca2-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="dfca2-125">concat</span><span class="sxs-lookup"><span data-stu-id="dfca2-125">concat</span></span>
<span data-ttu-id="dfca2-126">Concatenates one or more strings.</span><span class="sxs-lookup"><span data-stu-id="dfca2-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="dfca2-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="dfca2-128">substring</span><span class="sxs-lookup"><span data-stu-id="dfca2-128">substring</span></span>
<span data-ttu-id="dfca2-129">Returns the substring of the specified string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="dfca2-130">The substring starts at the specified index and has the specified length.</span><span class="sxs-lookup"><span data-stu-id="dfca2-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="dfca2-131">The following example returns `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="dfca2-132">replace</span><span class="sxs-lookup"><span data-stu-id="dfca2-132">replace</span></span>
<span data-ttu-id="dfca2-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="dfca2-134">The following example returns `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="dfca2-135">guid</span><span class="sxs-lookup"><span data-stu-id="dfca2-135">guid</span></span>
<span data-ttu-id="dfca2-136">Generates a globally unique string (GUID).</span><span class="sxs-lookup"><span data-stu-id="dfca2-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="dfca2-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="dfca2-138">toLower</span><span class="sxs-lookup"><span data-stu-id="dfca2-138">toLower</span></span>
<span data-ttu-id="dfca2-139">Returns a string converted to lowercase.</span><span class="sxs-lookup"><span data-stu-id="dfca2-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="dfca2-140">The following example returns `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="dfca2-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="dfca2-141">toUpper</span></span>
<span data-ttu-id="dfca2-142">Returns a string converted to uppercase.</span><span class="sxs-lookup"><span data-stu-id="dfca2-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="dfca2-143">The following example returns `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="dfca2-144">Collection functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-144">Collection functions</span></span>
<span data-ttu-id="dfca2-145">These functions can be used with collections, like JSON strings, arrays and objects.</span><span class="sxs-lookup"><span data-stu-id="dfca2-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="dfca2-146">contains</span><span class="sxs-lookup"><span data-stu-id="dfca2-146">contains</span></span>
<span data-ttu-id="dfca2-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span><span class="sxs-lookup"><span data-stu-id="dfca2-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-148">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-148">Example 1: string</span></span>
<span data-ttu-id="dfca2-149">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-150">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-150">Example 2: array</span></span>
<span data-ttu-id="dfca2-151">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-152">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-153">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-153">Example 3: object</span></span>
<span data-ttu-id="dfca2-154">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="dfca2-155">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="dfca2-156">length</span><span class="sxs-lookup"><span data-stu-id="dfca2-156">length</span></span>
<span data-ttu-id="dfca2-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span><span class="sxs-lookup"><span data-stu-id="dfca2-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-158">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-158">Example 1: string</span></span>
<span data-ttu-id="dfca2-159">The following example returns `6`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-160">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-160">Example 2: array</span></span>
<span data-ttu-id="dfca2-161">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-162">The following example returns `3`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-163">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-163">Example 3: object</span></span>
<span data-ttu-id="dfca2-164">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="dfca2-165">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="dfca2-166">empty</span><span class="sxs-lookup"><span data-stu-id="dfca2-166">empty</span></span>
<span data-ttu-id="dfca2-167">Returns `true` if the string, array, or object is null or empty.</span><span class="sxs-lookup"><span data-stu-id="dfca2-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-168">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-168">Example 1: string</span></span>
<span data-ttu-id="dfca2-169">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-170">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-170">Example 2: array</span></span>
<span data-ttu-id="dfca2-171">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-172">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-173">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-173">Example 3: object</span></span>
<span data-ttu-id="dfca2-174">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="dfca2-175">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="dfca2-176">Example 4: null and undefined</span><span class="sxs-lookup"><span data-stu-id="dfca2-176">Example 4: null and undefined</span></span>
<span data-ttu-id="dfca2-177">Assume `element1` is `null` or undefined.</span><span class="sxs-lookup"><span data-stu-id="dfca2-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="dfca2-178">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="dfca2-179">first</span><span class="sxs-lookup"><span data-stu-id="dfca2-179">first</span></span>
<span data-ttu-id="dfca2-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span><span class="sxs-lookup"><span data-stu-id="dfca2-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-181">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-181">Example 1: string</span></span>
<span data-ttu-id="dfca2-182">The following example returns `"f"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-183">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-183">Example 2: array</span></span>
<span data-ttu-id="dfca2-184">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-185">The following example returns `1`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-186">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-186">Example 3: object</span></span>
<span data-ttu-id="dfca2-187">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="dfca2-188">The following example returns `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="dfca2-189">last</span><span class="sxs-lookup"><span data-stu-id="dfca2-189">last</span></span>
<span data-ttu-id="dfca2-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span><span class="sxs-lookup"><span data-stu-id="dfca2-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-191">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-191">Example 1: string</span></span>
<span data-ttu-id="dfca2-192">The following example returns `"r"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-193">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-193">Example 2: array</span></span>
<span data-ttu-id="dfca2-194">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-195">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-196">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-196">Example 3: object</span></span>
<span data-ttu-id="dfca2-197">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="dfca2-198">The following example returns `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="dfca2-199">take</span><span class="sxs-lookup"><span data-stu-id="dfca2-199">take</span></span>
<span data-ttu-id="dfca2-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span><span class="sxs-lookup"><span data-stu-id="dfca2-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-201">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-201">Example 1: string</span></span>
<span data-ttu-id="dfca2-202">The following example returns `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-203">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-203">Example 2: array</span></span>
<span data-ttu-id="dfca2-204">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-205">The following example returns `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-206">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-206">Example 3: object</span></span>
<span data-ttu-id="dfca2-207">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="dfca2-208">The following example returns `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="dfca2-209">skip</span><span class="sxs-lookup"><span data-stu-id="dfca2-209">skip</span></span>
<span data-ttu-id="dfca2-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span><span class="sxs-lookup"><span data-stu-id="dfca2-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="dfca2-211">Example 1: string</span><span class="sxs-lookup"><span data-stu-id="dfca2-211">Example 1: string</span></span>
<span data-ttu-id="dfca2-212">The following example returns `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="dfca2-213">Example 2: array</span><span class="sxs-lookup"><span data-stu-id="dfca2-213">Example 2: array</span></span>
<span data-ttu-id="dfca2-214">Assume `element1` returns `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="dfca2-215">The following example returns `[3]`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="dfca2-216">Example 3: object</span><span class="sxs-lookup"><span data-stu-id="dfca2-216">Example 3: object</span></span>
<span data-ttu-id="dfca2-217">Assume `element1` returns:</span><span class="sxs-lookup"><span data-stu-id="dfca2-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="dfca2-218">The following example returns `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="dfca2-219">Logical functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-219">Logical functions</span></span>
<span data-ttu-id="dfca2-220">These functions can be used in conditionals.</span><span class="sxs-lookup"><span data-stu-id="dfca2-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="dfca2-221">Some functions may not support all JSON data types.</span><span class="sxs-lookup"><span data-stu-id="dfca2-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="dfca2-222">equals</span><span class="sxs-lookup"><span data-stu-id="dfca2-222">equals</span></span>
<span data-ttu-id="dfca2-223">Returns `true` if both parameters have the same type and value.</span><span class="sxs-lookup"><span data-stu-id="dfca2-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="dfca2-224">This function supports all JSON data types.</span><span class="sxs-lookup"><span data-stu-id="dfca2-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="dfca2-225">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="dfca2-226">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="dfca2-227">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="dfca2-228">less</span><span class="sxs-lookup"><span data-stu-id="dfca2-228">less</span></span>
<span data-ttu-id="dfca2-229">Returns `true` if the first parameter is strictly less than the second parameter.</span><span class="sxs-lookup"><span data-stu-id="dfca2-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="dfca2-230">This function supports parameters only of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="dfca2-231">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="dfca2-232">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="dfca2-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="dfca2-233">lessOrEquals</span></span>
<span data-ttu-id="dfca2-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span><span class="sxs-lookup"><span data-stu-id="dfca2-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="dfca2-235">This function supports parameters only of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="dfca2-236">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="dfca2-237">greater</span><span class="sxs-lookup"><span data-stu-id="dfca2-237">greater</span></span>
<span data-ttu-id="dfca2-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span><span class="sxs-lookup"><span data-stu-id="dfca2-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="dfca2-239">This function supports parameters only of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="dfca2-240">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="dfca2-241">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="dfca2-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="dfca2-242">greaterOrEquals</span></span>
<span data-ttu-id="dfca2-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span><span class="sxs-lookup"><span data-stu-id="dfca2-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="dfca2-244">This function supports parameters only of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="dfca2-245">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="dfca2-246">and</span><span class="sxs-lookup"><span data-stu-id="dfca2-246">and</span></span>
<span data-ttu-id="dfca2-247">Returns `true` if all the parameters evaluate to `true`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="dfca2-248">This function supports two or more parameters only of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="dfca2-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="dfca2-249">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="dfca2-250">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="dfca2-251">or</span><span class="sxs-lookup"><span data-stu-id="dfca2-251">or</span></span>
<span data-ttu-id="dfca2-252">Returns `true` if at least one of the parameters evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="dfca2-253">This function supports two or more parameters only of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="dfca2-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="dfca2-254">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="dfca2-255">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="dfca2-256">not</span><span class="sxs-lookup"><span data-stu-id="dfca2-256">not</span></span>
<span data-ttu-id="dfca2-257">Returns `true` if the parameter evaluates to `false`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="dfca2-258">This function supports parameters only of type Boolean.</span><span class="sxs-lookup"><span data-stu-id="dfca2-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="dfca2-259">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="dfca2-260">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="dfca2-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="dfca2-261">coalesce</span></span>
<span data-ttu-id="dfca2-262">Returns the value of the first non-null parameter.</span><span class="sxs-lookup"><span data-stu-id="dfca2-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="dfca2-263">This function supports all JSON data types.</span><span class="sxs-lookup"><span data-stu-id="dfca2-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="dfca2-264">Assume `element1` and `element2` are undefined.</span><span class="sxs-lookup"><span data-stu-id="dfca2-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="dfca2-265">The following example returns `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="dfca2-266">Conversion functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-266">Conversion functions</span></span>
<span data-ttu-id="dfca2-267">These functions can be used to convert values between JSON data types and encodings.</span><span class="sxs-lookup"><span data-stu-id="dfca2-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="dfca2-268">int</span><span class="sxs-lookup"><span data-stu-id="dfca2-268">int</span></span>
<span data-ttu-id="dfca2-269">Converts the parameter to an integer.</span><span class="sxs-lookup"><span data-stu-id="dfca2-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="dfca2-270">This function supports parameters of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="dfca2-271">The following example returns `1`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="dfca2-272">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="dfca2-273">float</span><span class="sxs-lookup"><span data-stu-id="dfca2-273">float</span></span>
<span data-ttu-id="dfca2-274">Converts the parameter to a floating-point.</span><span class="sxs-lookup"><span data-stu-id="dfca2-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="dfca2-275">This function supports parameters of type number and string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="dfca2-276">The following example returns `1.0`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="dfca2-277">The following example returns `2.9`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="dfca2-278">string</span><span class="sxs-lookup"><span data-stu-id="dfca2-278">string</span></span>
<span data-ttu-id="dfca2-279">Converts the parameter to a string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-279">Converts the parameter to a string.</span></span> <span data-ttu-id="dfca2-280">This function supports parameters of all JSON data types.</span><span class="sxs-lookup"><span data-stu-id="dfca2-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="dfca2-281">The following example returns `"1"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="dfca2-282">The following example returns `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="dfca2-283">The following example returns `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="dfca2-284">The following example returns `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="dfca2-285">bool</span><span class="sxs-lookup"><span data-stu-id="dfca2-285">bool</span></span>
<span data-ttu-id="dfca2-286">Converts the parameter to a Boolean.</span><span class="sxs-lookup"><span data-stu-id="dfca2-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="dfca2-287">This function supports parameters of type number, string, and Boolean.</span><span class="sxs-lookup"><span data-stu-id="dfca2-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="dfca2-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="dfca2-289">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="dfca2-290">The following example returns `false`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="dfca2-291">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="dfca2-292">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="dfca2-293">parse</span><span class="sxs-lookup"><span data-stu-id="dfca2-293">parse</span></span>
<span data-ttu-id="dfca2-294">Converts the parameter to a native type.</span><span class="sxs-lookup"><span data-stu-id="dfca2-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="dfca2-295">In other words, this function is the inverse of `string()`.</span><span class="sxs-lookup"><span data-stu-id="dfca2-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="dfca2-296">This function supports parameters only of type string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="dfca2-297">The following example returns `1`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="dfca2-298">The following example returns `true`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="dfca2-299">The following example returns `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="dfca2-300">The following example returns `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="dfca2-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="dfca2-301">encodeBase64</span></span>
<span data-ttu-id="dfca2-302">Encodes the parameter to a base-64 encoded string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="dfca2-303">This function supports parameters only of type string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="dfca2-304">The following example returns `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="dfca2-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="dfca2-305">decodeBase64</span></span>
<span data-ttu-id="dfca2-306">Decodes the parameter from a base-64 encoded string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="dfca2-307">This function supports parameters only of type string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="dfca2-308">The following example returns `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="dfca2-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="dfca2-309">encodeUriComponent</span></span>
<span data-ttu-id="dfca2-310">Encodes the parameter to a URL encoded string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="dfca2-311">This function supports parameters only of type string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="dfca2-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="dfca2-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="dfca2-313">decodeUriComponent</span></span>
<span data-ttu-id="dfca2-314">Decodes the parameter from a URL encoded string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="dfca2-315">This function supports parameters only of type string.</span><span class="sxs-lookup"><span data-stu-id="dfca2-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="dfca2-316">The following example returns `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="dfca2-317">Math functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="dfca2-318">add</span><span class="sxs-lookup"><span data-stu-id="dfca2-318">add</span></span>
<span data-ttu-id="dfca2-319">Adds two numbers, and returns the result.</span><span class="sxs-lookup"><span data-stu-id="dfca2-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="dfca2-320">The following example returns `3`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="dfca2-321">sub</span><span class="sxs-lookup"><span data-stu-id="dfca2-321">sub</span></span>
<span data-ttu-id="dfca2-322">Subtracts the second number from the first number, and returns the result.</span><span class="sxs-lookup"><span data-stu-id="dfca2-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="dfca2-323">The following example returns `1`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="dfca2-324">mul</span><span class="sxs-lookup"><span data-stu-id="dfca2-324">mul</span></span>
<span data-ttu-id="dfca2-325">Multiplies two numbers, and returns the result.</span><span class="sxs-lookup"><span data-stu-id="dfca2-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="dfca2-326">The following example returns `6`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="dfca2-327">div</span><span class="sxs-lookup"><span data-stu-id="dfca2-327">div</span></span>
<span data-ttu-id="dfca2-328">Divides the first number by the second number, and returns the result.</span><span class="sxs-lookup"><span data-stu-id="dfca2-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="dfca2-329">The result is always an integer.</span><span class="sxs-lookup"><span data-stu-id="dfca2-329">The result is always an integer.</span></span>

<span data-ttu-id="dfca2-330">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="dfca2-331">mod</span><span class="sxs-lookup"><span data-stu-id="dfca2-331">mod</span></span>
<span data-ttu-id="dfca2-332">Divides the first number by the second number, and returns the remainder.</span><span class="sxs-lookup"><span data-stu-id="dfca2-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="dfca2-333">The following example returns `0`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="dfca2-334">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="dfca2-335">min</span><span class="sxs-lookup"><span data-stu-id="dfca2-335">min</span></span>
<span data-ttu-id="dfca2-336">Returns the small of the two numbers.</span><span class="sxs-lookup"><span data-stu-id="dfca2-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="dfca2-337">The following example returns `1`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="dfca2-338">max</span><span class="sxs-lookup"><span data-stu-id="dfca2-338">max</span></span>
<span data-ttu-id="dfca2-339">Returns the larger of the two numbers.</span><span class="sxs-lookup"><span data-stu-id="dfca2-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="dfca2-340">The following example returns `2`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="dfca2-341">range</span><span class="sxs-lookup"><span data-stu-id="dfca2-341">range</span></span>
<span data-ttu-id="dfca2-342">Generates a sequence of integral numbers within the specified range.</span><span class="sxs-lookup"><span data-stu-id="dfca2-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="dfca2-343">The following example returns `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="dfca2-344">rand</span><span class="sxs-lookup"><span data-stu-id="dfca2-344">rand</span></span>
<span data-ttu-id="dfca2-345">Returns a random integral number within the specified range.</span><span class="sxs-lookup"><span data-stu-id="dfca2-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="dfca2-346">This function does not generate cryptographically secure random numbers.</span><span class="sxs-lookup"><span data-stu-id="dfca2-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="dfca2-347">The following example could return `42`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="dfca2-348">floor</span><span class="sxs-lookup"><span data-stu-id="dfca2-348">floor</span></span>
<span data-ttu-id="dfca2-349">Returns the largest integer less than or equal to the specified number.</span><span class="sxs-lookup"><span data-stu-id="dfca2-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="dfca2-350">The following example returns `3`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="dfca2-351">ceil</span><span class="sxs-lookup"><span data-stu-id="dfca2-351">ceil</span></span>
<span data-ttu-id="dfca2-352">Returns the largest integer greater than or equal to the specified number.</span><span class="sxs-lookup"><span data-stu-id="dfca2-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="dfca2-353">The following example returns `4`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="dfca2-354">Date functions</span><span class="sxs-lookup"><span data-stu-id="dfca2-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="dfca2-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="dfca2-355">utcNow</span></span>
<span data-ttu-id="dfca2-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span><span class="sxs-lookup"><span data-stu-id="dfca2-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="dfca2-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="dfca2-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="dfca2-358">addSeconds</span></span>
<span data-ttu-id="dfca2-359">Adds an integral number of seconds to the specified timestamp.</span><span class="sxs-lookup"><span data-stu-id="dfca2-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="dfca2-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="dfca2-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="dfca2-361">addMinutes</span></span>
<span data-ttu-id="dfca2-362">Adds an integral number of minutes to the specified timestamp.</span><span class="sxs-lookup"><span data-stu-id="dfca2-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="dfca2-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="dfca2-364">addHours</span><span class="sxs-lookup"><span data-stu-id="dfca2-364">addHours</span></span>
<span data-ttu-id="dfca2-365">Adds an integral number of hours to the specified timestamp.</span><span class="sxs-lookup"><span data-stu-id="dfca2-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="dfca2-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="dfca2-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="dfca2-367">Next steps</span><span class="sxs-lookup"><span data-stu-id="dfca2-367">Next steps</span></span>
* <span data-ttu-id="dfca2-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfca2-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

