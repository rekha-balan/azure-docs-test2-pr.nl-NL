---
title: Structured query expressions in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use structured query expressions in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 952f7da608f6d2760ab91da005febb7495cef746
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564618"
---
# <a name="structured-query-expression"></a><span data-ttu-id="23e4b-103">Structured Query Expression</span><span class="sxs-lookup"><span data-stu-id="23e4b-103">Structured Query Expression</span></span>
<span data-ttu-id="23e4b-104">A structured query expression specifies a set of operations to evaluate against the data index.</span><span class="sxs-lookup"><span data-stu-id="23e4b-104">A structured query expression specifies a set of operations to evaluate against the data index.</span></span>  <span data-ttu-id="23e4b-105">It consists of attribute query expressions and higher-level functions.</span><span class="sxs-lookup"><span data-stu-id="23e4b-105">It consists of attribute query expressions and higher-level functions.</span></span>  <span data-ttu-id="23e4b-106">Use the [*evaluate*](evaluateMethod.md) method to compute the objects matching the expression.</span><span class="sxs-lookup"><span data-stu-id="23e4b-106">Use the [*evaluate*](evaluateMethod.md) method to compute the objects matching the expression.</span></span>  <span data-ttu-id="23e4b-107">The following is an example from the academic publications domain that returns publications authored by Jaime Teevan since the year 2013.</span><span class="sxs-lookup"><span data-stu-id="23e4b-107">The following is an example from the academic publications domain that returns publications authored by Jaime Teevan since the year 2013.</span></span>

`And(Composite(Author.Name=='jaime teevan'),Y>=2013)`

<span data-ttu-id="23e4b-108">Structured query expressions may be obtained from [*interpret*](interpretMethod.md) requests, where the semantic output of each interpretation is a structured query expression that returns the index objects matching the input natural language query.</span><span class="sxs-lookup"><span data-stu-id="23e4b-108">Structured query expressions may be obtained from [*interpret*](interpretMethod.md) requests, where the semantic output of each interpretation is a structured query expression that returns the index objects matching the input natural language query.</span></span>  <span data-ttu-id="23e4b-109">Alternatively, they may be manually authored using the syntax described in this section.</span><span class="sxs-lookup"><span data-stu-id="23e4b-109">Alternatively, they may be manually authored using the syntax described in this section.</span></span>

## <a name="attribute-query-expression"></a><span data-ttu-id="23e4b-110">Attribute Query Expression</span><span class="sxs-lookup"><span data-stu-id="23e4b-110">Attribute Query Expression</span></span>
<span data-ttu-id="23e4b-111">An attribute query expression identifies a set of objects based on matching against a specific attribute.</span><span class="sxs-lookup"><span data-stu-id="23e4b-111">An attribute query expression identifies a set of objects based on matching against a specific attribute.</span></span>  <span data-ttu-id="23e4b-112">Different matching operations are supported depending on the attribute type and indexed operation specified in the [schema](SchemaFormat.md):</span><span class="sxs-lookup"><span data-stu-id="23e4b-112">Different matching operations are supported depending on the attribute type and indexed operation specified in the [schema](SchemaFormat.md):</span></span>

