---
title: JSON search syntax in the Academic Knowledge API | Microsoft Docs
description: Learn about the JSON search syntax you can use in the Academic Knowledge API in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 9210263671d6ac1fca1ced48f0e95030b82bb009
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553834"
---
# <a name="json-search-syntax"></a><span data-ttu-id="2113c-103">JSON Search Syntax</span><span class="sxs-lookup"><span data-stu-id="2113c-103">JSON Search Syntax</span></span>

```javascript
/* Query Object:
   Suppose we have a query path /v0/e0/v1/e1/...
   A query object contains constraints to be applied to graph nodes in a path.
   Constraints are given in <"node identifier", {constraint object}> key-value pairs: 
*/
{
    /* query path can also be set in the query object */
    path: "/v0/e0/v1/e1/.../vn/",
    v0: { /* A Constraint Object */ },
    v1: { /* A Constraint Object */ },
}
```

<span data-ttu-id="2113c-104">The node names in a query path (_v0, v1, ..._) serve as node identifiers that can be referenced in the query object; the edge names (_e0, e1, ..._) in the path represent the types of the corresponding edges.</span><span class="sxs-lookup"><span data-stu-id="2113c-104">The node names in a query path (_v0, v1, ..._) serve as node identifiers that can be referenced in the query object; the edge names (_e0, e1, ..._) in the path represent the types of the corresponding edges.</span></span> <span data-ttu-id="2113c-105">We can use an asterisk _\*_ as a node or edge name (except for the starting node, which must be given) to declare that there are no constraints on such an element.</span><span class="sxs-lookup"><span data-stu-id="2113c-105">We can use an asterisk _\*_ as a node or edge name (except for the starting node, which must be given) to declare that there are no constraints on such an element.</span></span> <span data-ttu-id="2113c-106">For example, a query path `/v0/*/v1/e1/*/` retrieves paths from the graph without restricting the type of the edge _(v0, v1)_.</span><span class="sxs-lookup"><span data-stu-id="2113c-106">For example, a query path `/v0/*/v1/e1/*/` retrieves paths from the graph without restricting the type of the edge _(v0, v1)_.</span></span> <span data-ttu-id="2113c-107">Meanwhile, the query does not have constraints on the destination (the last node) of the path either.</span><span class="sxs-lookup"><span data-stu-id="2113c-107">Meanwhile, the query does not have constraints on the destination (the last node) of the path either.</span></span>

<span data-ttu-id="2113c-108">When a path contains just one node, say _v0_, the query will simply return all entities that satisfy the constraints.</span><span class="sxs-lookup"><span data-stu-id="2113c-108">When a path contains just one node, say _v0_, the query will simply return all entities that satisfy the constraints.</span></span> <span data-ttu-id="2113c-109">A constraint object applied to the starting node is called a *Starting Query Object*, whose specification is given as follows.</span><span class="sxs-lookup"><span data-stu-id="2113c-109">A constraint object applied to the starting node is called a *Starting Query Object*, whose specification is given as follows.</span></span>

```javascript
/* Starting Query Object:
   Specifies constraints on the starting node
*/
{
    /* "match" operator searches for entities with the specified properties. 
       All properties defined in the graph schema be queried such as "Name" and "NormalizedTitle".
     */
    "match": { 
        "Name" : "some name",
        ...
    },
    /* "id" operator directly specifies the IDs of the starting nodes. 
       When it is present, the "match" operator is ignored. 
     */
    "id": [ id1, id2, id3... ],
    /* "type" operator limits results to a certain type of entities,
       for example, "Author" or "Paper".
     */
    "type": "Author",
    /* "select" operator pulls properties from the database and 
       returns them to the client.
     */
    "select": ["PaperRank", ...]
}
```

