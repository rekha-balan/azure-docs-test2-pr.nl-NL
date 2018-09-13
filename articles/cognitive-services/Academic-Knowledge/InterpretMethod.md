---
title: Interpret method in the Academic Knowledge API | Microsoft Docs
description: Use the Interpret method to return formatted interpretations of user query strings based on Academic Graph data and the Academic Grammar in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: 17f665a1f6f534a9a94b9828061840e42ccf28c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660550"
---
# <a name="interpret-method"></a><span data-ttu-id="2dd3c-103">Interpret Method</span><span class="sxs-lookup"><span data-stu-id="2dd3c-103">Interpret Method</span></span>

<span data-ttu-id="2dd3c-104">The **interpret** REST API takes an end user query string (i.e., a query entered by a user of your application) and returns formatted interpretations of user intent based on the Academic Graph data and the Academic Grammar.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-104">The **interpret** REST API takes an end user query string (i.e., a query entered by a user of your application) and returns formatted interpretations of user intent based on the Academic Graph data and the Academic Grammar.</span></span>

<span data-ttu-id="2dd3c-105">To provide an interactive experience, you can call this method repeatedly after each character entered by the user.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-105">To provide an interactive experience, you can call this method repeatedly after each character entered by the user.</span></span> <span data-ttu-id="2dd3c-106">In that case, you should set the **complete** parameter to 1 to enable auto-complete suggestions.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-106">In that case, you should set the **complete** parameter to 1 to enable auto-complete suggestions.</span></span> <span data-ttu-id="2dd3c-107">If your application does not need auto-completion, you should set the **complete** parameter to 0.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-107">If your application does not need auto-completion, you should set the **complete** parameter to 0.</span></span>

<span data-ttu-id="2dd3c-108">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-108">**REST endpoint:**</span></span>

    https://westus.api.cognitive.microsoft.com/academic/v1.0/interpret?

## <a name="request-parameters"></a><span data-ttu-id="2dd3c-109">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="2dd3c-109">Request Parameters</span></span>