| <span data-ttu-id="23e4b-113">Type</span><span class="sxs-lookup"><span data-stu-id="23e4b-113">Type</span></span> | <span data-ttu-id="23e4b-114">Operation</span><span class="sxs-lookup"><span data-stu-id="23e4b-114">Operation</span></span> | <span data-ttu-id="23e4b-115">Examples</span><span class="sxs-lookup"><span data-stu-id="23e4b-115">Examples</span></span> |
|------|-------------|------------|
| <span data-ttu-id="23e4b-116">String</span><span class="sxs-lookup"><span data-stu-id="23e4b-116">String</span></span> | <span data-ttu-id="23e4b-117">equals</span><span class="sxs-lookup"><span data-stu-id="23e4b-117">equals</span></span> | <span data-ttu-id="23e4b-118">Title='latent semantic analysis'  (canonical + synonyms)</span><span class="sxs-lookup"><span data-stu-id="23e4b-118">Title='latent semantic analysis'  (canonical + synonyms)</span></span> |
| <span data-ttu-id="23e4b-119">String</span><span class="sxs-lookup"><span data-stu-id="23e4b-119">String</span></span> | <span data-ttu-id="23e4b-120">equals</span><span class="sxs-lookup"><span data-stu-id="23e4b-120">equals</span></span> | <span data-ttu-id="23e4b-121">Author.Name=='susan t dumais'  (canonical only)</span><span class="sxs-lookup"><span data-stu-id="23e4b-121">Author.Name=='susan t dumais'  (canonical only)</span></span>|
| <span data-ttu-id="23e4b-122">String</span><span class="sxs-lookup"><span data-stu-id="23e4b-122">String</span></span> | <span data-ttu-id="23e4b-123">starts_with</span><span class="sxs-lookup"><span data-stu-id="23e4b-123">starts_with</span></span> | <span data-ttu-id="23e4b-124">Title='latent s'...</span><span class="sxs-lookup"><span data-stu-id="23e4b-124">Title='latent s'...</span></span> |
| <span data-ttu-id="23e4b-125">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="23e4b-125">Int32/Int64/Double</span></span> | <span data-ttu-id="23e4b-126">equals</span><span class="sxs-lookup"><span data-stu-id="23e4b-126">equals</span></span> | <span data-ttu-id="23e4b-127">Year=2000</span><span class="sxs-lookup"><span data-stu-id="23e4b-127">Year=2000</span></span> |
| <span data-ttu-id="23e4b-128">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="23e4b-128">Int32/Int64/Double</span></span> | <span data-ttu-id="23e4b-129">starts_with</span><span class="sxs-lookup"><span data-stu-id="23e4b-129">starts_with</span></span> | <span data-ttu-id="23e4b-130">Year='20'... (any decimal value starting with "20")</span><span class="sxs-lookup"><span data-stu-id="23e4b-130">Year='20'... (any decimal value starting with "20")</span></span> |
| <span data-ttu-id="23e4b-131">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="23e4b-131">Int32/Int64/Double</span></span> | <span data-ttu-id="23e4b-132">is_between</span><span class="sxs-lookup"><span data-stu-id="23e4b-132">is_between</span></span> | <span data-ttu-id="23e4b-133">Year&lt;2000</span><span class="sxs-lookup"><span data-stu-id="23e4b-133">Year&lt;2000</span></span> <br/> <span data-ttu-id="23e4b-134">Year&lt;=2000</span><span class="sxs-lookup"><span data-stu-id="23e4b-134">Year&lt;=2000</span></span> <br/> <span data-ttu-id="23e4b-135">Year&gt;2000</span><span class="sxs-lookup"><span data-stu-id="23e4b-135">Year&gt;2000</span></span> <br/> <span data-ttu-id="23e4b-136">Year&gt;=2000</span><span class="sxs-lookup"><span data-stu-id="23e4b-136">Year&gt;=2000</span></span> <br/> <span data-ttu-id="23e4b-137">Year=[2010,2012) *(includes only left boundary value: 2010, 2011)*</span><span class="sxs-lookup"><span data-stu-id="23e4b-137">Year=[2010,2012) *(includes only left boundary value: 2010, 2011)*</span></span> <br/> <span data-ttu-id="23e4b-138">Year=[2000,2012] *(includes both boundary values: 2010, 2011, 2012)*</span><span class="sxs-lookup"><span data-stu-id="23e4b-138">Year=[2000,2012] *(includes both boundary values: 2010, 2011, 2012)*</span></span> |
| <span data-ttu-id="23e4b-139">Date</span><span class="sxs-lookup"><span data-stu-id="23e4b-139">Date</span></span> | <span data-ttu-id="23e4b-140">equals</span><span class="sxs-lookup"><span data-stu-id="23e4b-140">equals</span></span> | <span data-ttu-id="23e4b-141">BirthDate='1984-05-14'</span><span class="sxs-lookup"><span data-stu-id="23e4b-141">BirthDate='1984-05-14'</span></span> |
| <span data-ttu-id="23e4b-142">Date</span><span class="sxs-lookup"><span data-stu-id="23e4b-142">Date</span></span> | <span data-ttu-id="23e4b-143">is_between</span><span class="sxs-lookup"><span data-stu-id="23e4b-143">is_between</span></span> | <span data-ttu-id="23e4b-144">BirthDate&lt;='2008/03/14'</span><span class="sxs-lookup"><span data-stu-id="23e4b-144">BirthDate&lt;='2008/03/14'</span></span> <br/> <span data-ttu-id="23e4b-145">PublishDate=['2000-01-01','2009-12-31']</span><span class="sxs-lookup"><span data-stu-id="23e4b-145">PublishDate=['2000-01-01','2009-12-31']</span></span> |
| <span data-ttu-id="23e4b-146">Guid</span><span class="sxs-lookup"><span data-stu-id="23e4b-146">Guid</span></span> | <span data-ttu-id="23e4b-147">equals</span><span class="sxs-lookup"><span data-stu-id="23e4b-147">equals</span></span> | <span data-ttu-id="23e4b-148">Id='602DD052-CC47-4B23-A16A-26B52D30C05B'</span><span class="sxs-lookup"><span data-stu-id="23e4b-148">Id='602DD052-CC47-4B23-A16A-26B52D30C05B'</span></span> |