<span data-ttu-id="2113c-110">When a path contains more than just a starting node, the query processor will perform a graph traversal following the specified path pattern.</span><span class="sxs-lookup"><span data-stu-id="2113c-110">When a path contains more than just a starting node, the query processor will perform a graph traversal following the specified path pattern.</span></span> <span data-ttu-id="2113c-111">When it arrives at a node, the user-specified traversal actions will be triggered, that is, whether to stop at the current node and return or to continue to explore the graph.</span><span class="sxs-lookup"><span data-stu-id="2113c-111">When it arrives at a node, the user-specified traversal actions will be triggered, that is, whether to stop at the current node and return or to continue to explore the graph.</span></span> <span data-ttu-id="2113c-112">When no traversal action is specified, default actions will be taken.</span><span class="sxs-lookup"><span data-stu-id="2113c-112">When no traversal action is specified, default actions will be taken.</span></span> <span data-ttu-id="2113c-113">For an intermediate node, the default action is to continue to explore the graph.</span><span class="sxs-lookup"><span data-stu-id="2113c-113">For an intermediate node, the default action is to continue to explore the graph.</span></span> <span data-ttu-id="2113c-114">For the last node of a path, the default action is to stop and return.</span><span class="sxs-lookup"><span data-stu-id="2113c-114">For the last node of a path, the default action is to stop and return.</span></span> <span data-ttu-id="2113c-115">A constraint object that specifies traversal actions is called a *Traversal Action Object*.</span><span class="sxs-lookup"><span data-stu-id="2113c-115">A constraint object that specifies traversal actions is called a *Traversal Action Object*.</span></span> <span data-ttu-id="2113c-116">Its specification is given as follows:</span><span class="sxs-lookup"><span data-stu-id="2113c-116">Its specification is given as follows:</span></span>

```javascript
/* Traversal Action Object:
   Specifies graph traversal actions on a node (except for the starting node).
 */
{
    /* Set the continue condition here. */
    continue: { 
        /* simple property exact match */
        "property_key" : "property_value", 
        /* Advanced query operators */
        /* -- Numerical comparisons */
        "property_key_2" : { "gt" /* or simply ">" */ : 123 },
        /* -- Substring query */
        "property_key_3" : { "substring" : "456" },
        /* -- CellID query */
        "id": [ 111, 222, 333... ],
        /* -- Entity type query */
        "type": "cell_type",
        /* -- Property existance query */
        "has" : "property_key_4",
        /* -- Logical operators */
        /* ---- Note that, by default the operators are combined with AND semantics */
        
        /* -- OR operator */
        "or": {
          /* Query operators... */
        },
        /* -- NOT operator */
        "not": {
            /* Query operators... */
        }
    },
    /* Set the return condition here. */
    return: {
        /* Same operators as the continue object */
    },
    /* The selected properties to return. */
    select: ["property_key_1", ...]
}
```

<span data-ttu-id="2113c-117">The POST body of a *json* search query should contain at least a *path* pattern.</span><span class="sxs-lookup"><span data-stu-id="2113c-117">The POST body of a *json* search query should contain at least a *path* pattern.</span></span> <span data-ttu-id="2113c-118">Traverse action objects are optional.</span><span class="sxs-lookup"><span data-stu-id="2113c-118">Traverse action objects are optional.</span></span> <span data-ttu-id="2113c-119">Here are two examples.</span><span class="sxs-lookup"><span data-stu-id="2113c-119">Here are two examples.</span></span>

```JSON
{
  "path": "/series/ConferenceInstanceIDs/conference/FieldOfStudyIDs/field",
  "series": {
    "type": "ConferenceSeries",
    "FullName": "graph",
    "select": [ "FullName", "ShortName" ]
  },
  "conference": {
    "type": "ConferenceInstance",
    "select": [ "FullName" ]
  },
  "field": {
    "type": "FieldOfStudy",
    "select": [ "Name" ],
    "return": { "Name": { "substring" : "World Wide Web" } }
  }
}
```

```JSON
{
  "path": "/author/PaperIDs/paper",
  "author": {
    "type": "Author",
    "select": [ "DisplayAuthorName" ],
    "match": { "Name": "leslie lamport" }
  },
  "paper": {
    "type": "Paper",
    "select": [ "OriginalTitle", "CitationCount" ],
    "return": { "CitationCount": { "gt": 100 } }
  }
}
```

