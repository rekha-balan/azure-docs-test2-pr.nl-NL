---
title: Structured query expressions in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use structured query expressions in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.component: knowledge-exploration
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 070ee311a1153bc9fb59870dce68f385a43b15f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803772"
---
# <a name="structured-query-expression"></a><span data-ttu-id="fb39f-103">Structured Query Expression</span><span class="sxs-lookup"><span data-stu-id="fb39f-103">Structured Query Expression</span></span>
<span data-ttu-id="fb39f-104">A structured query expression specifies a set of operations to evaluate against the data index.</span><span class="sxs-lookup"><span data-stu-id="fb39f-104">A structured query expression specifies a set of operations to evaluate against the data index.</span></span>  <span data-ttu-id="fb39f-105">It consists of attribute query expressions and higher-level functions.</span><span class="sxs-lookup"><span data-stu-id="fb39f-105">It consists of attribute query expressions and higher-level functions.</span></span>  <span data-ttu-id="fb39f-106">Use the [*evaluate*](evaluateMethod.md) method to compute the objects matching the expression.</span><span class="sxs-lookup"><span data-stu-id="fb39f-106">Use the [*evaluate*](evaluateMethod.md) method to compute the objects matching the expression.</span></span>  <span data-ttu-id="fb39f-107">The following is an example from the academic publications domain that returns publications authored by Jaime Teevan since the year 2013.</span><span class="sxs-lookup"><span data-stu-id="fb39f-107">The following is an example from the academic publications domain that returns publications authored by Jaime Teevan since the year 2013.</span></span>

`And(Composite(Author.Name=='jaime teevan'),Y>=2013)`

<span data-ttu-id="fb39f-108">Structured query expressions may be obtained from [*interpret*](interpretMethod.md) requests, where the semantic output of each interpretation is a structured query expression that returns the index objects matching the input natural language query.</span><span class="sxs-lookup"><span data-stu-id="fb39f-108">Structured query expressions may be obtained from [*interpret*](interpretMethod.md) requests, where the semantic output of each interpretation is a structured query expression that returns the index objects matching the input natural language query.</span></span>  <span data-ttu-id="fb39f-109">Alternatively, they may be manually authored using the syntax described in this section.</span><span class="sxs-lookup"><span data-stu-id="fb39f-109">Alternatively, they may be manually authored using the syntax described in this section.</span></span>

## <a name="attribute-query-expression"></a><span data-ttu-id="fb39f-110">Attribute Query Expression</span><span class="sxs-lookup"><span data-stu-id="fb39f-110">Attribute Query Expression</span></span>
<span data-ttu-id="fb39f-111">An attribute query expression identifies a set of objects based on matching against a specific attribute.</span><span class="sxs-lookup"><span data-stu-id="fb39f-111">An attribute query expression identifies a set of objects based on matching against a specific attribute.</span></span>  <span data-ttu-id="fb39f-112">Different matching operations are supported depending on the attribute type and indexed operation specified in the [schema](SchemaFormat.md):</span><span class="sxs-lookup"><span data-stu-id="fb39f-112">Different matching operations are supported depending on the attribute type and indexed operation specified in the [schema](SchemaFormat.md):</span></span>

