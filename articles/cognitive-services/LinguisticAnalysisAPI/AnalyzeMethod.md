---
title: Analyze method in the Linguistic Analysis API | Microsoft Docs
description: How to use the Analyze method in Linguistic Analysis API to analyze certain natural-language inputs.
services: cognitive-services
author: RichardSunMS
manager: wkwok
ms.service: cognitive-services
ms.technology: linguistic-analysis-api
ms.topic: article
ms.date: 12/13/2016
ms.author: lesun
ms.openlocfilehash: cad9d8a63ce5cad8cafde70faddf3580c347849a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555040"
---
# <a name="analyze-method"></a><span data-ttu-id="59db1-103">Analyze Method</span><span class="sxs-lookup"><span data-stu-id="59db1-103">Analyze Method</span></span>

<span data-ttu-id="59db1-104">The **analyze** REST API is used to analyze a given natural language input.</span><span class="sxs-lookup"><span data-stu-id="59db1-104">The **analyze** REST API is used to analyze a given natural language input.</span></span>
<span data-ttu-id="59db1-105">That might involve just finding the [sentences and tokens](Sentences-and-Tokens.md) within that input, finding the [part-of-speech tags](POS-tagging.md), or finding the [constitutency tree](Constituency-Parsing.md).</span><span class="sxs-lookup"><span data-stu-id="59db1-105">That might involve just finding the [sentences and tokens](Sentences-and-Tokens.md) within that input, finding the [part-of-speech tags](POS-tagging.md), or finding the [constitutency tree](Constituency-Parsing.md).</span></span>
<span data-ttu-id="59db1-106">You can specify which results you want by picking the relevant analyzers.</span><span class="sxs-lookup"><span data-stu-id="59db1-106">You can specify which results you want by picking the relevant analyzers.</span></span>
<span data-ttu-id="59db1-107">To list all available analyzers, look at the **[analyzers](AnalyzersMethod.md)**.</span><span class="sxs-lookup"><span data-stu-id="59db1-107">To list all available analyzers, look at the **[analyzers](AnalyzersMethod.md)**.</span></span>

<span data-ttu-id="59db1-108">Note that you need to specify the language of the input string.</span><span class="sxs-lookup"><span data-stu-id="59db1-108">Note that you need to specify the language of the input string.</span></span>

<span data-ttu-id="59db1-109">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="59db1-109">**REST endpoint:**</span></span>
```
https://westus.api.cognitive.microsoft.com/linguistics/v1.0/analyze
```
<br>

## <a name="request-parameters"></a><span data-ttu-id="59db1-110">Request parameters</span><span class="sxs-lookup"><span data-stu-id="59db1-110">Request parameters</span></span>

<span data-ttu-id="59db1-111">Name</span><span class="sxs-lookup"><span data-stu-id="59db1-111">Name</span></span> | <span data-ttu-id="59db1-112">Type</span><span class="sxs-lookup"><span data-stu-id="59db1-112">Type</span></span> | <span data-ttu-id="59db1-113">Required</span><span class="sxs-lookup"><span data-stu-id="59db1-113">Required</span></span> | <span data-ttu-id="59db1-114">Description</span><span class="sxs-lookup"><span data-stu-id="59db1-114">Description</span></span>
-----|-------|----------|------------
<span data-ttu-id="59db1-115">**language**</span><span class="sxs-lookup"><span data-stu-id="59db1-115">**language**</span></span>    | <span data-ttu-id="59db1-116">string</span><span class="sxs-lookup"><span data-stu-id="59db1-116">string</span></span> | <span data-ttu-id="59db1-117">Yes</span><span class="sxs-lookup"><span data-stu-id="59db1-117">Yes</span></span> | <span data-ttu-id="59db1-118">The two letter ISO language code to be used for analysis.</span><span class="sxs-lookup"><span data-stu-id="59db1-118">The two letter ISO language code to be used for analysis.</span></span> <span data-ttu-id="59db1-119">For instance, English is "en".</span><span class="sxs-lookup"><span data-stu-id="59db1-119">For instance, English is "en".</span></span>
<span data-ttu-id="59db1-120">**analyzerIds**</span><span class="sxs-lookup"><span data-stu-id="59db1-120">**analyzerIds**</span></span> | <span data-ttu-id="59db1-121">list of strings</span><span class="sxs-lookup"><span data-stu-id="59db1-121">list of strings</span></span> | <span data-ttu-id="59db1-122">Yes</span><span class="sxs-lookup"><span data-stu-id="59db1-122">Yes</span></span> | <span data-ttu-id="59db1-123">List of GUIDs of analyzers to apply.</span><span class="sxs-lookup"><span data-stu-id="59db1-123">List of GUIDs of analyzers to apply.</span></span> <span data-ttu-id="59db1-124">See the Analyzers documentation for more information.</span><span class="sxs-lookup"><span data-stu-id="59db1-124">See the Analyzers documentation for more information.</span></span>
<span data-ttu-id="59db1-125">**text**</span><span class="sxs-lookup"><span data-stu-id="59db1-125">**text**</span></span>        | <span data-ttu-id="59db1-126">string</span><span class="sxs-lookup"><span data-stu-id="59db1-126">string</span></span> | <span data-ttu-id="59db1-127">Yes</span><span class="sxs-lookup"><span data-stu-id="59db1-127">Yes</span></span> | <span data-ttu-id="59db1-128">Raw input to be analyzed.</span><span class="sxs-lookup"><span data-stu-id="59db1-128">Raw input to be analyzed.</span></span> <span data-ttu-id="59db1-129">This might be a short string such as a word or phrase, a full sentence, or a full paragraph or discourse.</span><span class="sxs-lookup"><span data-stu-id="59db1-129">This might be a short string such as a word or phrase, a full sentence, or a full paragraph or discourse.</span></span>

