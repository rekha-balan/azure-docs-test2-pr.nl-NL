---
title: Query expression syntax in the Academic Knowledge API | Microsoft Docs
description: Learn how to use query expression syntax in the Academic Knowledge API for Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: 839f68c035ed8992afe240cfe27ce4237e5228d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540981"
---
# <a name="query-expression-syntax"></a><span data-ttu-id="db7ec-103">Query Expression Syntax</span><span class="sxs-lookup"><span data-stu-id="db7ec-103">Query Expression Syntax</span></span>

<span data-ttu-id="db7ec-104">We have seen that the response to an **interpret** request includes a query expression.</span><span class="sxs-lookup"><span data-stu-id="db7ec-104">We have seen that the response to an **interpret** request includes a query expression.</span></span> <span data-ttu-id="db7ec-105">The grammar that interpreted the user’s query created a query expression for each interpretation.</span><span class="sxs-lookup"><span data-stu-id="db7ec-105">The grammar that interpreted the user’s query created a query expression for each interpretation.</span></span> <span data-ttu-id="db7ec-106">A query expression can then be used to issue an **evaluate** request to retrieve entity search results.</span><span class="sxs-lookup"><span data-stu-id="db7ec-106">A query expression can then be used to issue an **evaluate** request to retrieve entity search results.</span></span>

<span data-ttu-id="db7ec-107">You can also construct your own query expressions and use them in an **evaluate** request.</span><span class="sxs-lookup"><span data-stu-id="db7ec-107">You can also construct your own query expressions and use them in an **evaluate** request.</span></span> <span data-ttu-id="db7ec-108">This can be useful if you are building your own user interface which creates a query expression in response to the user’s actions.</span><span class="sxs-lookup"><span data-stu-id="db7ec-108">This can be useful if you are building your own user interface which creates a query expression in response to the user’s actions.</span></span> <span data-ttu-id="db7ec-109">To do this, you need to know the syntax for query expressions.</span><span class="sxs-lookup"><span data-stu-id="db7ec-109">To do this, you need to know the syntax for query expressions.</span></span>  

<span data-ttu-id="db7ec-110">Each entity attribute that can be included in a query expression has a specific data type and a set of possible query operators.</span><span class="sxs-lookup"><span data-stu-id="db7ec-110">Each entity attribute that can be included in a query expression has a specific data type and a set of possible query operators.</span></span> <span data-ttu-id="db7ec-111">The set of entity attributes and supported operators for each attribute is specified in [Entity Attributes](EntityAttributes.md).</span><span class="sxs-lookup"><span data-stu-id="db7ec-111">The set of entity attributes and supported operators for each attribute is specified in [Entity Attributes](EntityAttributes.md).</span></span> <span data-ttu-id="db7ec-112">A single-value query requires the attribute to support the *Equals* operation.</span><span class="sxs-lookup"><span data-stu-id="db7ec-112">A single-value query requires the attribute to support the *Equals* operation.</span></span> <span data-ttu-id="db7ec-113">A prefix query requires the attribute to support the *StartsWith* operation.</span><span class="sxs-lookup"><span data-stu-id="db7ec-113">A prefix query requires the attribute to support the *StartsWith* operation.</span></span> <span data-ttu-id="db7ec-114">Numeric range queries requires the attribute to support the *IsBetween* operation.</span><span class="sxs-lookup"><span data-stu-id="db7ec-114">Numeric range queries requires the attribute to support the *IsBetween* operation.</span></span>

<span data-ttu-id="db7ec-115">Some of the entity data are stored as composite attributes, as indicated by a dot '.' in the attribute name.</span><span class="sxs-lookup"><span data-stu-id="db7ec-115">Some of the entity data are stored as composite attributes, as indicated by a dot '.' in the attribute name.</span></span> <span data-ttu-id="db7ec-116">For example, Author/Affiliation information is represented as a composite attribute.</span><span class="sxs-lookup"><span data-stu-id="db7ec-116">For example, Author/Affiliation information is represented as a composite attribute.</span></span> <span data-ttu-id="db7ec-117">It contains 4 components: AuN, AuId, AfN, AfId.</span><span class="sxs-lookup"><span data-stu-id="db7ec-117">It contains 4 components: AuN, AuId, AfN, AfId.</span></span> <span data-ttu-id="db7ec-118">These components are separate pieces of data that form a single entity attribute value.</span><span class="sxs-lookup"><span data-stu-id="db7ec-118">These components are separate pieces of data that form a single entity attribute value.</span></span>


