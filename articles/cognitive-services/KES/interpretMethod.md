---
title: Interpret method in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use the Interpret method in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: cd4fe6da5f865aa5e04fbeefeaf8504840941d18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670346"
---
# <a name="interpret-method"></a><span data-ttu-id="80d97-103">interpret Method</span><span class="sxs-lookup"><span data-stu-id="80d97-103">interpret Method</span></span>
<span data-ttu-id="80d97-104">The *interpret* method takes a natural language query string and returns formatted interpretations of user intent based on the grammar and index data.</span><span class="sxs-lookup"><span data-stu-id="80d97-104">The *interpret* method takes a natural language query string and returns formatted interpretations of user intent based on the grammar and index data.</span></span>  <span data-ttu-id="80d97-105">To provide an interactive search experience, this method may be called as each character is entered by the user with the *complete* parameter set to 1 to enable auto-complete suggestions.</span><span class="sxs-lookup"><span data-stu-id="80d97-105">To provide an interactive search experience, this method may be called as each character is entered by the user with the *complete* parameter set to 1 to enable auto-complete suggestions.</span></span>

## <a name="request"></a><span data-ttu-id="80d97-106">Request</span><span class="sxs-lookup"><span data-stu-id="80d97-106">Request</span></span>
`http://<host>/interpret?query=<query>[&<options>]`

<span data-ttu-id="80d97-107">Name</span><span class="sxs-lookup"><span data-stu-id="80d97-107">Name</span></span>|<span data-ttu-id="80d97-108">Value</span><span class="sxs-lookup"><span data-stu-id="80d97-108">Value</span></span>| <span data-ttu-id="80d97-109">Description</span><span class="sxs-lookup"><span data-stu-id="80d97-109">Description</span></span>
----|----|----
<span data-ttu-id="80d97-110">query</span><span class="sxs-lookup"><span data-stu-id="80d97-110">query</span></span>    | <span data-ttu-id="80d97-111">Text string</span><span class="sxs-lookup"><span data-stu-id="80d97-111">Text string</span></span> | <span data-ttu-id="80d97-112">Query entered by user.</span><span class="sxs-lookup"><span data-stu-id="80d97-112">Query entered by user.</span></span>  <span data-ttu-id="80d97-113">If complete is set to 1, query will be interpreted as a prefix for generating query auto-completion suggestions.</span><span class="sxs-lookup"><span data-stu-id="80d97-113">If complete is set to 1, query will be interpreted as a prefix for generating query auto-completion suggestions.</span></span>        
<span data-ttu-id="80d97-114">complete</span><span class="sxs-lookup"><span data-stu-id="80d97-114">complete</span></span> | <span data-ttu-id="80d97-115">0 (default) or 1</span><span class="sxs-lookup"><span data-stu-id="80d97-115">0 (default) or 1</span></span> | <span data-ttu-id="80d97-116">1 means that auto-completion suggestions are generated based on the grammar and index data.</span><span class="sxs-lookup"><span data-stu-id="80d97-116">1 means that auto-completion suggestions are generated based on the grammar and index data.</span></span>         
<span data-ttu-id="80d97-117">count</span><span class="sxs-lookup"><span data-stu-id="80d97-117">count</span></span>    | <span data-ttu-id="80d97-118">Number (default=10)</span><span class="sxs-lookup"><span data-stu-id="80d97-118">Number (default=10)</span></span> | <span data-ttu-id="80d97-119">Maximum number of interpretations to return.</span><span class="sxs-lookup"><span data-stu-id="80d97-119">Maximum number of interpretations to return.</span></span>         
<span data-ttu-id="80d97-120">offset</span><span class="sxs-lookup"><span data-stu-id="80d97-120">offset</span></span>   | <span data-ttu-id="80d97-121">Number (default=0)</span><span class="sxs-lookup"><span data-stu-id="80d97-121">Number (default=0)</span></span> | <span data-ttu-id="80d97-122">Index of the first interpretation to return.</span><span class="sxs-lookup"><span data-stu-id="80d97-122">Index of the first interpretation to return.</span></span>  <span data-ttu-id="80d97-123">For example, *count=2&offset=0* returns interpretations 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="80d97-123">For example, *count=2&offset=0* returns interpretations 0 and 1.</span></span> <span data-ttu-id="80d97-124">*count=2&offset=2* returns interpretations 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="80d97-124">*count=2&offset=2* returns interpretations 2 and 3.</span></span>       
<span data-ttu-id="80d97-125">timeout</span><span class="sxs-lookup"><span data-stu-id="80d97-125">timeout</span></span>  | <span data-ttu-id="80d97-126">Number (default=1000)</span><span class="sxs-lookup"><span data-stu-id="80d97-126">Number (default=1000)</span></span> | <span data-ttu-id="80d97-127">Timeout in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="80d97-127">Timeout in milliseconds.</span></span> <span data-ttu-id="80d97-128">Only interpretations found before the timeout has elapsed are returned.</span><span class="sxs-lookup"><span data-stu-id="80d97-128">Only interpretations found before the timeout has elapsed are returned.</span></span>

