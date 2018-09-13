---
title: Graph Search method in the Academic Knowledge API | Microsoft Docs
description: Use the Graph Search method in the Academic Knowledge API to return a set of academic entities based on specific graph patterns in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: d811db117c934c0d41fbfea1220d241cc022e4a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812161"
---
# <a name="graph-search-method"></a><span data-ttu-id="909f4-103">Graph Search Method</span><span class="sxs-lookup"><span data-stu-id="909f4-103">Graph Search Method</span></span>

<span data-ttu-id="909f4-104">The **graph search** REST API is used to return a set of academic entities based on the given graph patterns.</span><span class="sxs-lookup"><span data-stu-id="909f4-104">The **graph search** REST API is used to return a set of academic entities based on the given graph patterns.</span></span>  <span data-ttu-id="909f4-105">The response is a set of graph paths satisfying the user-specified constraints.</span><span class="sxs-lookup"><span data-stu-id="909f4-105">The response is a set of graph paths satisfying the user-specified constraints.</span></span> <span data-ttu-id="909f4-106">A graph path is an interleaved sequence of graph nodes and edges in the form of _v0, e0, v1, e1, ..., vn_, where _v0_ is the starting node of the path.</span><span class="sxs-lookup"><span data-stu-id="909f4-106">A graph path is an interleaved sequence of graph nodes and edges in the form of _v0, e0, v1, e1, ..., vn_, where _v0_ is the starting node of the path.</span></span>
<br>

<span data-ttu-id="909f4-107">**REST endpoint:**</span><span class="sxs-lookup"><span data-stu-id="909f4-107">**REST endpoint:**</span></span>  
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?
```   
<br>

## <a name="request-parameters"></a><span data-ttu-id="909f4-108">Request Parameters</span><span class="sxs-lookup"><span data-stu-id="909f4-108">Request Parameters</span></span>  
<span data-ttu-id="909f4-109">Name</span><span class="sxs-lookup"><span data-stu-id="909f4-109">Name</span></span>     | <span data-ttu-id="909f4-110">Value</span><span class="sxs-lookup"><span data-stu-id="909f4-110">Value</span></span> | <span data-ttu-id="909f4-111">Required?</span><span class="sxs-lookup"><span data-stu-id="909f4-111">Required?</span></span>  | <span data-ttu-id="909f4-112">Description</span><span class="sxs-lookup"><span data-stu-id="909f4-112">Description</span></span>
-----------|-----------|---------|--------
<span data-ttu-id="909f4-113">**mode**</span><span class="sxs-lookup"><span data-stu-id="909f4-113">**mode**</span></span>       | <span data-ttu-id="909f4-114">Text string</span><span class="sxs-lookup"><span data-stu-id="909f4-114">Text string</span></span> | <span data-ttu-id="909f4-115">Yes</span><span class="sxs-lookup"><span data-stu-id="909f4-115">Yes</span></span> | <span data-ttu-id="909f4-116">Name of the mode that you wish to use.</span><span class="sxs-lookup"><span data-stu-id="909f4-116">Name of the mode that you wish to use.</span></span> <span data-ttu-id="909f4-117">The value is either *json* or *lambda*.</span><span class="sxs-lookup"><span data-stu-id="909f4-117">The value is either *json* or *lambda*.</span></span>

<span data-ttu-id="909f4-118">The graph search method must be called via an HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="909f4-118">The graph search method must be called via an HTTP POST request.</span></span> <span data-ttu-id="909f4-119">The post request should include the content type header: **application/json**.</span><span class="sxs-lookup"><span data-stu-id="909f4-119">The post request should include the content type header: **application/json**.</span></span>

##### <a name="json-search"></a><span data-ttu-id="909f4-120">JSON Search</span><span class="sxs-lookup"><span data-stu-id="909f4-120">JSON Search</span></span> 

<span data-ttu-id="909f4-121">For the *json* search, the POST body is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="909f4-121">For the *json* search, the POST body is a JSON object.</span></span> <span data-ttu-id="909f4-122">The JSON object describes a path pattern with user-specified constraints (see the [specification of JSON object](JSONSearchSyntax.md) for *json* search).</span><span class="sxs-lookup"><span data-stu-id="909f4-122">The JSON object describes a path pattern with user-specified constraints (see the [specification of JSON object](JSONSearchSyntax.md) for *json* search).</span></span>


##### <a name="lambda-search"></a><span data-ttu-id="909f4-123">Lambda Search</span><span class="sxs-lookup"><span data-stu-id="909f4-123">Lambda Search</span></span>

<span data-ttu-id="909f4-124">For the *lambda* search, the POST body is a plain-text string.</span><span class="sxs-lookup"><span data-stu-id="909f4-124">For the *lambda* search, the POST body is a plain-text string.</span></span> <span data-ttu-id="909f4-125">The POST body is a LIKQ lambda query string, which  is a single C# statement (see the [specification of query string](LambdaSearchSyntax.md) for *lambda* search).</span><span class="sxs-lookup"><span data-stu-id="909f4-125">The POST body is a LIKQ lambda query string, which  is a single C# statement (see the [specification of query string](LambdaSearchSyntax.md) for *lambda* search).</span></span> 

<br>
## <a name="response-json"></a><span data-ttu-id="909f4-126">Response (JSON)</span><span class="sxs-lookup"><span data-stu-id="909f4-126">Response (JSON)</span></span>
<span data-ttu-id="909f4-127">Name</span><span class="sxs-lookup"><span data-stu-id="909f4-127">Name</span></span> | <span data-ttu-id="909f4-128">Description</span><span class="sxs-lookup"><span data-stu-id="909f4-128">Description</span></span>
-------|-----   
<span data-ttu-id="909f4-129">**results**</span><span class="sxs-lookup"><span data-stu-id="909f4-129">**results**</span></span> | <span data-ttu-id="909f4-130">An array of 0 or more entities that match the query expression.</span><span class="sxs-lookup"><span data-stu-id="909f4-130">An array of 0 or more entities that match the query expression.</span></span> <span data-ttu-id="909f4-131">Each entity contains the values of requested attributes.</span><span class="sxs-lookup"><span data-stu-id="909f4-131">Each entity contains the values of requested attributes.</span></span> <span data-ttu-id="909f4-132">This field is present if the request has been successfully processed.</span><span class="sxs-lookup"><span data-stu-id="909f4-132">This field is present if the request has been successfully processed.</span></span>
<span data-ttu-id="909f4-133">**error**</span><span class="sxs-lookup"><span data-stu-id="909f4-133">**error**</span></span> | <span data-ttu-id="909f4-134">HTTP status codes.</span><span class="sxs-lookup"><span data-stu-id="909f4-134">HTTP status codes.</span></span> <span data-ttu-id="909f4-135">This field is present if the request fails.</span><span class="sxs-lookup"><span data-stu-id="909f4-135">This field is present if the request fails.</span></span>
<span data-ttu-id="909f4-136">**message**</span><span class="sxs-lookup"><span data-stu-id="909f4-136">**message**</span></span> | <span data-ttu-id="909f4-137">Error message.</span><span class="sxs-lookup"><span data-stu-id="909f4-137">Error message.</span></span> <span data-ttu-id="909f4-138">This field is present if the request fails.</span><span class="sxs-lookup"><span data-stu-id="909f4-138">This field is present if the request fails.</span></span>

<span data-ttu-id="909f4-139">If a query cannot be processed within _800 ms_, a _timeout_ error will be returned.</span><span class="sxs-lookup"><span data-stu-id="909f4-139">If a query cannot be processed within _800 ms_, a _timeout_ error will be returned.</span></span> 

<br>
#### <a name="example"></a><span data-ttu-id="909f4-140">Example:</span><span class="sxs-lookup"><span data-stu-id="909f4-140">Example:</span></span>

##### <a name="json-search"></a><span data-ttu-id="909f4-141">JSON Search</span><span class="sxs-lookup"><span data-stu-id="909f4-141">JSON Search</span></span>
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?mode=json
```
<br>
<span data-ttu-id="909f4-142">For the *json* search, if we want to get the papers whose titles contain "graph engine" and written by "bin shao", we can specify the query as follows.</span><span class="sxs-lookup"><span data-stu-id="909f4-142">For the *json* search, if we want to get the papers whose titles contain "graph engine" and written by "bin shao", we can specify the query as follows.</span></span>

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

