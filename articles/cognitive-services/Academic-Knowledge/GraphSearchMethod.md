---
title: Graph Search method in the Academic Knowledge API | Microsoft Docs
description: Use the Graph Search method in the Academic Knowledge API to return a set of academic entities based on specific graph patterns in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 9f519daa0f782e9b13a134f0f67d00f3078a7e5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551795"
---
# <a name="graph-search-method"></a><span data-ttu-id="74320-103">Graph Search Method</span><span class="sxs-lookup"><span data-stu-id="74320-103">Graph Search Method</span></span>

<span data-ttu-id="74320-104">The **graph search** REST API is used to return a set of academic entities based on the given graph patterns.</span><span class="sxs-lookup"><span data-stu-id="74320-104">The **graph search** REST API is used to return a set of academic entities based on the given graph patterns.</span></span>  <span data-ttu-id="74320-105">The response is a set of graph paths satisfying the user-specified constraints.</span><span class="sxs-lookup"><span data-stu-id="74320-105">The response is a set of graph paths satisfying the user-specified constraints.</span></span> <span data-ttu-id="74320-106">A graph path is an interleaved sequence of graph nodes and edges in the form of _v0, e0, v1, e1, ..., vn_, where _v0_ is the starting node of the path.</span><span class="sxs-lookup"><span data-stu-id="74320-106">A graph path is an interleaved sequence of graph nodes and edges in the form of _v0, e0, v1, e1, ..., vn_, where _v0_ is the starting node of the path.</span></span>
<br>

<span data-ttu-id="74320-107">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="74320-107">**REST endpoint:**</span></span>  
```
https://westus.api.cognitive.microsoft.com/academic/graph/v1.0/search?
```   
<br>

## <a name="request-parameters"></a><span data-ttu-id="74320-108">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="74320-108">Request Parameters</span></span>  
<span data-ttu-id="74320-109">Name</span><span class="sxs-lookup"><span data-stu-id="74320-109">Name</span></span>     | <span data-ttu-id="74320-110">Value</span><span class="sxs-lookup"><span data-stu-id="74320-110">Value</span></span> | <span data-ttu-id="74320-111">Required?</span><span class="sxs-lookup"><span data-stu-id="74320-111">Required?</span></span>  | <span data-ttu-id="74320-112">Description</span><span class="sxs-lookup"><span data-stu-id="74320-112">Description</span></span>
-----------|-----------|---------|--------
<span data-ttu-id="74320-113">**mode**</span><span class="sxs-lookup"><span data-stu-id="74320-113">**mode**</span></span>       | <span data-ttu-id="74320-114">Text string</span><span class="sxs-lookup"><span data-stu-id="74320-114">Text string</span></span> | <span data-ttu-id="74320-115">Yes</span><span class="sxs-lookup"><span data-stu-id="74320-115">Yes</span></span> | <span data-ttu-id="74320-116">Name of the mode that you wish to use.</span><span class="sxs-lookup"><span data-stu-id="74320-116">Name of the mode that you wish to use.</span></span> <span data-ttu-id="74320-117">The value is either *json* or *lambda*.</span><span class="sxs-lookup"><span data-stu-id="74320-117">The value is either *json* or *lambda*.</span></span>

<span data-ttu-id="74320-118">The graph search method must be called via an HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="74320-118">The graph search method must be called via an HTTP POST request.</span></span> <span data-ttu-id="74320-119">The post request should include the content type header: **application/json**.</span><span class="sxs-lookup"><span data-stu-id="74320-119">The post request should include the content type header: **application/json**.</span></span>

##### <a name="json-search"></a><span data-ttu-id="74320-120">JSON Search</span><span class="sxs-lookup"><span data-stu-id="74320-120">JSON Search</span></span> 

<span data-ttu-id="74320-121">For the *json* search, the POST body is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="74320-121">For the *json* search, the POST body is a JSON object.</span></span> <span data-ttu-id="74320-122">The JSON object describes a path pattern with user-specified constraints (see the [specification of JSON object](JSONSearchSyntax.md) for *json* search).</span><span class="sxs-lookup"><span data-stu-id="74320-122">The JSON object describes a path pattern with user-specified constraints (see the [specification of JSON object](JSONSearchSyntax.md) for *json* search).</span></span>