<span data-ttu-id="2dd3c-110">Name</span><span class="sxs-lookup"><span data-stu-id="2dd3c-110">Name</span></span>     | <span data-ttu-id="2dd3c-111">Value</span><span class="sxs-lookup"><span data-stu-id="2dd3c-111">Value</span></span> | <span data-ttu-id="2dd3c-112">Required?</span><span class="sxs-lookup"><span data-stu-id="2dd3c-112">Required?</span></span>  | <span data-ttu-id="2dd3c-113">Description</span><span class="sxs-lookup"><span data-stu-id="2dd3c-113">Description</span></span>
---------|---------|---------|---------
<span data-ttu-id="2dd3c-114">**query**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-114">**query**</span></span>    | <span data-ttu-id="2dd3c-115">Text string</span><span class="sxs-lookup"><span data-stu-id="2dd3c-115">Text string</span></span> | <span data-ttu-id="2dd3c-116">Yes</span><span class="sxs-lookup"><span data-stu-id="2dd3c-116">Yes</span></span> | <span data-ttu-id="2dd3c-117">Query entered by user.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-117">Query entered by user.</span></span>  <span data-ttu-id="2dd3c-118">If complete is set to 1, query will be interpreted as a prefix for generating query auto-completion suggestions.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-118">If complete is set to 1, query will be interpreted as a prefix for generating query auto-completion suggestions.</span></span>        
<span data-ttu-id="2dd3c-119">**model**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-119">**model**</span></span>    | <span data-ttu-id="2dd3c-120">Text string</span><span class="sxs-lookup"><span data-stu-id="2dd3c-120">Text string</span></span> | <span data-ttu-id="2dd3c-121">No</span><span class="sxs-lookup"><span data-stu-id="2dd3c-121">No</span></span>  | <span data-ttu-id="2dd3c-122">Name of the model that you wish to query.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-122">Name of the model that you wish to query.</span></span>  <span data-ttu-id="2dd3c-123">Currently, the value defaults to *latest*.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-123">Currently, the value defaults to *latest*.</span></span>        
<span data-ttu-id="2dd3c-124">**complete**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-124">**complete**</span></span> | <span data-ttu-id="2dd3c-125">0 or 1</span><span class="sxs-lookup"><span data-stu-id="2dd3c-125">0 or 1</span></span> | <span data-ttu-id="2dd3c-126">No</span><span class="sxs-lookup"><span data-stu-id="2dd3c-126">No</span></span><br><span data-ttu-id="2dd3c-127">default:0</span><span class="sxs-lookup"><span data-stu-id="2dd3c-127">default:0</span></span>  | <span data-ttu-id="2dd3c-128">1 means that auto-completion suggestions are generated based on the grammar and graph data.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-128">1 means that auto-completion suggestions are generated based on the grammar and graph data.</span></span>         
<span data-ttu-id="2dd3c-129">**count**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-129">**count**</span></span>    | <span data-ttu-id="2dd3c-130">Number</span><span class="sxs-lookup"><span data-stu-id="2dd3c-130">Number</span></span> | <span data-ttu-id="2dd3c-131">No</span><span class="sxs-lookup"><span data-stu-id="2dd3c-131">No</span></span><br><span data-ttu-id="2dd3c-132">default:10</span><span class="sxs-lookup"><span data-stu-id="2dd3c-132">default:10</span></span> | <span data-ttu-id="2dd3c-133">Maximum number of interpretations to return.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-133">Maximum number of interpretations to return.</span></span>         
<span data-ttu-id="2dd3c-134">**offset**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-134">**offset**</span></span>   | <span data-ttu-id="2dd3c-135">Number</span><span class="sxs-lookup"><span data-stu-id="2dd3c-135">Number</span></span> | <span data-ttu-id="2dd3c-136">No</span><span class="sxs-lookup"><span data-stu-id="2dd3c-136">No</span></span><br><span data-ttu-id="2dd3c-137">default:0</span><span class="sxs-lookup"><span data-stu-id="2dd3c-137">default:0</span></span>  | <span data-ttu-id="2dd3c-138">Index of the first interpretation to return.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-138">Index of the first interpretation to return.</span></span> <span data-ttu-id="2dd3c-139">For example, *count=2&offset=0* returns interpretations 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-139">For example, *count=2&offset=0* returns interpretations 0 and 1.</span></span> <span data-ttu-id="2dd3c-140">*count=2&offset=2* returns interpretations 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-140">*count=2&offset=2* returns interpretations 2 and 3.</span></span>       
<span data-ttu-id="2dd3c-141">**timeout**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-141">**timeout**</span></span>  | <span data-ttu-id="2dd3c-142">Number</span><span class="sxs-lookup"><span data-stu-id="2dd3c-142">Number</span></span> | <span data-ttu-id="2dd3c-143">No</span><span class="sxs-lookup"><span data-stu-id="2dd3c-143">No</span></span><br><span data-ttu-id="2dd3c-144">default:1000</span><span class="sxs-lookup"><span data-stu-id="2dd3c-144">default:1000</span></span> | <span data-ttu-id="2dd3c-145">Timeout in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-145">Timeout in milliseconds.</span></span> <span data-ttu-id="2dd3c-146">Only interpretations found before the timeout has elapsed are returned.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-146">Only interpretations found before the timeout has elapsed are returned.</span></span>
<br>
  
