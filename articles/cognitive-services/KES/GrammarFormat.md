---
title: Grammar format in the Knowledge Exploration Service API | Microsoft Docs
description: Learn about the grammar format in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: f347f991b8c64f1cd7674dd5ddab55fa9586a4bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663058"
---
# <a name="grammar-format"></a><span data-ttu-id="09a83-103">Grammar Format</span><span class="sxs-lookup"><span data-stu-id="09a83-103">Grammar Format</span></span>
<span data-ttu-id="09a83-104">The grammar is an XML file that specifies the weighted set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span><span class="sxs-lookup"><span data-stu-id="09a83-104">The grammar is an XML file that specifies the weighted set of natural language queries that the service can interpret, as well as how these natural language queries are translated into semantic query expressions.</span></span>  <span data-ttu-id="09a83-105">The grammar syntax is based on [SRGS](http://www.w3.org/TR/speech-grammar/), a W3C standard for speech recognition grammars, with extensions to support data index integration and semantic functions.</span><span class="sxs-lookup"><span data-stu-id="09a83-105">The grammar syntax is based on [SRGS](http://www.w3.org/TR/speech-grammar/), a W3C standard for speech recognition grammars, with extensions to support data index integration and semantic functions.</span></span>

<span data-ttu-id="09a83-106">The following describes each of the syntactic elements that can be used in a grammar.</span><span class="sxs-lookup"><span data-stu-id="09a83-106">The following describes each of the syntactic elements that can be used in a grammar.</span></span>  <span data-ttu-id="09a83-107">See [this example](#example) for a complete grammar that demonstrates the use of these elements in context.</span><span class="sxs-lookup"><span data-stu-id="09a83-107">See [this example](#example) for a complete grammar that demonstrates the use of these elements in context.</span></span>

### <a name="grammar-element"></a><span data-ttu-id="09a83-108">grammar Element</span><span class="sxs-lookup"><span data-stu-id="09a83-108">grammar Element</span></span> 
<span data-ttu-id="09a83-109">The `grammar` element is the top-level element in the grammar specification XML.</span><span class="sxs-lookup"><span data-stu-id="09a83-109">The `grammar` element is the top-level element in the grammar specification XML.</span></span>  <span data-ttu-id="09a83-110">The required `root` attribute specifies the name of the root rule that defines the starting point of the grammar.</span><span class="sxs-lookup"><span data-stu-id="09a83-110">The required `root` attribute specifies the name of the root rule that defines the starting point of the grammar.</span></span>

```xml
<grammar root="GetPapers">
```

### <a name="import-element"></a><span data-ttu-id="09a83-111">import Element</span><span class="sxs-lookup"><span data-stu-id="09a83-111">import Element</span></span>
<span data-ttu-id="09a83-112">The `import` element imports a schema definition from an external file to enable attribute references.</span><span class="sxs-lookup"><span data-stu-id="09a83-112">The `import` element imports a schema definition from an external file to enable attribute references.</span></span> <span data-ttu-id="09a83-113">The element must be a child of the top-level `grammar` element and appear before any `attrref` elements.</span><span class="sxs-lookup"><span data-stu-id="09a83-113">The element must be a child of the top-level `grammar` element and appear before any `attrref` elements.</span></span> <span data-ttu-id="09a83-114">The required `schema` attribute specifies the name of a schema file located in the same directory as the grammar XML file.</span><span class="sxs-lookup"><span data-stu-id="09a83-114">The required `schema` attribute specifies the name of a schema file located in the same directory as the grammar XML file.</span></span> <span data-ttu-id="09a83-115">The required `name` element specifies the schema alias that subsequent `attrref` elements use when referencing attributes defined within this schema.</span><span class="sxs-lookup"><span data-stu-id="09a83-115">The required `name` element specifies the schema alias that subsequent `attrref` elements use when referencing attributes defined within this schema.</span></span>

```xml
  <import schema="academic.schema" name="academic"/>
```

### <a name="rule-element"></a><span data-ttu-id="09a83-116">rule Element</span><span class="sxs-lookup"><span data-stu-id="09a83-116">rule Element</span></span>
<span data-ttu-id="09a83-117">The `rule` element defines a grammar rule, a structural unit that specifies a set of query expressions that the system can interpret.</span><span class="sxs-lookup"><span data-stu-id="09a83-117">The `rule` element defines a grammar rule, a structural unit that specifies a set of query expressions that the system can interpret.</span></span>  <span data-ttu-id="09a83-118">The element must be a child of the top-level `grammar` element.</span><span class="sxs-lookup"><span data-stu-id="09a83-118">The element must be a child of the top-level `grammar` element.</span></span>  <span data-ttu-id="09a83-119">The required `id` attribute specifies the name of the rule, which is referenced from `grammar` or `ruleref` elements.</span><span class="sxs-lookup"><span data-stu-id="09a83-119">The required `id` attribute specifies the name of the rule, which is referenced from `grammar` or `ruleref` elements.</span></span>

<span data-ttu-id="09a83-120">A `rule` element defines a set of legal expansions.</span><span class="sxs-lookup"><span data-stu-id="09a83-120">A `rule` element defines a set of legal expansions.</span></span>  <span data-ttu-id="09a83-121">Text tokens match against the input query directly.</span><span class="sxs-lookup"><span data-stu-id="09a83-121">Text tokens match against the input query directly.</span></span>  <span data-ttu-id="09a83-122">`item` elements specify repeats and alter interpretation probabilities.</span><span class="sxs-lookup"><span data-stu-id="09a83-122">`item` elements specify repeats and alter interpretation probabilities.</span></span>  <span data-ttu-id="09a83-123">`one-of` elements indicate alternative choices.</span><span class="sxs-lookup"><span data-stu-id="09a83-123">`one-of` elements indicate alternative choices.</span></span>  <span data-ttu-id="09a83-124">`ruleref` elements enable construction of more complex expansions from simpler ones.</span><span class="sxs-lookup"><span data-stu-id="09a83-124">`ruleref` elements enable construction of more complex expansions from simpler ones.</span></span>  <span data-ttu-id="09a83-125">`attrref` elements allow matches against attribute values from the index.</span><span class="sxs-lookup"><span data-stu-id="09a83-125">`attrref` elements allow matches against attribute values from the index.</span></span>  <span data-ttu-id="09a83-126">`tag` elements specify the semantics of the interpretation and can alter the interpretation probability.</span><span class="sxs-lookup"><span data-stu-id="09a83-126">`tag` elements specify the semantics of the interpretation and can alter the interpretation probability.</span></span>

```xml
<rule id="GetPapers">...</rule>
```

### <a name="example-element"></a><span data-ttu-id="09a83-127">example Element</span><span class="sxs-lookup"><span data-stu-id="09a83-127">example Element</span></span>
<span data-ttu-id="09a83-128">The optional `example` element specifies example phrases that may be accepted by the containing `rule` definition.</span><span class="sxs-lookup"><span data-stu-id="09a83-128">The optional `example` element specifies example phrases that may be accepted by the containing `rule` definition.</span></span>  <span data-ttu-id="09a83-129">This may be used for documentation and/or automated testing.</span><span class="sxs-lookup"><span data-stu-id="09a83-129">This may be used for documentation and/or automated testing.</span></span>

```xml
<example>papers about machine learning by michael jordan</example>
```

### <a name="item-element"></a><span data-ttu-id="09a83-130">item Element</span><span class="sxs-lookup"><span data-stu-id="09a83-130">item Element</span></span>
<span data-ttu-id="09a83-131">The `item` element groups a sequence of grammar constructs.</span><span class="sxs-lookup"><span data-stu-id="09a83-131">The `item` element groups a sequence of grammar constructs.</span></span>  <span data-ttu-id="09a83-132">It can be used to indicate repetitions of the expansion sequence, or to specify alternatives in conjunction with the `one-of` element.</span><span class="sxs-lookup"><span data-stu-id="09a83-132">It can be used to indicate repetitions of the expansion sequence, or to specify alternatives in conjunction with the `one-of` element.</span></span>

<span data-ttu-id="09a83-133">When an `item` element is not a child of a `one-of` element, it can specify repetition of the enclosed sequence by assigning the `repeat` attribute to a count value.</span><span class="sxs-lookup"><span data-stu-id="09a83-133">When an `item` element is not a child of a `one-of` element, it can specify repetition of the enclosed sequence by assigning the `repeat` attribute to a count value.</span></span>  <span data-ttu-id="09a83-134">A count value of "*n*" (where *n* is an integer) indicates that the sequence must occur exactly *n* times.</span><span class="sxs-lookup"><span data-stu-id="09a83-134">A count value of "*n*" (where *n* is an integer) indicates that the sequence must occur exactly *n* times.</span></span>  <span data-ttu-id="09a83-135">A count value of "*m*-*n*" allows the sequence to appear between *m* and *n* times, inclusively.</span><span class="sxs-lookup"><span data-stu-id="09a83-135">A count value of "*m*-*n*" allows the sequence to appear between *m* and *n* times, inclusively.</span></span>  <span data-ttu-id="09a83-136">A count value of "*m*-" specifies that the sequence must appear at least *m* times.</span><span class="sxs-lookup"><span data-stu-id="09a83-136">A count value of "*m*-" specifies that the sequence must appear at least *m* times.</span></span>  <span data-ttu-id="09a83-137">The optional `repeat-logprob` attribute can be used to alter the interpretation probability for each additional repetition beyond the minimum.</span><span class="sxs-lookup"><span data-stu-id="09a83-137">The optional `repeat-logprob` attribute can be used to alter the interpretation probability for each additional repetition beyond the minimum.</span></span>

```xml
<item repeat="1-" repeat-logprob="-10">...</item>
```

<span data-ttu-id="09a83-138">When `item` elements appear as children of a `one-of` element, they define the set of expansion alternatives.</span><span class="sxs-lookup"><span data-stu-id="09a83-138">When `item` elements appear as children of a `one-of` element, they define the set of expansion alternatives.</span></span>  <span data-ttu-id="09a83-139">In this usage, the optional `logprob` attribute specifies the relative log probability among the different choices.</span><span class="sxs-lookup"><span data-stu-id="09a83-139">In this usage, the optional `logprob` attribute specifies the relative log probability among the different choices.</span></span>  <span data-ttu-id="09a83-140">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the the natural log function.</span><span class="sxs-lookup"><span data-stu-id="09a83-140">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the the natural log function.</span></span>  <span data-ttu-id="09a83-141">If not specified, `logprob` defaults to 0, which does not alter the interpretation probability.</span><span class="sxs-lookup"><span data-stu-id="09a83-141">If not specified, `logprob` defaults to 0, which does not alter the interpretation probability.</span></span>  <span data-ttu-id="09a83-142">Note that log probability is always a negative floating-point value or 0.</span><span class="sxs-lookup"><span data-stu-id="09a83-142">Note that log probability is always a negative floating-point value or 0.</span></span>

```xml
<one-of>
  <item>by</item>
  <item logprob="-0.5">written by</item>
  <item logprob="-1">authored by</item>
</one-of>
```

### <a name="one-of-element"></a><span data-ttu-id="09a83-143">one-of Element</span><span class="sxs-lookup"><span data-stu-id="09a83-143">one-of Element</span></span>
<span data-ttu-id="09a83-144">The `one-of` element specifies alternative expansions among one of the child `item` elements.</span><span class="sxs-lookup"><span data-stu-id="09a83-144">The `one-of` element specifies alternative expansions among one of the child `item` elements.</span></span>  <span data-ttu-id="09a83-145">Only `item` elements may appear inside a `one-of` element.</span><span class="sxs-lookup"><span data-stu-id="09a83-145">Only `item` elements may appear inside a `one-of` element.</span></span>  <span data-ttu-id="09a83-146">Relative probabilities among the different choices may be specified via the `logprob` attribute in each child `item`.</span><span class="sxs-lookup"><span data-stu-id="09a83-146">Relative probabilities among the different choices may be specified via the `logprob` attribute in each child `item`.</span></span>

```xml
<one-of>
  <item>by</item>
  <item logprob="-0.5">written by</item>
  <item logprob="-1">authored by</item>
</one-of>
```

### <a name="ruleref-element"></a><span data-ttu-id="09a83-147">ruleref Element</span><span class="sxs-lookup"><span data-stu-id="09a83-147">ruleref Element</span></span>
<span data-ttu-id="09a83-148">The `ruleref` element specifies valid expansions via references to another `rule` element.</span><span class="sxs-lookup"><span data-stu-id="09a83-148">The `ruleref` element specifies valid expansions via references to another `rule` element.</span></span>  <span data-ttu-id="09a83-149">Through the use of `ruleref` elements, more complex expressions can be built from simpler rules.</span><span class="sxs-lookup"><span data-stu-id="09a83-149">Through the use of `ruleref` elements, more complex expressions can be built from simpler rules.</span></span>  <span data-ttu-id="09a83-150">The required `uri` attribute indicates the name of the referenced `rule` using the syntax "#*rulename*".</span><span class="sxs-lookup"><span data-stu-id="09a83-150">The required `uri` attribute indicates the name of the referenced `rule` using the syntax "#*rulename*".</span></span>  <span data-ttu-id="09a83-151">To capture the semantic output of the referenced rule, use the optional `name` attribute to specify the name of a variable to which the semantic output is assigned.</span><span class="sxs-lookup"><span data-stu-id="09a83-151">To capture the semantic output of the referenced rule, use the optional `name` attribute to specify the name of a variable to which the semantic output is assigned.</span></span>
 
```xml
<ruleref uri="#GetPaperYear" name="year"/>
```

### <a name="attrref-element"></a><span data-ttu-id="09a83-152">attrref Element</span><span class="sxs-lookup"><span data-stu-id="09a83-152">attrref Element</span></span>
<span data-ttu-id="09a83-153">The `attrref` element references an index attribute, allowing matching against attribute values observed in the index.</span><span class="sxs-lookup"><span data-stu-id="09a83-153">The `attrref` element references an index attribute, allowing matching against attribute values observed in the index.</span></span>  <span data-ttu-id="09a83-154">The required `uri` attribute specifies the index schema name and attribute name using the syntax "*schemaName*#*attrName*".</span><span class="sxs-lookup"><span data-stu-id="09a83-154">The required `uri` attribute specifies the index schema name and attribute name using the syntax "*schemaName*#*attrName*".</span></span>  <span data-ttu-id="09a83-155">There must be a preceding `import` element that imports the schema named *schemaName*.</span><span class="sxs-lookup"><span data-stu-id="09a83-155">There must be a preceding `import` element that imports the schema named *schemaName*.</span></span>  <span data-ttu-id="09a83-156">The attribute name is the name of an attribute defined in the corresponding schema.</span><span class="sxs-lookup"><span data-stu-id="09a83-156">The attribute name is the name of an attribute defined in the corresponding schema.</span></span>

<span data-ttu-id="09a83-157">In addition to matching user input, the `attrref` element also returns a structured query object as output that selects the subset of objects in the index matching the input value.</span><span class="sxs-lookup"><span data-stu-id="09a83-157">In addition to matching user input, the `attrref` element also returns a structured query object as output that selects the subset of objects in the index matching the input value.</span></span>  <span data-ttu-id="09a83-158">Use the optional `name` attribute to specify the name of the variable where the query object output should be stored.</span><span class="sxs-lookup"><span data-stu-id="09a83-158">Use the optional `name` attribute to specify the name of the variable where the query object output should be stored.</span></span>  <span data-ttu-id="09a83-159">The query object can be composed with other query objects to form more complex expressions.</span><span class="sxs-lookup"><span data-stu-id="09a83-159">The query object can be composed with other query objects to form more complex expressions.</span></span>  <span data-ttu-id="09a83-160">See [Semantic Interpretation](SemanticInterpretation.md) for details.</span><span class="sxs-lookup"><span data-stu-id="09a83-160">See [Semantic Interpretation](SemanticInterpretation.md) for details.</span></span>  

```xml
<attrref uri="academic#Keyword" name="keyword"/>
```

#### <a name="query-completion"></a><span data-ttu-id="09a83-161">Query Completion</span><span class="sxs-lookup"><span data-stu-id="09a83-161">Query Completion</span></span> 
<span data-ttu-id="09a83-162">To support query completions when interpreting partial user queries, each referenced attribute must include "starts_with" as an operation in the schema definition.</span><span class="sxs-lookup"><span data-stu-id="09a83-162">To support query completions when interpreting partial user queries, each referenced attribute must include "starts_with" as an operation in the schema definition.</span></span>  <span data-ttu-id="09a83-163">Given a user query prefix, `attrref` will match all values in the index that complete the prefix, and yield each complete value as a separate interpretation of the grammar.</span><span class="sxs-lookup"><span data-stu-id="09a83-163">Given a user query prefix, `attrref` will match all values in the index that complete the prefix, and yield each complete value as a separate interpretation of the grammar.</span></span>  

<span data-ttu-id="09a83-164">Examples:</span><span class="sxs-lookup"><span data-stu-id="09a83-164">Examples:</span></span>
* <span data-ttu-id="09a83-165">Matching `<attrref uri="academic#Keyword" name="keyword"/>` against the query prefix "dat" generates one interpretation for papers about "database", one interpretation for papers about "data mining", etc.</span><span class="sxs-lookup"><span data-stu-id="09a83-165">Matching `<attrref uri="academic#Keyword" name="keyword"/>` against the query prefix "dat" generates one interpretation for papers about "database", one interpretation for papers about "data mining", etc.</span></span>
* <span data-ttu-id="09a83-166">Matching `<attrref uri="academic#Year" name="year"/>` against the query prefix "200" generates one interpretation for papers in "2000", one interpretation for papers in "2001", etc.</span><span class="sxs-lookup"><span data-stu-id="09a83-166">Matching `<attrref uri="academic#Year" name="year"/>` against the query prefix "200" generates one interpretation for papers in "2000", one interpretation for papers in "2001", etc.</span></span>

#### <a name="matching-operations"></a><span data-ttu-id="09a83-167">Matching Operations</span><span class="sxs-lookup"><span data-stu-id="09a83-167">Matching Operations</span></span>
<span data-ttu-id="09a83-168">In addition to exact match, select attribute types also support prefix and inequality matches via the optional `op` attribute.</span><span class="sxs-lookup"><span data-stu-id="09a83-168">In addition to exact match, select attribute types also support prefix and inequality matches via the optional `op` attribute.</span></span>  <span data-ttu-id="09a83-169">If no object in the index has a value that matches, the grammar path is blocked and the service will not generate any interpretations traversing over this grammar path.</span><span class="sxs-lookup"><span data-stu-id="09a83-169">If no object in the index has a value that matches, the grammar path is blocked and the service will not generate any interpretations traversing over this grammar path.</span></span>   <span data-ttu-id="09a83-170">The `op` attribute defaults to "eq".</span><span class="sxs-lookup"><span data-stu-id="09a83-170">The `op` attribute defaults to "eq".</span></span>

```xml
in <attrref uri="academic#Year" name="year"/>
before <attrref uri="academic#Year" op="lt" name="year"/
```

<span data-ttu-id="09a83-171">The following table lists the supported `op` values for each attribute type.</span><span class="sxs-lookup"><span data-stu-id="09a83-171">The following table lists the supported `op` values for each attribute type.</span></span>  <span data-ttu-id="09a83-172">Their use requires the corresponding index operation to be included in the schema attribute definition.</span><span class="sxs-lookup"><span data-stu-id="09a83-172">Their use requires the corresponding index operation to be included in the schema attribute definition.</span></span>

| <span data-ttu-id="09a83-173">Attribute Type</span><span class="sxs-lookup"><span data-stu-id="09a83-173">Attribute Type</span></span> | <span data-ttu-id="09a83-174">Op Value</span><span class="sxs-lookup"><span data-stu-id="09a83-174">Op Value</span></span> | <span data-ttu-id="09a83-175">Description</span><span class="sxs-lookup"><span data-stu-id="09a83-175">Description</span></span> | <span data-ttu-id="09a83-176">Index Operation</span><span class="sxs-lookup"><span data-stu-id="09a83-176">Index Operation</span></span>
|----|----|----|----|
| <span data-ttu-id="09a83-177">String</span><span class="sxs-lookup"><span data-stu-id="09a83-177">String</span></span> | <span data-ttu-id="09a83-178">eq</span><span class="sxs-lookup"><span data-stu-id="09a83-178">eq</span></span> | <span data-ttu-id="09a83-179">String exact match</span><span class="sxs-lookup"><span data-stu-id="09a83-179">String exact match</span></span> | <span data-ttu-id="09a83-180">equals</span><span class="sxs-lookup"><span data-stu-id="09a83-180">equals</span></span> |
| <span data-ttu-id="09a83-181">String</span><span class="sxs-lookup"><span data-stu-id="09a83-181">String</span></span> | <span data-ttu-id="09a83-182">starts_with</span><span class="sxs-lookup"><span data-stu-id="09a83-182">starts_with</span></span> | <span data-ttu-id="09a83-183">String prefix match</span><span class="sxs-lookup"><span data-stu-id="09a83-183">String prefix match</span></span> | <span data-ttu-id="09a83-184">starts_with</span><span class="sxs-lookup"><span data-stu-id="09a83-184">starts_with</span></span> |
| <span data-ttu-id="09a83-185">Int32, Int64, Double</span><span class="sxs-lookup"><span data-stu-id="09a83-185">Int32, Int64, Double</span></span> | <span data-ttu-id="09a83-186">eq</span><span class="sxs-lookup"><span data-stu-id="09a83-186">eq</span></span> |  <span data-ttu-id="09a83-187">Numeric equality match</span><span class="sxs-lookup"><span data-stu-id="09a83-187">Numeric equality match</span></span> | <span data-ttu-id="09a83-188">equals</span><span class="sxs-lookup"><span data-stu-id="09a83-188">equals</span></span> |
| <span data-ttu-id="09a83-189">Int32, Int64, Double</span><span class="sxs-lookup"><span data-stu-id="09a83-189">Int32, Int64, Double</span></span> | <span data-ttu-id="09a83-190">lt, le, gt, ge</span><span class="sxs-lookup"><span data-stu-id="09a83-190">lt, le, gt, ge</span></span> | <span data-ttu-id="09a83-191">Numeric inequality match (<, <=, >, >=)</span><span class="sxs-lookup"><span data-stu-id="09a83-191">Numeric inequality match (<, <=, >, >=)</span></span> | <span data-ttu-id="09a83-192">is_between</span><span class="sxs-lookup"><span data-stu-id="09a83-192">is_between</span></span> |
| <span data-ttu-id="09a83-193">Int32, Int64, Double</span><span class="sxs-lookup"><span data-stu-id="09a83-193">Int32, Int64, Double</span></span> | <span data-ttu-id="09a83-194">starts_with</span><span class="sxs-lookup"><span data-stu-id="09a83-194">starts_with</span></span> | <span data-ttu-id="09a83-195">Prefix match of value in decimal notation</span><span class="sxs-lookup"><span data-stu-id="09a83-195">Prefix match of value in decimal notation</span></span> | <span data-ttu-id="09a83-196">starts_with</span><span class="sxs-lookup"><span data-stu-id="09a83-196">starts_with</span></span> |

<span data-ttu-id="09a83-197">Examples:</span><span class="sxs-lookup"><span data-stu-id="09a83-197">Examples:</span></span>
* <span data-ttu-id="09a83-198">`<attrref uri="academic#Year" op="lt" name="year"/>` matches the input string "2000" and returns all papers published before the year 2000, exclusively.</span><span class="sxs-lookup"><span data-stu-id="09a83-198">`<attrref uri="academic#Year" op="lt" name="year"/>` matches the input string "2000" and returns all papers published before the year 2000, exclusively.</span></span>
* <span data-ttu-id="09a83-199">`<attrref uri="academic#Year" op="lt" name="year"/>` does not match the input string "20" because there are no papers in the index published before the year 20.</span><span class="sxs-lookup"><span data-stu-id="09a83-199">`<attrref uri="academic#Year" op="lt" name="year"/>` does not match the input string "20" because there are no papers in the index published before the year 20.</span></span>
* <span data-ttu-id="09a83-200">`<attrref uri="academic#Keyword" op="starts_with" name="keyword"/>` matches the input string "dat" and returns in a single interpretation papers about "database", "data mining", etc.  This is a rare use case.</span><span class="sxs-lookup"><span data-stu-id="09a83-200">`<attrref uri="academic#Keyword" op="starts_with" name="keyword"/>` matches the input string "dat" and returns in a single interpretation papers about "database", "data mining", etc.  This is a rare use case.</span></span>
* <span data-ttu-id="09a83-201">`<attrref uri="academic#Year" op="starts_with" name="year"/>` matches the input string "20" and returns in a single interpretation papers published in 200-299, 2000-2999, etc.  This is a rare use case.</span><span class="sxs-lookup"><span data-stu-id="09a83-201">`<attrref uri="academic#Year" op="starts_with" name="year"/>` matches the input string "20" and returns in a single interpretation papers published in 200-299, 2000-2999, etc.  This is a rare use case.</span></span>

### <a name="tag-element"></a><span data-ttu-id="09a83-202">tag Element</span><span class="sxs-lookup"><span data-stu-id="09a83-202">tag Element</span></span>
<span data-ttu-id="09a83-203">The `tag` element specifies how a path through the grammar is to be interpreted.</span><span class="sxs-lookup"><span data-stu-id="09a83-203">The `tag` element specifies how a path through the grammar is to be interpreted.</span></span>  <span data-ttu-id="09a83-204">It contains a sequence of semicolon-terminated statements.</span><span class="sxs-lookup"><span data-stu-id="09a83-204">It contains a sequence of semicolon-terminated statements.</span></span>  <span data-ttu-id="09a83-205">A statement may be an assignment of a literal or a variable to another variable.</span><span class="sxs-lookup"><span data-stu-id="09a83-205">A statement may be an assignment of a literal or a variable to another variable.</span></span>  <span data-ttu-id="09a83-206">It may also assign the output of a function with 0 or more parameters to a variable.</span><span class="sxs-lookup"><span data-stu-id="09a83-206">It may also assign the output of a function with 0 or more parameters to a variable.</span></span>  <span data-ttu-id="09a83-207">Each function parameter may be specified using a literal or a variable.</span><span class="sxs-lookup"><span data-stu-id="09a83-207">Each function parameter may be specified using a literal or a variable.</span></span>  <span data-ttu-id="09a83-208">If the function does not return any output, the assignment is omitted.</span><span class="sxs-lookup"><span data-stu-id="09a83-208">If the function does not return any output, the assignment is omitted.</span></span>  <span data-ttu-id="09a83-209">Variable scope is local to the containing rule.</span><span class="sxs-lookup"><span data-stu-id="09a83-209">Variable scope is local to the containing rule.</span></span>

```xml
<tag>x = 1; y = x;</tag>
<tag>q = All(); q = And(q, q2);</tag>
<tag>AssertEquals(x, 1);</tag>
```

<span data-ttu-id="09a83-210">Each `rule` in the grammar has a predefined variable named "out", representing the semantic output of the rule.</span><span class="sxs-lookup"><span data-stu-id="09a83-210">Each `rule` in the grammar has a predefined variable named "out", representing the semantic output of the rule.</span></span>  <span data-ttu-id="09a83-211">Its value is computed by evaluating each of the semantic statements traversed by the path through the `rule` matching the user query input.</span><span class="sxs-lookup"><span data-stu-id="09a83-211">Its value is computed by evaluating each of the semantic statements traversed by the path through the `rule` matching the user query input.</span></span>  <span data-ttu-id="09a83-212">The value assigned to the "out" variable at the end of the evaluation is the semantic output of the rule.</span><span class="sxs-lookup"><span data-stu-id="09a83-212">The value assigned to the "out" variable at the end of the evaluation is the semantic output of the rule.</span></span>  <span data-ttu-id="09a83-213">The semantic output of interpreting a user query against the grammar is the semantic output of the root rule.</span><span class="sxs-lookup"><span data-stu-id="09a83-213">The semantic output of interpreting a user query against the grammar is the semantic output of the root rule.</span></span>

<span data-ttu-id="09a83-214">Some statements may alter the probability of an interpretation path by introducing an additive log probability offset.</span><span class="sxs-lookup"><span data-stu-id="09a83-214">Some statements may alter the probability of an interpretation path by introducing an additive log probability offset.</span></span>  <span data-ttu-id="09a83-215">Some statements may reject the interpretation altogether if specified conditions are not satisfied.</span><span class="sxs-lookup"><span data-stu-id="09a83-215">Some statements may reject the interpretation altogether if specified conditions are not satisfied.</span></span>

<span data-ttu-id="09a83-216">For a list of supported semantic functions, see [Semantic Functions](SemanticInterpretation.md#semantic-functions).</span><span class="sxs-lookup"><span data-stu-id="09a83-216">For a list of supported semantic functions, see [Semantic Functions](SemanticInterpretation.md#semantic-functions).</span></span>

## <a name="interpretation-probability"></a><span data-ttu-id="09a83-217">Interpretation Probability</span><span class="sxs-lookup"><span data-stu-id="09a83-217">Interpretation Probability</span></span>
<span data-ttu-id="09a83-218">The probability of an interpretation path through the grammar is the cumulative log probability of all the `<item>` elements and semantic functions encountered along the way.</span><span class="sxs-lookup"><span data-stu-id="09a83-218">The probability of an interpretation path through the grammar is the cumulative log probability of all the `<item>` elements and semantic functions encountered along the way.</span></span>  <span data-ttu-id="09a83-219">It describes the relative likelihood of matching a particular input sequence.</span><span class="sxs-lookup"><span data-stu-id="09a83-219">It describes the relative likelihood of matching a particular input sequence.</span></span>

<span data-ttu-id="09a83-220">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the natural log function.</span><span class="sxs-lookup"><span data-stu-id="09a83-220">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the natural log function.</span></span>  <span data-ttu-id="09a83-221">Using log probabilities allows the system to accumulate the joint probability of an interpretation path through simple addition.</span><span class="sxs-lookup"><span data-stu-id="09a83-221">Using log probabilities allows the system to accumulate the joint probability of an interpretation path through simple addition.</span></span>  <span data-ttu-id="09a83-222">It also avoids floating-point underflow common to such joint probability calculations.</span><span class="sxs-lookup"><span data-stu-id="09a83-222">It also avoids floating-point underflow common to such joint probability calculations.</span></span>  <span data-ttu-id="09a83-223">Note that by design, the log probability is always a negative floating-point value or 0, where larger values indicate higher likelihood.</span><span class="sxs-lookup"><span data-stu-id="09a83-223">Note that by design, the log probability is always a negative floating-point value or 0, where larger values indicate higher likelihood.</span></span>

<a name="example"></a>
## <a name="example"></a><span data-ttu-id="09a83-224">Example</span><span class="sxs-lookup"><span data-stu-id="09a83-224">Example</span></span>
<span data-ttu-id="09a83-225">The following is an example XML from the academic publications domain that demonstrates the various elements of a grammar:</span><span class="sxs-lookup"><span data-stu-id="09a83-225">The following is an example XML from the academic publications domain that demonstrates the various elements of a grammar:</span></span>

```xml
<grammar root="GetPapers">

  <!-- Import academic data schema-->
  <import schema="academic.schema" name="academic"/>
  
  <!-- Define root rule-->
  <rule id="GetPapers">
    <example>papers about machine learning by michael jordan</example>
    
    papers
    <tag>
      yearOnce = false;
      isBeyondEndOfQuery = false;
      query = All();
    </tag>
  
    <item repeat="1-" repeat-logprob="-10">
      <!-- Do not complete additional attributes beyond end of query -->
      <tag>AssertEquals(isBeyondEndOfQuery, false);</tag>
        
      <one-of>
        <!-- about <keyword> -->
        <item logprob="-0.5">
          about <attrref uri="academic#Keyword" name="keyword"/>
          <tag>query = And(query, keyword);</tag>
        </item>
        
        <!-- by <authorName> [while at <authorAffiliation>] -->
        <item logprob="-1">
          by <attrref uri="academic#Author.Name" name="authorName"/>
          <tag>authorQuery = authorName;</tag>
          <item repeat="0-1" repeat-logprob="-1.5">
            while at <attrref uri="academic#Author.Affiliation" name="authorAffiliation"/>
            <tag>authorQuery = And(authorQuery, authorAffiliation);</tag>
          </item>
          <tag>
            authorQuery = Composite(authorQuery);
            query = And(query, authorQuery);
          </tag>
        </item>
        
        <!-- written (in|before|after) <year> -->
        <item logprob="-1.5">
          <!-- Allow this grammar path to be traversed only once -->
          <tag>
            AssertEquals(yearOnce, false);
            yearOnce = true;
          </tag>
          <ruleref uri="#GetPaperYear" name="year"/>
          <tag>query = And(query, year);</tag>
        </item>
      </one-of>

      <!-- Determine if current parse position is beyond end of query -->
      <tag>isBeyondEndOfQuery = GetVariable("IsBeyondEndOfQuery", "system");</tag>
    </item>
    <tag>out = query;</tag>
  </rule>
  
  <rule id="GetPaperYear">
    <tag>year = All();</tag>
    written
    <one-of>
      <item>
        in <attrref uri="academic#Year" name="year"/>
      </item>
      <item>
        before
        <one-of>
          <item>[year]</item>
          <item><attrref uri="academic#Year" op="lt" name="year"/></item>
        </one-of>
      </item>
      <item>
        after
        <one-of>
          <item>[year]</item>
          <item><attrref uri="academic#Year" op="gt" name="year"/></item>
        </one-of>
      </item>
    </one-of>
    <tag>out = year;</tag>
  </rule>
</grammar>
```
