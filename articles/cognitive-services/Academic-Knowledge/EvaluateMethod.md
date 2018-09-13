---
title: Evaluate method in the Academic Knowledge API | Microsoft Docs
description: Use the Evaluate method to return a set of academic entities based on a query expression in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: bcef8214ebb1b7739f50a7e5c742721bc85bfe11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549343"
---
# <a name="evaluate-method"></a><span data-ttu-id="8837d-103">Evaluate Method</span><span class="sxs-lookup"><span data-stu-id="8837d-103">Evaluate Method</span></span>

<span data-ttu-id="8837d-104">The **evaluate** REST API is used to return a set of academic entities based on a query expression.</span><span class="sxs-lookup"><span data-stu-id="8837d-104">The **evaluate** REST API is used to return a set of academic entities based on a query expression.</span></span>
<br>

<span data-ttu-id="8837d-105">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="8837d-105">**REST endpoint:**</span></span>  
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/evaluate? 
```   
<br>
## <a name="request-parameters"></a><span data-ttu-id="8837d-106">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="8837d-106">Request Parameters</span></span>  
<span data-ttu-id="8837d-107">Name</span><span class="sxs-lookup"><span data-stu-id="8837d-107">Name</span></span>     | <span data-ttu-id="8837d-108">Value</span><span class="sxs-lookup"><span data-stu-id="8837d-108">Value</span></span> | <span data-ttu-id="8837d-109">Required?</span><span class="sxs-lookup"><span data-stu-id="8837d-109">Required?</span></span>  | <span data-ttu-id="8837d-110">Description</span><span class="sxs-lookup"><span data-stu-id="8837d-110">Description</span></span>
-----------|-----------|---------|--------
<span data-ttu-id="8837d-111">**expr**</span><span class="sxs-lookup"><span data-stu-id="8837d-111">**expr**</span></span>       | <span data-ttu-id="8837d-112">Text string</span><span class="sxs-lookup"><span data-stu-id="8837d-112">Text string</span></span> | <span data-ttu-id="8837d-113">Yes</span><span class="sxs-lookup"><span data-stu-id="8837d-113">Yes</span></span> | <span data-ttu-id="8837d-114">A query expression that specifies which entities should be returned.</span><span class="sxs-lookup"><span data-stu-id="8837d-114">A query expression that specifies which entities should be returned.</span></span>
<span data-ttu-id="8837d-115">**model**</span><span class="sxs-lookup"><span data-stu-id="8837d-115">**model**</span></span>      | <span data-ttu-id="8837d-116">Text string</span><span class="sxs-lookup"><span data-stu-id="8837d-116">Text string</span></span> | <span data-ttu-id="8837d-117">No</span><span class="sxs-lookup"><span data-stu-id="8837d-117">No</span></span>  | <span data-ttu-id="8837d-118">Name of the model that you wish to query.</span><span class="sxs-lookup"><span data-stu-id="8837d-118">Name of the model that you wish to query.</span></span>  <span data-ttu-id="8837d-119">Currently, the value defaults to *latest*.</span><span class="sxs-lookup"><span data-stu-id="8837d-119">Currently, the value defaults to *latest*.</span></span>        
<span data-ttu-id="8837d-120">**attributes**</span><span class="sxs-lookup"><span data-stu-id="8837d-120">**attributes**</span></span> | <span data-ttu-id="8837d-121">Text string</span><span class="sxs-lookup"><span data-stu-id="8837d-121">Text string</span></span> | <span data-ttu-id="8837d-122">No</span><span class="sxs-lookup"><span data-stu-id="8837d-122">No</span></span><br><span data-ttu-id="8837d-123">default: Id</span><span class="sxs-lookup"><span data-stu-id="8837d-123">default: Id</span></span> | <span data-ttu-id="8837d-124">A comma-delimited list that specifies the attribute values that are included in the response.</span><span class="sxs-lookup"><span data-stu-id="8837d-124">A comma-delimited list that specifies the attribute values that are included in the response.</span></span> <span data-ttu-id="8837d-125">Attribute names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="8837d-125">Attribute names are case-sensitive.</span></span>
<span data-ttu-id="8837d-126">**count**</span><span class="sxs-lookup"><span data-stu-id="8837d-126">**count**</span></span>        | <span data-ttu-id="8837d-127">Number</span><span class="sxs-lookup"><span data-stu-id="8837d-127">Number</span></span> | <span data-ttu-id="8837d-128">No</span><span class="sxs-lookup"><span data-stu-id="8837d-128">No</span></span><br><span data-ttu-id="8837d-129">Default: 10</span><span class="sxs-lookup"><span data-stu-id="8837d-129">Default: 10</span></span> | <span data-ttu-id="8837d-130">Number of results to return.</span><span class="sxs-lookup"><span data-stu-id="8837d-130">Number of results to return.</span></span>
<span data-ttu-id="8837d-131">**offset**</span><span class="sxs-lookup"><span data-stu-id="8837d-131">**offset**</span></span>     | <span data-ttu-id="8837d-132">Number</span><span class="sxs-lookup"><span data-stu-id="8837d-132">Number</span></span> |   <span data-ttu-id="8837d-133">No</span><span class="sxs-lookup"><span data-stu-id="8837d-133">No</span></span><br><span data-ttu-id="8837d-134">Default: 0</span><span class="sxs-lookup"><span data-stu-id="8837d-134">Default: 0</span></span>    | <span data-ttu-id="8837d-135">Index of the first result to return.</span><span class="sxs-lookup"><span data-stu-id="8837d-135">Index of the first result to return.</span></span>
<span data-ttu-id="8837d-136">**orderby**</span><span class="sxs-lookup"><span data-stu-id="8837d-136">**orderby**</span></span> |   <span data-ttu-id="8837d-137">Text string</span><span class="sxs-lookup"><span data-stu-id="8837d-137">Text string</span></span> | <span data-ttu-id="8837d-138">No</span><span class="sxs-lookup"><span data-stu-id="8837d-138">No</span></span><br><span data-ttu-id="8837d-139">Default: by decreasing prob</span><span class="sxs-lookup"><span data-stu-id="8837d-139">Default: by decreasing prob</span></span> | <span data-ttu-id="8837d-140">Name of an attribute that is used for sorting the entities.</span><span class="sxs-lookup"><span data-stu-id="8837d-140">Name of an attribute that is used for sorting the entities.</span></span> <span data-ttu-id="8837d-141">Optionally, ascending/descending can be specified.</span><span class="sxs-lookup"><span data-stu-id="8837d-141">Optionally, ascending/descending can be specified.</span></span> <span data-ttu-id="8837d-142">The format is: *name:asc* or *name:desc*.</span><span class="sxs-lookup"><span data-stu-id="8837d-142">The format is: *name:asc* or *name:desc*.</span></span>
  
 <br>
## <a name="response-json"></a><span data-ttu-id="8837d-143">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="8837d-143">Response (JSON)</span></span>
<span data-ttu-id="8837d-144">Name</span><span class="sxs-lookup"><span data-stu-id="8837d-144">Name</span></span> | <span data-ttu-id="8837d-145">Description</span><span class="sxs-lookup"><span data-stu-id="8837d-145">Description</span></span>
-------|-----   
<span data-ttu-id="8837d-146">**expr**</span><span class="sxs-lookup"><span data-stu-id="8837d-146">**expr**</span></span> |  <span data-ttu-id="8837d-147">The *expr* parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="8837d-147">The *expr* parameter from the request.</span></span>
<span data-ttu-id="8837d-148">**entities**</span><span class="sxs-lookup"><span data-stu-id="8837d-148">**entities**</span></span> |  <span data-ttu-id="8837d-149">An array of 0 or more entities that matched the query expression.</span><span class="sxs-lookup"><span data-stu-id="8837d-149">An array of 0 or more entities that matched the query expression.</span></span> <span data-ttu-id="8837d-150">Each entity contains a natural log probability value and the values of other requested attributes.</span><span class="sxs-lookup"><span data-stu-id="8837d-150">Each entity contains a natural log probability value and the values of other requested attributes.</span></span>
<span data-ttu-id="8837d-151">**aborted**</span><span class="sxs-lookup"><span data-stu-id="8837d-151">**aborted**</span></span> | <span data-ttu-id="8837d-152">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="8837d-152">True if the request timed out.</span></span>

<br>
#### <a name="example"></a><span data-ttu-id="8837d-153">Example:</span><span class="sxs-lookup"><span data-stu-id="8837d-153">Example:</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/evaluate?expr=
Composite(AA.AuN=='jaime teevan')&count=2&attributes=Ti,Y,CC,AA.AuN,AA.AuId
```
<br><span data-ttu-id="8837d-154">Typically, an expression will be obtained from a response to the **interpret** method.</span><span class="sxs-lookup"><span data-stu-id="8837d-154">Typically, an expression will be obtained from a response to the **interpret** method.</span></span>  <span data-ttu-id="8837d-155">But you can also compose query expressions yourself (see [Query Expression Syntax](QueryExpressionSyntax.md)).</span><span class="sxs-lookup"><span data-stu-id="8837d-155">But you can also compose query expressions yourself (see [Query Expression Syntax](QueryExpressionSyntax.md)).</span></span>  
  