<br>
## <a name="response-json"></a><span data-ttu-id="59db1-130">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="59db1-130">Response (JSON)</span></span>
<span data-ttu-id="59db1-131">An array of analysis outputs, one for each attribute specified in the request.</span><span class="sxs-lookup"><span data-stu-id="59db1-131">An array of analysis outputs, one for each attribute specified in the request.</span></span>

<span data-ttu-id="59db1-132">The results look as follows:</span><span class="sxs-lookup"><span data-stu-id="59db1-132">The results look as follows:</span></span>

<span data-ttu-id="59db1-133">Name</span><span class="sxs-lookup"><span data-stu-id="59db1-133">Name</span></span> | <span data-ttu-id="59db1-134">Type</span><span class="sxs-lookup"><span data-stu-id="59db1-134">Type</span></span> | <span data-ttu-id="59db1-135">Description</span><span class="sxs-lookup"><span data-stu-id="59db1-135">Description</span></span>
-----|------|--------------
<span data-ttu-id="59db1-136">analyzerId</span><span class="sxs-lookup"><span data-stu-id="59db1-136">analyzerId</span></span> | <span data-ttu-id="59db1-137">string</span><span class="sxs-lookup"><span data-stu-id="59db1-137">string</span></span> | <span data-ttu-id="59db1-138">GUID of the analyzer specified</span><span class="sxs-lookup"><span data-stu-id="59db1-138">GUID of the analyzer specified</span></span>
<span data-ttu-id="59db1-139">result</span><span class="sxs-lookup"><span data-stu-id="59db1-139">result</span></span> | <span data-ttu-id="59db1-140">object</span><span class="sxs-lookup"><span data-stu-id="59db1-140">object</span></span> | <span data-ttu-id="59db1-141">analyzer result</span><span class="sxs-lookup"><span data-stu-id="59db1-141">analyzer result</span></span>

<span data-ttu-id="59db1-142">Note that the type of the result depends on the input analyzer type.</span><span class="sxs-lookup"><span data-stu-id="59db1-142">Note that the type of the result depends on the input analyzer type.</span></span>

### <a name="tokens-response-json"></a><span data-ttu-id="59db1-143">Tokens Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="59db1-143">Tokens Response (JSON)</span></span>

