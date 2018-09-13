---
title: How to query graph data in Azure Cosmos DB? | Microsoft Docs
description: Learn to query graph data in Azure Cosmos DB
services: cosmos-db
author: luisbosquez
manager: kfile
editor: ''
tags: ''
ms.service: cosmos-db
ms.component: cosmosdb-graph
ms.devlang: na
ms.topic: tutorial
ms.date: 01/02/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: e3ed90d0b706e742588a5a0966d9ac3bda44ecbd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867143"
---
# <a name="tutorial-query-azure-cosmos-db-gremlin-api-by-using-gremlin"></a><span data-ttu-id="63cb8-104">Tutorial: Query Azure Cosmos DB Gremlin API by using Gremlin</span><span class="sxs-lookup"><span data-stu-id="63cb8-104">Tutorial: Query Azure Cosmos DB Gremlin API by using Gremlin</span></span>

<span data-ttu-id="63cb8-105">The Azure Cosmos DB [Gremlin API](graph-introduction.md) supports [Gremlin](https://github.com/tinkerpop/gremlin/wiki) queries.</span><span class="sxs-lookup"><span data-stu-id="63cb8-105">The Azure Cosmos DB [Gremlin API](graph-introduction.md) supports [Gremlin](https://github.com/tinkerpop/gremlin/wiki) queries.</span></span> <span data-ttu-id="63cb8-106">This article provides sample documents and queries to get you started.</span><span class="sxs-lookup"><span data-stu-id="63cb8-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="63cb8-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span><span class="sxs-lookup"><span data-stu-id="63cb8-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="63cb8-108">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="63cb8-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="63cb8-109">Querying data with Gremlin</span><span class="sxs-lookup"><span data-stu-id="63cb8-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63cb8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63cb8-110">Prerequisites</span></span>

<span data-ttu-id="63cb8-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span><span class="sxs-lookup"><span data-stu-id="63cb8-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="63cb8-112">Don't have any of those?</span><span class="sxs-lookup"><span data-stu-id="63cb8-112">Don't have any of those?</span></span> <span data-ttu-id="63cb8-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span><span class="sxs-lookup"><span data-stu-id="63cb8-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="63cb8-114">You can run the following queries using the [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span><span class="sxs-lookup"><span data-stu-id="63cb8-114">You can run the following queries using the [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="63cb8-115">Count vertices in the graph</span><span class="sxs-lookup"><span data-stu-id="63cb8-115">Count vertices in the graph</span></span>

<span data-ttu-id="63cb8-116">The following snippet shows how to count the number of vertices in the graph:</span><span class="sxs-lookup"><span data-stu-id="63cb8-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="63cb8-117">Filters</span><span class="sxs-lookup"><span data-stu-id="63cb8-117">Filters</span></span>

<span data-ttu-id="63cb8-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span><span class="sxs-lookup"><span data-stu-id="63cb8-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="63cb8-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span><span class="sxs-lookup"><span data-stu-id="63cb8-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="63cb8-120">Projection</span><span class="sxs-lookup"><span data-stu-id="63cb8-120">Projection</span></span>

<span data-ttu-id="63cb8-121">You can project certain properties in the query results using the `values` step:</span><span class="sxs-lookup"><span data-stu-id="63cb8-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="63cb8-122">Find related edges and vertices</span><span class="sxs-lookup"><span data-stu-id="63cb8-122">Find related edges and vertices</span></span>

<span data-ttu-id="63cb8-123">So far, we've only seen query operators that work in any database.</span><span class="sxs-lookup"><span data-stu-id="63cb8-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="63cb8-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span><span class="sxs-lookup"><span data-stu-id="63cb8-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="63cb8-125">Let's find all friends of Thomas.</span><span class="sxs-lookup"><span data-stu-id="63cb8-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="63cb8-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span><span class="sxs-lookup"><span data-stu-id="63cb8-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="63cb8-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span><span class="sxs-lookup"><span data-stu-id="63cb8-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="63cb8-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span><span class="sxs-lookup"><span data-stu-id="63cb8-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="63cb8-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="63cb8-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="63cb8-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="63cb8-130">Next steps</span></span>

<span data-ttu-id="63cb8-131">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="63cb8-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63cb8-132">Learned how to query using Graph</span><span class="sxs-lookup"><span data-stu-id="63cb8-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="63cb8-133">You can now proceed to the Concepts section for more information about Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="63cb8-133">You can now proceed to the Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63cb8-134">Global distribution</span><span class="sxs-lookup"><span data-stu-id="63cb8-134">Global distribution</span></span>](distribute-data-globally.md) 