<span data-ttu-id="db7ec-119">**String Attribute: Single value** (includes matches against synonyms)</span><span class="sxs-lookup"><span data-stu-id="db7ec-119">**String Attribute: Single value** (includes matches against synonyms)</span></span>  
<span data-ttu-id="db7ec-120">Ti='indexing by latent semantic analysis'</span><span class="sxs-lookup"><span data-stu-id="db7ec-120">Ti='indexing by latent semantic analysis'</span></span>  
<span data-ttu-id="db7ec-121">Composite(AA.AuN='sue dumais')</span><span class="sxs-lookup"><span data-stu-id="db7ec-121">Composite(AA.AuN='sue dumais')</span></span>

<span data-ttu-id="db7ec-122">**String Attribute: Exact single value** (matches only canonical values)</span><span class="sxs-lookup"><span data-stu-id="db7ec-122">**String Attribute: Exact single value** (matches only canonical values)</span></span>  
<span data-ttu-id="db7ec-123">Ti=='indexing by latent semantic analysis'</span><span class="sxs-lookup"><span data-stu-id="db7ec-123">Ti=='indexing by latent semantic analysis'</span></span>  
<span data-ttu-id="db7ec-124">Composite(AA.AuN=='susan t dumais')</span><span class="sxs-lookup"><span data-stu-id="db7ec-124">Composite(AA.AuN=='susan t dumais')</span></span>
     
<span data-ttu-id="db7ec-125">**String Attribute: Prefix value** </span><span class="sxs-lookup"><span data-stu-id="db7ec-125">**String Attribute: Prefix value** </span></span>  
<span data-ttu-id="db7ec-126">Ti='indexing by latent seman'...</span><span class="sxs-lookup"><span data-stu-id="db7ec-126">Ti='indexing by latent seman'...</span></span>  
<span data-ttu-id="db7ec-127">Composite(AA.AuN='sue du'...)</span><span class="sxs-lookup"><span data-stu-id="db7ec-127">Composite(AA.AuN='sue du'...)</span></span>

<span data-ttu-id="db7ec-128">**Numeric Attribute: Single value**</span><span class="sxs-lookup"><span data-stu-id="db7ec-128">**Numeric Attribute: Single value**</span></span>  
<span data-ttu-id="db7ec-129">Y=2010</span><span class="sxs-lookup"><span data-stu-id="db7ec-129">Y=2010</span></span>
 
<span data-ttu-id="db7ec-130">**Numeric Attribute: Range value**</span><span class="sxs-lookup"><span data-stu-id="db7ec-130">**Numeric Attribute: Range value**</span></span>  
<span data-ttu-id="db7ec-131">Y>2005</span><span class="sxs-lookup"><span data-stu-id="db7ec-131">Y>2005</span></span>  
<span data-ttu-id="db7ec-132">Y>=2005</span><span class="sxs-lookup"><span data-stu-id="db7ec-132">Y>=2005</span></span>  
<span data-ttu-id="db7ec-133">Y<2010</span><span class="sxs-lookup"><span data-stu-id="db7ec-133">Y<2010</span></span>  
<span data-ttu-id="db7ec-134">Y<=2010</span><span class="sxs-lookup"><span data-stu-id="db7ec-134">Y<=2010</span></span>  
<span data-ttu-id="db7ec-135">Y=\[2010, 2012\) (includes only left boundary value: 2010, 2011)</span><span class="sxs-lookup"><span data-stu-id="db7ec-135">Y=\[2010, 2012\) (includes only left boundary value: 2010, 2011)</span></span>  
<span data-ttu-id="db7ec-136">Y=\[2010, 2012\] (includes both boundary values: 2010, 2011, 2012)</span><span class="sxs-lookup"><span data-stu-id="db7ec-136">Y=\[2010, 2012\] (includes both boundary values: 2010, 2011, 2012)</span></span>
 