<span data-ttu-id="80d97-129">Using the *count* and *offset* parameters, a large number of results may be obtained incrementally over multiple requests.</span><span class="sxs-lookup"><span data-stu-id="80d97-129">Using the *count* and *offset* parameters, a large number of results may be obtained incrementally over multiple requests.</span></span>

## <a name="response-json"></a><span data-ttu-id="80d97-130">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="80d97-130">Response (JSON)</span></span>
<span data-ttu-id="80d97-131">JSONPath</span><span class="sxs-lookup"><span data-stu-id="80d97-131">JSONPath</span></span>     | <span data-ttu-id="80d97-132">Description</span><span class="sxs-lookup"><span data-stu-id="80d97-132">Description</span></span>
---------|---------
<span data-ttu-id="80d97-133">$.query</span><span class="sxs-lookup"><span data-stu-id="80d97-133">$.query</span></span> |<span data-ttu-id="80d97-134">*query* parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="80d97-134">*query* parameter from the request.</span></span>
<span data-ttu-id="80d97-135">$.interpretations</span><span class="sxs-lookup"><span data-stu-id="80d97-135">$.interpretations</span></span>   |<span data-ttu-id="80d97-136">Array of 0 or more ways to match the input query against the grammar.</span><span class="sxs-lookup"><span data-stu-id="80d97-136">Array of 0 or more ways to match the input query against the grammar.</span></span>
<span data-ttu-id="80d97-137">$.interpretations[\*].logprob</span><span class="sxs-lookup"><span data-stu-id="80d97-137">$.interpretations[\*].logprob</span></span>   |<span data-ttu-id="80d97-138">Relative log probability of the interpretation (<= 0).</span><span class="sxs-lookup"><span data-stu-id="80d97-138">Relative log probability of the interpretation (<= 0).</span></span>  <span data-ttu-id="80d97-139">Higher values are more likely.</span><span class="sxs-lookup"><span data-stu-id="80d97-139">Higher values are more likely.</span></span>
<span data-ttu-id="80d97-140">$.interpretations[\*].parse</span><span class="sxs-lookup"><span data-stu-id="80d97-140">$.interpretations[\*].parse</span></span> |<span data-ttu-id="80d97-141">XML string that shows how each part of the query was interpreted.</span><span class="sxs-lookup"><span data-stu-id="80d97-141">XML string that shows how each part of the query was interpreted.</span></span>
<span data-ttu-id="80d97-142">$.interpretations[\*].rules</span><span class="sxs-lookup"><span data-stu-id="80d97-142">$.interpretations[\*].rules</span></span> |<span data-ttu-id="80d97-143">Array of 1 or more rules defined in the grammar invoked during interpretation.</span><span class="sxs-lookup"><span data-stu-id="80d97-143">Array of 1 or more rules defined in the grammar invoked during interpretation.</span></span>
<span data-ttu-id="80d97-144">$.interpretations[\*].rules[\*].name</span><span class="sxs-lookup"><span data-stu-id="80d97-144">$.interpretations[\*].rules[\*].name</span></span>    |<span data-ttu-id="80d97-145">Name of the rule.</span><span class="sxs-lookup"><span data-stu-id="80d97-145">Name of the rule.</span></span>
<span data-ttu-id="80d97-146">$.interpretations[\*].rules[\*].output</span><span class="sxs-lookup"><span data-stu-id="80d97-146">$.interpretations[\*].rules[\*].output</span></span>  |<span data-ttu-id="80d97-147">Semantic output of the rule.</span><span class="sxs-lookup"><span data-stu-id="80d97-147">Semantic output of the rule.</span></span>
<span data-ttu-id="80d97-148">$.interpretations[\*].rules[\*].output.type</span><span class="sxs-lookup"><span data-stu-id="80d97-148">$.interpretations[\*].rules[\*].output.type</span></span> |<span data-ttu-id="80d97-149">Data type of the semantic output.</span><span class="sxs-lookup"><span data-stu-id="80d97-149">Data type of the semantic output.</span></span>
<span data-ttu-id="80d97-150">$.interpretations[\*].rules[\*].output.value</span><span class="sxs-lookup"><span data-stu-id="80d97-150">$.interpretations[\*].rules[\*].output.value</span></span>|<span data-ttu-id="80d97-151">Value of the semantic output.</span><span class="sxs-lookup"><span data-stu-id="80d97-151">Value of the semantic output.</span></span>  
<span data-ttu-id="80d97-152">$.aborted</span><span class="sxs-lookup"><span data-stu-id="80d97-152">$.aborted</span></span> | <span data-ttu-id="80d97-153">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="80d97-153">True if the request timed out.</span></span>