<span data-ttu-id="59db1-144">Name</span><span class="sxs-lookup"><span data-stu-id="59db1-144">Name</span></span> | <span data-ttu-id="59db1-145">Type</span><span class="sxs-lookup"><span data-stu-id="59db1-145">Type</span></span> | <span data-ttu-id="59db1-146">Description</span><span class="sxs-lookup"><span data-stu-id="59db1-146">Description</span></span>
-----|------|-------------
<span data-ttu-id="59db1-147">result</span><span class="sxs-lookup"><span data-stu-id="59db1-147">result</span></span> | <span data-ttu-id="59db1-148">list of sentence objects</span><span class="sxs-lookup"><span data-stu-id="59db1-148">list of sentence objects</span></span> | <span data-ttu-id="59db1-149">sentence boundaries identified within the text</span><span class="sxs-lookup"><span data-stu-id="59db1-149">sentence boundaries identified within the text</span></span> |
<span data-ttu-id="59db1-150">result[x].Offset</span><span class="sxs-lookup"><span data-stu-id="59db1-150">result[x].Offset</span></span> | <span data-ttu-id="59db1-151">int</span><span class="sxs-lookup"><span data-stu-id="59db1-151">int</span></span> | <span data-ttu-id="59db1-152">starting character offset of each sentence</span><span class="sxs-lookup"><span data-stu-id="59db1-152">starting character offset of each sentence</span></span> |
<span data-ttu-id="59db1-153">result[x].Len</span><span class="sxs-lookup"><span data-stu-id="59db1-153">result[x].Len</span></span> | <span data-ttu-id="59db1-154">int</span><span class="sxs-lookup"><span data-stu-id="59db1-154">int</span></span> | <span data-ttu-id="59db1-155">length in characters of each sentence</span><span class="sxs-lookup"><span data-stu-id="59db1-155">length in characters of each sentence</span></span> |
<span data-ttu-id="59db1-156">result[x].Tokens</span><span class="sxs-lookup"><span data-stu-id="59db1-156">result[x].Tokens</span></span> | <span data-ttu-id="59db1-157">list of token objects</span><span class="sxs-lookup"><span data-stu-id="59db1-157">list of token objects</span></span> | <span data-ttu-id="59db1-158">token boundaries identified within the sentence</span><span class="sxs-lookup"><span data-stu-id="59db1-158">token boundaries identified within the sentence</span></span> |
<span data-ttu-id="59db1-159">result[x].Tokens[y].Offset</span><span class="sxs-lookup"><span data-stu-id="59db1-159">result[x].Tokens[y].Offset</span></span> | <span data-ttu-id="59db1-160">int</span><span class="sxs-lookup"><span data-stu-id="59db1-160">int</span></span> | <span data-ttu-id="59db1-161">starting character offset of the token</span><span class="sxs-lookup"><span data-stu-id="59db1-161">starting character offset of the token</span></span> |
<span data-ttu-id="59db1-162">result[x].Tokens[y].Len</span><span class="sxs-lookup"><span data-stu-id="59db1-162">result[x].Tokens[y].Len</span></span> | <span data-ttu-id="59db1-163">int</span><span class="sxs-lookup"><span data-stu-id="59db1-163">int</span></span> | <span data-ttu-id="59db1-164">length in characters of the token</span><span class="sxs-lookup"><span data-stu-id="59db1-164">length in characters of the token</span></span> |
<span data-ttu-id="59db1-165">result[x].Tokens[y].RawToken</span><span class="sxs-lookup"><span data-stu-id="59db1-165">result[x].Tokens[y].RawToken</span></span> | <span data-ttu-id="59db1-166">string</span><span class="sxs-lookup"><span data-stu-id="59db1-166">string</span></span> | <span data-ttu-id="59db1-167">the characters inside that token, before normalization</span><span class="sxs-lookup"><span data-stu-id="59db1-167">the characters inside that token, before normalization</span></span> |
<span data-ttu-id="59db1-168">result[x].Tokens[y].NormalizedToken</span><span class="sxs-lookup"><span data-stu-id="59db1-168">result[x].Tokens[y].NormalizedToken</span></span> | <span data-ttu-id="59db1-169">string</span><span class="sxs-lookup"><span data-stu-id="59db1-169">string</span></span> | <span data-ttu-id="59db1-170">a normalized form of the character, safe for use in a [parse tree](Constituency-Parsing.md); for instance, an open parenthesis character '(' becomes '-LRB-'</span><span class="sxs-lookup"><span data-stu-id="59db1-170">a normalized form of the character, safe for use in a [parse tree](Constituency-Parsing.md); for instance, an open parenthesis character '(' becomes '-LRB-'</span></span> |

