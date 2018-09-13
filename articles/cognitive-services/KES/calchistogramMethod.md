---
title: CalcHistogram method in the Knowledge Exploration Service API | Microsoft Docs
description: Learn how to use the CalcHistogram method in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 5e8b9906ef4f2f30cd805779a5858345e0a9f95d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554264"
---
# <a name="calchistogram-method"></a><span data-ttu-id="bb48f-103">calchistogram Method</span><span class="sxs-lookup"><span data-stu-id="bb48f-103">calchistogram Method</span></span>
<span data-ttu-id="bb48f-104">The *calchistogram* method computes the objects matching a structured query expression and calculates the distribution of their attribute values.</span><span class="sxs-lookup"><span data-stu-id="bb48f-104">The *calchistogram* method computes the objects matching a structured query expression and calculates the distribution of their attribute values.</span></span>

## <a name="request"></a><span data-ttu-id="bb48f-105">Request</span><span class="sxs-lookup"><span data-stu-id="bb48f-105">Request</span></span>
`http://<host>/calchistogram?expr=<expr>[&options]` 

<span data-ttu-id="bb48f-106">Name</span><span class="sxs-lookup"><span data-stu-id="bb48f-106">Name</span></span>|<span data-ttu-id="bb48f-107">Value</span><span class="sxs-lookup"><span data-stu-id="bb48f-107">Value</span></span>|<span data-ttu-id="bb48f-108">Description</span><span class="sxs-lookup"><span data-stu-id="bb48f-108">Description</span></span>
----|-----|-----------
<span data-ttu-id="bb48f-109">expr</span><span class="sxs-lookup"><span data-stu-id="bb48f-109">expr</span></span> | <span data-ttu-id="bb48f-110">Text string</span><span class="sxs-lookup"><span data-stu-id="bb48f-110">Text string</span></span> | <span data-ttu-id="bb48f-111">Structured query expression that specifies the index entities over which to calculate histograms.</span><span class="sxs-lookup"><span data-stu-id="bb48f-111">Structured query expression that specifies the index entities over which to calculate histograms.</span></span>
<span data-ttu-id="bb48f-112">attributes</span><span class="sxs-lookup"><span data-stu-id="bb48f-112">attributes</span></span> | <span data-ttu-id="bb48f-113">Text string (default="")</span><span class="sxs-lookup"><span data-stu-id="bb48f-113">Text string (default="")</span></span> | <span data-ttu-id="bb48f-114">Comma-delimited list of attribute to included in the response.</span><span class="sxs-lookup"><span data-stu-id="bb48f-114">Comma-delimited list of attribute to included in the response.</span></span>
<span data-ttu-id="bb48f-115">count</span><span class="sxs-lookup"><span data-stu-id="bb48f-115">count</span></span>   | <span data-ttu-id="bb48f-116">Number (default=10)</span><span class="sxs-lookup"><span data-stu-id="bb48f-116">Number (default=10)</span></span> | <span data-ttu-id="bb48f-117">Number of results to return.</span><span class="sxs-lookup"><span data-stu-id="bb48f-117">Number of results to return.</span></span>
<span data-ttu-id="bb48f-118">offset</span><span class="sxs-lookup"><span data-stu-id="bb48f-118">offset</span></span>  | <span data-ttu-id="bb48f-119">Number (default=0)</span><span class="sxs-lookup"><span data-stu-id="bb48f-119">Number (default=0)</span></span> | <span data-ttu-id="bb48f-120">Index of the first result to return.</span><span class="sxs-lookup"><span data-stu-id="bb48f-120">Index of the first result to return.</span></span>