### <a name="parse-xml"></a><span data-ttu-id="80d97-154">Parse XML</span><span class="sxs-lookup"><span data-stu-id="80d97-154">Parse XML</span></span>
<span data-ttu-id="80d97-155">The parse XML annotates the (completed) query with information about how it matches against the rules in the grammar and attributes in the index.</span><span class="sxs-lookup"><span data-stu-id="80d97-155">The parse XML annotates the (completed) query with information about how it matches against the rules in the grammar and attributes in the index.</span></span>  <span data-ttu-id="80d97-156">Below is an example from the academic publications domain:</span><span class="sxs-lookup"><span data-stu-id="80d97-156">Below is an example from the academic publications domain:</span></span>

```xml
<rule name="#GetPapers">
  papers by 
  <attr name="academic#Author.Name" canonical="heungyeung shum">harry shum</attr>
  <rule name="#GetPaperYear">
    written in
    <attr name="academic#Year">2000</attr>
  </rule>
</rule>
```

<span data-ttu-id="80d97-157">The `<rule>` element delimits the range in the query matching the rule specified by its `name` attribute.</span><span class="sxs-lookup"><span data-stu-id="80d97-157">The `<rule>` element delimits the range in the query matching the rule specified by its `name` attribute.</span></span>  <span data-ttu-id="80d97-158">It may be nested when the parse involves rule references in the grammar.</span><span class="sxs-lookup"><span data-stu-id="80d97-158">It may be nested when the parse involves rule references in the grammar.</span></span>

<span data-ttu-id="80d97-159">The `<attr>` element delimits the range in the query matching the index attribute specified by its `name` attribute.</span><span class="sxs-lookup"><span data-stu-id="80d97-159">The `<attr>` element delimits the range in the query matching the index attribute specified by its `name` attribute.</span></span>  <span data-ttu-id="80d97-160">When the match involves a synonym in the input query, the `canonical` attribute will contain the canonical value matching the synonym from the index.</span><span class="sxs-lookup"><span data-stu-id="80d97-160">When the match involves a synonym in the input query, the `canonical` attribute will contain the canonical value matching the synonym from the index.</span></span>

## <a name="example"></a><span data-ttu-id="80d97-161">Example</span><span class="sxs-lookup"><span data-stu-id="80d97-161">Example</span></span>
<span data-ttu-id="80d97-162">In the academic publications example, the following request returns up to 2 auto-completion suggestions for the prefix query "papers by jaime":</span><span class="sxs-lookup"><span data-stu-id="80d97-162">In the academic publications example, the following request returns up to 2 auto-completion suggestions for the prefix query "papers by jaime":</span></span>

`http://<host>/interpret?query=papers by jaime&complete=1&count=2`

<span data-ttu-id="80d97-163">The response contains the top two ("count=2") most likely interpretations that complete the partial query "papers by jaime": "papers by jaime teevan" and "papers by jaime green".</span><span class="sxs-lookup"><span data-stu-id="80d97-163">The response contains the top two ("count=2") most likely interpretations that complete the partial query "papers by jaime": "papers by jaime teevan" and "papers by jaime green".</span></span>  <span data-ttu-id="80d97-164">The service generated query completions instead of considering only exact matches for the author "jaime" because the request specified "complete=1".</span><span class="sxs-lookup"><span data-stu-id="80d97-164">The service generated query completions instead of considering only exact matches for the author "jaime" because the request specified "complete=1".</span></span> <span data-ttu-id="80d97-165">Note that the canonical value "j l green" matched via the synonym "jamie green", as indicated in the parse.</span><span class="sxs-lookup"><span data-stu-id="80d97-165">Note that the canonical value "j l green" matched via the synonym "jamie green", as indicated in the parse.</span></span>


```json
{
  "query": "papers by jaime",
  "interpretations": [
    {
      "logprob": -5.615,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#Author.Name\">jaime teevan</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(Author.Name=='jaime teevan')"
          }
        }
      ]
    },
    {
      "logprob": -5.849,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#Author.Name\" canonical=\"j l green\">jaime green</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(Author.Name=='j l green')"
          }
        }
      ]
    }
  ]
}
```  

<span data-ttu-id="80d97-166">When the type of semantic output is "query", as in this example, the matching objects can be retrieved by passing *output.value* to the [*evaluate*](evaluateMethod.md) API via the *expr* parameter.</span><span class="sxs-lookup"><span data-stu-id="80d97-166">When the type of semantic output is "query", as in this example, the matching objects can be retrieved by passing *output.value* to the [*evaluate*](evaluateMethod.md) API via the *expr* parameter.</span></span>

`http://<host>/evaluate?expr=Composite(AA.AuN=='jaime teevan')`
  