##### <a name="lambda-search"></a><span data-ttu-id="74320-123">Lambda Search</span><span class="sxs-lookup"><span data-stu-id="74320-123">Lambda Search</span></span>

<span data-ttu-id="74320-124">For the *lambda* search, the POST body is a plain-text string.</span><span class="sxs-lookup"><span data-stu-id="74320-124">For the *lambda* search, the POST body is a plain-text string.</span></span> <span data-ttu-id="74320-125">The POST body is a LIKQ lambda query string, which  is a single C# statement (see the [specification of query string](LambdaSearchSyntax.md) for *lambda* search).</span><span class="sxs-lookup"><span data-stu-id="74320-125">The POST body is a LIKQ lambda query string, which  is a single C# statement (see the [specification of query string](LambdaSearchSyntax.md) for *lambda* search).</span></span> 

<br>
## <a name="response-json"></a><span data-ttu-id="74320-126">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="74320-126">Response (JSON)</span></span>
<span data-ttu-id="74320-127">Name</span><span class="sxs-lookup"><span data-stu-id="74320-127">Name</span></span> | <span data-ttu-id="74320-128">Description</span><span class="sxs-lookup"><span data-stu-id="74320-128">Description</span></span>
-------|-----   
<span data-ttu-id="74320-129">**results**</span><span class="sxs-lookup"><span data-stu-id="74320-129">**results**</span></span> | <span data-ttu-id="74320-130">An array of 0 or more entities that match the query expression.</span><span class="sxs-lookup"><span data-stu-id="74320-130">An array of 0 or more entities that match the query expression.</span></span> <span data-ttu-id="74320-131">Each entity contains the values of requested attributes.</span><span class="sxs-lookup"><span data-stu-id="74320-131">Each entity contains the values of requested attributes.</span></span> <span data-ttu-id="74320-132">This field is present if the request has been successfully processed.</span><span class="sxs-lookup"><span data-stu-id="74320-132">This field is present if the request has been successfully processed.</span></span>
<span data-ttu-id="74320-133">**error**</span><span class="sxs-lookup"><span data-stu-id="74320-133">**error**</span></span> | <span data-ttu-id="74320-134">HTTP status codes.</span><span class="sxs-lookup"><span data-stu-id="74320-134">HTTP status codes.</span></span> <span data-ttu-id="74320-135">This field is present if the request fails.</span><span class="sxs-lookup"><span data-stu-id="74320-135">This field is present if the request fails.</span></span>
<span data-ttu-id="74320-136">**message**</span><span class="sxs-lookup"><span data-stu-id="74320-136">**message**</span></span> | <span data-ttu-id="74320-137">Error message.</span><span class="sxs-lookup"><span data-stu-id="74320-137">Error message.</span></span> <span data-ttu-id="74320-138">This field is present if the request fails.</span><span class="sxs-lookup"><span data-stu-id="74320-138">This field is present if the request fails.</span></span>

<span data-ttu-id="74320-139">If a query cannot be processed within _800 ms_, a _timeout_ error will be returned.</span><span class="sxs-lookup"><span data-stu-id="74320-139">If a query cannot be processed within _800 ms_, a _timeout_ error will be returned.</span></span> 

<br>
#### <a name="example"></a><span data-ttu-id="74320-140">Example:</span><span class="sxs-lookup"><span data-stu-id="74320-140">Example:</span></span>

