---
title: CalcHistogram method in the Academic Knowledge API | Microsoft Docs
description: Use the CalcHistogram method to calculate the distribution of attribute values for a set of paper entities in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: e0b773fb9791ee638c8cfdbbc9dca40543e50ec0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827307"
---
# <a name="calchistogram-method"></a><span data-ttu-id="6ae4a-103">CalcHistogram Method</span><span class="sxs-lookup"><span data-stu-id="6ae4a-103">CalcHistogram Method</span></span>

<span data-ttu-id="6ae4a-104">The **calchistogram** REST API is used to calculate the distribution of attribute values for a set of paper entities.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-104">The **calchistogram** REST API is used to calculate the distribution of attribute values for a set of paper entities.</span></span>          


<span data-ttu-id="6ae4a-105">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-105">**REST endpoint:**</span></span>
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?
``` 
<br>
  
## <a name="request-parameters"></a><span data-ttu-id="6ae4a-106">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="6ae4a-106">Request Parameters</span></span>

<span data-ttu-id="6ae4a-107">Name</span><span class="sxs-lookup"><span data-stu-id="6ae4a-107">Name</span></span>  |<span data-ttu-id="6ae4a-108">Value</span><span class="sxs-lookup"><span data-stu-id="6ae4a-108">Value</span></span> | <span data-ttu-id="6ae4a-109">Required?</span><span class="sxs-lookup"><span data-stu-id="6ae4a-109">Required?</span></span>  |<span data-ttu-id="6ae4a-110">Description</span><span class="sxs-lookup"><span data-stu-id="6ae4a-110">Description</span></span>
-----------|----------|--------|----------
<span data-ttu-id="6ae4a-111">**expr**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-111">**expr**</span></span>    |<span data-ttu-id="6ae4a-112">Text string</span><span class="sxs-lookup"><span data-stu-id="6ae4a-112">Text string</span></span> | <span data-ttu-id="6ae4a-113">Yes</span><span class="sxs-lookup"><span data-stu-id="6ae4a-113">Yes</span></span>  |<span data-ttu-id="6ae4a-114">A query expression that specifies the entities over which to calculate histograms.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-114">A query expression that specifies the entities over which to calculate histograms.</span></span>
<span data-ttu-id="6ae4a-115">**model**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-115">**model**</span></span> |<span data-ttu-id="6ae4a-116">Text string</span><span class="sxs-lookup"><span data-stu-id="6ae4a-116">Text string</span></span> | <span data-ttu-id="6ae4a-117">No</span><span class="sxs-lookup"><span data-stu-id="6ae4a-117">No</span></span> |<span data-ttu-id="6ae4a-118">Select the name of the model that you wish to query.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-118">Select the name of the model that you wish to query.</span></span>  <span data-ttu-id="6ae4a-119">Currently, the value defaults to *latest*.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-119">Currently, the value defaults to *latest*.</span></span>
<span data-ttu-id="6ae4a-120">**attributes**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-120">**attributes**</span></span> | <span data-ttu-id="6ae4a-121">Text string</span><span class="sxs-lookup"><span data-stu-id="6ae4a-121">Text string</span></span> | <span data-ttu-id="6ae4a-122">No</span><span class="sxs-lookup"><span data-stu-id="6ae4a-122">No</span></span><br><span data-ttu-id="6ae4a-123">default:</span><span class="sxs-lookup"><span data-stu-id="6ae4a-123">default:</span></span> | <span data-ttu-id="6ae4a-124">A comma-delimited list that specifies the attribute values that are included in the response.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-124">A comma-delimited list that specifies the attribute values that are included in the response.</span></span> <span data-ttu-id="6ae4a-125">Attribute names are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-125">Attribute names are case-sensitive.</span></span>
<span data-ttu-id="6ae4a-126">**count**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-126">**count**</span></span> |<span data-ttu-id="6ae4a-127">Number</span><span class="sxs-lookup"><span data-stu-id="6ae4a-127">Number</span></span> | <span data-ttu-id="6ae4a-128">No</span><span class="sxs-lookup"><span data-stu-id="6ae4a-128">No</span></span><br><span data-ttu-id="6ae4a-129">Default: 10</span><span class="sxs-lookup"><span data-stu-id="6ae4a-129">Default: 10</span></span> |<span data-ttu-id="6ae4a-130">Number of results to return.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-130">Number of results to return.</span></span>
<span data-ttu-id="6ae4a-131">**offset**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-131">**offset**</span></span>  |<span data-ttu-id="6ae4a-132">Number</span><span class="sxs-lookup"><span data-stu-id="6ae4a-132">Number</span></span> | <span data-ttu-id="6ae4a-133">No</span><span class="sxs-lookup"><span data-stu-id="6ae4a-133">No</span></span><br><span data-ttu-id="6ae4a-134">Default: 0</span><span class="sxs-lookup"><span data-stu-id="6ae4a-134">Default: 0</span></span> |<span data-ttu-id="6ae4a-135">Index of the first result to return.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-135">Index of the first result to return.</span></span>
<br>
## <a name="response-json"></a><span data-ttu-id="6ae4a-136">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="6ae4a-136">Response (JSON)</span></span>
<span data-ttu-id="6ae4a-137">Name</span><span class="sxs-lookup"><span data-stu-id="6ae4a-137">Name</span></span> | <span data-ttu-id="6ae4a-138">Description</span><span class="sxs-lookup"><span data-stu-id="6ae4a-138">Description</span></span>
--------|---------
<span data-ttu-id="6ae4a-139">**expr**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-139">**expr**</span></span>  |<span data-ttu-id="6ae4a-140">The expr parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-140">The expr parameter from the request.</span></span>
<span data-ttu-id="6ae4a-141">**num_entities**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-141">**num_entities**</span></span> | <span data-ttu-id="6ae4a-142">Total number of matching entities.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-142">Total number of matching entities.</span></span>
<span data-ttu-id="6ae4a-143">**histograms**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-143">**histograms**</span></span> |  <span data-ttu-id="6ae4a-144">An array of histograms, one for each attribute specified in the request.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-144">An array of histograms, one for each attribute specified in the request.</span></span>
<span data-ttu-id="6ae4a-145">**histograms[x].attribute**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-145">**histograms[x].attribute**</span></span> | <span data-ttu-id="6ae4a-146">Name of the attribute over which the histogram was computed.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-146">Name of the attribute over which the histogram was computed.</span></span>
<span data-ttu-id="6ae4a-147">**histograms[x].distinct_values**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-147">**histograms[x].distinct_values**</span></span> | <span data-ttu-id="6ae4a-148">Number of distinct values among matching entities for this attribute.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-148">Number of distinct values among matching entities for this attribute.</span></span>
<span data-ttu-id="6ae4a-149">**histograms[x].total_count**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-149">**histograms[x].total_count**</span></span> | <span data-ttu-id="6ae4a-150">Total number of value instances among matching entities for this attribute.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-150">Total number of value instances among matching entities for this attribute.</span></span>
<span data-ttu-id="6ae4a-151">**histograms[x].histogram**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-151">**histograms[x].histogram**</span></span> | <span data-ttu-id="6ae4a-152">Histogram data for this attribute.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-152">Histogram data for this attribute.</span></span>
<span data-ttu-id="6ae4a-153">**histograms[x].histogram[y].value**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-153">**histograms[x].histogram[y].value**</span></span> |  <span data-ttu-id="6ae4a-154">A value for the attribute.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-154">A value for the attribute.</span></span>
<span data-ttu-id="6ae4a-155">**histograms[x].histogram[y].logprob**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-155">**histograms[x].histogram[y].logprob**</span></span>  |<span data-ttu-id="6ae4a-156">Total natural log probability of matching entities with this attribute value.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-156">Total natural log probability of matching entities with this attribute value.</span></span>
<span data-ttu-id="6ae4a-157">**histograms[x].histogram[y].count**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-157">**histograms[x].histogram[y].count**</span></span>  |<span data-ttu-id="6ae4a-158">Number of matching entities with this attribute value.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-158">Number of matching entities with this attribute value.</span></span>
<span data-ttu-id="6ae4a-159">**aborted**</span><span class="sxs-lookup"><span data-stu-id="6ae4a-159">**aborted**</span></span> | <span data-ttu-id="6ae4a-160">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-160">True if the request timed out.</span></span>

 <br>
#### <a name="example"></a><span data-ttu-id="6ae4a-161">Example:</span><span class="sxs-lookup"><span data-stu-id="6ae4a-161">Example:</span></span>
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?expr=And(Composite(AA.AuN=='jaime teevan'),Y>2012)&attributes=Y,F.FN&count=4
```
<br><span data-ttu-id="6ae4a-162">In this example, in order to generate a histogram of the count of publications by year for a particular author since 2010, we can first generate the query expression using the **interpret** API with query string: *papers by jaime teevan after 2012*.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-162">In this example, in order to generate a histogram of the count of publications by year for a particular author since 2010, we can first generate the query expression using the **interpret** API with query string: *papers by jaime teevan after 2012*.</span></span>