| <span data-ttu-id="fb39f-113">Type</span><span class="sxs-lookup"><span data-stu-id="fb39f-113">Type</span></span> | <span data-ttu-id="fb39f-114">Operation</span><span class="sxs-lookup"><span data-stu-id="fb39f-114">Operation</span></span> | <span data-ttu-id="fb39f-115">Examples</span><span class="sxs-lookup"><span data-stu-id="fb39f-115">Examples</span></span> |
|------|-------------|------------|
| <span data-ttu-id="fb39f-116">String</span><span class="sxs-lookup"><span data-stu-id="fb39f-116">String</span></span> | <span data-ttu-id="fb39f-117">equals</span><span class="sxs-lookup"><span data-stu-id="fb39f-117">equals</span></span> | <span data-ttu-id="fb39f-118">Title='latent semantic analysis'  (canonical + synonyms)</span><span class="sxs-lookup"><span data-stu-id="fb39f-118">Title='latent semantic analysis'  (canonical + synonyms)</span></span> |
| <span data-ttu-id="fb39f-119">String</span><span class="sxs-lookup"><span data-stu-id="fb39f-119">String</span></span> | <span data-ttu-id="fb39f-120">equals</span><span class="sxs-lookup"><span data-stu-id="fb39f-120">equals</span></span> | <span data-ttu-id="fb39f-121">Author.Name=='susan t dumais'  (canonical only)</span><span class="sxs-lookup"><span data-stu-id="fb39f-121">Author.Name=='susan t dumais'  (canonical only)</span></span>|
| <span data-ttu-id="fb39f-122">String</span><span class="sxs-lookup"><span data-stu-id="fb39f-122">String</span></span> | <span data-ttu-id="fb39f-123">starts_with</span><span class="sxs-lookup"><span data-stu-id="fb39f-123">starts_with</span></span> | <span data-ttu-id="fb39f-124">Title='latent s'...</span><span class="sxs-lookup"><span data-stu-id="fb39f-124">Title='latent s'...</span></span> |
| <span data-ttu-id="fb39f-125">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="fb39f-125">Int32/Int64/Double</span></span> | <span data-ttu-id="fb39f-126">equals</span><span class="sxs-lookup"><span data-stu-id="fb39f-126">equals</span></span> | <span data-ttu-id="fb39f-127">Year=2000</span><span class="sxs-lookup"><span data-stu-id="fb39f-127">Year=2000</span></span> |
| <span data-ttu-id="fb39f-128">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="fb39f-128">Int32/Int64/Double</span></span> | <span data-ttu-id="fb39f-129">starts_with</span><span class="sxs-lookup"><span data-stu-id="fb39f-129">starts_with</span></span> | <span data-ttu-id="fb39f-130">Year='20'... (any decimal value starting with "20")</span><span class="sxs-lookup"><span data-stu-id="fb39f-130">Year='20'... (any decimal value starting with "20")</span></span> |
| <span data-ttu-id="fb39f-131">Int32/Int64/Double</span><span class="sxs-lookup"><span data-stu-id="fb39f-131">Int32/Int64/Double</span></span> | <span data-ttu-id="fb39f-132">is_between</span><span class="sxs-lookup"><span data-stu-id="fb39f-132">is_between</span></span> | <span data-ttu-id="fb39f-133">Year&lt;2000</span><span class="sxs-lookup"><span data-stu-id="fb39f-133">Year&lt;2000</span></span> <br/> <span data-ttu-id="fb39f-134">Year&lt;=2000</span><span class="sxs-lookup"><span data-stu-id="fb39f-134">Year&lt;=2000</span></span> <br/> <span data-ttu-id="fb39f-135">Year&gt;2000</span><span class="sxs-lookup"><span data-stu-id="fb39f-135">Year&gt;2000</span></span> <br/> <span data-ttu-id="fb39f-136">Year&gt;=2000</span><span class="sxs-lookup"><span data-stu-id="fb39f-136">Year&gt;=2000</span></span> <br/> <span data-ttu-id="fb39f-137">Year=[2010,2012) *(includes only left boundary value: 2010, 2011)*</span><span class="sxs-lookup"><span data-stu-id="fb39f-137">Year=[2010,2012) *(includes only left boundary value: 2010, 2011)*</span></span> <br/> <span data-ttu-id="fb39f-138">Year=[2000,2012] *(includes both boundary values: 2010, 2011, 2012)*</span><span class="sxs-lookup"><span data-stu-id="fb39f-138">Year=[2000,2012] *(includes both boundary values: 2010, 2011, 2012)*</span></span> |
| <span data-ttu-id="fb39f-139">Date</span><span class="sxs-lookup"><span data-stu-id="fb39f-139">Date</span></span> | <span data-ttu-id="fb39f-140">equals</span><span class="sxs-lookup"><span data-stu-id="fb39f-140">equals</span></span> | <span data-ttu-id="fb39f-141">BirthDate='1984-05-14'</span><span class="sxs-lookup"><span data-stu-id="fb39f-141">BirthDate='1984-05-14'</span></span> |
| <span data-ttu-id="fb39f-142">Date</span><span class="sxs-lookup"><span data-stu-id="fb39f-142">Date</span></span> | <span data-ttu-id="fb39f-143">is_between</span><span class="sxs-lookup"><span data-stu-id="fb39f-143">is_between</span></span> | <span data-ttu-id="fb39f-144">BirthDate&lt;='2008/03/14'</span><span class="sxs-lookup"><span data-stu-id="fb39f-144">BirthDate&lt;='2008/03/14'</span></span> <br/> <span data-ttu-id="fb39f-145">PublishDate=['2000-01-01','2009-12-31']</span><span class="sxs-lookup"><span data-stu-id="fb39f-145">PublishDate=['2000-01-01','2009-12-31']</span></span> |
| <span data-ttu-id="fb39f-146">Guid</span><span class="sxs-lookup"><span data-stu-id="fb39f-146">Guid</span></span> | <span data-ttu-id="fb39f-147">equals</span><span class="sxs-lookup"><span data-stu-id="fb39f-147">equals</span></span> | <span data-ttu-id="fb39f-148">Id='602DD052-CC47-4B23-A16A-26B52D30C05B'</span><span class="sxs-lookup"><span data-stu-id="fb39f-148">Id='602DD052-CC47-4B23-A16A-26B52D30C05B'</span></span> |