## <a name="response-json"></a><span data-ttu-id="bb48f-121">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="bb48f-121">Response (JSON)</span></span>
<span data-ttu-id="bb48f-122">JSONPath</span><span class="sxs-lookup"><span data-stu-id="bb48f-122">JSONPath</span></span> | <span data-ttu-id="bb48f-123">Description</span><span class="sxs-lookup"><span data-stu-id="bb48f-123">Description</span></span>
----|----
<span data-ttu-id="bb48f-124">$.expr</span><span class="sxs-lookup"><span data-stu-id="bb48f-124">$.expr</span></span> | <span data-ttu-id="bb48f-125">*expr* parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="bb48f-125">*expr* parameter from the request.</span></span>
<span data-ttu-id="bb48f-126">$.num_entities</span><span class="sxs-lookup"><span data-stu-id="bb48f-126">$.num_entities</span></span> | <span data-ttu-id="bb48f-127">Total number of matching entities.</span><span class="sxs-lookup"><span data-stu-id="bb48f-127">Total number of matching entities.</span></span>
<span data-ttu-id="bb48f-128">$.histograms</span><span class="sxs-lookup"><span data-stu-id="bb48f-128">$.histograms</span></span> |  <span data-ttu-id="bb48f-129">Array of histograms, one for each requested attribute.</span><span class="sxs-lookup"><span data-stu-id="bb48f-129">Array of histograms, one for each requested attribute.</span></span>
<span data-ttu-id="bb48f-130">$.histograms[\*].attribute</span><span class="sxs-lookup"><span data-stu-id="bb48f-130">$.histograms[\*].attribute</span></span> | <span data-ttu-id="bb48f-131">Name of the attribute over which the histogram was computed.</span><span class="sxs-lookup"><span data-stu-id="bb48f-131">Name of the attribute over which the histogram was computed.</span></span>
<span data-ttu-id="bb48f-132">$.histograms[\*].distinct_values</span><span class="sxs-lookup"><span data-stu-id="bb48f-132">$.histograms[\*].distinct_values</span></span> | <span data-ttu-id="bb48f-133">Number of distinct values among matching entities for this attribute.</span><span class="sxs-lookup"><span data-stu-id="bb48f-133">Number of distinct values among matching entities for this attribute.</span></span>
<span data-ttu-id="bb48f-134">$.histograms[\*].total_count</span><span class="sxs-lookup"><span data-stu-id="bb48f-134">$.histograms[\*].total_count</span></span> | <span data-ttu-id="bb48f-135">Total number of value instances among matching entities for this attribute.</span><span class="sxs-lookup"><span data-stu-id="bb48f-135">Total number of value instances among matching entities for this attribute.</span></span>
<span data-ttu-id="bb48f-136">$.histograms[\*].histogram</span><span class="sxs-lookup"><span data-stu-id="bb48f-136">$.histograms[\*].histogram</span></span> | <span data-ttu-id="bb48f-137">Histogram data for this attribute.</span><span class="sxs-lookup"><span data-stu-id="bb48f-137">Histogram data for this attribute.</span></span>
<span data-ttu-id="bb48f-138">$.histograms[\*].histogram[\*].value</span><span class="sxs-lookup"><span data-stu-id="bb48f-138">$.histograms[\*].histogram[\*].value</span></span> | <span data-ttu-id="bb48f-139">Attribute value.</span><span class="sxs-lookup"><span data-stu-id="bb48f-139">Attribute value.</span></span>
<span data-ttu-id="bb48f-140">$.histograms[\*].histogram[\*].logprob</span><span class="sxs-lookup"><span data-stu-id="bb48f-140">$.histograms[\*].histogram[\*].logprob</span></span>  | <span data-ttu-id="bb48f-141">Total natural log probability of matching entities with this attribute value.</span><span class="sxs-lookup"><span data-stu-id="bb48f-141">Total natural log probability of matching entities with this attribute value.</span></span>
<span data-ttu-id="bb48f-142">$.histograms[\*].histogram[\*].count</span><span class="sxs-lookup"><span data-stu-id="bb48f-142">$.histograms[\*].histogram[\*].count</span></span>    | <span data-ttu-id="bb48f-143">Number of matching entities with this attribute value.</span><span class="sxs-lookup"><span data-stu-id="bb48f-143">Number of matching entities with this attribute value.</span></span>
<span data-ttu-id="bb48f-144">$.aborted</span><span class="sxs-lookup"><span data-stu-id="bb48f-144">$.aborted</span></span> | <span data-ttu-id="bb48f-145">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="bb48f-145">True if the request timed out.</span></span>