<span data-ttu-id="8837d-156">Using the *count* and *offset* parameters, a large number of results may be obtained without sending a single request that results in a huge (and potentially slow) response.</span><span class="sxs-lookup"><span data-stu-id="8837d-156">Using the *count* and *offset* parameters, a large number of results may be obtained without sending a single request that results in a huge (and potentially slow) response.</span></span>  <span data-ttu-id="8837d-157">In this example, the request used the expression for the first interpretation from the **interpret** API response as the *expr* value.</span><span class="sxs-lookup"><span data-stu-id="8837d-157">In this example, the request used the expression for the first interpretation from the **interpret** API response as the *expr* value.</span></span> <span data-ttu-id="8837d-158">The *count=2* parameter specifies that 2 entity results are being requested.</span><span class="sxs-lookup"><span data-stu-id="8837d-158">The *count=2* parameter specifies that 2 entity results are being requested.</span></span> <span data-ttu-id="8837d-159">And the *attributes=Ti,Y,CC,AA.AuN,AA.AuId* parameter indicates that the title, year, citation count, author name, and author ID are requested for each result.</span><span class="sxs-lookup"><span data-stu-id="8837d-159">And the *attributes=Ti,Y,CC,AA.AuN,AA.AuId* parameter indicates that the title, year, citation count, author name, and author ID are requested for each result.</span></span>  <span data-ttu-id="8837d-160">See [Entity Attributes](EntityAttributes.md) for a list of attributes.</span><span class="sxs-lookup"><span data-stu-id="8837d-160">See [Entity Attributes](EntityAttributes.md) for a list of attributes.</span></span>
  
```JSON
{
  "expr": "Composite(AA.AuN=='jaime teevan')",
  "entities": 
  [
    {
      "logprob": -15.08,
      "Ti": "personalizing search via automated analysis of interests and activities",
      "Y": 2005,
      "CC": 372,
      "AA": [
        {
          "AuN": "jaime teevan",
          "AuId": 1968481722
        },
        {
          "AuN": "susan t dumais",
          "AuId": 676500258
        },
        {
          "AuN": "eric horvitz",
          "AuId": 1470530979
        }
      ]
    },
    {
      "logprob": -15.389,
      "Ti": "the perfect search engine is not enough a study of orienteering behavior in directed search",
      "Y": 2004,
      "CC": 237,
      "AA": [
        {
          "AuN": "jaime teevan",
          "AuId": 1982462162
        },
        {
          "AuN": "christine alvarado",
          "AuId": 2163512453
        },
        {
          "AuN": "mark s ackerman",
          "AuId": 2055132526
        },
        {
          "AuN": "david r karger",
          "AuId": 2012534293
        }
      ]
    }
  ]
}
 ```
 