<span data-ttu-id="db7ec-137">**Numeric Attribute: Prefix value**</span><span class="sxs-lookup"><span data-stu-id="db7ec-137">**Numeric Attribute: Prefix value**</span></span>  
<span data-ttu-id="db7ec-138">Y='19'... (any numeric value that starts with 19)</span><span class="sxs-lookup"><span data-stu-id="db7ec-138">Y='19'... (any numeric value that starts with 19)</span></span> 
 
<span data-ttu-id="db7ec-139">**Date Attribute: Single value**</span><span class="sxs-lookup"><span data-stu-id="db7ec-139">**Date Attribute: Single value**</span></span>  
<span data-ttu-id="db7ec-140">D='2010-02-04'</span><span class="sxs-lookup"><span data-stu-id="db7ec-140">D='2010-02-04'</span></span>

<span data-ttu-id="db7ec-141">**Date Attribute: Range value**</span><span class="sxs-lookup"><span data-stu-id="db7ec-141">**Date Attribute: Range value**</span></span>  
<span data-ttu-id="db7ec-142">D>'2010-02-03'</span><span class="sxs-lookup"><span data-stu-id="db7ec-142">D>'2010-02-03'</span></span>  
<span data-ttu-id="db7ec-143">D=['2010-02-03','2010-02-05']</span><span class="sxs-lookup"><span data-stu-id="db7ec-143">D=['2010-02-03','2010-02-05']</span></span>

<span data-ttu-id="db7ec-144">**And/Or Queries:**</span><span class="sxs-lookup"><span data-stu-id="db7ec-144">**And/Or Queries:**</span></span>  
<span data-ttu-id="db7ec-145">And(Y=1985, Ti='disordered electronic systems')</span><span class="sxs-lookup"><span data-stu-id="db7ec-145">And(Y=1985, Ti='disordered electronic systems')</span></span>  
<span data-ttu-id="db7ec-146">Or(Ti='disordered electronic systems', Ti='fault tolerance principles and practice')</span><span class="sxs-lookup"><span data-stu-id="db7ec-146">Or(Ti='disordered electronic systems', Ti='fault tolerance principles and practice')</span></span>  
<span data-ttu-id="db7ec-147">And(Or(Y=1985,Y=2008), Ti='disordered electronic systems')</span><span class="sxs-lookup"><span data-stu-id="db7ec-147">And(Or(Y=1985,Y=2008), Ti='disordered electronic systems')</span></span>
 
<span data-ttu-id="db7ec-148">**Composite Queries:**</span><span class="sxs-lookup"><span data-stu-id="db7ec-148">**Composite Queries:**</span></span>  
<span data-ttu-id="db7ec-149">To query components of a composite attribute, you need to enclose the part of the query expression that refers to the composite attribute in the Composite() function.</span><span class="sxs-lookup"><span data-stu-id="db7ec-149">To query components of a composite attribute, you need to enclose the part of the query expression that refers to the composite attribute in the Composite() function.</span></span> 

<span data-ttu-id="db7ec-150">For example, to query for papers by author name, use the following query:</span><span class="sxs-lookup"><span data-stu-id="db7ec-150">For example, to query for papers by author name, use the following query:</span></span>
```
Composite(AA.AuN='mike smith')
```
<br><span data-ttu-id="db7ec-151">To query for papers by a particular author while the author was at a particular institution, use the following query:</span><span class="sxs-lookup"><span data-stu-id="db7ec-151">To query for papers by a particular author while the author was at a particular institution, use the following query:</span></span>
```
Composite(And(AA.AuN='mike smith',AA.AfN='harvard university'))
```
<br><span data-ttu-id="db7ec-152">The Composite() function ties the two parts of the composite attribute together.</span><span class="sxs-lookup"><span data-stu-id="db7ec-152">The Composite() function ties the two parts of the composite attribute together.</span></span> <span data-ttu-id="db7ec-153">This means that we only get papers where one of the authors is “Mike Smith” while he was at Harvard.</span><span class="sxs-lookup"><span data-stu-id="db7ec-153">This means that we only get papers where one of the authors is “Mike Smith” while he was at Harvard.</span></span> 