<span data-ttu-id="fb39f-149">For example, the expression "Title='latent s'..." matches all academic publications whose title starts with the string "latent s".</span><span class="sxs-lookup"><span data-stu-id="fb39f-149">For example, the expression "Title='latent s'..." matches all academic publications whose title starts with the string "latent s".</span></span>  <span data-ttu-id="fb39f-150">In order to evaluate this expression, the attribute Title must specify the "starts_with" operation in the schema used to build the index.</span><span class="sxs-lookup"><span data-stu-id="fb39f-150">In order to evaluate this expression, the attribute Title must specify the "starts_with" operation in the schema used to build the index.</span></span>

<span data-ttu-id="fb39f-151">For attributes with associated synonyms, a query expression may specify objects whose canonical value matches a given string using the "==" operator, or objects where any of its canonical/synonym values match using the "=" operator.</span><span class="sxs-lookup"><span data-stu-id="fb39f-151">For attributes with associated synonyms, a query expression may specify objects whose canonical value matches a given string using the "==" operator, or objects where any of its canonical/synonym values match using the "=" operator.</span></span>  <span data-ttu-id="fb39f-152">Both require the "equals" operator to be specified in the attribute definition.</span><span class="sxs-lookup"><span data-stu-id="fb39f-152">Both require the "equals" operator to be specified in the attribute definition.</span></span>


## <a name="functions"></a><span data-ttu-id="fb39f-153">Functions</span><span class="sxs-lookup"><span data-stu-id="fb39f-153">Functions</span></span>
<span data-ttu-id="fb39f-154">There is a built-in set of functions allowing the construction of more sophisticated query expressions from basic attribute queries.</span><span class="sxs-lookup"><span data-stu-id="fb39f-154">There is a built-in set of functions allowing the construction of more sophisticated query expressions from basic attribute queries.</span></span>

### <a name="and-function"></a><span data-ttu-id="fb39f-155">And Function</span><span class="sxs-lookup"><span data-stu-id="fb39f-155">And Function</span></span>
`And(expr1, expr2)`

<span data-ttu-id="fb39f-156">Returns the intersection of the two input query expressions.</span><span class="sxs-lookup"><span data-stu-id="fb39f-156">Returns the intersection of the two input query expressions.</span></span>

<span data-ttu-id="fb39f-157">The following example returns academic publications published in the year 2000 about information retrieval:</span><span class="sxs-lookup"><span data-stu-id="fb39f-157">The following example returns academic publications published in the year 2000 about information retrieval:</span></span>

`And(Year=2000, Keyword=='information retrieval')`

### <a name="or-function"></a><span data-ttu-id="fb39f-158">Or Function</span><span class="sxs-lookup"><span data-stu-id="fb39f-158">Or Function</span></span>
`Or(expr1, expr2)`

<span data-ttu-id="fb39f-159">Returns the union of the two input query expressions.</span><span class="sxs-lookup"><span data-stu-id="fb39f-159">Returns the union of the two input query expressions.</span></span>

<span data-ttu-id="fb39f-160">The following example returns academic publications published in the year 2000 about information retrieval or user modeling:</span><span class="sxs-lookup"><span data-stu-id="fb39f-160">The following example returns academic publications published in the year 2000 about information retrieval or user modeling:</span></span>

`And(Year=2000, Or(Keyword='information retrieval', Keyword='user modeling'))`

### <a name="composite-function"></a><span data-ttu-id="fb39f-161">Composite Function</span><span class="sxs-lookup"><span data-stu-id="fb39f-161">Composite Function</span></span>
`Composite(expr)`

<span data-ttu-id="fb39f-162">Returns an expression that encapsulates an inner expression composed of queries against sub-attributes of a common composite attribute.</span><span class="sxs-lookup"><span data-stu-id="fb39f-162">Returns an expression that encapsulates an inner expression composed of queries against sub-attributes of a common composite attribute.</span></span>  <span data-ttu-id="fb39f-163">The encapsulation requires the composite attribute of any matching data object to have at least one value that individually satisfies the inner expression.</span><span class="sxs-lookup"><span data-stu-id="fb39f-163">The encapsulation requires the composite attribute of any matching data object to have at least one value that individually satisfies the inner expression.</span></span>  <span data-ttu-id="fb39f-164">Note that a query expression on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other query expressions.</span><span class="sxs-lookup"><span data-stu-id="fb39f-164">Note that a query expression on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other query expressions.</span></span>

<span data-ttu-id="fb39f-165">For example, the following expression returns academic publications by "harry shum" while he was at "microsoft":</span><span class="sxs-lookup"><span data-stu-id="fb39f-165">For example, the following expression returns academic publications by "harry shum" while he was at "microsoft":</span></span>

```
Composite(And(Author.Name="harry shum", 
              Author.Affiliation="microsoft"))
```

<span data-ttu-id="fb39f-166">On the other hand, the following expression returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span><span class="sxs-lookup"><span data-stu-id="fb39f-166">On the other hand, the following expression returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":</span></span>

```
And(Composite(Author.Name="harry shum"), 
    Composite(Author.Affiliation="microsoft"))
```
