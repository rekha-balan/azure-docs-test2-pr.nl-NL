---
title: Semantic interpretation in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use semantic interpretation in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: f38b74d04ce11379d11fccbf4573c8549eae8e0e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552087"
---
# <a name="semantic-interpretation"></a><span data-ttu-id="3d3b0-103">Semantic Interpretation</span><span class="sxs-lookup"><span data-stu-id="3d3b0-103">Semantic Interpretation</span></span>
<span data-ttu-id="3d3b0-104">Semantic interpretation associates semantic output with each interpreted path through the grammar.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-104">Semantic interpretation associates semantic output with each interpreted path through the grammar.</span></span>  <span data-ttu-id="3d3b0-105">In particular, the service evaluates the sequence of statements in the `tag` elements traversed by the interpretation to compute the final output.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-105">In particular, the service evaluates the sequence of statements in the `tag` elements traversed by the interpretation to compute the final output.</span></span>  

<span data-ttu-id="3d3b0-106">A statement may be an assignment of a literal or a variable to another variable.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-106">A statement may be an assignment of a literal or a variable to another variable.</span></span>  <span data-ttu-id="3d3b0-107">It may also assign the output of a function with 0 or more parameters to a variable.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-107">It may also assign the output of a function with 0 or more parameters to a variable.</span></span>  <span data-ttu-id="3d3b0-108">Each function parameter may be specified using a literal or a variable.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-108">Each function parameter may be specified using a literal or a variable.</span></span>  <span data-ttu-id="3d3b0-109">If the function does not return any output, the assignment is omitted.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-109">If the function does not return any output, the assignment is omitted.</span></span>

```xml
<tag>x = 1; y = x;</tag>
<tag>q = All(); q = And(q, q2);</tag>
<tag>AssertEquals(x, 1);</tag>
```

<span data-ttu-id="3d3b0-110">A variable is specified using a name identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (\_).</span><span class="sxs-lookup"><span data-stu-id="3d3b0-110">A variable is specified using a name identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (\_).</span></span>  <span data-ttu-id="3d3b0-111">Its type is implicitly inferred from the literal or function output value assigned to it.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-111">Its type is implicitly inferred from the literal or function output value assigned to it.</span></span> 

<span data-ttu-id="3d3b0-112">Below is a list of currently supported data types:</span><span class="sxs-lookup"><span data-stu-id="3d3b0-112">Below is a list of currently supported data types:</span></span>

