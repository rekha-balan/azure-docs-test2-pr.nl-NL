---
title: How to query with SQL in Azure Cosmos DB? | Microsoft Docs
description: Learn to query with SQL in Azure Cosmos DB
services: cosmos-db
author: rafats
manager: kfile
editor: ''
tags: ''
ms.service: cosmos-db
ms.custom: tutorial-develop, mvc
ms.devlang: na
ms.topic: tutorial
ms.date: 05/10/2017
ms.author: rafats
ms.openlocfilehash: 5f5a98f0f28eba499b7ea3fa76944c21cf8bf8db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870268"
---
# <a name="tutorial-query-azure-cosmos-db-by-using-the-sql-api"></a><span data-ttu-id="116f0-104">Tutorial: Query Azure Cosmos DB by using the SQL API</span><span class="sxs-lookup"><span data-stu-id="116f0-104">Tutorial: Query Azure Cosmos DB by using the SQL API</span></span>

<span data-ttu-id="116f0-105">The Azure Cosmos DB [SQL API](documentdb-introduction.md) supports querying documents using SQL.</span><span class="sxs-lookup"><span data-stu-id="116f0-105">The Azure Cosmos DB [SQL API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="116f0-106">This article provides a sample document and two sample SQL queries and results.</span><span class="sxs-lookup"><span data-stu-id="116f0-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="116f0-107">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="116f0-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="116f0-108">Querying data with SQL</span><span class="sxs-lookup"><span data-stu-id="116f0-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="116f0-109">Sample document</span><span class="sxs-lookup"><span data-stu-id="116f0-109">Sample document</span></span>

<span data-ttu-id="116f0-110">The SQL queries in this article use the following sample document.</span><span class="sxs-lookup"><span data-stu-id="116f0-110">The SQL queries in this article use the following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="116f0-111">Where can I run SQL queries?</span><span class="sxs-lookup"><span data-stu-id="116f0-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="116f0-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](sql-api-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span><span class="sxs-lookup"><span data-stu-id="116f0-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](sql-api-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="116f0-113">For more information about SQL queries, see:</span><span class="sxs-lookup"><span data-stu-id="116f0-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="116f0-114">SQL query and SQL syntax</span><span class="sxs-lookup"><span data-stu-id="116f0-114">SQL query and SQL syntax</span></span>](sql-api-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="116f0-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="116f0-115">Prerequisites</span></span>

<span data-ttu-id="116f0-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span><span class="sxs-lookup"><span data-stu-id="116f0-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="116f0-117">Don't have any of those?</span><span class="sxs-lookup"><span data-stu-id="116f0-117">Don't have any of those?</span></span> <span data-ttu-id="116f0-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="116f0-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md).</span></span>

## <a name="example-query-1"></a><span data-ttu-id="116f0-119">Example query 1</span><span class="sxs-lookup"><span data-stu-id="116f0-119">Example query 1</span></span>

<span data-ttu-id="116f0-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="116f0-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="116f0-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span><span class="sxs-lookup"><span data-stu-id="116f0-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="116f0-122">**Query**</span><span class="sxs-lookup"><span data-stu-id="116f0-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="116f0-123">**Results**</span><span class="sxs-lookup"><span data-stu-id="116f0-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="116f0-124">Example query 2</span><span class="sxs-lookup"><span data-stu-id="116f0-124">Example query 2</span></span>

<span data-ttu-id="116f0-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span><span class="sxs-lookup"><span data-stu-id="116f0-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="116f0-126">**Query**</span><span class="sxs-lookup"><span data-stu-id="116f0-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'

<span data-ttu-id="116f0-127">**Results**</span><span class="sxs-lookup"><span data-stu-id="116f0-127">**Results**</span></span>

<span data-ttu-id="116f0-128">[ { "givenName": "Jesse" }, { "givenName": "Lisa" } ]</span><span class="sxs-lookup"><span data-stu-id="116f0-128">[ { "givenName": "Jesse" }, { "givenName": "Lisa" } ]</span></span>


## <a name="next-steps"></a><span data-ttu-id="116f0-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="116f0-129">Next steps</span></span>

<span data-ttu-id="116f0-130">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="116f0-130">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="116f0-131">Learned how to query using SQL</span><span class="sxs-lookup"><span data-stu-id="116f0-131">Learned how to query using SQL</span></span>  

<span data-ttu-id="116f0-132">You can now proceed to the next tutorial to learn how to distribute your data globally.</span><span class="sxs-lookup"><span data-stu-id="116f0-132">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="116f0-133">Distribute your data globally</span><span class="sxs-lookup"><span data-stu-id="116f0-133">Distribute your data globally</span></span>](tutorial-global-distribution-sql-api.md)