```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/interpret?query=papers by jaime teevan after 2012
```
<br><span data-ttu-id="6ae4a-163">The expression in the first interpretation that is returned from the interpret API is *And(Composite(AA.AuN=='jaime teevan'),Y>2012)*.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-163">The expression in the first interpretation that is returned from the interpret API is *And(Composite(AA.AuN=='jaime teevan'),Y>2012)*.</span></span>
<br><span data-ttu-id="6ae4a-164">This expression value is then passed in to the **calchistogram** API.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-164">This expression value is then passed in to the **calchistogram** API.</span></span> <span data-ttu-id="6ae4a-165">The *attributes=Y,F.FN* parameter indicates that the distributions of paper counts should be by Year and Field of Study, e.g.:</span><span class="sxs-lookup"><span data-stu-id="6ae4a-165">The *attributes=Y,F.FN* parameter indicates that the distributions of paper counts should be by Year and Field of Study, e.g.:</span></span>
```
https:// westus.api.cognitive.microsoft.com/academic/v1.0/calchistogram?expr=And(Composite(AA.AuN=='jaime teevan'),Y>2012)&attributes=Y,F.FN&count=4
```
<br><span data-ttu-id="6ae4a-166">The response to this request first indicates that there are 37 papers that match the query expression.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-166">The response to this request first indicates that there are 37 papers that match the query expression.</span></span>  <span data-ttu-id="6ae4a-167">For the *Year* attribute, there are 3 distinct values, one for each year after 2012 (i.e. 2013, 2014, and 2015) as specified in the query.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-167">For the *Year* attribute, there are 3 distinct values, one for each year after 2012 (i.e. 2013, 2014, and 2015) as specified in the query.</span></span>  <span data-ttu-id="6ae4a-168">The total paper count over the 3 distinct values is 37.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-168">The total paper count over the 3 distinct values is 37.</span></span>  <span data-ttu-id="6ae4a-169">For each *Year*, the histogram shows the value, total natural log probability, and count of matching entities.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-169">For each *Year*, the histogram shows the value, total natural log probability, and count of matching entities.</span></span>     