|<span data-ttu-id="3d3b0-113">Type</span><span class="sxs-lookup"><span data-stu-id="3d3b0-113">Type</span></span>|<span data-ttu-id="3d3b0-114">Description</span><span class="sxs-lookup"><span data-stu-id="3d3b0-114">Description</span></span>|<span data-ttu-id="3d3b0-115">Examples</span><span class="sxs-lookup"><span data-stu-id="3d3b0-115">Examples</span></span>|
|----|----|----|
|<span data-ttu-id="3d3b0-116">String</span><span class="sxs-lookup"><span data-stu-id="3d3b0-116">String</span></span>|<span data-ttu-id="3d3b0-117">Sequence of 0 or more characters</span><span class="sxs-lookup"><span data-stu-id="3d3b0-117">Sequence of 0 or more characters</span></span>|<span data-ttu-id="3d3b0-118">"Hello World!"</span><span class="sxs-lookup"><span data-stu-id="3d3b0-118">"Hello World!"</span></span><br/><span data-ttu-id="3d3b0-119">""</span><span class="sxs-lookup"><span data-stu-id="3d3b0-119">""</span></span>|
|<span data-ttu-id="3d3b0-120">Bool</span><span class="sxs-lookup"><span data-stu-id="3d3b0-120">Bool</span></span>|<span data-ttu-id="3d3b0-121">Boolean value</span><span class="sxs-lookup"><span data-stu-id="3d3b0-121">Boolean value</span></span>|<span data-ttu-id="3d3b0-122">true</span><span class="sxs-lookup"><span data-stu-id="3d3b0-122">true</span></span><br/><span data-ttu-id="3d3b0-123">false</span><span class="sxs-lookup"><span data-stu-id="3d3b0-123">false</span></span>|
|<span data-ttu-id="3d3b0-124">Int32</span><span class="sxs-lookup"><span data-stu-id="3d3b0-124">Int32</span></span>|<span data-ttu-id="3d3b0-125">32-bit signed integer.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-125">32-bit signed integer.</span></span>  <span data-ttu-id="3d3b0-126">-2.1e9 to 2.1e9</span><span class="sxs-lookup"><span data-stu-id="3d3b0-126">-2.1e9 to 2.1e9</span></span>|<span data-ttu-id="3d3b0-127">123</span><span class="sxs-lookup"><span data-stu-id="3d3b0-127">123</span></span><br/><span data-ttu-id="3d3b0-128">-321</span><span class="sxs-lookup"><span data-stu-id="3d3b0-128">-321</span></span>|
|<span data-ttu-id="3d3b0-129">Int64</span><span class="sxs-lookup"><span data-stu-id="3d3b0-129">Int64</span></span>|<span data-ttu-id="3d3b0-130">64-bit signed integer.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-130">64-bit signed integer.</span></span> <span data-ttu-id="3d3b0-131">-9.2e18 and 9.2e18</span><span class="sxs-lookup"><span data-stu-id="3d3b0-131">-9.2e18 and 9.2e18</span></span>|<span data-ttu-id="3d3b0-132">9876543210</span><span class="sxs-lookup"><span data-stu-id="3d3b0-132">9876543210</span></span>|
|<span data-ttu-id="3d3b0-133">Double</span><span class="sxs-lookup"><span data-stu-id="3d3b0-133">Double</span></span>|<span data-ttu-id="3d3b0-134">Double precision floating-point.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-134">Double precision floating-point.</span></span> <span data-ttu-id="3d3b0-135">1.7e+/-308 (15 digits)</span><span class="sxs-lookup"><span data-stu-id="3d3b0-135">1.7e+/-308 (15 digits)</span></span>|<span data-ttu-id="3d3b0-136">123.456789</span><span class="sxs-lookup"><span data-stu-id="3d3b0-136">123.456789</span></span><br/><span data-ttu-id="3d3b0-137">1.23456789e2</span><span class="sxs-lookup"><span data-stu-id="3d3b0-137">1.23456789e2</span></span>|
|<span data-ttu-id="3d3b0-138">Guid</span><span class="sxs-lookup"><span data-stu-id="3d3b0-138">Guid</span></span>|<span data-ttu-id="3d3b0-139">Globally unique identifier</span><span class="sxs-lookup"><span data-stu-id="3d3b0-139">Globally unique identifier</span></span>|<span data-ttu-id="3d3b0-140">"602DD052-CC47-4B23-A16A-26B52D30C05B"</span><span class="sxs-lookup"><span data-stu-id="3d3b0-140">"602DD052-CC47-4B23-A16A-26B52D30C05B"</span></span>|
|<span data-ttu-id="3d3b0-141">Query</span><span class="sxs-lookup"><span data-stu-id="3d3b0-141">Query</span></span>|<span data-ttu-id="3d3b0-142">Query expression that specifies a subset of data objects in the index</span><span class="sxs-lookup"><span data-stu-id="3d3b0-142">Query expression that specifies a subset of data objects in the index</span></span>|<span data-ttu-id="3d3b0-143">All()</span><span class="sxs-lookup"><span data-stu-id="3d3b0-143">All()</span></span><br/><span data-ttu-id="3d3b0-144">And(*q1*, *q2*)</span><span class="sxs-lookup"><span data-stu-id="3d3b0-144">And(*q1*, *q2*)</span></span>|