## <a name="response-json"></a><span data-ttu-id="2dd3c-147">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="2dd3c-147">Response (JSON)</span></span>
<span data-ttu-id="2dd3c-148">Name</span><span class="sxs-lookup"><span data-stu-id="2dd3c-148">Name</span></span>     | <span data-ttu-id="2dd3c-149">Description</span><span class="sxs-lookup"><span data-stu-id="2dd3c-149">Description</span></span>
---------|---------
<span data-ttu-id="2dd3c-150">**query**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-150">**query**</span></span> |<span data-ttu-id="2dd3c-151">The *query* parameter from the request.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-151">The *query* parameter from the request.</span></span>
<span data-ttu-id="2dd3c-152">**interpretations**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-152">**interpretations**</span></span> |<span data-ttu-id="2dd3c-153">An array of 0 or more different ways of matching user input against the grammar.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-153">An array of 0 or more different ways of matching user input against the grammar.</span></span>
<span data-ttu-id="2dd3c-154">**interpretations[x].logprob**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-154">**interpretations[x].logprob**</span></span>  |<span data-ttu-id="2dd3c-155">The relative natural log probability of the interpretation.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-155">The relative natural log probability of the interpretation.</span></span> <span data-ttu-id="2dd3c-156">Larger values are more likely.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-156">Larger values are more likely.</span></span>
<span data-ttu-id="2dd3c-157">**interpretations[x].parse**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-157">**interpretations[x].parse**</span></span>  |<span data-ttu-id="2dd3c-158">An XML string that shows how each part of the query was interpreted.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-158">An XML string that shows how each part of the query was interpreted.</span></span>
<span data-ttu-id="2dd3c-159">**interpretations[x].rules**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-159">**interpretations[x].rules**</span></span>  |<span data-ttu-id="2dd3c-160">An array of 1 or more rules defined in the grammar that were invoked during interpretation.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-160">An array of 1 or more rules defined in the grammar that were invoked during interpretation.</span></span> <span data-ttu-id="2dd3c-161">For the Academic Knowledge API, there will always be 1 rule.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-161">For the Academic Knowledge API, there will always be 1 rule.</span></span>
<span data-ttu-id="2dd3c-162">**interpretations[x].rules[y].name**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-162">**interpretations[x].rules[y].name**</span></span>  |<span data-ttu-id="2dd3c-163">Name of the rule.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-163">Name of the rule.</span></span>
<span data-ttu-id="2dd3c-164">**interpretations[x].rules[y].output**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-164">**interpretations[x].rules[y].output**</span></span>  |<span data-ttu-id="2dd3c-165">Output of the rule.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-165">Output of the rule.</span></span>
<span data-ttu-id="2dd3c-166">**interpretations[x].rules[y].output.type**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-166">**interpretations[x].rules[y].output.type**</span></span> |<span data-ttu-id="2dd3c-167">The data type of the output of the rule.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-167">The data type of the output of the rule.</span></span>  <span data-ttu-id="2dd3c-168">For the Academic Knowledge API, this will always be "query".</span><span class="sxs-lookup"><span data-stu-id="2dd3c-168">For the Academic Knowledge API, this will always be "query".</span></span>
<span data-ttu-id="2dd3c-169">**interpretations[x].rules[y].output.value**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-169">**interpretations[x].rules[y].output.value**</span></span>  |<span data-ttu-id="2dd3c-170">The output of the rule.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-170">The output of the rule.</span></span> <span data-ttu-id="2dd3c-171">For the Academic Knowledge API, this is a query expression string that can be passed to the evaluate and calchistogram methods.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-171">For the Academic Knowledge API, this is a query expression string that can be passed to the evaluate and calchistogram methods.</span></span>
<span data-ttu-id="2dd3c-172">**aborted**</span><span class="sxs-lookup"><span data-stu-id="2dd3c-172">**aborted**</span></span> | <span data-ttu-id="2dd3c-173">True if the request timed out.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-173">True if the request timed out.</span></span>

<br>
#### <a name="example"></a><span data-ttu-id="2dd3c-174">Example:</span><span class="sxs-lookup"><span data-stu-id="2dd3c-174">Example:</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/interpret?query=papers by jaime&complete=1&count=2
 ```
<br><span data-ttu-id="2dd3c-175">The response below contains the top two (because of the parameter *count=2*) most likely interpretations that complete the partial user input *papers by jaime*: *papers by jaime teevan* and *papers by jaime green*.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-175">The response below contains the top two (because of the parameter *count=2*) most likely interpretations that complete the partial user input *papers by jaime*: *papers by jaime teevan* and *papers by jaime green*.</span></span>  <span data-ttu-id="2dd3c-176">The service generated query completions instead of considering only exact matches for the author *jaime* because the request specified *complete=1*.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-176">The service generated query completions instead of considering only exact matches for the author *jaime* because the request specified *complete=1*.</span></span> <span data-ttu-id="2dd3c-177">Note that the canonical value *j l green* matched via the synonym *jamie green*, as indicated in the parse.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-177">Note that the canonical value *j l green* matched via the synonym *jamie green*, as indicated in the parse.</span></span>


```JSON
{
  "query": "papers by jaime",
  "interpretations": [
    {
      "logprob": -12.728,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#AA.AuN\">jaime teevan</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(AA.AuN=='jaime teevan')"
          }
        }
      ]
    },
    {
      "logprob": -12.774,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#AA.AuN\" canonical=\"j l green\">jaime green</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(AA.AuN=='j l green')"
          }
        }
      ]
    }
  ]
}
```  
<br><span data-ttu-id="2dd3c-178">To retrieve entity results for an interpretation, use *output.value* from the **interpret** API, and pass that into the **evaluate** API via the *expr* parameter.</span><span class="sxs-lookup"><span data-stu-id="2dd3c-178">To retrieve entity results for an interpretation, use *output.value* from the **interpret** API, and pass that into the **evaluate** API via the *expr* parameter.</span></span> <span data-ttu-id="2dd3c-179">In this example, the query for the first interpretation is:</span><span class="sxs-lookup"><span data-stu-id="2dd3c-179">In this example, the query for the first interpretation is:</span></span> 
```
evaluate?expr=Composite(AA.AuN=='jaime teevan')
```
 