### <a name="example"></a><span data-ttu-id="bb48f-146">Example</span><span class="sxs-lookup"><span data-stu-id="bb48f-146">Example</span></span>
<span data-ttu-id="bb48f-147">In the academic publications example, the following calculates a histogram of publication counts by year and by keyword for a particular author since 2013:</span><span class="sxs-lookup"><span data-stu-id="bb48f-147">In the academic publications example, the following calculates a histogram of publication counts by year and by keyword for a particular author since 2013:</span></span>

`http://<host>/calchistogram?expr=And(Composite(Author.Name=='jaime teevan'),Year>=2013)&attributes=Year,Keyword&count=4`

<span data-ttu-id="bb48f-148">The response indicates that there are 37 papers matching the query expression.</span><span class="sxs-lookup"><span data-stu-id="bb48f-148">The response indicates that there are 37 papers matching the query expression.</span></span>  <span data-ttu-id="bb48f-149">For the *Year* attribute, there are 3 distinct values, one for each year since 2013.</span><span class="sxs-lookup"><span data-stu-id="bb48f-149">For the *Year* attribute, there are 3 distinct values, one for each year since 2013.</span></span>  <span data-ttu-id="bb48f-150">The total paper count over the 3 distinct values is 37.</span><span class="sxs-lookup"><span data-stu-id="bb48f-150">The total paper count over the 3 distinct values is 37.</span></span>  <span data-ttu-id="bb48f-151">For each *Year*, the histogram shows the value, total natural log probability, and count of matching entities.</span><span class="sxs-lookup"><span data-stu-id="bb48f-151">For each *Year*, the histogram shows the value, total natural log probability, and count of matching entities.</span></span>     

<span data-ttu-id="bb48f-152">The histogram for *Keyword* shows that there are 34 distinct keywords.</span><span class="sxs-lookup"><span data-stu-id="bb48f-152">The histogram for *Keyword* shows that there are 34 distinct keywords.</span></span> <span data-ttu-id="bb48f-153">As a paper may be associated with multiple keywords, the total count (53) can be larger than the number of matching entities.</span><span class="sxs-lookup"><span data-stu-id="bb48f-153">As a paper may be associated with multiple keywords, the total count (53) can be larger than the number of matching entities.</span></span>  <span data-ttu-id="bb48f-154">Although there are 34 distinct values, the response only includes the top 4 because of the "count=4" parameter.</span><span class="sxs-lookup"><span data-stu-id="bb48f-154">Although there are 34 distinct values, the response only includes the top 4 because of the "count=4" parameter.</span></span>

```json
{
  "expr": "And(Composite(Author.Name=='jaime teevan'),Y>=2013)",
  "num_entities": 37,
  "histograms": [
    {
      "attribute": "Y",
      "distinct_values": 3,
      "total_count": 37,
      "histogram": [
        {
          "value": 2014,
          "logprob": -6.894,
          "count": 15
        },
        {
          "value": 2013,
          "logprob": -6.927,
          "count": 12
        },
        {
          "value": 2015,
          "logprob": -7.082,
          "count": 10
        }
      ]
    },
    {
      "attribute": "Keyword",
      "distinct_values": 34,
      "total_count": 53,
      "histogram": [
        {
          "value": "crowdsourcing",
          "logprob": -7.142,
          "count": 9
        },
        {
          "value": "information retrieval",
          "logprob": -7.389,
          "count": 4
        },
        {
          "value": "personalization",
          "logprob": -7.623,
          "count": 3
        },
        {
          "value": "mobile search",
          "logprob": -7.674,
          "count": 2
        }
      ]
    }
  ]
}
``` 