<a name="semantic-functions"></a>
## <a name="semantic-functions"></a><span data-ttu-id="3d3b0-145">Semantic Functions</span><span class="sxs-lookup"><span data-stu-id="3d3b0-145">Semantic Functions</span></span>
<span data-ttu-id="3d3b0-146">There is a built-in set of semantic functions.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-146">There is a built-in set of semantic functions.</span></span>  <span data-ttu-id="3d3b0-147">They allow the construction of sophisticated queries, and provide context sensitive control over grammar interpretations.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-147">They allow the construction of sophisticated queries, and provide context sensitive control over grammar interpretations.</span></span>

### <a name="and-function"></a><span data-ttu-id="3d3b0-148">And Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-148">And Function</span></span>
`query = And(query1, query2);`

<span data-ttu-id="3d3b0-149">Returns a query composed from the intersection of two input queries.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-149">Returns a query composed from the intersection of two input queries.</span></span>

### <a name="or-function"></a><span data-ttu-id="3d3b0-150">Or Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-150">Or Function</span></span>
`query = Or(query1, query2);`

<span data-ttu-id="3d3b0-151">Returns a query composed from the union of two input queries.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-151">Returns a query composed from the union of two input queries.</span></span>

### <a name="all-function"></a><span data-ttu-id="3d3b0-152">All Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-152">All Function</span></span>
`query = All();`

<span data-ttu-id="3d3b0-153">Returns a query that includes all data objects.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-153">Returns a query that includes all data objects.</span></span>

<span data-ttu-id="3d3b0-154">In the following example, we use the All() function to iteratively build up a query based on the intersection of 1 or more keywords.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-154">In the following example, we use the All() function to iteratively build up a query based on the intersection of 1 or more keywords.</span></span>

```
<tag>query = All();</tag>
<item repeat="1-">
  <attrref uri="academic#Keyword" name="keyword">
  <tag>query = And(query, keyword);</tag>
</item>
```

### <a name="none-function"></a><span data-ttu-id="3d3b0-155">None Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-155">None Function</span></span>
`query = None();`

<span data-ttu-id="3d3b0-156">Returns a query that includes no data objects.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-156">Returns a query that includes no data objects.</span></span>

<span data-ttu-id="3d3b0-157">In the following example, we use the None() function to iteratively build up a query based on the union of 1 or more keywords.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-157">In the following example, we use the None() function to iteratively build up a query based on the union of 1 or more keywords.</span></span>

```
<tag>query = None();</tag>
<item repeat="1-">
  <attrref uri="academic#Keyword" name="keyword">
  <tag>query = Or(query, keyword);</tag>
</item>
```

### <a name="query-function"></a><span data-ttu-id="3d3b0-158">Query Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-158">Query Function</span></span>
```
query = Query(attrName, value)
query = Query(attrName, value, op)
```

<span data-ttu-id="3d3b0-159">Returns a query that includes only data objects whose attribute *attrName* matches value *value* according to the specified operation *op*, which defaults to "eq".</span><span class="sxs-lookup"><span data-stu-id="3d3b0-159">Returns a query that includes only data objects whose attribute *attrName* matches value *value* according to the specified operation *op*, which defaults to "eq".</span></span>  <span data-ttu-id="3d3b0-160">Typically, use an `attrref` element to create a query based on the matched input query string.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-160">Typically, use an `attrref` element to create a query based on the matched input query string.</span></span>  <span data-ttu-id="3d3b0-161">If a value is given or obtained through other means, the Query() function can be used to create a query matching this value.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-161">If a value is given or obtained through other means, the Query() function can be used to create a query matching this value.</span></span>

<span data-ttu-id="3d3b0-162">In the following example, we use the Query() function to implement support for specifying academic publications from a particular decade.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-162">In the following example, we use the Query() function to implement support for specifying academic publications from a particular decade.</span></span>

```xml
written in the 90s
<tag>
  beginYear = Query("academic#Year", 1990, "ge");
  endYear = Query("academic#Year", 2000, "lt");
  year = And(beginYear, endYear);
</tag>
```

