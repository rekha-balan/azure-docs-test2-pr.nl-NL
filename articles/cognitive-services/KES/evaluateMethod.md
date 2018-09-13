---
title: Evaluate method in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use the Evaluate method in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 8d2671c22b04839af232037dfcd85624e81ec0f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553947"
---
# <a name="evaluate-method"></a><span data-ttu-id="f0284-103">evaluate Method</span><span class="sxs-lookup"><span data-stu-id="f0284-103">evaluate Method</span></span>
<span data-ttu-id="f0284-104">The *evaluate* method evaluates and returns the output of a structured query expression based on the index data.</span><span class="sxs-lookup"><span data-stu-id="f0284-104">The *evaluate* method evaluates and returns the output of a structured query expression based on the index data.</span></span>

<span data-ttu-id="f0284-105">Typically, an expression will be obtained from a response to the interpret method.</span><span class="sxs-lookup"><span data-stu-id="f0284-105">Typically, an expression will be obtained from a response to the interpret method.</span></span>  <span data-ttu-id="f0284-106">But you can also compose query expressions yourself (see [Structured Query Expression](Expressions.md)).</span><span class="sxs-lookup"><span data-stu-id="f0284-106">But you can also compose query expressions yourself (see [Structured Query Expression](Expressions.md)).</span></span>  

## <a name="request"></a><span data-ttu-id="f0284-107">Request</span><span class="sxs-lookup"><span data-stu-id="f0284-107">Request</span></span> 
`http://<host>/evaluate?expr=<expr>&attributes=<attrs>[&<options>]`   

<span data-ttu-id="f0284-108">Name</span><span class="sxs-lookup"><span data-stu-id="f0284-108">Name</span></span>|<span data-ttu-id="f0284-109">Value</span><span class="sxs-lookup"><span data-stu-id="f0284-109">Value</span></span>|<span data-ttu-id="f0284-110">Description</span><span class="sxs-lookup"><span data-stu-id="f0284-110">Description</span></span>
----|----|----
<span data-ttu-id="f0284-111">expr</span><span class="sxs-lookup"><span data-stu-id="f0284-111">expr</span></span>       | <span data-ttu-id="f0284-112">Text string</span><span class="sxs-lookup"><span data-stu-id="f0284-112">Text string</span></span> | <span data-ttu-id="f0284-113">Structured query expression that selects a subset of index entities.</span><span class="sxs-lookup"><span data-stu-id="f0284-113">Structured query expression that selects a subset of index entities.</span></span>
<span data-ttu-id="f0284-114">attributes</span><span class="sxs-lookup"><span data-stu-id="f0284-114">attributes</span></span> | <span data-ttu-id="f0284-115">Text string</span><span class="sxs-lookup"><span data-stu-id="f0284-115">Text string</span></span> | <span data-ttu-id="f0284-116">Comma-delimited list of attributes to include in response.</span><span class="sxs-lookup"><span data-stu-id="f0284-116">Comma-delimited list of attributes to include in response.</span></span>
<span data-ttu-id="f0284-117">count</span><span class="sxs-lookup"><span data-stu-id="f0284-117">count</span></span>      | <span data-ttu-id="f0284-118">Number (default=10)</span><span class="sxs-lookup"><span data-stu-id="f0284-118">Number (default=10)</span></span> | <span data-ttu-id="f0284-119">Maximum number of results to return.</span><span class="sxs-lookup"><span data-stu-id="f0284-119">Maximum number of results to return.</span></span>
<span data-ttu-id="f0284-120">offset</span><span class="sxs-lookup"><span data-stu-id="f0284-120">offset</span></span>     | <span data-ttu-id="f0284-121">Number (default=0)</span><span class="sxs-lookup"><span data-stu-id="f0284-121">Number (default=0)</span></span> | <span data-ttu-id="f0284-122">Index of the first result to return.</span><span class="sxs-lookup"><span data-stu-id="f0284-122">Index of the first result to return.</span></span>
<span data-ttu-id="f0284-123">orderby</span><span class="sxs-lookup"><span data-stu-id="f0284-123">orderby</span></span> |   <span data-ttu-id="f0284-124">Text string</span><span class="sxs-lookup"><span data-stu-id="f0284-124">Text string</span></span> | <span data-ttu-id="f0284-125">Name of attribute used to sort the results, followed by optional sort order (default=asc): "*attrname*[:(asc&#124;desc)]".</span><span class="sxs-lookup"><span data-stu-id="f0284-125">Name of attribute used to sort the results, followed by optional sort order (default=asc): "*attrname*[:(asc&#124;desc)]".</span></span>  <span data-ttu-id="f0284-126">If not specified, the results are returned by decreasing natural log probability.</span><span class="sxs-lookup"><span data-stu-id="f0284-126">If not specified, the results are returned by decreasing natural log probability.</span></span>
<span data-ttu-id="f0284-127">timeout</span><span class="sxs-lookup"><span data-stu-id="f0284-127">timeout</span></span>  | <span data-ttu-id="f0284-128">Number (default=1000)</span><span class="sxs-lookup"><span data-stu-id="f0284-128">Number (default=1000)</span></span> | <span data-ttu-id="f0284-129">Timeout in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="f0284-129">Timeout in milliseconds.</span></span> <span data-ttu-id="f0284-130">Only results computed before the timeout has elapsed are returned.</span><span class="sxs-lookup"><span data-stu-id="f0284-130">Only results computed before the timeout has elapsed are returned.</span></span>