<span data-ttu-id="6ae4a-170">The histogram for *Field of Study* shows that there are 34 distinct fields of study.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-170">The histogram for *Field of Study* shows that there are 34 distinct fields of study.</span></span> <span data-ttu-id="6ae4a-171">As a paper may be associated with multiple fields of study, the total count (53) can be larger than the number of matching entities.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-171">As a paper may be associated with multiple fields of study, the total count (53) can be larger than the number of matching entities.</span></span>  <span data-ttu-id="6ae4a-172">Although there are 34 distinct values, the response only includes the top 4 because of the *count=4* parameter.</span><span class="sxs-lookup"><span data-stu-id="6ae4a-172">Although there are 34 distinct values, the response only includes the top 4 because of the *count=4* parameter.</span></span>

```JSON
{
  "expr": "And(Composite(AA.AuN=='jaime teevan'),Y>2012)",
  "num_entities": 37,
  "histograms": [
    {
      "attribute": "Y",
      "distinct_values": 3,
      "total_count": 37,
      "histogram": [
        {
          "value": 2014,
          "logprob": -15.753,
          "count": 15
        },
        {
          "value": 2013,
          "logprob": -15.805,
          "count": 12
        },
        {
          "value": 2015,
          "logprob": -16.035,
          "count": 10
        }
      ]
    },
    {
      "attribute": "F.FN",
      "distinct_values": 34,
      "total_count": 53,
      "histogram": [
        {
          "value": "crowdsourcing",
          "logprob": -15.258,
          "count": 9
        },
        {
          "value": "information retrieval",
          "logprob": -16.002,
          "count": 4
        },
        {
          "value": "personalization",
          "logprob": -16.226,
          "count": 3
        },
        {
          "value": "mobile search",
          "logprob": -17.228,
          "count": 2
        }
      ]
    }
  ]
}
```