<a name="composite-function"/>
### <a name="composite-function"></a><span data-ttu-id="3d3b0-163">Composite Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-163">Composite Function</span></span>
`query = Composite(innerQuery);`

<span data-ttu-id="3d3b0-164">Returns a query that encapsulates an *innerQuery* composed of matches against sub-attributes of a common composite attribute *attr*.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-164">Returns a query that encapsulates an *innerQuery* composed of matches against sub-attributes of a common composite attribute *attr*.</span></span>  <span data-ttu-id="3d3b0-165">The encapsulation requires the composite attribute *attr* of any matching data object to have at least one value that individually satisfies the *innerQuery*.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-165">The encapsulation requires the composite attribute *attr* of any matching data object to have at least one value that individually satisfies the *innerQuery*.</span></span>  <span data-ttu-id="3d3b0-166">Note that a query on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other queries.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-166">Note that a query on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other queries.</span></span>

<span data-ttu-id="3d3b0-167">For example, the following query returns academic publications by "harry shum" while he was at "microsoft":</span><span class="sxs-lookup"><span data-stu-id="3d3b0-167">For example, the following query returns academic publications by "harry shum" while he was at "microsoft":</span></span>
```
Composite(And(Query("academic#Author.Name", "harry shum"), 
              Query("academic#Author.Affiliation", "microsoft")));
```

<span data-ttu-id="3d3b0-168">On the other hand, the following query returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span><span class="sxs-lookup"><span data-stu-id="3d3b0-168">On the other hand, the following query returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span></span>
```
And(Composite(Query("academic#Author.Name", "harry shum"), 
    Composite(Query("academic#Author.Affiliation", "microsoft")));
```

### <a name="getvariable-function"></a><span data-ttu-id="3d3b0-169">GetVariable Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-169">GetVariable Function</span></span>
`value = GetVariable(name, scope);`

<span data-ttu-id="3d3b0-170">Returns the value of variable *name* defined under the specified *scope*.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-170">Returns the value of variable *name* defined under the specified *scope*.</span></span>  <span data-ttu-id="3d3b0-171">*name* is an identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (_).</span><span class="sxs-lookup"><span data-stu-id="3d3b0-171">*name* is an identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (_).</span></span>  <span data-ttu-id="3d3b0-172">*scope* can be set to "request" or "system".</span><span class="sxs-lookup"><span data-stu-id="3d3b0-172">*scope* can be set to "request" or "system".</span></span>  <span data-ttu-id="3d3b0-173">Note that variables defined under different scopes are distinct from each other, including ones defined via the output of semantic functions.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-173">Note that variables defined under different scopes are distinct from each other, including ones defined via the output of semantic functions.</span></span>

<span data-ttu-id="3d3b0-174">Request scope variables are shared across all interpretations within the current interpret request.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-174">Request scope variables are shared across all interpretations within the current interpret request.</span></span>  <span data-ttu-id="3d3b0-175">They can be used to control the search for interpretations over the grammar.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-175">They can be used to control the search for interpretations over the grammar.</span></span>

<span data-ttu-id="3d3b0-176">System variables are predefined by the service and can be used to retrieve various statistics about the current state of the system.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-176">System variables are predefined by the service and can be used to retrieve various statistics about the current state of the system.</span></span>  <span data-ttu-id="3d3b0-177">Below is the set of currently supported system variables:</span><span class="sxs-lookup"><span data-stu-id="3d3b0-177">Below is the set of currently supported system variables:</span></span>