<span data-ttu-id="db7ec-154">To query for papers by a particular author in affiliations with (other) authors from a particular institution, use the following query:</span><span class="sxs-lookup"><span data-stu-id="db7ec-154">To query for papers by a particular author in affiliations with (other) authors from a particular institution, use the following query:</span></span>
```
And(Composite(AA.AuN='mike smith'),Composite(AA.AfN='harvard university'))
```
<br><span data-ttu-id="db7ec-155">In this version, because Composite() is applied to the author and affiliation individually before And(), we get all papers where one of the authors is “Mike Smith” and one of the authors' affiliations is “Harvard”.</span><span class="sxs-lookup"><span data-stu-id="db7ec-155">In this version, because Composite() is applied to the author and affiliation individually before And(), we get all papers where one of the authors is “Mike Smith” and one of the authors' affiliations is “Harvard”.</span></span> <span data-ttu-id="db7ec-156">This sounds similar to the previous query example, but it's not the same thing.</span><span class="sxs-lookup"><span data-stu-id="db7ec-156">This sounds similar to the previous query example, but it's not the same thing.</span></span>

<span data-ttu-id="db7ec-157">In general, consider the following example: We have a composite attribute C that has two components A and B. An entity may have multiple values for C. These are our entities:</span><span class="sxs-lookup"><span data-stu-id="db7ec-157">In general, consider the following example: We have a composite attribute C that has two components A and B. An entity may have multiple values for C. These are our entities:</span></span>
```
E1: C={A=1, B=1}  C={A=1,B=2}  C={A=2,B=3}
E2: C={A=1, B=3}  C={A=3,B=2}
```

<br><span data-ttu-id="db7ec-158">The query</span><span class="sxs-lookup"><span data-stu-id="db7ec-158">The query</span></span> 
```
Composite(And(C.A=1, C.B=2))
```

<br><span data-ttu-id="db7ec-159">matches only entities that have a value for C where the component C.A is 1 and the component C.B is 2.</span><span class="sxs-lookup"><span data-stu-id="db7ec-159">matches only entities that have a value for C where the component C.A is 1 and the component C.B is 2.</span></span> <span data-ttu-id="db7ec-160">Only E1 matches this query.</span><span class="sxs-lookup"><span data-stu-id="db7ec-160">Only E1 matches this query.</span></span>

<span data-ttu-id="db7ec-161">The query</span><span class="sxs-lookup"><span data-stu-id="db7ec-161">The query</span></span> 
```
And(Composite(C.A=1), Composite(C.B=2))
```
<br><span data-ttu-id="db7ec-162">matches entities that have a value for C where C.A is 1 and also have a value for C where C.B is 2.</span><span class="sxs-lookup"><span data-stu-id="db7ec-162">matches entities that have a value for C where C.A is 1 and also have a value for C where C.B is 2.</span></span> <span data-ttu-id="db7ec-163">Both E1 and E2 match this query.</span><span class="sxs-lookup"><span data-stu-id="db7ec-163">Both E1 and E2 match this query.</span></span>

<span data-ttu-id="db7ec-164">Please note:</span><span class="sxs-lookup"><span data-stu-id="db7ec-164">Please note:</span></span>  
- <span data-ttu-id="db7ec-165">You cannot reference a part of a composite attribute outside of a Composite() function.</span><span class="sxs-lookup"><span data-stu-id="db7ec-165">You cannot reference a part of a composite attribute outside of a Composite() function.</span></span>
- <span data-ttu-id="db7ec-166">You cannot reference parts of two different composite attributes inside the same Composite() function.</span><span class="sxs-lookup"><span data-stu-id="db7ec-166">You cannot reference parts of two different composite attributes inside the same Composite() function.</span></span>
- <span data-ttu-id="db7ec-167">You cannot reference an attribute that is not part of a composite attribute inside a Composite() function.</span><span class="sxs-lookup"><span data-stu-id="db7ec-167">You cannot reference an attribute that is not part of a composite attribute inside a Composite() function.</span></span>