<span data-ttu-id="909f4-143">The output of a query is an array of graph paths.</span><span class="sxs-lookup"><span data-stu-id="909f4-143">The output of a query is an array of graph paths.</span></span> <span data-ttu-id="909f4-144">A graph path is an array of node objects corresponding to the nodes specified in the query path.</span><span class="sxs-lookup"><span data-stu-id="909f4-144">A graph path is an array of node objects corresponding to the nodes specified in the query path.</span></span> <span data-ttu-id="909f4-145">These node objects have at least one property *CellID*, which represents the entity ID.</span><span class="sxs-lookup"><span data-stu-id="909f4-145">These node objects have at least one property *CellID*, which represents the entity ID.</span></span> <span data-ttu-id="909f4-146">Other properties can be retrieved by specifying the property names via the select operator of a [*Traversal Action Object*](JSONSearchSyntax.md).</span><span class="sxs-lookup"><span data-stu-id="909f4-146">Other properties can be retrieved by specifying the property names via the select operator of a [*Traversal Action Object*](JSONSearchSyntax.md).</span></span>

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

##### <a name="lambda-search"></a><span data-ttu-id="909f4-147">Lambda Search</span><span class="sxs-lookup"><span data-stu-id="909f4-147">Lambda Search</span></span> 

```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?mode=lambda
```
<br>
<span data-ttu-id="909f4-148">For the *lambda* search, if we want to get the author IDs of a given paper, we can write a query like the following one.</span><span class="sxs-lookup"><span data-stu-id="909f4-148">For the *lambda* search, if we want to get the author IDs of a given paper, we can write a query like the following one.</span></span>

```
MAG.StartFrom(@"{
    type  : ""Paper"",
    match : {
        NormalizedTitle : ""trinity: a distributed graph engine on a memory cloud""
    }
}").FollowEdge("AuthorIDs").VisitNode(Action.Return)
```

<span data-ttu-id="909f4-149">The output of a *lambda* search query is also an array of graph paths:</span><span class="sxs-lookup"><span data-stu-id="909f4-149">The output of a *lambda* search query is also an array of graph paths:</span></span>

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
 
## <a name="graph-schema"></a><span data-ttu-id="909f4-150">Graph Schema</span><span class="sxs-lookup"><span data-stu-id="909f4-150">Graph Schema</span></span>

<span data-ttu-id="909f4-151">Graph schema is useful for writing graph search queries.</span><span class="sxs-lookup"><span data-stu-id="909f4-151">Graph schema is useful for writing graph search queries.</span></span> <span data-ttu-id="909f4-152">It is shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="909f4-152">It is shown in the following figure.</span></span>

![Microsoft Academic Graph Schema](./Images/AcademicGraphSchema.png)