|<span data-ttu-id="3d3b0-178">Name</span><span class="sxs-lookup"><span data-stu-id="3d3b0-178">Name</span></span>|<span data-ttu-id="3d3b0-179">Type</span><span class="sxs-lookup"><span data-stu-id="3d3b0-179">Type</span></span>|<span data-ttu-id="3d3b0-180">Description</span><span class="sxs-lookup"><span data-stu-id="3d3b0-180">Description</span></span>|
|----|----|----|
|<span data-ttu-id="3d3b0-181">IsAtEndOfQuery</span><span class="sxs-lookup"><span data-stu-id="3d3b0-181">IsAtEndOfQuery</span></span>|<span data-ttu-id="3d3b0-182">Bool</span><span class="sxs-lookup"><span data-stu-id="3d3b0-182">Bool</span></span>|<span data-ttu-id="3d3b0-183">true if the current interpretation has matched all input query text</span><span class="sxs-lookup"><span data-stu-id="3d3b0-183">true if the current interpretation has matched all input query text</span></span>|
|<span data-ttu-id="3d3b0-184">IsBeyondEndOfQuery</span><span class="sxs-lookup"><span data-stu-id="3d3b0-184">IsBeyondEndOfQuery</span></span>|<span data-ttu-id="3d3b0-185">Bool</span><span class="sxs-lookup"><span data-stu-id="3d3b0-185">Bool</span></span>|<span data-ttu-id="3d3b0-186">true if the current interpretation has suggested completions beyond the input query text</span><span class="sxs-lookup"><span data-stu-id="3d3b0-186">true if the current interpretation has suggested completions beyond the input query text</span></span>|

### <a name="setvariable-function"></a><span data-ttu-id="3d3b0-187">SetVariable Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-187">SetVariable Function</span></span>
`SetVariable(name, value, scope);`

<span data-ttu-id="3d3b0-188">Assigns *value* to variable *name* under the specified *scope*.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-188">Assigns *value* to variable *name* under the specified *scope*.</span></span>  <span data-ttu-id="3d3b0-189">*name* is an identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (_).</span><span class="sxs-lookup"><span data-stu-id="3d3b0-189">*name* is an identifier that starts with a letter and consists only of letters (A-Z), numbers (0-9), and the underscore (_).</span></span>  <span data-ttu-id="3d3b0-190">Currently, the only valid value for *scope* is "request".</span><span class="sxs-lookup"><span data-stu-id="3d3b0-190">Currently, the only valid value for *scope* is "request".</span></span>  <span data-ttu-id="3d3b0-191">There are no settable system variables.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-191">There are no settable system variables.</span></span>

<span data-ttu-id="3d3b0-192">Request scope variables are shared across all interpretations within the current interpret request.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-192">Request scope variables are shared across all interpretations within the current interpret request.</span></span>  <span data-ttu-id="3d3b0-193">They can be used to control the search for interpretations over the grammar.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-193">They can be used to control the search for interpretations over the grammar.</span></span>

### <a name="assertequals-function"></a><span data-ttu-id="3d3b0-194">AssertEquals Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-194">AssertEquals Function</span></span>
`AssertEquals(value1, value2);`

<span data-ttu-id="3d3b0-195">If *value1* and *value2* are equivalent, the function succeeds and has no side effects.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-195">If *value1* and *value2* are equivalent, the function succeeds and has no side effects.</span></span>  <span data-ttu-id="3d3b0-196">Otherwise, the function fails and rejects the interpretation.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-196">Otherwise, the function fails and rejects the interpretation.</span></span>

### <a name="assertnotequals-function"></a><span data-ttu-id="3d3b0-197">AssertNotEquals Function</span><span class="sxs-lookup"><span data-stu-id="3d3b0-197">AssertNotEquals Function</span></span>
`AssertNotEquals(value1, value2);`

<span data-ttu-id="3d3b0-198">If *value1* and *value2* are not equivalent, the function succeeds and has no side effects.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-198">If *value1* and *value2* are not equivalent, the function succeeds and has no side effects.</span></span>  <span data-ttu-id="3d3b0-199">Otherwise, the function fails and rejects the interpretation.</span><span class="sxs-lookup"><span data-stu-id="3d3b0-199">Otherwise, the function fails and rejects the interpretation.</span></span>