<span data-ttu-id="23e4b-149">For example, the expression "Title='latent s'..." matches all academic publications whose title starts with the string "latent s".</span><span class="sxs-lookup"><span data-stu-id="23e4b-149">For example, the expression "Title='latent s'..." matches all academic publications whose title starts with the string "latent s".</span></span>  <span data-ttu-id="23e4b-150">In order to evaluate this expression, the attribute Title must specify the "starts_with" operation in the schema used to build the index.</span><span class="sxs-lookup"><span data-stu-id="23e4b-150">In order to evaluate this expression, the attribute Title must specify the "starts_with" operation in the schema used to build the index.</span></span>

<span data-ttu-id="23e4b-151">For attributes with associated synonyms, a query expression may specify objects whose canonical value matches a given string using the "==" operator, or objects where any of its canonical/synonym values match using the "=" operator.</span><span class="sxs-lookup"><span data-stu-id="23e4b-151">For attributes with associated synonyms, a query expression may specify objects whose canonical value matches a given string using the "==" operator, or objects where any of its canonical/synonym values match using the "=" operator.</span></span>  <span data-ttu-id="23e4b-152">Both require the "equals" operator to be specified in the attribute definition.</span><span class="sxs-lookup"><span data-stu-id="23e4b-152">Both require the "equals" operator to be specified in the attribute definition.</span></span>


## <a name="functions"></a><span data-ttu-id="23e4b-153">Functions</span><span class="sxs-lookup"><span data-stu-id="23e4b-153">Functions</span></span>
<span data-ttu-id="23e4b-154">There is a built-in set of functions allowing the construction of more sophisticated query expressions from basic attribute queries.</span><span class="sxs-lookup"><span data-stu-id="23e4b-154">There is a built-in set of functions allowing the construction of more sophisticated query expressions from basic attribute queries.</span></span>

### <a name="and-function"></a><span data-ttu-id="23e4b-155">And Function</span><span class="sxs-lookup"><span data-stu-id="23e4b-155">And Function</span></span>
`And(expr1, expr2)`

<span data-ttu-id="23e4b-156">Returns the intersection of the two input query expressions.</span><span class="sxs-lookup"><span data-stu-id="23e4b-156">Returns the intersection of the two input query expressions.</span></span>

<span data-ttu-id="23e4b-157">The following example returns academic publications published in the year 2000 about information retrieval:</span><span class="sxs-lookup"><span data-stu-id="23e4b-157">The following example returns academic publications published in the year 2000 about information retrieval:</span></span>

`And(Year=2000, Keyword=='information retrieval')`

### <a name="or-function"></a><span data-ttu-id="23e4b-158">Or Function</span><span class="sxs-lookup"><span data-stu-id="23e4b-158">Or Function</span></span>
`Or(expr1, expr2)`

<span data-ttu-id="23e4b-159">Returns the union of the two input query expressions.</span><span class="sxs-lookup"><span data-stu-id="23e4b-159">Returns the union of the two input query expressions.</span></span>

<span data-ttu-id="23e4b-160">The following example returns academic publications published in the year 2000 about information retrieval or user modeling:</span><span class="sxs-lookup"><span data-stu-id="23e4b-160">The following example returns academic publications published in the year 2000 about information retrieval or user modeling:</span></span>

`And(Year=2000, Or(Keyword='information retrieval', Keyword='user modeling'))`

### <a name="composite-function"></a><span data-ttu-id="23e4b-161">Composite Function</span><span class="sxs-lookup"><span data-stu-id="23e4b-161">Composite Function</span></span>
`Composite(expr)`

<span data-ttu-id="23e4b-162">Returns an expression that encapsulates an inner expression composed of queries against sub-attributes of a common composite attribute.</span><span class="sxs-lookup"><span data-stu-id="23e4b-162">Returns an expression that encapsulates an inner expression composed of queries against sub-attributes of a common composite attribute.</span></span>  <span data-ttu-id="23e4b-163">The encapsulation requires the composite attribute of any matching data object to have at least one value that individually satisfies the inner expression.</span><span class="sxs-lookup"><span data-stu-id="23e4b-163">The encapsulation requires the composite attribute of any matching data object to have at least one value that individually satisfies the inner expression.</span></span>  <span data-ttu-id="23e4b-164">Note that a query expression on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other query expressions.</span><span class="sxs-lookup"><span data-stu-id="23e4b-164">Note that a query expression on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other query expressions.</span></span>

<span data-ttu-id="23e4b-165">For example, the following expression returns academic publications by "harry shum" while he was at "microsoft":</span><span class="sxs-lookup"><span data-stu-id="23e4b-165">For example, the following expression returns academic publications by "harry shum" while he was at "microsoft":</span></span>

```
Composite(And(Author.Name="harry shum", 
              Author.Affiliation="microsoft"))
```

<span data-ttu-id="23e4b-166">On the other hand, the following expression returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span><span class="sxs-lookup"><span data-stu-id="23e4b-166">On the other hand, the following expression returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span></span>

```
And(Composite(Author.Name="harry shum"), 
    Composite(Author.Affiliation="microsoft"))
```
