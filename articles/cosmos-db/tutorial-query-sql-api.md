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
# <a name="tutorial-query-azure-cosmos-db-by-using-the-sql-api"></a>Tutorial: Query Azure Cosmos DB by using the SQL API

The Azure Cosmos DB [SQL API](documentdb-introduction.md) supports querying documents using SQL. This article provides a sample document and two sample SQL queries and results.

This article covers the following tasks: 

> [!div class="checklist"]
> * Querying data with SQL

## <a name="sample-document"></a>Sample document

The SQL queries in this article use the following sample document.

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
## <a name="where-can-i-run-sql-queries"></a>Where can I run SQL queries?

You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](sql-api-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.

For more information about SQL queries, see:
* [SQL query and SQL syntax](sql-api-sql-query.md)

## <a name="prerequisites"></a>Prerequisites

This tutorial assumes you have an Azure Cosmos DB account and collection. Don't have any of those? Complete the [5-minute quickstart](create-mongodb-nodejs.md).

## <a name="example-query-1"></a>Example query 1

Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`. Since it's a `SELECT *` statement, the output of the query is the complete JSON document:

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Results**

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

## <a name="example-query-2"></a>Example query 2

The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.

**Query**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'

**Results**

[ { "givenName": "Jesse" }, { "givenName": "Lisa" } ]


## <a name="next-steps"></a>Next steps

In this tutorial, you've done the following:

> [!div class="checklist"]
> * Learned how to query using SQL  

You can now proceed to the next tutorial to learn how to distribute your data globally.

> [!div class="nextstepaction"]
> [Distribute your data globally](tutorial-global-distribution-sql-api.md)

