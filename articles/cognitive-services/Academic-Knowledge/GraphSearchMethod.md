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
# <a name="graph-search-method"></a>Graph Search Method

The **graph search** REST API is used to return a set of academic entities based on the given graph patterns.  The response is a set of graph paths satisfying the user-specified constraints. A graph path is an interleaved sequence of graph nodes and edges in the form of _v0, e0, v1, e1, ..., vn_, where _v0_ is the starting node of the path.
<br>

**REST endpoint:**  
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?
```   
<br>

## <a name="request-parameters"></a>Request Parameters  
Name     | Value | Required?  | Description
-----------|-----------|---------|--------
**mode**       | Text string | Yes | Name of the mode that you wish to use. The value is either *json* or *lambda*.

The graph search method must be called via an HTTP POST request. The post request should include the content type header: **application/json**.

##### <a name="json-search"></a>JSON Search 

For the *json* search, the POST body is a JSON object. The JSON object describes a path pattern with user-specified constraints (see the [specification of JSON object](JSONSearchSyntax.md) for *json* search).


##### <a name="lambda-search"></a>Lambda Search

For the *lambda* search, the POST body is a plain-text string. The POST body is a LIKQ lambda query string, which  is a single C# statement (see the [specification of query string](LambdaSearchSyntax.md) for *lambda* search). 

<br>
## <a name="response-json"></a>Response (JSON)
Name | Description
-------|-----   
**results** | An array of 0 or more entities that match the query expression. Each entity contains the values of requested attributes. This field is present if the request has been successfully processed.
**error** | HTTP status codes. This field is present if the request fails.
**message** | Error message. This field is present if the request fails.

If a query cannot be processed within _800 ms_, a _timeout_ error will be returned. 

<br>
#### <a name="example"></a>Example:

##### <a name="json-search"></a>JSON Search
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?mode=json
```
<br>
For the *json* search, if we want to get the papers whose titles contain "graph engine" and written by "bin shao", we can specify the query as follows.

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

The output of a query is an array of graph paths. A graph path is an array of node objects corresponding to the nodes specified in the query path. These node objects have at least one property *CellID*, which represents the entity ID. Other properties can be retrieved by specifying the property names via the select operator of a [*Traversal Action Object*](JSONSearchSyntax.md).

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

##### <a name="lambda-search"></a>Lambda Search 

```
https://westus.api.cognitive.microsoft.com/academic/v1.0/graph/search?mode=lambda
```
<br>
For the *lambda* search, if we want to get the author IDs of a given paper, we can write a query like the following one.

```
MAG.StartFrom(@"{
    type  : ""Paper"",
    match : {
        NormalizedTitle : ""trinity: a distributed graph engine on a memory cloud""
    }
}").FollowEdge("AuthorIDs").VisitNode(Action.Return)
```

The output of a *lambda* search query is also an array of graph paths:

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
 
## <a name="graph-schema"></a>Graph Schema

Graph schema is useful for writing graph search queries. It is shown in the following figure.

![Microsoft Academic Graph Schema](./Images/AcademicGraphSchema.png)