<span data-ttu-id="59db1-171">Example input: \`This is a test.</span><span class="sxs-lookup"><span data-stu-id="59db1-171">Example input: \`This is a test.</span></span> <span data-ttu-id="59db1-172">Hello.'</span><span class="sxs-lookup"><span data-stu-id="59db1-172">Hello.'</span></span>
<span data-ttu-id="59db1-173">Example JSON response:</span><span class="sxs-lookup"><span data-stu-id="59db1-173">Example JSON response:</span></span>
```json
[
  {
    "Len": 15,
    "Offset": 0,
    "Tokens": [
      {
        "Len": 4,
        "NormalizedToken": "This",
        "Offset": 0,
        "RawToken": "This"
      },
      {
        "Len": 2,
        "NormalizedToken": "is",
        "Offset": 5,
        "RawToken": "is"
      },
      {
        "Len": 1,
        "NormalizedToken": "a",
        "Offset": 8,
        "RawToken": "a"
      },
      {
        "Len": 4,
        "NormalizedToken": "test",
        "Offset": 10,
        "RawToken": "test"
      },
      {
        "Len": 1,
        "NormalizedToken": ".",
        "Offset": 14,
        "RawToken": "."
      }
    ]
  },
  {
    "Len": 6,
    "Offset": 16,
    "Tokens": [
      {
        "Len": 5,
        "NormalizedToken": "Hello",
        "Offset": 16,
        "RawToken": "Hello"
      },
      {
        "Len": 1,
        "NormalizedToken": ".",
        "Offset": 21,
        "RawToken": "."
      }
    ]
  }
]
```


### <a name="pos-tags-response-json"></a><span data-ttu-id="59db1-174">POS Tags Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="59db1-174">POS Tags Response (JSON)</span></span>

<span data-ttu-id="59db1-175">The result is list of lists of strings.</span><span class="sxs-lookup"><span data-stu-id="59db1-175">The result is list of lists of strings.</span></span>
<span data-ttu-id="59db1-176">For each sentence, there is a list of POS tags, one POS tag for each token.</span><span class="sxs-lookup"><span data-stu-id="59db1-176">For each sentence, there is a list of POS tags, one POS tag for each token.</span></span>
<span data-ttu-id="59db1-177">To find the token corresponding to each POS tag, you'll want to ask for a tokenization object as well.</span><span class="sxs-lookup"><span data-stu-id="59db1-177">To find the token corresponding to each POS tag, you'll want to ask for a tokenization object as well.</span></span>

### <a name="constituency-tree-response-json"></a><span data-ttu-id="59db1-178">Constituency Tree Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="59db1-178">Constituency Tree Response (JSON)</span></span>

<span data-ttu-id="59db1-179">The result is a list of strings, one parse tree for each sentence found in the input.</span><span class="sxs-lookup"><span data-stu-id="59db1-179">The result is a list of strings, one parse tree for each sentence found in the input.</span></span>
<span data-ttu-id="59db1-180">The parse trees are represented in a parenthesized form.</span><span class="sxs-lookup"><span data-stu-id="59db1-180">The parse trees are represented in a parenthesized form.</span></span>

<br>

## <a name="example"></a><span data-ttu-id="59db1-181">Example</span><span class="sxs-lookup"><span data-stu-id="59db1-181">Example</span></span>

`POST /analyze`

<span data-ttu-id="59db1-182">Request Body: JSON payload</span><span class="sxs-lookup"><span data-stu-id="59db1-182">Request Body: JSON payload</span></span>
```json
{
  "language": "en",
  "analyzerIds": [
    "4FA79AF1-F22C-408D-98BB-B7D7AEEF7F04",
    "22A6B758-420F-4745-8A3C-46835A67C0D2" ],
  "text": "Hi, Tom! How are you today?" 
}
```

<span data-ttu-id="59db1-183">Response: JSON</span><span class="sxs-lookup"><span data-stu-id="59db1-183">Response: JSON</span></span>
```json
[
  {
    "analyzerId": "4FA79AF1-F22C-408D-98BB-B7D7AEEF7F04", 
    "result": [ ["NNP",",","NNP","."], ["WRB","VBP","PRP","NN","."] ]
  },
  {
    "analyzerId": "22A6B758-420F-4745-8A3C-46835A67C0D2", 
    "result":["(TOP (S (NNP Hi) (, ,) (NNP Tom) (. !)))","(TOP (SBARQ (WHADVP (WRB How)) (SQ (VP (VBP are)) (NP (PRP you)) (NN today) (. ?))))"]
  }
]
```