<span data-ttu-id="f0284-131">Using the *count* and *offset* parameters, a large number of results may be obtained incrementally over multiple requests.</span><span class="sxs-lookup"><span data-stu-id="f0284-131">Using the *count* and *offset* parameters, a large number of results may be obtained incrementally over multiple requests.</span></span>
  
## <a name="response-json"></a><span data-ttu-id="f0284-132">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="f0284-132">Response (JSON)</span></span>
<span data-ttu-id="f0284-133">JSONPath</span><span class="sxs-lookup"><span data-stu-id="f0284-133">JSONPath</span></span>|<span data-ttu-id="f0284-134">Description</span><span class="sxs-lookup"><span data-stu-id="f0284-134">Description</span></span>
----|----
<span data-ttu-id="f0284-135">$.expr</span><span class="sxs-lookup"><span data-stu-id="f0284-135">$.expr</span></span> | <span data-ttu-id="f0284-136">*expr* parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="f0284-136">*expr* parameter from the request.</span></span>
<span data-ttu-id="f0284-137">$.entities</span><span class="sxs-lookup"><span data-stu-id="f0284-137">$.entities</span></span> | <span data-ttu-id="f0284-138">Array of 0 or more object entities matching the structured query expression.</span><span class="sxs-lookup"><span data-stu-id="f0284-138">Array of 0 or more object entities matching the structured query expression.</span></span> 
<span data-ttu-id="f0284-139">$.aborted</span><span class="sxs-lookup"><span data-stu-id="f0284-139">$.aborted</span></span> | <span data-ttu-id="f0284-140">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="f0284-140">True if the request timed out.</span></span>

<span data-ttu-id="f0284-141">Each entity contains a *logprob* value and the values of the requested attributes.</span><span class="sxs-lookup"><span data-stu-id="f0284-141">Each entity contains a *logprob* value and the values of the requested attributes.</span></span>

## <a name="example"></a><span data-ttu-id="f0284-142">Example</span><span class="sxs-lookup"><span data-stu-id="f0284-142">Example</span></span>
<span data-ttu-id="f0284-143">In the academic publications example, the following request passes a structured query expression (potentially from the output of an *interpret* request) and retrieves a few attributes for the top 2 matching entities:</span><span class="sxs-lookup"><span data-stu-id="f0284-143">In the academic publications example, the following request passes a structured query expression (potentially from the output of an *interpret* request) and retrieves a few attributes for the top 2 matching entities:</span></span>

`http://<host>/evaluate?expr=Composite(Author.Name=='jaime teevan')&attributes=Title,Y,Author.Name,Author.Id&count=2`

<span data-ttu-id="f0284-144">The response contains the top 2 ("count=2") most likely matching entities.</span><span class="sxs-lookup"><span data-stu-id="f0284-144">The response contains the top 2 ("count=2") most likely matching entities.</span></span>  <span data-ttu-id="f0284-145">For each entity, the title, year, author name, and author ID attributes are returned.</span><span class="sxs-lookup"><span data-stu-id="f0284-145">For each entity, the title, year, author name, and author ID attributes are returned.</span></span>  <span data-ttu-id="f0284-146">Note how the structure of composite attribute values matches the way they are specified in the data file.</span><span class="sxs-lookup"><span data-stu-id="f0284-146">Note how the structure of composite attribute values matches the way they are specified in the data file.</span></span> 

```json
{
  "expr": "Composite(Author.Name=='jaime teevan')",
  "entities": 
  [
    {
      "logprob": -6.645,
      "Ti": "personalizing search via automated analysis of interests and activities",
      "Y": 2005,
      "Author": [
        {
          "Name": "jaime teevan",
          "Id": 1968481722
        },
        {
          "Name": "susan t dumais",
          "Id": 676500258
        },
        {
          "Name": "eric horvitz",
          "Id": 1470530979
        }
      ]
    },
    {
      "logprob": -6.764,
      "Ti": "the perfect search engine is not enough a study of orienteering behavior in directed search",
      "Y": 2004,
      "Author": [
        {
          "Name": "jaime teevan",
          "Id": 1982462162
        },
        {
          "Name": "christine alvarado",
          "Id": 2163512453
        },
        {
          "Name": "mark s ackerman",
          "Id": 2055132526
        },
        {
          "Name": "david r karger",
          "Id": 2012534293
        }
      ]
    }
  ]
}
```