##### <a name="json-search"></a><span data-ttu-id="74320-141">JSON Search</span><span class="sxs-lookup"><span data-stu-id="74320-141">JSON Search</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/graph/v1.0/search?mode=json
```
<br>
<span data-ttu-id="74320-142">For the *json* search, if we want to get the papers whose titles contain "graph engine" and written by "bin shao", we can specify the query as follows.</span><span class="sxs-lookup"><span data-stu-id="74320-142">For the *json* search, if we want to get the papers whose titles contain "graph engine" and written by "bin shao", we can specify the query as follows.</span></span>

```JSON
{
  "path": "/paper/AuthorIDs/author",
  "paper": {
    "type": "Paper",
    "NormalizedTitle": "graph engine",
    "select": [
      "OriginalTitle"
    ]
  },
  "author": {
    "return": {
      "type": "Author",
      "Name": "bin shao"
    }
  }
}
```

<span data-ttu-id="74320-143">The output of a query is an array of graph paths.</span><span class="sxs-lookup"><span data-stu-id="74320-143">The output of a query is an array of graph paths.</span></span> <span data-ttu-id="74320-144">A graph path is an array of node objects corresponding to the nodes specified in the query path.</span><span class="sxs-lookup"><span data-stu-id="74320-144">A graph path is an array of node objects corresponding to the nodes specified in the query path.</span></span> <span data-ttu-id="74320-145">These node objects have at least one property *CellID*, which represents the entity ID.</span><span class="sxs-lookup"><span data-stu-id="74320-145">These node objects have at least one property *CellID*, which represents the entity ID.</span></span> <span data-ttu-id="74320-146">Other properties can be retrieved by specifying the property names via the select operator of a [*Traversal Action Object*](JSONSearchSyntax.md).</span><span class="sxs-lookup"><span data-stu-id="74320-146">Other properties can be retrieved by specifying the property names via the select operator of a [*Traversal Action Object*](JSONSearchSyntax.md).</span></span>

```JSON
{
  "Results": [
    [
      {
        "CellID": 2160459668,
        "OriginalTitle": "Trinity: a distributed graph engine on a memory cloud"
      },
      {
        "CellID": 2093502026
      }
    ],
    [
      {
        "CellID": 2171539317,
        "OriginalTitle": "A distributed graph engine for web scale RDF data"
      },
      {
        "CellID": 2093502026
      }
    ],
    [
      {
        "CellID": 2411554868,
        "OriginalTitle": "A distributed graph engine for web scale RDF data"
      },
      {
        "CellID": 2093502026
      }
    ],
    [
      {
        "CellID": 73304046,
        "OriginalTitle": "The Trinity graph engine"
      },
      {
        "CellID": 2093502026
      }
    ]
  ]
}
 ```

##### <a name="lambda-search"></a><span data-ttu-id="74320-147">Lambda Search</span><span class="sxs-lookup"><span data-stu-id="74320-147">Lambda Search</span></span> 

```
https://westus.api.cognitive.microsoft.com/academic/graph/v1.0/search?mode=lambda
```
<br>
<span data-ttu-id="74320-148">For the *lambda* search, if we want to get the author IDs of a given paper, we can write a query like the following one.</span><span class="sxs-lookup"><span data-stu-id="74320-148">For the *lambda* search, if we want to get the author IDs of a given paper, we can write a query like the following one.</span></span>

```
MAG.StartFrom(@"{
    type  : ""Paper"",
    match : {
        NormalizedTitle : ""trinity: a distributed graph engine on a memory cloud""
    }
}").FollowEdge("AuthorIDs").VisitNode(Action.Return)
```

<span data-ttu-id="74320-149">The output of a *lambda* search query is also an array of graph paths:</span><span class="sxs-lookup"><span data-stu-id="74320-149">The output of a *lambda* search query is also an array of graph paths:</span></span>

```JSON
{
  "Results": [
    [
      {
        "CellID": 2160459668
      },
      {
        "CellID": 2142490828
      }
    ],
    [
      {
        "CellID": 2160459668
      },
      {
        "CellID": 2116756368
      }
    ],
    [
      {
        "CellID": 2160459668
      },
      {
        "CellID": 2093502026
      }
    ]
  ]
}
```
 
## <a name="graph-schema"></a><span data-ttu-id="74320-150">Graph Schema</span><span class="sxs-lookup"><span data-stu-id="74320-150">Graph Schema</span></span>

<span data-ttu-id="74320-151">Graph schema is useful for writing graph search queries.</span><span class="sxs-lookup"><span data-stu-id="74320-151">Graph schema is useful for writing graph search queries.</span></span> <span data-ttu-id="74320-152">It is shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="74320-152">It is shown in the following figure.</span></span>

![Microsoft Academic Graph Schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Academic-Knowledge/Images/AcademicGraphSchema.png)

